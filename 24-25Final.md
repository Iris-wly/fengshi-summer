# INT305 — Machine Learning

## 2024/25 Semester 1 Final Examination

| Field | Details |
| --- | --- |
| Paper code | `INT305/24-25/S1/Final` |
| Programme | Bachelor Degree — Year 4 |
| Time allowed | 3 hours |
| Total marks | 100 |

Answer all questions. Marks are shown with each question or sub-question.

## Question 1 — Computation-graph gradients [16 marks]

Fill in the missing gradients underneath the forward-pass activations in each circuit diagram. The gradient of the output with respect to the loss is one (1.00) and has already been filled in. Output values for each unit are represented above the line and gradients are below the line. Calculate the corresponding gradient below each unit in the brackets.

![Two computation graphs with gradient blanks](assets/24-25-final-q1-computation-graphs.png)

Each blank is worth 1 mark.

## Question 2 — Zero–one loss [12 marks]

The zero–one loss is a simple classification loss function that intuitively counts how many mistakes the model makes. In binary classification, the loss for a single example \(x_i\), with label \(y_i\in\{0,1\}\), is

$$
L(x_i)=\mathbb{1}\left[s_{y_i}-s_{(1-y_i)}<0\right],
$$

where \(s_j\) represents the model's predicted score for the \(j\)-th class, and \(\mathbb{1}\) is an indicator function that is 1 if the condition inside is true and 0 otherwise.

1. How do you derive the critical point of zero–one loss? **[4 marks]**
2. Is it a good idea to use zero–one loss for the gradient-descent optimisation process? Why? **[8 marks]**

## Question 3 — Decision tree with sleep and exercise [16 marks]

You are given a dataset with attributes **Hours of Sleep** (Low, Medium, High), whether a person **Exercised** (Yes/No), and whether they performed well in an exam (**Performance**: Good/Bad). Using this dataset, construct a decision tree to predict whether a person performs well.

| Hours of Sleep | Exercised | Performance |
| --- | --- | --- |
| Low | No | Bad |
| Low | Yes | Bad |
| Medium | No | Bad |
| Medium | Yes | Good |
| High | No | Good |
| High | Yes | Good |

1. What is the entropy \(H(\mathit{Performance})\)? **[4 marks]**
2. What is the conditional entropy \(H(\mathit{Performance}\mid\mathit{Hours\ of\ Sleep})\)? **[4 marks]**
3. What is the conditional entropy \(H(\mathit{Performance}\mid\mathit{Exercised})\)? **[4 marks]**
4. Construct the optimal decision tree. Explain why your decision tree is optimal. **[4 marks]**

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
1&2&0&1\\
3&1&2&1\\
0&2&1&3\\
1&0&2&1
\end{pmatrix},
$$

and the convolution filter is

$$
g=
\begin{pmatrix}
1&0&-1\\
0&-1&0\\
1&0&1
\end{pmatrix}.
$$

1. Perform a valid convolution on input matrix \(f\) using filter \(g\), with stride 1 and no padding. Provide the final output matrix. **[6 marks]**
2. Perform the same convolution using the same input matrix \(f\) and filter \(g\), with zero-padding of 1. Provide the padded input and the corresponding output matrix. **[10 marks]**
3. Explain how changing the stride affects the output-matrix size. If the stride is increased to 2 for the same filter and padded input in part 2, what will the output-matrix size be? **[4 marks]**

## Question 5 — Fully connected ReLU network [16 marks]

Given the following neural network with fully connected layers and ReLU activations, there are two input units \((i_1,i_2)\), four hidden units \((h_1,h_2)\) and \((h_3,h_4)\), and two output units \((o_1,o_2)\). Targets are \((t_1,t_2)\). Weights and biases use the subscripts shown in the diagram.

![Fully connected ReLU network](assets/24-25-final-q5-network.png)

Hint:

$$
h_1=[w_{11}\;w_{21}]
\begin{bmatrix}i_1\\i_2\end{bmatrix}+b_1.
$$

| Variable | \(i_1\) | \(i_2\) | \(w_{11}\) | \(w_{12}\) | \(w_{21}\) | \(w_{22}\) | \(w_{31}\) | \(w_{32}\) | \(w_{41}\) | \(w_{42}\) | \(b_1\) | \(b_2\) | \(b_3\) | \(b_4\) | \(t_1\) | \(t_2\) |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Value | 2.0 | -1.0 | 1.0 | -0.5 | 0.5 | -1.0 | 0.5 | -1.0 | -0.5 | 1.0 | 0.5 | -0.5 | -1.0 | 0.5 | 1.0 | 0.5 |

1. List the parameters in this network. **[2 marks]**
2. Compute the output \((o_1,o_2)\) with the given input and network parameters. Show all calculations, including intermediate layer results. **[4 marks]**
3. Compute the squared-error loss of output \((o_1,o_2)\) and target \((t_1,t_2)\). **[4 marks]**
4. Update weight \(w_{21}\) using gradient descent with learning rate 0.1 and the loss computed previously. Show all computations. **[6 marks]**

## Question 6 — Gaussian mixture model [20 marks]

We will use Gaussian Mixture Models (GMM) to perform clustering on a given dataset \(\mathcal{D}\). Assume a data point \(\mathbf{x}\) is generated through

$$
p(z=k)=\pi_k,
\qquad
p(\mathbf{x}\mid z=k)=\mathcal{N}(\mathbf{x}\mid\boldsymbol{\mu}_k,\mathbf{I}).
$$

This defines the joint distribution \(p(z,\mathbf{x})=p(z)p(\mathbf{x}\mid z)\) with parameters \(\{\pi_k,\boldsymbol{\mu}_k\}_{k=1}^{K}\).

1. Derive the probability distribution \(p(\mathbf{x})\). **[5 marks]**
2. What is the log-likelihood function to be maximised for this GMM? **[5 marks]**
3. How do you optimise the log-likelihood function derived in part 2? **[10 marks]**
