# Preconditioning Technique for an Image Deblurring Problem using TFOV Model

## Course
22MAT230 – Mathematics for Computing IV

---

## 1. Team Members

| S.No | Name           | Roll Number      |
|------|----------------|------------------|
| 1    | Deepika Reddy  | CB.SC.U4AIE24215 |
| 2    | Jithin Reddy   | CB.SC.U4AIE24230 |
| 3    | Police Aryan  | CB.SC.U4AIE24241 |
| 4    |  Praveen Reddy  | CB.SC.U4AIE24243 |

---

## 2. Base / Reference Paper(s)

This project is inspired by research works on:

- Image deblurring as an inverse problem  
- Total Variation (TV) regularization methods  
- Fractional-order variation models for image restoration  
- Preconditioning techniques to speed up numerical solvers  

The main idea is taken from research papers that propose **Total Fractional-Order Variation (TFOV)** models to overcome limitations of classical TV methods, especially the staircase effect.

---

## 3. Project Outline

The aim of this project is to **restore blurred images** using an advanced regularization approach.

- Image deblurring is a challenging problem due to noise and information loss  
- Traditional methods either oversmooth the image or amplify noise  
- Total Variation preserves edges but creates staircase artifacts  
- TFOV introduces fractional-order information to balance smoothness and edge preservation  
- Preconditioning techniques are used to **improve convergence speed** and reduce computation time  

Overall, the project studies how TFOV combined with preconditioning provides better and faster image restoration.

---

## 4. Updates / Progress

- Studied the basics of image deblurring and inverse problems  
- Analyzed drawbacks of classical deblurring techniques  
- Understood Total Variation and its limitations  
- Explored Fractional-Order Variation concepts  
- Implemented the TFOV-based approach  
- Applied preconditioning to improve performance  
- Observed improved convergence and visual quality  

---

## 5. Challenges / Issues Faced

- Understanding the concept of fractional-order derivatives  
- High computational cost due to nonlocal behavior  
- Difficulty in choosing suitable parameters  
- Increased memory usage due to large matrices  
- Debugging convergence issues during iterations  

---

## 6. Future Plans

- Apply the method to real-world blurred images  
- Extend the model to handle color images  
- Compare results with deep learning-based deblurring methods  
- Improve computational efficiency using optimized solvers  
- Explore adaptive parameter selection techniques  

---

## Conclusion

This project demonstrates that combining the TFOV model with preconditioning techniques can effectively improve image deblurring results. The approach reduces common artifacts, preserves important image details, and improves computational efficiency.

---
