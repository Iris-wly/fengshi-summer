# 颈椎与脊柱姿态监测与康复指导系统：文献总结与论文使用指南

> 项目题目：**基于单目视觉的颈椎与脊柱姿态监测与康复指导系统**  
> 版本：2026-06-26  
> 用途：用于撰写 proposal / poster / final report / dissertation 的 Literature Review、Methodology、Evaluation 与 Discussion 部分。  
> 说明：本整理基于当前文献列表、公开题录/摘要/论文页面信息以及项目目标进行归纳；若后续需要逐句精读或提取精确数值，请进一步阅读 PDF 原文并补充页码。

---

## 0. 总体写作定位

本项目不应被描述为“替代医学影像诊断的颈椎测量系统”，更合适的定位是：

> A low-cost monocular vision-based posture monitoring and rehabilitation guidance system for real-time screening, risk feedback, and exercise quality assessment, rather than a replacement for radiographic cervical diagnosis.

中文表述：

> 本系统面向日常场景下的低成本姿态监测、风险预警和康复动作反馈，不替代影像学诊断；其核心贡献在于将临床常用姿态指标、单目实时人体姿态估计、RGB-D 精度验证和虚拟教练反馈整合为一个闭环系统。

---

## 1. 文献地图：每篇文献在论文中的作用

| 编号 | 文献 | 类型 | 推荐优先级 | 最适合放在论文哪里 | 对本项目的直接价值 |
|---|---|---|---|---|---|
| 1 | Mylonas et al., 2022 | FHP 非放射学测量系统综述 | ★★★★★ | Related Work / Clinical background | 支撑 CVA、摄影测量等非放射学方法用于 FHP 评估 |
| 2 | Carrasco-Uribarren et al., 2023 | 计算机视觉 app 测量 CVA 的可靠性/效度研究 | ★★★★★ | Related Work / Method justification | 直接支撑“普通摄像头/手机 + CVA 测量”的可行性 |
| 3 | Cote et al., 2021 | 视频平台测量 CVA 的 inter/intra-rater reliability | ★★★★☆ | Related Work / Remote assessment | 支撑远程、居家、视频场景下测量 CVA 的合理性 |
| 4 | Oakley et al., 2024 | CVA 与 X-ray 颈椎 sagittal alignment 关系 | ★★★★★ | Discussion / Limitations | 支撑局限性：CVA 不能替代 X-ray 颈椎诊断 |
| 5 | Titcomb et al., 2024 | 坐姿/站姿 CVA 差异与阈值讨论 | ★★★★☆ | Threshold design / Discussion | 支撑 CVA 阈值选择，并说明阈值需按场景校准 |
| 6 | MediaPipe Pose 官方文档 | 技术文档 | ★★★★★ | Methodology | 支撑 33 个 pose landmarks、2D/3D 输出、实时流处理 |
| 7 | BlazePose / BlazePose GHUM Holistic | 单目实时 3D 人体姿态估计 | ★★★★★ | Methodology / Technical background | 支撑 MediaPipe Pose 背后的模型依据 |
| 8 | MediaPipe Face Landmarker 官方文档 | 技术文档 | ★★★★★ | Methodology | 支撑 head pitch/yaw/roll 的提取依据 |
| 9 | Lee et al., 2024 | 3D pose + GCN 识别 Forward Head Posture | ★★★★★ | Related Work / Gap | 与本项目最接近，证明 3D pose 可用于 FHP 识别 |
| 10 | UCO Physical Rehabilitation Dataset, 2023 | 康复动作 RGB + OptiTrack 数据集 | ★★★★☆ | Dataset / Evaluation design | 支撑多视角 RGB 与 motion capture ground truth 的验证范式 |
| 11 | IntelliRehabDS / IRDS, 2021 | Kinect 康复动作数据集 | ★★★★☆ | Related Work / Dataset | 支撑 Kinect/RGB-D 用于康复动作反馈与 correctness label |
| 12 | Mendeley Stroke Rehabilitation Exercise Dataset, 2024 | Kinect v2 + IMU + 评分数据集 | ★★★★☆ | Evaluation / Future work | 支撑动作质量评分、传感器融合和康复数据结构设计 |
| 13 | MobiPhysio, 2026 | 2D 视频物理治疗动作数据集 | ★★★☆☆ | Future work / Dataset | 支撑 2D 视频康复动作评估的最新趋势 |
| 14 | KERAAL Low Back Pain Rehabilitation Dataset | RGB/Kinect/Vicon/OpenPose/BlazePose + 医学标注 | ★★★★★ | Dataset / Validation / Discussion | 支撑比较 Kinect、OpenPose、BlazePose 与医学标注的思路 |
| 15/16 | Yu & Xiong, 2019 | DTW 评估 Kinect 居家康复动作 | ★★★★★ | Rehabilitation module | 直接支撑 DTW 模板匹配和动作质量评分 |
| 17 | AI-based digital patient twins in rehabilitation, 2024 | 数字孪生康复综述 | ★★★★☆ | Digital twin / Discussion | 支撑个性化、远程、实时反馈和数字孪生康复的理论意义 |
| 18 | KneE-PAD, 2025 | 可穿戴传感器康复动作评估数据集 | ★★★☆☆ | Future work / Multimodal extension | 支撑后续 RGB + IMU/sEMG 多模态扩展 |

---

## 2. 主题一：CVA、Forward Head Posture 与非放射学测量

### 2.1 Mylonas et al., 2022  
**题目**：Reliability and Validity of Non-radiographic Methods of Forward Head Posture Measurement: A Systematic Review  
**类别**：系统综述  
**关键词**：Forward Head Posture, non-radiographic measurement, reliability, validity, craniovertebral angle

#### 核心内容
这篇系统综述总结了 forward head posture（FHP）的非放射学测量方法，重点关注不同方法的 reliability 和 validity。对本项目最重要的是，它说明 FHP 不一定只能通过 X-ray 测量，摄影测量、CVA、手机/图像测量等非侵入式方法在临床和研究中已有一定基础。

#### 如何用于论文
可用于支撑：
- 为什么项目选择 **CVA** 作为核心颈椎/头前伸姿态指标；
- 为什么可以使用非放射学、低成本、视觉化的方法做姿态筛查；
- 为什么本项目不是医学诊断系统，而是监测与风险提示系统。

#### 可直接写入论文的句子
> Non-radiographic methods have been widely investigated for forward head posture assessment, with reliability and validity being key considerations when selecting a measurement approach.

中文：
> 既有研究已经系统总结了头前伸姿态的非放射学测量方法，其中测量可靠性和效度是选择评估方法时的核心因素。因此，本研究采用 CVA 等非侵入式指标作为日常姿态监测的基础。

#### 在本项目中的使用方式
- **Introduction**：说明长期低头、头前伸姿态监测的必要性；
- **Related Work**：作为 CVA 与非放射学姿态评估的总引文；
- **Methodology**：说明 CVA 的临床来源；
- **Limitations**：强调视觉估计不能替代影像学诊断。

---

### 2.2 Carrasco-Uribarren et al., 2023  
**题目**：A Computer Vision-Based Application for the Assessment of Head Posture: A Validation and Reliability Study  
**类别**：计算机视觉应用验证研究  
**关键词**：computer vision, smartphone app, CVA, head posture, reliability, validity

#### 核心内容
该研究验证了一个基于计算机视觉的智能手机应用测量 CVA 的可靠性与效度。研究对象包括健康人、颈痛患者和紧张型头痛患者，并评估 test-retest reliability、inter-rater reliability 和 concurrent validity。

#### 如何用于论文
这是最贴近你项目的一篇 CVA + computer vision 文献。它可以用来证明：
- 普通手机/摄像头图像可以用于头部姿态评估；
- CVA 可作为计算机视觉系统输出的可解释指标；
- 本项目在此基础上进一步扩展为实时监测、时序记录、风险分级和康复反馈。

#### 可直接写入论文的句子
> Previous work has demonstrated that a computer vision-based smartphone application can achieve reliable and valid measurement of the craniovertebral angle, suggesting the feasibility of low-cost image-based head posture assessment.

中文：
> 已有研究表明，基于计算机视觉的手机应用能够较可靠地测量颅椎角，这为本项目使用普通摄像头进行低成本头部姿态评估提供了直接依据。

#### 在本项目中的使用方式
- **Related Work**：说明 CV app 测量 CVA 的研究基础；
- **Methodology**：说明本项目沿用 CVA，但采用实时关键点追踪而非单张照片；
- **Gap**：强调该文更偏静态 app 测量，本项目增加实时风险反馈和康复指导。

---

### 2.3 Cote et al., 2021  
**题目**：Inter and Intra-Rater Reliability of Measuring Photometric Craniovertebral Angle Using a Cloud-Based Video Communication Platform  
**类别**：远程视频测量可靠性研究  
**关键词**：telehealth, CVA, photometric measurement, reliability

#### 核心内容
该研究考察了通过云端视频通信平台测量 photometric CVA 的 inter-rater 和 intra-rater reliability。它与居家监测和远程康复场景高度相关。

#### 如何用于论文
可用于支持：
- CVA 可以在远程视频条件下测量；
- 居家康复系统不一定依赖昂贵实验室设备；
- 视频平台/摄像头环境仍可产生可用的姿态评估指标。

#### 可直接写入论文的句子
> Telehealth-based photometric measurement of CVA has shown acceptable inter- and intra-rater reliability, supporting the feasibility of remote posture assessment.

中文：
> 远程视频平台上的 CVA 测量已被证明具有可接受的评分者间和评分者内可靠性，这支持了本项目面向居家场景进行姿态监测的可行性。

#### 在本项目中的使用方式
- **Introduction**：说明远程姿态评估的应用价值；
- **Related Work**：连接 CVA 与 telerehabilitation；
- **Discussion**：说明实际部署时仍需考虑光线、摄像头角度、距离等因素。

---

### 2.4 Oakley et al., 2024  
**题目**：Two Methods of Forward Head Posture Assessment: Radiography vs Posture and Their Clinical Comparison  
**类别**：CVA 与 X-ray 放射学参数对比研究  
**关键词**：CVA, radiography, C2-C7 SVA, cervical lordosis, sagittal alignment

#### 核心内容
该研究比较了 CVA 与 X-ray 中的 C2-C7 sagittal vertical axis、颈椎前凸等放射学指标之间的关系。对本项目非常重要的一点是：CVA 与放射学颈椎排列存在一定联系，但不能被理解为完全等价或可替代。

#### 如何用于论文
这篇文献最适合放在 **Discussion / Limitations**：
- 说明本系统不做医学影像诊断；
- CVA 是姿态筛查指标，不是颈椎病诊断指标；
- 使用 RGB-D ground truth 验证几何估计误差，但这仍不同于 X-ray 诊断。

#### 可直接写入论文的句子
> Although CVA is a clinically relevant postural indicator, it should not be treated as a direct substitute for radiographic cervical alignment parameters.

中文：
> 尽管 CVA 是具有临床相关性的姿态指标，但它不能被视为放射学颈椎排列参数的直接替代。因此，本系统定位为日常姿态风险监测和康复反馈工具，而非医学诊断设备。

#### 在本项目中的使用方式
- **Limitations**：防止过度 claim；
- **Ethical / Safety statement**：说明需要专业医疗人员诊断；
- **Evaluation**：解释为什么用 RGB-D 验证的是系统测量精度，而不是诊断效度。

---

### 2.5 Titcomb et al., 2024  
**题目**：Evaluation of the Craniovertebral Angle in Standing versus Sitting Positions in Young Adults with and without Severe Forward Head Posture  
**类别**：CVA 体位差异与阈值讨论  
**关键词**：CVA, sitting, standing, forward head posture, threshold

#### 核心内容
该研究关注坐姿与站姿对 CVA 的影响，并讨论正常头姿与 FHP 的 CVA 参考范围。文献中常见阈值并不完全统一，有的研究将 CVA < 50° 视为 FHP，也有研究把 >53° 或 ≥55° 作为正常头姿参考。

#### 如何用于论文
这篇文献可以直接支持你的风险阈值设计：
- `< 50°` 作为提醒阈值；
- `< 45°` 作为高风险阈值；
- 但必须说明这些阈值应通过实验数据进一步校准，尤其是你的系统是坐姿侧面场景。

#### 可直接写入论文的句子
> Because reported CVA thresholds vary across populations and measurement conditions, the thresholds in this system are used as engineering risk indicators rather than diagnostic cut-offs.

中文：
> 由于不同研究对 CVA 正常值和 FHP 阈值的设定并不完全一致，本项目中的阈值主要作为工程化风险预警标准，而非医学诊断分界值。

#### 在本项目中的使用方式
- **Methodology**：风险评分规则的文献依据；
- **Discussion**：说明坐姿/站姿差异可能影响阈值；
- **Future Work**：使用更多被试数据个性化校准阈值。

---

## 3. 主题二：单目视觉、MediaPipe 与 Forward Head Posture 识别

### 3.1 MediaPipe Pose 官方文档  
**类别**：官方技术文档  
**关键词**：MediaPipe Pose Landmarker, 33 landmarks, image coordinates, world coordinates, real-time stream

#### 核心内容
MediaPipe Pose Landmarker 可以在图像、视频和实时流中检测人体关键点，输出 2D 图像坐标和 3D world coordinates。它适合作为本项目实时姿态监测的感知层。

#### 如何用于论文
支撑技术路线：
- 为什么选择 MediaPipe Pose；
- 关键点来源：耳、肩、髋等；
- 如何从关键点计算 CVA、头前伸距离、躯干前倾；
- 为什么系统可以在普通摄像头上实时运行。

#### 可直接写入论文的句子
> MediaPipe Pose Landmarker provides body pose landmarks in both image coordinates and three-dimensional world coordinates, enabling real-time extraction of posture-related geometric features from monocular RGB input.

中文：
> MediaPipe Pose Landmarker 能够从单目 RGB 输入中输出人体关键点的图像坐标和三维坐标，因此可用于实时提取与姿态相关的几何特征。

---

### 3.2 BlazePose / BlazePose GHUM Holistic  
**题目**：BlazePose: On-device Real-time Body Pose Tracking / BlazePose GHUM Holistic: Real-time 3D Human Landmarks and Pose Estimation  
**类别**：姿态估计模型论文  
**关键词**：BlazePose, GHUM, monocular RGB, real-time, 3D human landmarks

#### 核心内容
BlazePose 是 MediaPipe Pose 的核心模型之一，面向移动端实时人体姿态估计。BlazePose GHUM Holistic 进一步扩展到从单目 RGB 图像估计 3D 人体 landmarks，并支持 avatar control、fitness tracking、AR/VR 等应用。

#### 如何用于论文
这部分用于支撑本项目的核心技术可行性：
- 单目 RGB 可以产生可用于分析的人体骨架表示；
- 实时姿态估计适合居家姿态监测；
- 3D landmarks 可用于 3D avatar 映射和康复反馈。

#### 可直接写入论文的句子
> BlazePose and BlazePose GHUM demonstrate that lightweight monocular pose estimation can provide real-time 2D/3D body landmarks, making it suitable for low-cost posture monitoring and avatar-based feedback.

中文：
> BlazePose 系列模型表明，轻量级单目姿态估计可以实时输出 2D/3D 人体关键点，这使其适合用于低成本姿态监测和虚拟化身反馈。

#### 在本项目中的使用方式
- **Methodology**：解释姿态估计模型；
- **System Pipeline**：感知层；
- **Discussion**：说明单目 3D landmarks 是估计值，不是真实深度测量。

---

### 3.3 MediaPipe Face Landmarker 官方文档  
**类别**：官方技术文档  
**关键词**：Face Landmarker, facial transformation matrix, head pose, pitch, yaw, roll

#### 核心内容
Face Landmarker 可以输出面部 3D landmarks、blendshape scores 和 facial transformation matrix。对本项目而言，最重要的是可以用 face transformation matrix 估计头部姿态角，尤其是 head pitch。

#### 如何用于论文
支撑你项目中 `head pitch` 指标：
- MediaPipe Pose 没有直接提供颈椎角度；
- Face Landmarker 可补充头部姿态估计；
- head pitch 反映低头/抬头程度，可与 CVA 形成互补。

#### 可直接写入论文的句子
> Since body pose landmarks do not directly encode cervical spine angles, MediaPipe Face Landmarker is used to estimate head pitch from the facial transformation matrix as a complementary indicator of neck flexion.

中文：
> 由于人体姿态关键点无法直接表示颈椎角度，本项目使用 MediaPipe Face Landmarker 的头部变换矩阵估计 head pitch，作为低头程度的补充指标。

---

### 3.4 Lee et al., 2024  
**题目**：Recognition of Forward Head Posture Through 3D Human Pose Estimation With a Graph Convolutional Network: Development and Feasibility Study  
**类别**：FHP 识别模型研究  
**关键词**：Forward Head Posture, 3D human pose estimation, GCN, posture recognition

#### 核心内容
该研究使用 2D 图像输入和 3D human pose estimation 关节输入，通过 GCN 学习 FHP 相关特征，实现头前伸姿态识别。该文与你项目最接近，因为它同样把 3D human pose estimation 用于 FHP 识别。

#### 如何用于论文
这篇文献适合用于说明：
- 单目/图像姿态估计可以捕捉 FHP 相关特征；
- skeleton-based learning 可用于姿态风险分类；
- 你的项目区别在于采用可解释几何指标 + 实时反馈 + 康复动作指导，而不是仅做分类模型。

#### 可直接写入论文的句子
> Recent work has shown that FHP-related features can be learned from 3D human pose estimation outputs using graph convolutional networks, supporting the feasibility of skeleton-based FHP recognition.

中文：
> 近期研究表明，基于 3D 人体姿态估计输出的骨架数据可以学习到头前伸相关特征，这支持了本项目使用人体关键点进行 FHP 风险识别的可行性。

#### 在本项目中的使用方式
- **Related Work**：最直接相关工作；
- **Gap**：该研究偏模型识别，本项目强调可解释指标、实时监测和康复指导闭环；
- **Future Work**：后续可把规则阈值升级为 GCN/LSTM/Transformer 模型。

---

## 4. 主题三：RGB-D / Kinect / 数据集与 Ground Truth 验证

### 4.1 UCO Physical Rehabilitation Dataset, 2023  
**类别**：多视角 RGB + OptiTrack ground truth 康复数据集  
**关键词**：physical rehabilitation, RGB cameras, OptiTrack, human pose estimation, dataset

#### 核心内容
UCO Physical Rehabilitation 数据集包含 27 名受试者执行 8 类康复动作，使用 5 个 RGB 摄像头从不同视角拍摄，并使用 OptiTrack 红外 motion capture 系统作为 ground truth。

#### 如何用于论文
非常适合支持你的实验设计：
- 单目 RGB 姿态估计需要 ground truth 验证；
- 多视角/不同摄像头视角会影响姿态估计结果；
- OptiTrack/RGB-D/运动捕捉可作为高精度参考。

#### 可直接写入论文的句子
> Existing rehabilitation datasets often combine RGB videos with high-accuracy motion capture systems, such as OptiTrack, to evaluate the performance of human pose estimation methods under different camera viewpoints.

中文：
> 既有康复数据集常将 RGB 视频与 OptiTrack 等高精度运动捕捉系统结合，用于评估不同摄像头视角下人体姿态估计方法的表现。

#### 在本项目中的使用方式
- **Evaluation Design**：支撑 RGB-D/高精度传感器作为 ground truth；
- **Robustness Test**：支撑不同距离、光线、视角的鲁棒性测试；
- **Future Work**：可考虑多视角扩展。

---

### 4.2 IntelliRehabDS / IRDS, 2021  
**题目**：A Dataset of Physical Rehabilitation Movements  
**类别**：Kinect 康复动作数据集  
**关键词**：Kinect, rehabilitation movement, correctness label, automatic feedback

#### 核心内容
IntelliRehabDS 包含 29 名被试，其中 15 名患者和 14 名健康人，记录 9 类康复动作。数据使用 Kinect 采集，包含 3D 关节点坐标，并带有动作类型和正确性标注。

#### 如何用于论文
可用于支撑：
- Kinect / RGB-D skeleton 数据在康复动作评估中的常见使用；
- 运动正确性标注可用于训练或验证动作质量评估模型；
- 自动反馈是居家康复系统的重要目标。

#### 可直接写入论文的句子
> Kinect-based rehabilitation datasets provide 3D joint trajectories and correctness labels, which are commonly used to develop automatic feedback systems for rehabilitation exercises.

中文：
> Kinect 康复数据集通常提供 3D 关节轨迹和动作正确性标签，可用于开发自动康复动作反馈系统。

#### 在本项目中的使用方式
- **Related Work**：康复动作数据集背景；
- **Evaluation**：说明 ground truth skeleton 和 correctness labels 的价值；
- **Methodology**：借鉴动作正确性标注和动作类型分类。

---

### 4.3 Mendeley Stroke Rehabilitation Exercise Dataset, 2024  
**类别**：Kinect v2 + IMU + performance score 数据集  
**关键词**：stroke rehabilitation, Kinect v2, IMU, skeleton data, performance score

#### 核心内容
该数据集包含 128 名参与者的 IMU 数据与 Kinect v2 skeleton 数据，并包含 performance scores。对你的第二阶段动作质量评分非常有启发意义。

#### 如何用于论文
可用于支持：
- 动作质量不仅可以做 correct/incorrect 二分类，也可以输出连续评分；
- Kinect skeleton 与 IMU 可融合用于更稳定的动作评估；
- 对康复动作评估而言，performance score 是比单纯动作识别更有价值的输出。

#### 可直接写入论文的句子
> Rehabilitation datasets with both skeleton trajectories and performance scores indicate the importance of moving beyond exercise recognition toward quantitative exercise quality assessment.

中文：
> 同时包含骨架轨迹和动作表现评分的康复数据集表明，康复系统不应只识别动作类别，还应进一步量化动作质量。

#### 在本项目中的使用方式
- **Rehabilitation module**：动作质量评分设计；
- **Future Work**：RGB + IMU 融合；
- **User Study**：将系统评分与专家评分对比。

---

### 4.4 MobiPhysio, 2026  
**题目**：A 2D video dataset of physiotherapy exercises for AI-driven assessment and monitoring  
**类别**：2D 视频康复动作数据集  
**关键词**：2D video, physiotherapy, assessment, monitoring, AI-driven rehabilitation

#### 核心内容
MobiPhysio 是面向 AI 物理治疗评估与监测的 2D 视频数据集。它的重要性在于：它说明普通 2D 视频数据正在成为康复动作评估的重要数据来源，而不一定完全依赖昂贵的 MoCap 或 RGB-D 设备。

#### 如何用于论文
可用于支撑：
- 使用普通 RGB 摄像头做康复动作监测具有研究趋势；
- 居家场景下 2D 视频数据更容易获取；
- 未来可用公开 2D physiotherapy 数据集做预训练或 benchmark。

#### 可直接写入论文的句子
> Recent 2D video-based physiotherapy datasets highlight a growing trend toward low-cost, camera-based rehabilitation monitoring in realistic environments.

中文：
> 近期 2D 视频物理治疗数据集表明，低成本摄像头驱动的康复动作监测正在成为一个重要研究方向。

#### 在本项目中的使用方式
- **Future Work**：扩展到公开 2D 视频数据集；
- **Discussion**：说明低成本居家康复的研究趋势；
- **Dataset section**：如果使用外部数据集，可作为候选。

---

### 4.5 KERAAL Low Back Pain Rehabilitation Dataset  
**类别**：医疗康复动作数据集，含 RGB/Kinect/Vicon/OpenPose/BlazePose 与医学标注  
**关键词**：low back pain, rehabilitation, Kinect, Vicon, OpenPose, BlazePose, medical annotation

#### 核心内容
KERAAL 数据集包含 RGB 视频、Kinect skeleton、Vicon skeleton、OpenPose、BlazePose 以及医学标注。它的价值在于同时包含真实传感器数据、视觉姿态估计输出和医学评价标注，非常适合作为“如何验证姿态估计系统”的参考。

#### 如何用于论文
可用于支持：
- 将 BlazePose/OpenPose 与 Kinect/Vicon 进行比较是合理的；
- 医学标注对康复动作质量评估很重要；
- 本项目使用 RGB-D 作为 ground truth 的思路与已有数据集设计一致。

#### 可直接写入论文的句子
> Datasets such as KERAAL demonstrate the value of combining RGB video, depth-based skeletons, marker-based motion capture, pose estimation outputs, and medical annotations for rehabilitation movement analysis.

中文：
> KERAAL 等数据集展示了将 RGB 视频、深度骨架、运动捕捉、姿态估计输出和医学标注结合用于康复动作分析的价值。

#### 在本项目中的使用方式
- **Evaluation**：借鉴多源 ground truth 设计；
- **Discussion**：说明未来可加入医学标注；
- **Future Work**：与物理治疗师合作进行动作错误标注。

---

## 5. 主题四：康复动作质量评分、DTW、虚拟教练与数字孪生

### 5.1 Yu & Xiong, 2019  
**题目**：A Dynamic Time Warping Based Algorithm to Evaluate Kinect-Enabled Home-Based Physical Rehabilitation Exercises for Older People  
**类别**：康复动作质量评估方法  
**关键词**：DTW, Kinect, home-based rehabilitation, virtual coach, exercise quality

#### 核心内容
该研究使用 Dynamic Time Warping（DTW）比较用户动作序列与标准动作序列，评估 Kinect 居家康复动作质量，并支持 virtual gaming / auto-coaching 场景。

#### 如何用于论文
这篇是你第二阶段最关键的方法文献之一。它直接支撑：
- 使用 DTW 做标准模板与用户动作序列匹配；
- 不同用户动作速度不同，DTW 可以对齐时间差异；
- 动作质量可从轨迹相似性、角度偏差、完整度等方面评分。

#### 可直接写入论文的句子
> Dynamic Time Warping is suitable for rehabilitation exercise assessment because it can compare a user’s motion trajectory with a reference template while allowing temporal variations in execution speed.

中文：
> DTW 适合用于康复动作评估，因为它可以在允许动作速度差异的情况下，将用户动作轨迹与标准模板进行时序对齐和相似度比较。

#### 在本项目中的使用方式
- **Stage 2 Methodology**：动作模板匹配；
- **Quality Score**：角度偏差、速度、完整度评分；
- **Feedback**：将误差最大的关节或动作阶段高亮显示。

#### 可设计的评分公式
可以参考以下工程化设计：

```text
Quality Score = 100 
                - w1 * normalized_angle_error
                - w2 * normalized_DTW_distance
                - w3 * incompleteness_penalty
                - w4 * speed_penalty
```

其中：
- `normalized_angle_error`：用户动作角度与标准角度的平均偏差；
- `normalized_DTW_distance`：用户序列与模板序列的 DTW 距离；
- `incompleteness_penalty`：动作幅度不足惩罚；
- `speed_penalty`：动作过快或过慢惩罚。

---

### 5.2 Tsiouris et al., 2020  
**题目**：A Review of Virtual Coaching Systems in Healthcare: Closing the Loop With Real-Time Feedback  
**类别**：医疗虚拟教练综述  
**关键词**：virtual coach, healthcare, sensing, real-time feedback, closed-loop system

#### 核心内容
该综述总结了医疗虚拟教练系统，强调 sensing technology、user interaction 和 real-time feedback 的结合。标题中的 “closing the loop” 对你的项目很重要：系统不应只是记录数据，而应根据数据给出反馈。

#### 如何用于论文
可用于支撑：
- 虚拟教练需要感知、评估、反馈闭环；
- 康复系统需要实时或准实时反馈；
- 本项目从监测模块扩展到康复指导模块具有合理性。

#### 可直接写入论文的句子
> Virtual coaching systems in healthcare aim to close the loop between sensing, interpretation, and personalized feedback, which motivates the integration of real-time posture monitoring with corrective guidance.

中文：
> 医疗虚拟教练系统的核心目标是将感知、理解和个性化反馈形成闭环，这为本项目将实时姿态监测与纠正指导结合提供了理论依据。

#### 在本项目中的使用方式
- **Related Work**：虚拟教练背景；
- **System Design**：闭环系统设计；
- **Discussion**：说明本项目从姿态监测到康复指导的延展价值。

---

### 5.3 AI-based Digital Patient Twins in Rehabilitation, 2024  
**题目**：Applications of Artificial Intelligence-Based Patient Digital Twins in Decision Support in Rehabilitation and Physical Therapy  
**类别**：AI 数字孪生康复综述  
**关键词**：digital patient twin, rehabilitation, physical therapy, personalization, decision support

#### 核心内容
该综述强调 AI-based patient digital twins 在康复和物理治疗中的潜力，包括个性化治疗计划、远程康复、实时监测和进展可视化。

#### 如何用于论文
可用于支撑你的 Unity avatar / digital twin coach 部分：
- avatar 不只是动画展示，而是用户姿态状态的数字化表示；
- 长期记录可以形成个性化康复档案；
- 可根据用户活动范围和表现调整反馈。

#### 可直接写入论文的句子
> AI-based digital patient twins can support rehabilitation by enabling personalized monitoring, simulation, and adaptive feedback based on patient-specific data.

中文：
> 基于 AI 的患者数字孪生可以通过个体化监测、状态模拟和自适应反馈支持康复过程。

#### 在本项目中的使用方式
- **Stage 2**：Unity 3D avatar 的理论支撑；
- **Future Work**：个性化关节活动范围建模；
- **Discussion**：把系统从“姿态检测工具”提升为“数字孪生康复教练”。

---

### 5.4 KneE-PAD, 2025  
**题目**：A Knee Rehabilitation Exercises Dataset for Postural Assessment using Wearable Devices  
**类别**：可穿戴设备康复动作评估数据集  
**关键词**：knee rehabilitation, IMU, sEMG, postural assessment, virtual coach

#### 核心内容
KneE-PAD 是用于膝关节康复动作姿态评估的数据集，包含 IMU 和 sEMG 等可穿戴传感器数据。虽然它不是颈椎或脊柱方向，但可以支持多模态康复评估和虚拟教练反馈的未来扩展。

#### 如何用于论文
可用于：
- Future Work：加入 IMU 或肌电传感器；
- Discussion：单目视觉容易受遮挡和视角影响，多模态可提升鲁棒性；
- Rehabilitation：动作正确性不仅由几何角度决定，也可能与肌肉激活模式有关。

#### 可直接写入论文的句子
> Wearable-device rehabilitation datasets suggest that future systems may combine vision-based posture estimation with inertial or physiological signals to improve robustness and assessment quality.

中文：
> 可穿戴康复数据集表明，未来系统可以将视觉姿态估计与惯性或生理信号结合，以提升鲁棒性和动作评估质量。

---

## 6. 论文 Related Work 推荐结构

### 6.1 第一段：临床姿态指标与 CVA
写作目的：说明为什么 CVA 是合理指标。

可写内容：
- FHP 是常见颈部姿态问题；
- CVA 是常用非放射学评估指标；
- 非放射学方法已有 reliability / validity 研究；
- 但阈值会受体位、测量方式和人群影响。

可引用：
- Mylonas et al., 2022
- Titcomb et al., 2024
- Oakley et al., 2024

推荐句：
> The craniovertebral angle has been widely used as a non-radiographic indicator of forward head posture. However, reported thresholds vary across studies and measurement conditions, suggesting that CVA-based warnings should be interpreted as risk indicators rather than diagnostic labels.

---

### 6.2 第二段：视觉化 CVA 测量与远程姿态评估
写作目的：说明普通摄像头/视频测量可行。

可写内容：
- 手机 app / 计算机视觉已经用于 CVA 测量；
- 视频平台也可进行 photometric CVA 测量；
- 既有研究多偏静态测量，本项目强调实时监测和持续记录。

可引用：
- Carrasco-Uribarren et al., 2023
- Cote et al., 2021

推荐句：
> Prior studies have validated image- or video-based CVA measurement, but most existing systems focus on static assessment rather than continuous real-time monitoring and interactive feedback.

---

### 6.3 第三段：单目人体姿态估计与 MediaPipe
写作目的：说明技术路线可靠。

可写内容：
- MediaPipe Pose / BlazePose 可实时输出人体关键点；
- Face Landmarker 可补充头部姿态；
- 单目 3D landmarks 是估计值，需要 ground truth 验证。

可引用：
- MediaPipe Pose docs
- BlazePose / BlazePose GHUM
- MediaPipe Face Landmarker docs
- Lee et al., 2024

推荐句：
> Lightweight monocular pose estimation models such as BlazePose make it possible to extract body landmarks in real time from RGB input, enabling low-cost posture monitoring outside laboratory environments.

---

### 6.4 第四段：康复动作数据集与 ground truth 验证
写作目的：说明为什么需要 RGB-D / Kinect / motion capture 做验证。

可写内容：
- 康复动作数据集常使用 Kinect、OptiTrack、Vicon；
- 骨架轨迹与 correctness labels 可用于动作质量评估；
- 本项目使用 RGB-D ground truth 验证单目估计误差是合理的。

可引用：
- UCO Physical Rehabilitation Dataset
- IntelliRehabDS
- Mendeley Stroke Rehabilitation Exercise Dataset
- KERAAL

推荐句：
> Rehabilitation datasets often combine RGB video with depth-based or marker-based motion capture data, providing a practical evaluation paradigm for validating vision-based pose estimation against more reliable ground truth sources.

---

### 6.5 第五段：虚拟教练、DTW 与数字孪生康复
写作目的：支撑第二阶段系统扩展。

可写内容：
- DTW 可用于用户动作与标准模板的时序匹配；
- 虚拟教练强调感知-评估-反馈闭环；
- 数字孪生可用于个性化康复和长期监测。

可引用：
- Yu & Xiong, 2019
- Tsiouris et al., 2020
- AI-based digital patient twins in rehabilitation, 2024
- KneE-PAD, 2025

推荐句：
> For rehabilitation guidance, DTW-based template matching and virtual coaching systems provide a foundation for evaluating exercise quality and delivering personalized corrective feedback.

---

## 7. 本项目可以提炼出的 Research Gap

结合上述文献，可以把研究缺口写成：

1. **临床指标与实时视觉系统之间存在断层**  
   CVA 等指标在临床和摄影测量中已有基础，但很多研究仍偏静态测量或人工标注。

2. **单目姿态估计系统需要 ground truth 验证**  
   MediaPipe/BlazePose 可以实时输出关键点，但其 3D landmarks 并不等同于真实深度，因此需要与 RGB-D 或 motion capture 数据对比。

3. **现有 FHP 研究多做分类，缺少完整反馈闭环**  
   例如基于 GCN 的 FHP 识别可以判断姿态类别，但通常不提供面向用户的实时可视化纠正建议。

4. **康复指导需要从动作识别走向动作质量评估**  
   康复系统不仅要识别用户是否完成某个动作，还要评估角度、速度、完整度和左右对称性。

5. **数字孪生/虚拟教练需要结合个体化数据**  
   Unity avatar 不应只是可视化骨架，而应结合用户个人 ROM、历史数据和动作表现进行个性化反馈。

推荐 research gap 表述：

> Although CVA-based posture assessment, monocular pose estimation, and virtual rehabilitation coaching have each been investigated separately, few systems integrate real-time monocular estimation of clinically interpretable cervical and spinal posture indicators, RGB-D based accuracy validation, and personalized avatar-based rehabilitation feedback into a single closed-loop framework.

中文：

> 尽管 CVA 姿态评估、单目人体姿态估计和虚拟康复教练分别已有研究基础，但目前仍缺少一个将临床可解释的颈椎/脊柱姿态指标实时估计、RGB-D 精度验证和个性化虚拟化身康复反馈整合在一起的闭环系统。

---

## 8. 如何把文献对应到你论文的章节

### 8.1 Introduction
使用文献：
- Mylonas et al., 2022
- Carrasco-Uribarren et al., 2023
- Tsiouris et al., 2020
- AI-based digital patient twins, 2024

写作目标：
- 说明姿态问题普遍；
- 说明低成本、居家、实时监测有价值；
- 引出单目视觉系统的必要性。

---

### 8.2 Related Work
建议分小节：

#### 2.1 Forward Head Posture and CVA Assessment
引用：
- Mylonas et al., 2022
- Titcomb et al., 2024
- Oakley et al., 2024

#### 2.2 Vision-Based Posture Assessment
引用：
- Carrasco-Uribarren et al., 2023
- Cote et al., 2021
- Lee et al., 2024

#### 2.3 Monocular Human Pose Estimation
引用：
- MediaPipe Pose docs
- BlazePose / BlazePose GHUM
- MediaPipe Face Landmarker docs

#### 2.4 Rehabilitation Exercise Assessment and Virtual Coaching
引用：
- Yu & Xiong, 2019
- Tsiouris et al., 2020
- IntelliRehabDS
- KERAAL
- AI-based digital patient twins, 2024

---

### 8.3 Methodology
使用文献：
- MediaPipe Pose docs
- BlazePose / BlazePose GHUM
- MediaPipe Face Landmarker docs
- Titcomb et al., 2024
- Yu & Xiong, 2019

写作目标：
- 说明输入：侧面单目 RGB；
- 说明关键点：耳、肩、髋、头部姿态；
- 说明指标：CVA、head pitch、head-forward displacement、trunk inclination；
- 说明风险评分规则；
- 说明康复动作模板匹配与评分。

---

### 8.4 Evaluation
使用文献：
- UCO Physical Rehabilitation Dataset
- IntelliRehabDS
- Mendeley Stroke Rehabilitation Dataset
- KERAAL

写作目标：
- 说明为什么使用 RGB-D sensor 作为 ground truth；
- 说明评价指标：MAE、Pearson correlation、Bland-Altman plot、ICC；
- 说明鲁棒性测试：光线、距离、体型、摄像头角度。

---

### 8.5 Discussion / Limitations
使用文献：
- Oakley et al., 2024
- Titcomb et al., 2024
- KERAAL
- KneE-PAD

写作目标：
- 说明 CVA 不是 X-ray 替代；
- 说明单目深度估计存在误差；
- 说明阈值需个体化；
- 说明可扩展 RGB + IMU / 多摄像头 / 医学标注。

---

## 9. 推荐论文中使用的核心论点

### 论点 1：CVA 是合适但有限的指标
> CVA 是常用的 FHP 非放射学指标，但其阈值受体位、人群和测量条件影响，因此适合作为风险预警指标，而非诊断标准。

支持文献：
- Mylonas et al., 2022
- Titcomb et al., 2024
- Oakley et al., 2024

---

### 论点 2：普通摄像头用于头部姿态测量是可行的
> 既有研究已验证基于计算机视觉的 CVA 测量和远程视频 CVA 测量具有一定可靠性，因此单目 RGB 摄像头具有低成本姿态监测潜力。

支持文献：
- Carrasco-Uribarren et al., 2023
- Cote et al., 2021

---

### 论点 3：MediaPipe 适合作为实时感知模块
> MediaPipe/BlazePose 支持从 RGB 输入实时提取人体关键点，Face Landmarker 可补充头部姿态角，因此适合构建轻量级实时姿态监测原型。

支持文献：
- MediaPipe Pose docs
- BlazePose / BlazePose GHUM
- MediaPipe Face Landmarker docs

---

### 论点 4：系统必须进行 ground truth 验证
> 单目 3D landmarks 是模型估计结果，不是真实深度测量，因此需要使用 RGB-D、Kinect、OptiTrack 或 Vicon 等作为 ground truth 进行误差验证。

支持文献：
- UCO Physical Rehabilitation Dataset
- IntelliRehabDS
- KERAAL

---

### 论点 5：康复指导应从识别走向评分和反馈
> 康复系统不仅要识别动作类别，还应评价动作质量，并通过虚拟教练或数字孪生形式向用户提供纠正建议。

支持文献：
- Yu & Xiong, 2019
- Tsiouris et al., 2020
- AI-based digital patient twins, 2024
- KneE-PAD, 2025

---

## 10. 建议的引用优先级

### 必须引用
1. Mylonas et al., 2022  
2. Carrasco-Uribarren et al., 2023  
3. MediaPipe Pose docs / BlazePose  
4. Lee et al., 2024  
5. Oakley et al., 2024  
6. Yu & Xiong, 2019  
7. KERAAL 或 UCO dataset  

### 有空间就引用
8. Cote et al., 2021  
9. Titcomb et al., 2024  
10. IntelliRehabDS  
11. Tsiouris et al., 2020  
12. AI-based digital patient twins, 2024  

### 放在 Future Work 更合适
13. Mendeley Stroke Rehabilitation Dataset  
14. MobiPhysio  
15. KneE-PAD  

---

## 11. 可以直接放进论文的 Related Work 草稿

### 英文版

Forward head posture has commonly been assessed using non-radiographic postural indicators such as the craniovertebral angle (CVA). Previous reviews have highlighted the importance of reliability and validity when selecting non-radiographic FHP measurement methods. Image-based and video-based approaches have further shown that CVA can be measured using computer vision or remote video platforms with acceptable reliability, suggesting the feasibility of low-cost head posture assessment outside clinical laboratories. However, CVA thresholds vary across studies and measurement conditions, and CVA should not be considered a direct replacement for radiographic cervical alignment parameters.

Recent advances in monocular human pose estimation make it possible to extract body landmarks from RGB images in real time. MediaPipe Pose and BlazePose provide lightweight body landmark estimation suitable for on-device applications, while Face Landmarker can provide complementary head pose information. These tools enable the extraction of interpretable posture indicators such as CVA, head pitch, head-forward displacement, and trunk inclination. Nevertheless, monocular 3D landmarks are model-based estimates rather than true depth measurements, so validation against RGB-D or motion-capture ground truth remains necessary.

For rehabilitation guidance, prior work has used Kinect, RGB-D sensors, and motion-capture systems to collect skeleton trajectories and correctness labels for exercise assessment. DTW-based methods have been used to compare user motion with reference templates while allowing temporal differences in movement speed. Virtual coaching and digital patient twin research further suggests that effective rehabilitation systems should close the loop between sensing, interpretation, and personalized feedback. Building on these studies, this project integrates monocular posture monitoring, RGB-D accuracy validation, and avatar-based rehabilitation feedback into a single low-cost closed-loop system.

### 中文版

头前伸姿态通常可以通过颅椎角（CVA）等非放射学姿态指标进行评估。已有综述指出，在选择头前伸测量方法时，可靠性和效度是关键因素。基于图像或视频的研究进一步表明，计算机视觉应用和远程视频平台均可用于 CVA 测量，并具有一定可靠性，这说明低成本摄像头在非实验室环境下进行头部姿态评估具有可行性。然而，不同研究中的 CVA 阈值会受体位、人群和测量条件影响，同时 CVA 也不能被视为放射学颈椎排列参数的直接替代。

近年来，单目人体姿态估计的发展使得系统可以从 RGB 图像中实时提取人体关键点。MediaPipe Pose 和 BlazePose 提供了适合移动端和实时应用的轻量级人体关键点估计能力，而 Face Landmarker 可以补充头部姿态角信息。这些工具使系统能够提取 CVA、head pitch、头前伸距离和躯干前倾等可解释姿态指标。然而，单目 3D landmarks 本质上是模型估计结果，并不等同于真实深度测量，因此仍需要使用 RGB-D 或运动捕捉数据进行精度验证。

在康复指导方面，已有研究使用 Kinect、RGB-D 和 motion capture 系统采集骨架轨迹与动作正确性标签，用于康复动作评估。DTW 方法可以在允许动作速度差异的情况下比较用户动作序列与标准动作模板。虚拟教练和患者数字孪生研究进一步指出，有效的康复系统应将感知、理解和个性化反馈形成闭环。基于这些研究，本项目将单目姿态监测、RGB-D 精度验证和虚拟化身康复反馈整合为一个低成本闭环系统。

---

## 12. 参考文献整理清单

> 以下为建议你在 Zotero / Mendeley / EndNote 中统一整理的条目。正式论文中请按学校要求使用 Harvard / IEEE / APA 等格式重新导出。

1. Mylonas, K., Tsekoura, M., Billis, E., Aggelopoulos, P., Tsepis, E., & Fousekis, K. (2022). *Reliability and Validity of Non-radiographic Methods of Forward Head Posture Measurement: A Systematic Review*. Cureus, 14(8), e27696. https://doi.org/10.7759/cureus.27696

2. Carrasco-Uribarren, A., et al. (2023). *A Computer Vision-Based Application for the Assessment of Head Posture: A Validation and Reliability Study*. Applied Sciences, 13(6), 3910. https://doi.org/10.3390/app13063910

3. Cote, R., et al. (2021). *Inter and Intra-Rater Reliability of Measuring Photometric Craniovertebral Angle Using a Cloud-Based Video Communication Platform*. International Journal of Telerehabilitation.

4. Oakley, P. A., et al. (2024). *Two Methods of Forward Head Posture Assessment: Radiography vs Posture and Their Clinical Comparison*. Journal of Clinical Medicine, 13(7), 2149.

5. Titcomb, D. A., Melton, B. F., Bland, H. W., & Miyashita, T. (2024). *Evaluation of the Craniovertebral Angle in Standing versus Sitting Positions in Young Adults with and without Severe Forward Head Posture*. International Journal of Exercise Science, 17(1), 73–85.

6. Google AI Edge. *MediaPipe Pose Landmarker Documentation*. https://developers.google.com/edge/mediapipe/solutions/vision/pose_landmarker

7. Bazarevsky, V., et al. (2020). *BlazePose: On-device Real-time Body Pose Tracking*. arXiv:2006.10204.

8. Grishchenko, I., et al. (2022). *BlazePose GHUM Holistic: Real-time 3D Human Landmarks and Pose Estimation*. arXiv:2206.11678.

9. Google AI Edge. *MediaPipe Face Landmarker Documentation*. https://developers.google.com/edge/mediapipe/solutions/vision/face_landmarker

10. Lee, H., et al. (2024). *Recognition of Forward Head Posture Through 3D Human Pose Estimation With a Graph Convolutional Network: Development and Feasibility Study*. JMIR Formative Research.

11. Aguilar-Ortega, R., et al. (2023). *UCO Physical Rehabilitation: New Dataset and Study of Human Pose Estimation Methods on Physical Rehabilitation Exercises*. Sensors, 23(21), 8862.

12. Miron, A., et al. (2021). *A Dataset of Physical Rehabilitation Movements*. Data, 6(5), 46.

13. Mendeley Data. (2024). *Stroke Rehabilitation Exercise Data Utilizing 3D Depth Cameras and Inertial Sensors*. https://data.mendeley.com/datasets/ygpdzx52g2

14. Iqbal, M. T. B., et al. (2026). *A 2D Video Dataset of Physiotherapy Exercises for AI-driven Assessment and Monitoring*. PubMed record.

15. Nguyen, S. M., et al. *KERAAL Low Back Pain Physical Rehabilitation Dataset*. https://keraal.enstb.org/KeraalDataset.html

16. Yu, X., & Xiong, S. (2019). *A Dynamic Time Warping Based Algorithm to Evaluate Kinect-Enabled Home-Based Physical Rehabilitation Exercises for Older People*. Sensors.

17. Tsiouris, K. M., et al. (2020). *A Review of Virtual Coaching Systems in Healthcare: Closing the Loop With Real-Time Feedback*. Frontiers in Digital Health.

18. Mikołajewska, E., et al. (2024). *Applications of Artificial Intelligence-Based Patient Digital Twins in Decision Support in Rehabilitation and Physical Therapy*. Electronics, 13(24), 4994.

19. Kasnesis, P., et al. (2025). *A Knee Rehabilitation Exercises Dataset for Postural Assessment using Wearable Devices*. Scientific Data.

---

## 13. 下一步建议

1. 用 Zotero 建一个项目文件夹，按本文献地图分为：
   - `Clinical posture indicators`
   - `Computer vision posture assessment`
   - `Pose estimation methods`
   - `Rehabilitation datasets`
   - `Virtual coach and digital twin`

2. 每篇 PDF 精读时补充：
   - 样本量；
   - 设备；
   - 指标；
   - 主要结果；
   - 统计方法；
   - 局限性；
   - 可引用原句与页码。

3. 阶段一报告中优先写：
   - Mylonas 2022；
   - Carrasco-Uribarren 2023；
   - MediaPipe / BlazePose；
   - Lee 2024；
   - Oakley 2024；
   - UCO 或 KERAAL；
   - Yu & Xiong 2019 可简要放在 future work。

4. 阶段二 FYP 中重点扩展：
   - DTW 动作质量评分；
   - virtual coach；
   - digital patient twin；
   - 用户实验和个性化反馈。
