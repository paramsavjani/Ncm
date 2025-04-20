# Root-Finding Methods: Bisection, Secant, Regula Falsi, Newton-Raphson, and Muller

---

## Bisection Method

The **Bisection Method** is a bracketing method for finding the root of a function. It works by repeatedly halving the interval in which the root lies.

- Given a continuous function $f(x)$ and an interval $[a, b]$ such that $f(a) \cdot f(b) < 0$, a root exists between $a$ and $b$.
- Compute the midpoint:
  $$
  c = \frac{a + b}{2}
  $$
- Evaluate $f(c)$:
  - If $f(a) \cdot f(c) < 0$, set $b = c$
  - Else, set $a = c$
- Repeat until the interval $[a, b]$ is sufficiently small.

✅ **Advantages**: Always converges (if root exists in interval)  
⚠️ **Disadvantages**: Slower convergence rate

---

## Secant Method (Chord Method)

The **Secant Method** is an open method that uses a secant line (a straight line through two points on the curve) to approximate the root.

- Given two initial guesses $x_0$ and $x_1$, draw a secant line passing through the points $(x_0, f(x_0))$ and $(x_1, f(x_1))$.
- The x-intercept of the secant gives the next approximation:

  $$
  x_n = x_{n-1} - f(x_{n-1}) \cdot \frac{x_{n-1} - x_{n-2}}{f(x_{n-1}) - f(x_{n-2})}
  $$

- Use the latest two approximations $x_{n-1}$ and $x_{n-2}$ for each new iteration.

Unlike the bisection method, the secant method does **not require bracketing**, and it often converges faster, but convergence is **not guaranteed**.

📝 In most problems, you are given $x_0$ and $x_1$, and the iteration proceeds using the last two approximations ($x_{n-1}$ and $x_{n-2}$).

✅ **Advantages**: Faster than bisection  
⚠️ **Disadvantages**: No guaranteed convergence

---

## Regula Falsi Method (False Position Method)

The **Regula Falsi Method** is a hybrid of the bisection and secant methods. It uses a secant-like formula but keeps the root bracketed like in the bisection method.

- Start with two points $a$ and $b$ such that $f(a) \cdot f(b) < 0$.
- Use the following formula to find the x-intercept of the secant:

  $$
  x = a - f(a) \cdot \frac{b - a}{f(b) - f(a)}
  $$

- Check the sign of $f(x)$:
  - If $f(a) \cdot f(x) < 0$, set $b = x$
  - Else, set $a = x$
- Repeat the process while keeping the interval $[a, b]$ bracketing the root.

✅ **Advantages**: Safer than secant, faster than bisection  
⚠️ **Disadvantages**: Can stagnate if one endpoint doesn't change

---

## Newton-Raphson Method

The **Newton-Raphson Method** is a powerful open method that uses the first derivative to approximate the root of a function.

- Given an initial guess $x_0$, use the iterative formula:

  $$
  x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
  $$

- Repeat until $x_n$ converges to a root.

It requires that the derivative $f'(x)$ exists and is not zero at the root.

✅ **Advantages**: Very fast convergence (quadratic), especially near the root  
⚠️ **Disadvantages**: Requires derivative, may diverge if starting point is poor

---

## Muller Method

The **Muller Method** fits a parabola through three points and computes the root of that parabola. It can also find complex roots.

Given three approximations $x_{k-2}, x_{k-1}, x_k$, define:

### Coefficients

$$
a_0 = \frac{(x_k - x_{k-2})(f_k - f_{k-1}) - (x_k - x_{k-1})(f_k - f_{k-2})}{(x_k - x_{k-1})(x_k - x_{k-2})(x_{k-1} - x_{k-2})}
$$

$$
a_1 = \frac{(x_k - x_{k-2})^2(f_k - f_{k-1}) - (x_k - x_{k-1})^2(f_k - f_{k-2})}{(x_k - x_{k-1})(x_k - x_{k-2})(x_{k-1} - x_{k-2})}
$$

$$
a_2 = f_k
$$

### Iterative Formula

Solve the quadratic equation:

$$
a_0(x - x_k)^2 + a_1(x - x_k) + a_2 = 0
$$

Then:

$$
x_{k+1} = x_k - \frac{2a_2}{a_1 \pm \sqrt{a_1^2 - 4a_0a_2}}
$$

> **Note**: Choose the sign in the denominator that gives the **larger magnitude**, i.e., the **same sign as $a_1$**, to avoid small denominators and improve convergence.

✅ **Advantages**: Can find complex roots, superlinear convergence  
⚠️ **Disadvantages**: More computation, requires 3 initial points

---

## Chebyshev Method

The **Chebyshev Method** is an open root-finding method that improves the Newton-Raphson method by incorporating the second derivative for faster convergence.

- Given an initial guess $x_0$, use the iteration formula:

  $$
  x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} - \frac{1}{2} \cdot \left( \frac{f(x_n)^2 \cdot f''(x_n)}{f'(x_n)^3} \right)
  $$

✅ **Advantages**: Cubic convergence near root  
⚠️ **Disadvantages**: Requires both first and second derivatives

---

## Method of Successive Approximations

The **Method of Successive Approximations** (also known as **Fixed Point Iteration**) is an iterative technique to solve equations of the form:

$$
x = g(x)
$$

### Algorithm

1. Start with an initial guess $x_0$.
2. Iterate using:
   $$
   x_{n+1} = g(x_n)
   $$
3. Continue until $|x_{n+1} - x_n| < \epsilon$ (a small tolerance).

### Convergence Criteria

- $g(x)$ must be continuous.
- $|g'(x)| < 1$ near the root.

✅ **Advantages**: Simple to implement  
⚠️ **Disadvantages**: Only works under certain conditions, slower than Newton's method.

---

## Gauss-Jordan Elimination Method

The **Gauss-Jordan Elimination Method** is a direct method for solving systems of linear equations by transforming the augmented matrix into **reduced row-echelon form (RREF)**.

### Steps

1. Convert the augmented matrix $[A | b]$ to RREF.
2. Make the leading diagonal elements 1.
3. Make all other elements in the pivot columns 0.
4. The resulting matrix directly gives the solution:
   $$
   x_1, x_2, \dots, x_n
   $$

✅ **Advantages**: Direct solution  
⚠️ **Disadvantages**: Computationally expensive for large matrices

---

## LU Decomposition Method

The **LU Decomposition Method** factorizes a square matrix $A$ into a **Lower triangular matrix (L)** and an **Upper triangular matrix (U)** such that:

$$
A = LU
$$

Then solve:

- $LUx = b$ ⟹ Let $Ux = z$, then:
  1. Solve $Lz = b$ (forward substitution)
  2. Solve $Ux = z$ (backward substitution)

### Variants

- **Doolittle Method**: $L$ has 1s on the diagonal ($l_{ii} = 1$)
- **Crout Method**: $U$ has 1s on the diagonal ($u_{ii} = 1$)

✅ **Advantages**: Efficient for multiple right-hand sides $b$  
⚠️ **Disadvantages**: Requires pivoting for numerical stability

---

## Cholesky Factorization Method

The **Cholesky Factorization** is used for **symmetric positive-definite matrices**.

### Decomposition

$$
A = LL^T
$$
Where:

- $L$ is a lower triangular matrix
- $L^T$ is the transpose of $L$

### Steps to Solve

Given $Ax = b$:

1. Solve $Lz = b$ (forward substitution)
2. Solve $L^Tx = z$ (backward substitution)

### Positive Definite Matrix

A matrix $A$ is **positive definite** if:
$$
x^T A x > 0 \quad \text{for all } x \neq 0
$$

✅ **Advantages**: Fast and stable for symmetric positive-definite matrices  
⚠️ **Disadvantages**: Only applicable for positive-definite matrices

---

## Partition Method

The **Partition Method** solves systems by partitioning the matrix and its inverse into submatrices.

Given:
$$
A = \begin{pmatrix} B & C \\ E & D \end{pmatrix}
\quad \text{and} \quad
A^{-1} = \begin{pmatrix} X & Y \\ Z & V \end{pmatrix}
$$

Then the inverse components are given by:

- $V = (D - EB^{-1}C)^{-1}$
- $Z = -VEB^{-1}$
- $X = B^{-1} + B^{-1}CZ$
- $Y = -B^{-1}CV$

✅ **Advantages**: Useful in block matrix computations  
⚠️ **Disadvantages**: Matrix inversion required, not ideal for sparse matrices

---
