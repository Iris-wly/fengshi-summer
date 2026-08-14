# INT305 — Machine Learning

## 2024/25 Semester 1 Resit Examination

| Field | Details |
| --- | --- |
| Paper code shown on PDF | `INT305/24-25/S1/Final` |
| Programme | Bachelor Degree — Year 4 |
| Time allowed | 3 hours |
| Total marks | 100 |

Answer all questions. Marks are shown with each question or sub-question.

## Question 1 — Zero–one loss [12 marks]

The zero–one loss is a simple classification loss function that intuitively counts how many mistakes the model makes. In binary classification, the loss for a single example \(x_i\), with label \(y_i\in\{0,1\}\), is

$$
L(x_i)=\mathbb{1}\left[s_{y_i}-s_{(1-y_i)}<0\right],
$$

where \(s_j\) represents the model's predicted score for the \(j\)-th class, and \(\mathbb{1}\) is an indicator function that is 1 if the condition inside is true and 0 otherwise.

A friend suggests training a linear model classifier by performing gradient descent over the zero–one loss function. Is this a good idea? Briefly explain why or why not.

## Question 2 — Pooling [16 marks]

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

## Question 3 — Decision tree with GPA and study [16 marks]

Use the following dataset to learn a decision tree that predicts whether people pass machine learning (Yes or No), based on their previous GPA (High, Medium or Low) and whether they studied.

| GPA | Studied | Passed |
| --- | --- | --- |
| L | F | F |
| L | T | T |
| M | F | F |
| M | T | T |
| H | F | T |
| H | T | T |

1. What is the entropy \(H(\mathit{Passed})\)? **[4 marks]**
2. What is the conditional entropy \(H(\mathit{Passed}\mid\mathit{GPA})\)? **[4 marks]**
3. What is the conditional entropy \(H(\mathit{Passed}\mid\mathit{Studied})\)? **[4 marks]**
4. Draw the best decision tree learned for this dataset. State why the decision tree is the best. **[4 marks]**

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
1&1&3&1&1
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

Evaluate the convolution results for the following two cases:

1. Stride is equal to 1, and zero-padding of 1 is used. **[10 marks]**
2. Stride is equal to 2, and padding is **not** used. **[10 marks]**

## Question 5 — Computation-graph gradients [16 marks]

Fill in the missing gradients underneath the forward-pass activations in each circuit diagram. The gradient of the output with respect to the loss is one (1.00) and has already been filled in. Output values for each unit are represented above the line and gradients are below the line. Calculate the corresponding gradient below each unit in the brackets.

![Two computation graphs with gradient blanks](assets/24-25-resit-q5-computation-graphs.png)

Each blank is worth 1 mark.

## Question 6 — Gaussian mixture model [20 marks]

We will work with clustering by GMM for data \(\mathcal{D}\). Assume a data point \(\mathbf{x}\) is generated as follows:

- Choose a cluster \(z\in\{1,\ldots,K\}\) such that \(p(z=k)=\pi_k\).
- Given \(z\), sample \(\mathbf{x}\) from a Gaussian distribution \(\mathcal{N}(\mathbf{x}\mid\boldsymbol{\mu}_z,\mathbf{I})\).

1. What is the distribution of \(p(\mathbf{x})\), and what is the log-likelihood loss function to be maximised? **[10 marks]**
2. Illustrate the Expectation-Maximization algorithm for this GMM. List the steps for the EM algorithm. **[10 marks]**
