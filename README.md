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

Image deblurring is an **inverse problem** where the goal is to recover the original image \(u\) from a blurred observation \(z\).

The mathematical model is

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

The **condition number** measures how sensitive a matrix is to numerical errors.

$$
\kappa_2(A) =
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

Large condition numbers often appear in **image deblurring problems** because blur operators remove high-frequency information.

---

# 2. Ill-Conditioned Case

After discretization, the optimization problem becomes a **saddle-point system**

$$
\begin{bmatrix}
I_n & K_h \\
-K_h^* & \lambda L_h^\alpha(U_h)
\end{bmatrix}
\begin{bmatrix}
V_h \\
U_h
\end{bmatrix}
=
\begin{bmatrix}
Z_h \\
0
\end{bmatrix}
$$

Where

- \(n = N^2\) pixels
- system size = \(2n \times 2n\)

The **Schur complement**

$$
S = K_h^*K_h + \lambda L_h^\alpha(U_h)
$$

becomes extremely ill-conditioned.

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

Another version

$$
P_2 =
\begin{bmatrix}
I_n & K_h \\
0 & -(C^*C + \lambda L_{TV})
\end{bmatrix}
$$

Where \(C\) is a **circulant approximation of \(K_h\)** enabling fast FFT inversion.

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

### Advantages

- Edge preserving
- Noise reduction

### Problem

TV produces **staircase artifacts** where smooth regions become piecewise constant.

---

# 5. Total Fractional Order Variation (TFOV) Model

The TFOV model generalizes TV using fractional derivatives.

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
- \( \beta \) = small regularization constant

### Fractional Divergence

$$
\mathrm{div}^{\alpha}\phi =
\frac{\partial^{\alpha}\phi_1}{\partial x^{\alpha}}
+
\frac{\partial^{\alpha}\phi_2}{\partial y^{\alpha}}
$$

TFOV reduces staircase artifacts due to **non-local smoothing**.

---

# 6. Small Example for Preconditioning

Consider a simple linear system

$$
A =
\begin{bmatrix}
4 & 1 \\
1 & 3
\end{bmatrix}
$$

Solving

$$
Ax = b
$$

If we choose preconditioner

$$
P =
\begin{bmatrix}
4 & 0 \\
0 & 3
\end{bmatrix}
$$

Then

$$
P^{-1}A
=
\begin{bmatrix}
1 & 0.25 \\
0.33 & 1
\end{bmatrix}
$$

The condition number becomes smaller and iterative solvers converge faster.

---

# 7. Example of Staircase Effect

The staircase effect occurs when smooth gradients become flat blocks.

Example:

Original signal

```
Smooth gradient
```

TV reconstruction

```
Step-like regions
```

### Example Image

![Staircase Example](Screenshot%202026-03-13%20202142.png)

---

# 8. Examples of Blur Operators \(K\)

Common blur operators include:

### 1. Gaussian Blur

$$
K(x,y) =
\frac{1}{2\pi\sigma^2}
e^{-\frac{x^2+y^2}{2\sigma^2}}
$$

Used for camera lens blur.

---

### 2. Motion Blur

Blur caused by camera motion:

$$
K(x,y) =
\frac{1}{L}
\text{rect}\left(\frac{x}{L}\right)
$$

---

### 3. Defocus Blur

Circular blur caused by out-of-focus lens.

---

Example blur image:

![Blur Example](Screenshot%202026-03-13%20202301.png)

---

# 9. TV vs TFOV Demonstration

TV reconstruction often produces staircase artifacts.

Example TV result:

![TV Result](Screenshot%202026-03-13%20202317.png)

TFOV improves smoothness and preserves texture.

Example TFOV result:

![TFOV Result](Screenshot%202026-03-13%20202335.png)

### Observations

| Model | Result |
|------|------|
| TV | staircase artifacts |
| TFOV | smoother edges |
| TFOV | better texture preservation |

---

# Conclusion

This project studied **preconditioning methods for image deblurring using the TFOV model**.

Key results:

- Ill-conditioned systems arise in deblurring problems
- Preconditioning improves solver convergence
- TV model preserves edges but introduces staircase artifacts
- TFOV reduces staircase artifacts and improves reconstruction quality

Thus TFOV combined with Krylov solvers provides an efficient framework for **high-quality image restoration**.

---

# References

1. Al-Mahdi, A.M. (2023)  
Preconditioning Technique for an Image Deblurring Problem with the Total Fractional-Order Variation Model

2. Mathematical and Computational Applications

3. https://doi.org/10.3390/mca28050097
4. 
