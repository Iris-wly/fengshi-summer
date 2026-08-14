# INT305 — Machine Learning

## 2023/24 Semester 1 Final Examination

| Field | Details |
| --- | --- |
| Paper code | `INT305/23-24/S1/Final` |
| Programme | Bachelor Degree — Year 4 |
| Time allowed | 3 hours |
| Total marks | 100 |

Answer all questions. Marks are shown with each question or sub-question.

## Question 1 — Pooling [16 marks]

Pooling units take \(n\) values \(x_i,\ i\in[1,n]\), and compute a scalar output whose value is invariant to permutations of the inputs.

1. The \(L_p\)-pooling module takes positive inputs and computes

   $$
   y=\left(\sum_i x_i^p\right)^{1/p}.
   $$

   Assuming \(y'=\frac{\partial\mathcal{L}}{\partial y}\) is known, what is \(x_i'=\frac{\partial\mathcal{L}}{\partial x_i}\)? **[8 marks]**

2. The log-average module computes

   $$
   y=\frac{1}{\beta}\ln\left(\frac{1}{n}\sum_i\exp(\beta x_i)\right).
   $$

   Assuming \(y'=\frac{\partial\mathcal{L}}{\partial y}\) is known, what is \(x_i'=\frac{\partial\mathcal{L}}{\partial x_i}\)? **[8 marks]**

## Question 2 — Linear classification [9 marks]

Recall two linear classification methods:

**Model 1**

$$
y=\mathbf{w}^T\mathbf{x}+b,
\qquad
\mathcal{L}_{SE}(y,t)=\frac{1}{2}(y-t)^2.
$$

**Model 2**

$$
z=\mathbf{w}^T\mathbf{x}+b,
\qquad
y=\sigma(z),
\qquad
\mathcal{L}_{SE}(y,t)=\frac{1}{2}(y-t)^2.
$$

Here \(\sigma\) denotes the logistic (sigmoid) function, and the target label \(t\) takes values in \(\{0,1\}\). Briefly explain the reason for preferring Model 2 to Model 1.

## Question 3 — Decision-tree split [15 marks]

We are constructing a decision tree. Considering the following data, we would like to split the instances at one level. There are two options, A and B, for the split. Select the better option from the perspective of information gain.

![Decision-tree split options A and B](assets/23-24-final-q3-splits.png)

## Question 4 — Two-dimensional convolution [20 marks]

The convolution operation is defined as

$$
f[x,y]*g[x,y]=\sum_{n_1=-\infty}^{\infty}\sum_{n_2=-\infty}^{\infty}
f[n_1,n_2]\cdot g[x-n_1,y-n_2].
$$

The image patch is

$$
f=
\begin{pmatrix}
1&2&1&1&1\\
1&2&1&2&2\\
1&2&1&3&3\\
1&2&2&2&2\\
1&2&3&1&1
\end{pmatrix},
$$

and the convolution kernel is

$$
g=
\begin{pmatrix}
1&2&1\\
2&3&2\\
1&2&1
\end{pmatrix}.
$$

Evaluate the convolution results for the following cases:

1. Stride is equal to 1, and padding is **not** used. **[10 marks]**
2. Stride is equal to 2, and zero padding is used. **[10 marks]**

## Question 5 — Three-layer sigmoid network [20 marks]

Consider the following three-layer network, where the activation function \(\sigma(\cdot)\) is the sigmoid function and

$$
\sigma'(x)=\sigma(x)(1-\sigma(x)).
$$

![Three-layer sigmoid network](assets/23-24-final-q5-network.png)

The layer definitions are

$$
Z^{[1]}=
\begin{bmatrix}z_1^{[1]}\\z_2^{[1]}\end{bmatrix}
=
\begin{bmatrix}w_{11}^{[1]}&w_{12}^{[1]}\\w_{21}^{[1]}&w_{22}^{[1]}\end{bmatrix}
\begin{bmatrix}x_1\\x_2\end{bmatrix},
\qquad
A^{[1]}=
\begin{bmatrix}a_1^{[1]}\\a_2^{[1]}\end{bmatrix}
=
\begin{bmatrix}\sigma(z_1^{[1]})\\\sigma(z_2^{[1]})\end{bmatrix},
$$

$$
Z^{[2]}=
\begin{bmatrix}z_1^{[2]}\\z_2^{[2]}\end{bmatrix}
=
\begin{bmatrix}w_{11}^{[2]}&w_{12}^{[2]}\\w_{21}^{[2]}&w_{22}^{[2]}\end{bmatrix}
\begin{bmatrix}a_1^{[1]}\\a_2^{[1]}\end{bmatrix},
\qquad
A^{[2]}=
\begin{bmatrix}a_1^{[2]}\\a_2^{[2]}\end{bmatrix}
=
\begin{bmatrix}\sigma(z_1^{[2]})\\\sigma(z_2^{[2]})\end{bmatrix}.
$$

Given

$$
f=w_1^{[3]}a_1^{[2]}+w_2^{[3]}a_2^{[2]},
$$

compute:

1. \(\delta_1=\frac{\partial f(\mathbf{x})}{\partial z_1^{[2]}}\). **[5 marks]**
2. \(\delta_2=\frac{\partial f(\mathbf{x})}{\partial z_1^{[1]}}\). **[5 marks]**
3. \(\delta_3=\frac{\partial f(\mathbf{x})}{\partial z_2^{[1]}}\). **[5 marks]**
4. \(\delta_4=\frac{\partial f(\mathbf{x})}{\partial w_{11}^{[1]}}\). **[5 marks]**

## Question 6 — Gaussian mixture model [20 marks]

We will work with clustering by GMM for data \(\mathcal{D}\). Assume a data point \(\mathbf{x}\) is generated as follows:

- Choose a cluster \(z\in\{1,\ldots,K\}\) such that \(p(z=k)=\pi_k\).
- Given \(z\), sample \(\mathbf{x}\) from a Gaussian distribution \(\mathcal{N}(\mathbf{x}\mid\boldsymbol{\mu}_z,\mathbf{I})\).

1. What is \(p(\mathbf{x})\)? **[5 marks]**
2. What is the log-likelihood function to be maximised? **[5 marks]**
3. If using Expectation-Maximization for optimisation, derive the E-step for this model. Draw a rectangle around the derived formula. **[5 marks]**
4. Derive the M-step for this model. Draw a rectangle around the derived formula. **[5 marks]**
