# INT305 — Machine Learning

## 2022/23 Semester 1 Final Examination

| Field | Details |
| --- | --- |
| Paper code | `INT305/22-23/S1/Final` |
| Programme | Bachelor Degree — Year 4 |
| Time allowed | 3 hours |
| Total marks | 100 |

Answer all questions. Marks are shown with each question or sub-question.

## Question 1 — Pooling [16 marks]

Pooling units take \(n\) values \(x_i,\ i \in [1,n]\), and compute a scalar output whose value is invariant to permutations of the inputs.

1. The \(L_p\)-pooling module takes positive inputs and computes

   $$
   y = \left(\sum_i x_i^p\right)^{1/p}.
   $$

   Assuming that \(y' = \frac{\partial \mathcal{L}}{\partial y}\) is known, what is \(x_i' = \frac{\partial \mathcal{L}}{\partial x_i}\)? **[8 marks]**

2. The log-average module computes

   $$
   y = \frac{1}{\beta}\ln\left(\frac{1}{n}\sum_i \exp(\beta x_i)\right).
   $$

   Assuming that \(y' = \frac{\partial \mathcal{L}}{\partial y}\) is known, what is \(x_i' = \frac{\partial \mathcal{L}}{\partial x_i}\)? **[8 marks]**

## Question 2 — Linear classification [14 marks]

Recall two linear classification methods:

**Model 1**

$$
y = \mathbf{w}^T\mathbf{x}+b,
\qquad
\mathcal{L}_{SE}(y,t) = \frac{1}{2}(y-t)^2.
$$

**Model 2**

$$
z = \mathbf{w}^T\mathbf{x}+b,
\qquad
y=\sigma(z),
\qquad
\mathcal{L}_{SE}(y,t) = \frac{1}{2}(y-t)^2.
$$

Here \(\sigma\) denotes the logistic (sigmoid) function, and the target label \(t\) takes values in \(\{0,1\}\). Briefly explain the reason for preferring Model 2 to Model 1.

## Question 3 — Decision-tree split [15 marks]

We are constructing a decision tree. Considering the following data, we would like to split the instances at one level. There are two options, A and B, for the split. Select the better option from the perspective of information gain.

![Decision-tree split options A and B](assets/22-23-final-q3-splits.png)

## Question 4 — Convolution, ReLU and max pooling [20 marks]

The sub-system shown below has a convolution unit (convolution kernel \(1\times3\)), followed by a ReLU and then a max-pooling unit. Assume that the convolution operation uses zero padding.

Input vector:

$$
X=[1,\ 1,\ 1,\ -2,\ 1,\ -1,\ 2,\ -1].
$$

Convolution kernel:

$$
[1,\ -2,\ 1].
$$

![Convolution–ReLU–max-pooling sub-system](assets/22-23-final-q4-cnn-pipeline.png)

1. Fill in all empty elements in vector \(Y\). **[4 marks]**
2. Fill in all empty elements in vector \(Z\). **[4 marks]**
3. Fill in all empty elements in vector \(V\). **[4 marks]**
4. How many learnable parameters does this sub-system have? **[4 marks]**
5. Given the pictorial representation above, what is the stride size of the convolution unit? **[4 marks]**

## Question 5 — Back-propagation rules [15 marks]

You want to train the following model using gradient descent. The input \(x\) and target \(t\) are both scalar-valued:

$$
z=\omega_0+\omega_1x+\omega_2x^2+\omega_3x^3,
$$

$$
y=1+e^{\max(z,0)},
$$

$$
\mathcal{L}=\frac{1}{2}(\ln y-\ln t)^2.
$$

Determine the back-propagation rules that compute the loss derivative

$$
\bar{\omega}_2=\frac{\partial\mathcal{L}}{\partial\omega_2}.
$$

Variables with a bar are the gradients of the variables. Your equations should refer to previously computed values (for example, the formula for \(\bar z\) should be a function of \(\bar y\)). You do not need to show a derivation. The dummy step is filled in:

$$
\bar{\mathcal{L}}=1.
$$

Complete:

$$
\bar y=\ ?
\qquad
\bar z=\ ?
\qquad
\bar{\omega}_2=\ ?
$$

## Question 6 — Gaussian mixture model with shared mean [20 marks]

In this question, derive the EM update rules for a univariate Gaussian mixture model (GMM) with two mixture components. Unlike the GMM covered in the course, the mean \(\mu\) is shared between the two mixture components, while each component has its own standard deviation \(\sigma_k\) (\(\sigma_0\) and \(\sigma_1\)). The mixture component is indicated by a latent variable \(z\in\{0,1\}\). The model is:

$$
z\sim\operatorname{Bernoulli}(\theta),
\qquad
P(z=1\mid\theta)=\theta,
\qquad
P(z=0\mid\theta)=1-\theta,
$$

$$
x\mid z=k\sim\mathcal{N}(\mu,\sigma_k),
\qquad k\in\{0,1\}.
$$

The parameters are \(\theta,\mu,\sigma_0,\sigma_1\). Suppose the observed dataset is \(\{x^{(i)}\}_{i=1}^{N}\). For reference,

$$
\mathcal{N}(x;\mu,\sigma)=\frac{1}{\sqrt{2\pi}\sigma}
\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).
$$

1. Write the complete-data log-likelihood for this model. Assume \(z^{(i)}\) is known for every \(x^{(i)}\), so the dataset is \(\{z^{(i)},x^{(i)}\}_{i=1}^{N}\). **[5 marks]**
2. In the E-step, for each data point \(x^{(i)}\), compute the posterior probability

   $$
   r^{(i)}=\Pr\left(z^{(i)}=1\mid x^{(i)}\right).
   $$

   Give a formula for \(r^{(i)}\). You may use \(\mathcal{N}(x^{(i)};\mu,\sigma)\) to denote the Gaussian PDF. **[5 marks]**
3. Write the expected complete-data log-likelihood — the objective maximised in the M-step — in terms of \(r^{(i)}\) and the Gaussian PDF \(\mathcal{N}(x^{(i)};\mu,\sigma)\). **[5 marks]**
4. Derive the M-step update rule for \(\mu\) by maximising this objective with respect to \(\mu\). In this step, \(\sigma_k\) are fixed at their previous values. **[5 marks]**
