# World Scratch Journey / 刮开世界：项目指南

> 最后更新：2026-08-14  
> 本文是 `world-scratch-journey` 的唯一项目说明，以当前仓库源码和运行时素材为准。历史交付计划、内容确认单和美术需求单已在开发完成后移除。

## 1. 项目概述

World Scratch Journey 是一款面向移动端 WebView 的旅行偏好测试与地点收集游戏。玩家每轮回答 4 道旅行偏好题，系统根据答案权重匹配六大地区之一，再从该地区分配一个目的地。玩家通过 Canvas 刮开隐藏明信片，揭晓结果并将地点收藏到 Passport，同时在 World Map 查看全球探索进度。

核心体验链路：

```text
Welcome
  → Quiz（4 题）
  → Scratch（刮除达到 70%）
  → Result（解锁或重访地点）
  → Next stop（下一轮 Quiz）/ Passport
```

游戏没有标准答案、失败状态或分数排行，核心目标是“表达偏好 → 匹配地点 → 主动揭晓 → 长期收集”。

## 2. 当前交付规格

| 项目 | 当前实现 |
|---|---|
| 游戏 ID | `world-scratch-journey` |
| 路由 | `/world-scratch-journey` |
| payloadKey | `world-scratch-journey` |
| 英文名 | World Scratch Journey |
| 中文名 | 刮开世界 |
| adType | `quiz`，仅保留平台契约，游戏内没有广告触发 |
| 首页封面 | `694×256` RGB WebP，60,748 bytes |
| 页面 | Welcome、Quiz、Scratch、Result、Passport、World Map |
| 题库 | 28 题、84 个题库选项 |
| 每轮 | 4 题：2 道 Yes / No + 2 道普通偏好题 |
| 轮次 | 7 轮为一个完整牌组周期，前 7 轮题目不重复 |
| 选项数量 | Yes / No 题各 2 项；普通偏好题各 4 项 |
| 地区 | Europe、North America、Asia、South America、Africa、Oceania |
| 目的地 | 50 个，每个目的地有独立图片和 Travel Knowledge |
| 刮卡阈值 | 实际刮除覆盖率达到 70% 后完成揭晓 |
| 存档 | `localStorage`，schema v2 |
| 音效 | Web Audio API 合成，不依赖外部音频文件 |
| 运行时素材 | CDN 托管 167 个文件，本地运行时资源已清理 |
| 外部依赖 | 未新增 npm 依赖 |
| 当前 UI 语言 | 英文 |

## 3. 仓库边界与开发红线

本游戏只能修改：

```text
src/games/world-scratch-journey/
public/games/world-scratch-journey/
```

不要为本游戏修改共享 `App.tsx`、`Home.tsx`、`registry.ts`、`AdService`、`GlobalStore`、`LogService`、共享组件或 `package.json`。游戏注册、路由、首页标题和封面必须通过 `manifest.ts` 表达。

Manifest 的关键契约：

- `id`、目录名和 `payloadKey` 必须一致；
- `route` 保持 `/world-scratch-journey`；
- `component` 保持 `() => import('./index')`；
- `adType` 当前复用 `quiz`；
- iOS/Android 广告位保持占位值，由集成者配置；
- 游戏必须保留返回共享 `/home` 的路径。

## 4. 页面和玩家流程

### 4.1 Welcome

Welcome 是游戏内部入口，提供：

- `Start the travel quiz`：创建新 Quiz session；
- `Travel Passport`：查看已收集地点；
- `World Map`：查看六地区与全球进度；
- 左上返回按钮：离开游戏并导航到共享 `/home`。

### 4.2 Quiz

每轮依次展示 4 道题。玩家选择答案后，按钮先显示约 170 ms 的选中反馈，再执行以下操作：

1. 将答案的地区权重累计到当前 session；
2. 写入答案 ID；
3. 推进当前题号；
4. 第 4 题完成后确定地区和目的地；
5. 将最终 `matchedRegion` 和 `destinationId` 写入 session；
6. 进入 Scratch。

Scratch 和 Result 始终读取同一个已确定目的地，不会在页面切换时重新随机。

### 4.3 Scratch

目的地图片位于 DOM 下层，可擦除 Canvas 位于上层。玩家可以使用鼠标、手指或触控笔刮除覆盖层，也可以点击 `Reveal now` 一键揭晓：

- 真实覆盖率达到 70% 后，界面进度显示为 100%；
- Canvas 淡出并停止接收 Pointer 事件；
- 普通动效模式下保留完整照片约 850 ms 后进入 Result；
- `prefers-reduced-motion` 模式下跳过等待；
- 覆盖纹理或印章加载失败时使用程序化 Canvas 兜底。

### 4.4 Result

Result 展示城市、国家、地标、推荐理由和 Travel Knowledge：

- 首次收集显示 `DESTINATION UNLOCKED` 和较强庆祝动画；
- 重复访问显示 `WELCOME BACK`，收藏数不重复增加；
- `Next stop` 使用专用罗盘前进图标，创建新 session 并进入下一轮 Quiz；
- `Passport` 打开收藏图鉴；
- 返回按钮结束当前流程并回到 Welcome。

### 4.5 Passport 与 World Map

Passport：

- 支持 `All` 和六地区筛选；
- 已收藏地点可以打开详情；
- 未收藏地点显示 Hidden；
- 展示地区收藏数与全部 50 个地点的进度。

World Map：

- 展示六个地区入口；
- 展示每个地区的收藏计数；
- 展示全局 `collected / 50` 和百分比；
- 点击地区会打开对应筛选的 Passport。

## 5. 题库、牌组与权重

### 5.1 题库结构

`quizData.ts` 是题目、选项、结果特征和地区权重的唯一数据源。

当前结构：

- 14 道 `yes-no` 题，每题 2 个选项；
- 14 道 `choice` 题，每题 4 个选项；
- 合计 28 题、84 个选项；
- 所有选项均包含稳定 ID、文案、`resultTrait`、`regionScores` 和视觉资源；
- 题目没有正确或错误答案。

修改题库时必须保持：

- question ID 和 answer ID 全局稳定；
- 题库总数与牌组基线同步；
- 每一轮恰好包含 2 道 `yes-no` 和 2 道 `choice`；
- `yes-no` 保持 2 个选项；
- `choice` 保持 4 个选项；
- 每个选项图片路径可解析；
- 地区权重只使用六个合法 `RegionId`。

### 5.2 七轮题目基线

```text
Round 1: travel-feeling, sunrise-start, solo-or-friends, unknown-flavor
Round 2: favorite-scenery, scenic-detour, street-food-or-dinner, local-market
Round 3: travel-rhythm, travel-light, train-or-road, public-transit
Round 4: first-stop, rainy-museum, stars-or-city-lights, local-celebration
Round 5: craft-or-postcards, wildlife-dawn, nature-or-landmark, live-music
Round 6: cafe-or-square, no-itinerary, hidden-lane-or-icon, food-first
Round 7: beach-or-mountain, boat-for-view, stories-or-photos, travel-journal
```

运行时会打乱七个轮次的先后顺序，并打乱每轮内部题序，但不会拆散每轮的题型配比。

### 5.3 牌组持久化

`PlayerData` 持久化：

- `questionDeck`：完整 28 题牌组；
- `questionCursor`：下一轮读取位置；
- `lastRoundQuestionIds`：上一轮 4 个题目 ID；
- `activeSession`：当前轮题目、答案、权重和最终地点。

`startNewQuiz()` 从牌组游标连续取 4 题。28 题耗尽后创建新牌组，并尽量避免新周期第一轮与上一轮重复。

### 5.4 地区和目的地分配

第 4 题完成后：

1. 计算六地区累计得分；
2. 选出最高分地区；
3. 最高分并列时只在并列地区中随机；
4. 从匹配地区优先选择未收藏地点；
5. 该地区全部收集完后才允许重复访问。

地区内容规模：

| 地区 | 目的地数 |
|---|---:|
| Europe | 15 |
| North America | 8 |
| Asia | 12 |
| South America | 5 |
| Africa | 6 |
| Oceania | 4 |
| 合计 | 50 |

## 6. 状态、存档与幂等

### 6.1 页面状态

游戏使用一个路由根组件和内部 view 状态：

```ts
type GameView =
  | 'welcome'
  | 'quiz'
  | 'scratch'
  | 'result'
  | 'passport'
  | 'world-map';
```

没有为游戏子页面增加共享路由。

### 6.2 存档结构

存档键：

```text
world-scratch-journey:player:v2
```

核心结构：

```ts
interface PlayerData {
  schemaVersion: 2;
  collectedPlaceIds: string[];
  resultHistory: ResultHistoryItem[];
  activeSession: QuizSession | null;
  questionDeck: string[];
  questionCursor: number;
  lastRoundQuestionIds: string[];
  soundEnabled: boolean;
}
```

读取时会校验 schema、题目、答案、地区、目的地、日期和分数；无效数据安全回退。写入失败会被捕获，游戏仍可继续运行，但刷新后可能无法保留进度。

### 6.3 刷新策略

牌组、游标、收藏、历史和声音设置会持久化，但页面初始化时会主动清除未完成的 `activeSession` 并回到 Welcome。因此当前版本不会恢复半途 Quiz 或刮卡进度。

### 6.4 收藏幂等

`revealActiveDestination()` 通过 `collectionApplied` 保证同一 session 只提交一次：

- 新地点只向 `collectedPlaceIds` 添加一次；
- 每次完成会向 `resultHistory` 添加一条记录；
- 重复调用 reveal 不会重复写收藏或历史；
- 重访地点会写历史，但不会增加收藏数。

## 7. Canvas 与反馈实现

### 7.1 ScratchCanvas

关键参数：

| 参数 | 当前值 |
|---|---:|
| 笔刷半径 | 34 CSS px |
| 揭晓阈值 | 70% |
| 覆盖率检测间隔 | 150 ms |
| 采样 Canvas 宽度 | 72 px |
| 揭晓照片停留 | 850 ms |
| DPR 上限 | 2 |
| 已清除 alpha 阈值 | 64 |

实现要点：

- 使用 Pointer Events 统一鼠标、触摸和触控笔；
- 使用 Pointer Capture 维持连续手势；
- 前后坐标之间绘制圆头粗线，避免快速移动断点；
- 使用 `destination-out` 擦除；
- 覆盖率在缩小后的离屏 Canvas 上检测，避免频繁扫描高 DPR 全尺寸像素；
- `ResizeObserver` 重设 Canvas 尺寸。

### 7.2 CelebrationCanvas

结果页粒子动画使用 Canvas 实现：

- 新发现约 40 个粒子；
- 重访约 14 个粒子；
- `runKey` 生成确定性随机序列；
- DPR 上限为 2；
- reduced-motion 环境不启动动画。

### 7.3 音效

点击和揭晓音效由 Web Audio API 的 oscillator 与 gain 合成。环境不支持或 AudioContext 无法启动时静默降级，不影响玩法。

## 8. 资源系统

### 8.1 统一资源入口

所有运行时资源路径集中在 `assetUrls.ts`：

```text
VITE_WORLD_SCRATCH_JOURNEY_ASSET_ROOT
  ↓ 未配置时
import.meta.env.BASE_URL + document.baseURI
  ↓
ASSET_URLS
```

组件、题库、数据和 CSS 自定义变量均通过 `ASSET_URLS` 获取路径。不要在组件或 CSS 中新增散落的 `/games/world-scratch-journey/...` 硬编码。

环境变量可以在 CDN 阶段覆盖资源根：

```text
VITE_WORLD_SCRATCH_JOURNEY_ASSET_ROOT=https://d2vfwj9kj1j1h1.cloudfront.net/game_center/world-scratch-journey/
```

### 8.2 CDN 运行时素材

```text
https://d2vfwj9kj1j1h1.cloudfront.net/game_center/world-scratch-journey/
├─ backgrounds/   Welcome 背景与 fallback
├─ covers/        694×256 首页封面
├─ destinations/  50 张目的地图片
├─ fallback/      明信片 SVG 占位图
├─ maps/          世界地图 fallback
├─ quiz-art/      题库图标与场景图
├─ regions/       六地区图片
└─ ui-art/        按钮、刮卡、结果、Welcome、地图等 UI 素材
```

当前统计：

- 167 个运行时文件；
- 157 个 WebP、9 个 JPG、1 个 SVG；
- CDN 资源包约 15.60 MB（本地运行时目录已清理）；
- 题库视觉目录共 88 张 WebP（85 张 icon、3 张 scene）；当前 84 个选项引用其中 82 张 icon 和 2 张 scene，另有 4 张历史保留素材；
- 所有图片均小于 300 KB；
- 所有文件名只使用英文、数字、连字符和下划线；
- 资源根目录没有散落文件；
- 不包含 source、staging、preview、缩略图、映射表或生成记录。

### 8.3 图片降级

- 内容图：优先使用同地区图片，再使用通用明信片 SVG；
- 装饰图：失败时隐藏，不阻塞内容；
- 按钮图标：失败时显示字符图标；
- Scratch 覆盖素材：失败时由 Canvas 绘制兜底；
- 世界地图正式图失败时使用 atlas fallback。

## 9. 关键文件职责

| 文件 | 职责 |
|---|---|
| `manifest.ts` | 平台契约、路由和首页卡片 |
| `index.tsx` | 页面组件、根状态和用户动作 |
| `types.ts` | 游戏领域类型 |
| `quizData.ts` | 28 题、84 个选项、地区权重和七轮基线 |
| `data.ts` | 六地区和 50 个目的地 |
| `gameLogic.ts` | 牌组、答题、匹配、目的地分配与幂等收藏 |
| `storage.ts` | v2 存档读取、校验和写入 |
| `ScratchCanvas.tsx` | 刮卡绘制、Pointer 输入和覆盖率检测 |
| `CelebrationCanvas.tsx` | 结果页粒子动画 |
| `assetUrls.ts` | CDN 默认根、环境变量覆盖与资源 URL 生成 |
| `audio.ts` | Web Audio 点击和揭晓音效 |
| `styles.css` | 全页面布局、视觉、响应式与 reduced-motion |

## 10. 已完成验证

截至 2026-08-14，已完成：

- 28 题、84 个选项和七轮题型配比检查；
- 题目牌组、游标和 session 持久化回归；
- 前七轮不重复和新牌组衔接逻辑检查；
- 第四题后地点确定、Scratch/Result 一致性检查；
- reveal 幂等和收藏去重检查；
- 84 个题库选项视觉引用检查；
- 首页封面调整为严格 `694×256`；
- Apia 目的地图片替换为独立的 Vailima / Mount Vaea 构图，避免与 Kingston 视觉重复；
- Welcome 的点击手势使用正式 `welcome-tap-hand.webp`，运行时镜像后指向 `Start the travel quiz` 文案；
- `public` 非运行时美术源文件与交付记录清理；
- 所有运行时图片小于 300 KB；
- 167 个 CDN 文件 HEAD 可访问性验证通过；
- 本地 `public/games/world-scratch-journey/` 已按 workflow 删除；
- ESLint 通过；
- `npm run build` 通过；
- `npm run package:fb -- world-scratch-journey` 通过；
- 最终 CDN 版 FB 包为 141,503 bytes，包内不含本地图片、音频、source、preview、staging 或交付记录；
- 最终 FB 包 SHA-256：`0F5396224391A15D74B982C17173D57D0E1C34BA3A16DCFB72EE88772B6F69EE`。

## 11. 发布状态与剩余流程

游戏功能开发、FB 真机测试和 CDN 资源发布已完成。当前仅剩最终主项目集成、Meta 最终审核与发布流程：

1. 在 360×640、390×844、430×932 视口继续保持手动交互烟测记录；
2. 按主项目集成流程合并游戏模块；
3. 完成 Meta 最终版本上传、审核和发布通知。

CDN 根地址已配置为 `https://d2vfwj9kj1j1h1.cloudfront.net/game_center/world-scratch-journey/`，167 个文件均已通过 HEAD 可访问性验证；本地 `public/games/world-scratch-journey/` 已按 workflow 清理。

## 12. 已知边界

以下是当前实现的真实边界，不应描述为已完成能力：

- Meta 测试版和 CDN 资源发布已完成，最终审核与正式发布仍由集成/发布阶段完成；
- 没有接入真实广告、分享、排行榜或业务埋点；
- 没有游戏级多语言，当前 UI 为英文；
- `soundEnabled` 已持久化，但当前页面没有声音开关入口；
- 页面切入后台时没有专门的 `visibilitychange` / `pagehide` 处理；
- Canvas 尺寸变化会重绘完整覆盖层，可能重置当前刮除进度；
- 刷新不会恢复半途 Quiz 或 Scratch；
- `resultHistory` 当前没有数量上限；
- 题库视觉目录有 4 张不属于当前 84 个选项引用的历史保留素材；
- 当前工作区存在其他游戏和共享文档改动，提交时必须精确限定路径。

## 13. 维护回归清单

修改游戏后至少验证：

### 代码与边界

- [ ] 改动只在当前游戏的 `src` / `public` 目录；
- [ ] Manifest 的 ID、路由、payloadKey 和异步 component 正确；
- [ ] `npx eslint src/games/world-scratch-journey --no-cache` 通过；
- [ ] `npm run build` 通过；
- [ ] 没有新增依赖或共享文件改动。

### Quiz 与结果

- [ ] 题库仍为 28 题；
- [ ] 每轮仍为 2 道 Yes / No + 2 道四选项偏好题；
- [ ] 前七轮不重复；
- [ ] 第四题后进入 Scratch；
- [ ] Scratch 与 Result 使用同一地点；
- [ ] Next stop 创建新 session 并进入下一轮；
- [ ] 同一 session 重复 reveal 不重复收藏。

### 交互与存档

- [ ] 鼠标、触摸和触控笔可以连续刮除；
- [ ] 覆盖率达到 70% 后只触发一次揭晓；
- [ ] 收藏、历史、牌组和游标刷新后保留；
- [ ] 未完成 session 刷新后回到 Welcome；
- [ ] Passport、地图和返回 `/home` 正常；
- [ ] 图片失败时 fallback 不造成白屏或循环报错。

### 资源与发布

- [ ] 首页封面保持 `694×256` 且小于 300 KB；
- [ ] 每张运行时图片小于 300 KB；
- [ ] 资源路径继续统一通过 `assetUrls.ts`；
- [ ] CDN 根地址下全部运行时文件 HEAD 返回 2xx；
- [ ] CDN 验证完成后，本地 `public/games/world-scratch-journey/` 不再保留；
- [ ] FB ZIP 根包含 `index.html`、`assets/`、`fbapp-config.json`；
- [ ] ZIP 不留在最终 Git 提交中。

## 14. 集成方式

游戏继续保持自包含模块结构。需要集成到主项目时，按仓库约定由开发者选择标准脚本：

```bash
npm run integrate -- world-scratch-journey F:/business/framework-project/boredday/project
```

或生成迁移清单：

```bash
npm run export-migration
```

不要手工修改共享 registry 或 Home 页面。真实广告位、CDN 根地址和主项目平台配置由集成与发布阶段统一处理。
