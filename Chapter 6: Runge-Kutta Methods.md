This chapter treats the topic of numerical integration, that is, the numerical solving of ODEs
[[_TOC_]]


---
## An important realization

Numerical integration methods assume that our ODE is first order and autonomous (i.e. not explicitly dependent on $t$). Thankfully every possible ODE can be written as a **system of autonomous first-order ODEs**.

$$
 \dot {\textbf y} =\textbf f (\textbf y)
$$

with

$$\dot {\textbf y}=\begin{bmatrix}\dot y_1 \\
\dot y_2 \\
\vdots \\
\dot y_n
\end{bmatrix}=\begin{bmatrix}
f_1(y_1, y_2, ...,y_n ) \\
f_2(y_1, y_2, ...,y_n )\\
\vdots \\
f_3(y_1, y_2, ...,y_n )\\
\end{bmatrix}
$$



## The Evolution operator

The **evolution operator** ($\Phi$) is a mapping that, given a certain system of autonomous first-order ODEs with $\dot {\textbf y}={\textbf f} $ and a time-step $t$, assigns to each initial datum ${\textbf y}(T)$ and outputs ${\textbf y}(T+t)$.

> When an ODE is autonomous we always have that  $\Phi^s\circ \Phi^t=\Phi ^{s+t}$

There are 2 different ways of lookin

# The Euler Method

This is the most "naïve" approach to the numerical solution of ODEs. As the name suggests it was first invented by Euler.

### We have:
- An ODE $\dot {\textbf y}={\textbf f}({\textbf y})$
- An initial value $(t_0, {\textbf y_0})$
- A given time-step interval $\Delta t$ (in theory it could not always ne the same between each node)

We compute the time series $(y_n)_{n \in N}$ by recusively defining 

$$
   {\textbf y_{n+1}}= {\textbf y_n}+h\cdot {\textbf f}({\textbf y_n})
$$

This basically amounts to repeatedly doing a first-order Taylor approximation. 

# Convergence

We want to measure how quickly different methods converge towards the analytical solutions as $h \to 0$.

We will evaluate the **h-convergence** of different SSMs. Foe each methods we consider the family $h_m := (\max\limits_k h_k)\to 0$ 

## Discretization errors
- $\max\limits_k ||y_k - y(t_k)||$
- $||y_M - y(t_M)||$

##Exmaple 6.3.2.5
Here we see that both the **explicit** and **implicit** Euler methods converge in $O(h)=O(M^{-1})$

This means that the order is 1 (because it’s a 1st order Taylor Exp.).

As for the **midpoint** method it’s convergence is of order 2.

> *Theorem*: The discretization error of SSMs always shrinks at an algebraic rate w.r.t. $h$, as $h \to 0$.

## How do we establish the order of a SSM (example with Euler Method)

We can split the errors in 2 contributions:
- **one-step error**: the difference between what we obtain by applying the continuous vs. the discrete evolution operator on $y(t_k)$
- **propagated error**: This is the difference between what we obtain by applying the discrete evolution operator on $y_{k-1}$ vs $y(t_{k-1})$: this error can be further split in:
  1. Accumulation of previous one-step errors
  2. The fact that the slope field does not only depend on time

Total error $y_k-y(t_k)=$ one-step error + propagated error.

Interestingly, to find out the order of a SSM, we just need to find the order of its one-step error. The order of the entire SSM will be that of the one-step error minus 1.

# Single Step Methods

The general recursion in the explicit Euler method is:

$$
y_{k+1}=y_k+h_k\cdot f(y_k)
$$

We now generalize the right hand side for arbitrary single step-methods:

$$
y_{k+1}=\Psi(h_k, y_k)
$$

**Note**: also for the generic SSM, we only need the previous $y$-value to compute the next one, no other one is needed.

> **SSM**: Given a Discrete Evolution $\Psi:I\times D\to R^N$ and a temporal mesh $M:=\{0=t_0, t_1, …,t_M=T\}$ the recursion 

>$$
y_{k+1}=\Psi(h_k, y_k)
$$

> defines a SSM for an autonomous IVP, $\dot {\textbf y} ={\textbf f} ({\textbf y}), \textbf {y}(0)=y_0 $
