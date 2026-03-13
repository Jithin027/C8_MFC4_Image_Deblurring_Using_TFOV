# Image Deblurring using TFOV Model with Preconditioning

## Course
**22MAT230 – Mathematics for Computing IV**

---

# Team Members

| S.No | Name | Roll Number |
|-----|------|-------------|
| 1 | Deepika Reddy | CB.SC.U4AIE24215 |
| 2 | Jithin Reddy | CB.SC.U4AIE24230 |
| 3 | Police Aryan | CB.SC.U4AIE24241 |
| 4 | Praveen Reddy | CB.SC.U4AIE24243 |

---

# Reference Paper

Al-Mahdi, A.M. (2023)  
*Preconditioning Technique for an Image Deblurring Problem with the Total Fractional-Order Variation Model*

Mathematical and Computational Applications  
Volume 28, Issue 5, Article 97

https://doi.org/10.3390/mca28050097

---

# Introduction

Image deblurring is an inverse problem where the goal is to recover the original image \(u\) from a blurred observation \(z\).

$$
z = Ku + \varepsilon
$$

Where

- \(K\) = blur operator  
- \(u\) = original image  
- \(z\) = observed blurred image  
- \(\varepsilon\) = noise

---

# 1. Condition Number

The condition number measures numerical stability of a matrix.

$$
\kappa_2(A)=
\frac{\sigma_{\max}(A)}{\sigma_{\min}(A)}
$$

Where

- \( \sigma_{\max} \) = largest singular value  
- \( \sigma_{\min} \) = smallest singular value

If

$$
\kappa(A) \gg 1
$$

then the system is **ill-conditioned**.

---

# 2. Ill-Conditioned Case

After discretization the problem becomes a **saddle-point system**

$$
\begin{bmatrix}
I_n & K_h \\
-K_h^* & \lambda L_h^\alpha(U_h)
\end{bmatrix}
\begin{bmatrix}
V_h \\
U_h
\end{bmatrix}
=\begin{bmatrix}
Z_h \\
0
\end{bmatrix}
$$

Where

- \(n = N^2\) pixels
- system size = \(2n \times 2n\)

---

## Schur Complement

$$
S = K_h^*K_h + \lambda L_h^\alpha(U_h)
$$

This matrix becomes extremely ill-conditioned.

---

# 3. Preconditioning

Preconditioning improves convergence of iterative solvers.

Instead of solving

$$
Ax = b
$$

we solve

$$
P^{-1}Ax = P^{-1}b
$$

Where \(P\) approximates \(A\).

### Block Preconditioner

$$
P_1 =
\begin{bmatrix}
I_n & K_h \\
0 & -(I + \lambda L_{TV})
\end{bmatrix}
$$

Another preconditioner

$$
P_2 =
\begin{bmatrix}
I_n & K_h \\
0 & -(C^*C + \lambda L_{TV})
\end{bmatrix}
$$

Where \(C\) is a circulant approximation of \(K_h\).

---

# 4. Total Variation (TV) Model

The TV regularization model is

$$
\min_u
\left(
\frac{1}{2}\|Ku - z\|_2^2
+
\lambda \int_{\Omega} |\nabla u| dx
\right)
$$

TV preserves edges but introduces **staircase artifacts**.

---

# 5. Total Fractional Order Variation (TFOV)

The TFOV model extends TV using fractional derivatives.

$$
\min_u
\left(
\frac{1}{2}\|Ku - z\|_2^2
+
\lambda
\int_{\Omega}
\sqrt{|\nabla^\alpha u|^2 + \beta^2}
dx
\right)
$$

Where

- \( \alpha \) = fractional derivative order
- \( \beta \) = regularization parameter

---

## Fractional Divergence

$$
\mathrm{div}^\alpha \phi =
\frac{\partial^\alpha \phi_1}{\partial x^\alpha}
+
\frac{\partial^\alpha \phi_2}{\partial y^\alpha}
$$

---

# 6. Small Example for Preconditioning

Consider

$$
A =
\begin{bmatrix}
4 & 1 \\
1 & 3
\end{bmatrix}
$$

Choose preconditioner

$$
P =
\begin{bmatrix}
4 & 0 \\
0 & 3
\end{bmatrix}
$$

Then

$$
P^{-1}A =
\begin{bmatrix}
1 & 0.25 \\
0.33 & 1
\end{bmatrix}
$$

This reduces the condition number and improves convergence.

---

# 7. Staircase Effect Example

TV reconstruction may produce piecewise constant regions.

![Staircase Example](Screenshot%202026-03-13%20202142.png)

---

# 8. Examples of Blur Operators

### Gaussian Blur

$$
K(x,y)=
\frac{1}{2\pi\sigma^2}
e^{-\frac{x^2+y^2}{2\sigma^2}}
$$

### Motion Blur

$$
K(x,y)=
\frac{1}{L}
\text{rect}\left(\frac{x}{L}\right)
$$

Example blurred image

![Blur Example](Screenshot%202026-03-13%20202301.png)

---

# 9. TV vs TFOV Demonstration

TV result

![TV Result](Screenshot%202026-03-13%20202317.png)

TFOV result

![TFOV Result](Screenshot%202026-03-13%20202335.png)

| Model | Observation |
|------|-------------|
| TV | staircase artifacts |
| TFOV | smoother reconstruction |

---

# Conclusion

This project studies **preconditioning techniques for image deblurring using TFOV**.

Key results:

- Deblurring problems are ill-conditioned
- Preconditioning improves solver convergence
- TV produces staircase artifacts
- TFOV reduces staircase artifacts and improves image quality

---

# References

1. Al-Mahdi, A.M. (2023)  
Preconditioning Technique for an Image Deblurring Problem with the Total Fractional-Order Variation Model

2. Mathematical and Computational Applications

3. https://doi.org/10.3390/mca28050097
