# Fitting Data to Linear Models Using p-Norms
> **Source:** [Fitting Data to Linear Models - Math Modelling - Lecture 21](https://www.youtube.com/watch?v=JlDCfTGkJZc) by Math Modelling · 36:11 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** Students in mathematical modeling or data science who want to understand how different distance measures affect linear regression and outlier sensitivity.
## Learning objectives

After working through this document you can:

1. Define the 1-norm, 2-norm, and infinity norm of a vector using real-world examples
2. Compute the p-norm of a vector for any p greater than or equal to 1
3. Explain how different p-norms emphasize different aspects of data (e.g., average vs. maximum)
4. Formulate an error function for fitting a linear model using a p-norm
5. Describe the effect of outliers on linear fits for different values of p
6. Identify the trade-off between robustness to outliers and mathematical convenience when choosing p=2
7. Interpret results from a convex optimization solver applied to linear regression with various p-norms
## Prerequisites

- Familiarity with vectors and vector components
- Basic calculus including derivatives
- Understanding of linear functions and slope-intercept form
## Introduction: Why Measure Distances for Data Fitting

In previous lessons, you learned how to analyze dynamical systems and derive mathematical models from theoretical principles. A dynamical system is a model that describes how a quantity changes over time, often using differential equations. However, purely theoretical models may not capture real-world behavior perfectly.

We are currently living in the age of big data. Large datasets are available from laboratories, research institutes, and public sources on the internet. These datasets contain measurements of actual phenomena. Your goal as a modeler is to use this real-world data to inform and improve your models. This process is called **data fitting**: adjusting a model so that its predictions match observed data as closely as possible.

To perform data fitting, you need a way to quantify how well a model’s predictions match the data. This requires measuring the distance (or error) between each observed data point and the corresponding model prediction. Different distance measures lead to different fitting methods. In this course, you will learn how to use **p-norms** to define these distances. A p-norm is a family of mathematical functions that measure the size of a vector; the choice of p (for example, p=1, p=2, or p=∞) changes how errors are aggregated and penalized.

By the end of this section, you will understand why measuring distances is a fundamental step in fitting data to linear models, setting the stage for the specific techniques that follow.

### Check your understanding

1.  What is the main motivation for fitting models to real-world data?
    <details>
    <summary>Answer</summary>
    To improve the accuracy of theoretical models by adjusting them to match actual observations from big data sources.
    </details>

2.  Why do we need to measure distances when fitting a model to data?
    <details>
    <summary>Answer</summary>
    To quantify the error between the model’s predictions and the observed data points. This error measurement guides the model adjustment process.
    </details>

3.  What role do p-norms play in data fitting?
    <details>
    <summary>Answer</summary>
    They provide a family of distance metrics that define how the error between predictions and observations is measured. Different p-norms yield different fitting behaviors and properties.
    </details>
## Three Intuitive Examples of Distance Measures

This section introduces three different ways to measure the "size" or "length" of a vector. Each method is called a **p-norm**, where the value of *p* determines how the distance is calculated. You will learn these through three concrete, everyday examples.

### Example 1: The Two Norm (Euclidean Distance)

Imagine you are standing at a reference point. Two airplanes are in the air around you. Their positions relative to you are given as vectors in three-dimensional space (north, east, up).

- **Airplane 1**: 25 kilometers north, 30 kilometers east, 1 kilometer up. This is the vector (25, 30, 1).
- **Airplane 2**: 35 kilometers north, 10 kilometers east, 2 kilometers up. This is the vector (35, 10, 2).

**Question:** Which airplane is farther from you?

The standard way to answer this is to use the **two norm** (also called the Euclidean norm or the Pythagorean distance). This is the "straight line" distance, or "as the crow flies."

**How to compute the two norm:**

For a vector **v** with components (v₁, v₂, v₃), the two norm is:

||**v**||₂ = √(v₁² + v₂² + v₃²)

Apply this to each airplane:

- **Airplane 1**: √(25² + 30² + 1²) = √(625 + 900 + 1) = √1526 ≈ 39.0
- **Airplane 2**: √(35² + 10² + 2²) = √(1225 + 100 + 4) = √1329 ≈ 36.5

**Result:** Using the two norm, Airplane 1 (distance ≈ 39) is farther from you than Airplane 2 (distance ≈ 36).

**Why is it called the "two norm"?** Look at the exponents in the calculation. Each component is raised to the power of 2 (squared), and the final result is raised to the power of 1/2 (square root). The number 2 appears throughout. This pattern will be different for the other norms.

### Example 2: The One Norm (Sum of Absolute Values)

Now consider a different scenario. You taught two classes the same material. Each class has five students. Their final grades are:

- **Class 1**: 82, 86, 90, 71, 74
- **Class 2**: 91, 76, 63, 85, 81

**Question:** Which class performed better overall?

You would not use the two norm here because it would not give a meaningful comparison of class performance. Instead, you would compare the class averages. To find the average, you add all the grades and divide by the number of students (5). Since both classes have the same number of students, you can simply compare the sums.

This sum is called the **one norm** (also called the Manhattan norm or taxicab norm).

**How to compute the one norm:**

For a vector **v** with components (v₁, v₂, v₃, v₄, v₅), the one norm is:

||**v**||₁ = |v₁| + |v₂| + |v₃| + |v₄| + |v₅|

The absolute value bars ensure that negative values (if they existed) would still contribute positively to the total distance from zero. In this example, all grades are positive, so the absolute values do not change the numbers.

Apply this to each class:

- **Class 1**: 82 + 86 + 90 + 71 + 74 = 403
- **Class 2**: 91 + 76 + 63 + 85 + 81 = 396

**Result:** Class 1 has a higher sum (403) than Class 2 (396). Therefore, Class 1 performed better overall. The low grade of 63 in Class 2 pulled its total down.

**Why is it called the "one norm"?** Each component is raised to the power of 1 (no exponent change), and the final result is raised to the power of 1/1 (no root). The number 1 appears throughout.

### Example 3: The Infinity Norm (Maximum Absolute Value)

Finally, imagine you and a friend are practicing javelin throws. Each person gets three throws. The winner is the person whose single longest throw is the farthest.

- **Person 1**: 82 meters, 73 meters, 79 meters
- **Person 2**: 81 meters, 78 meters, 83 meters

**Question:** Who wins?

You only care about the longest throw. This is measured by the **infinity norm** (also called the max norm or Chebyshev distance).

**How to compute the infinity norm:**

For a vector **v** with components (v₁, v₂, v₃), the infinity norm is:

||**v**||∞ = max(|v₁|, |v₂|, |v₃|)

You take the absolute value of each component (to measure distance from zero regardless of direction) and then select the largest value.

Apply this to each person:

- **Person 1**: max(|82|, |73|, |79|) = max(82, 73, 79) = 82
- **Person 2**: max(|81|, |78|, |83|) = max(81, 78, 83) = 83

**Result:** Person 2 wins with a longest throw of 83 meters, compared to Person 1's longest throw of 82 meters.

**Why is it called the "infinity norm"?** As the value of *p* in a p-norm increases, the norm becomes more dominated by the largest component. In the limit as *p* approaches infinity, the norm equals the maximum absolute value.

### Summary of the Three Norms

| Norm Name | Symbol | Formula for vector **v** with *n* components | What it measures | Example use case |
|-----------|--------|----------------------------------------------|------------------|------------------|
| One norm | ||**v**||₁ | Σᵢ |vᵢ| | Sum of absolute values | Class total scores |
| Two norm | ||**v**||₂ | √(Σᵢ vᵢ²) | Straight line distance | Distance between points |
| Infinity norm | ||**v**||∞ | maxᵢ |vᵢ| | Largest component | Best single performance |

### Check your understanding

1.  A vector is (3, -4, 0). What is its two norm? What is its one norm? What is its infinity norm?

    <details>
    <summary>Answer</summary>
    Two norm: √(3² + (-4)² + 0²) = √(9 + 16 + 0) = √25 = 5. One norm: |3| + |-4| + |0| = 3 + 4 + 0 = 7. Infinity norm: max(|3|, |-4|, |0|) = max(3, 4, 0) = 4.
    </details>

2.  You have two vectors representing daily sales for a week: A = (100, 200, 150) and B = (300, 50, 100). Which vector has a larger one norm? Which has a larger infinity norm?

    <details>
    <summary>Answer</summary>
    One norm of A: 100 + 200 + 150 = 450. One norm of B: 300 + 50 + 100 = 450. They are equal. Infinity norm of A: max(100, 200, 150) = 200. Infinity norm of B: max(300, 50, 100) = 300. B has a larger infinity norm.
    </details>

3.  Why does the one norm use absolute values around each component?

    <details>
    <summary>Answer</summary>
    The absolute value measures the distance of each component from zero, regardless of direction (positive or negative). This ensures that a negative value (like a loss or a throw in the wrong direction) still contributes positively to the total "size" of the vector, just as a positive value of the same magnitude would.
    </details>
## General Definition of p-Norms

A **norm** is a mathematical function that assigns a non-negative length or distance to a vector. The **p-norm** (written with a subscript p) is a family of norms that let you choose how the distance is measured. The value of p determines the specific formula. For any real number p greater than or equal to 1, the p-norm of a vector **x** with components x₁, x₂, …, xₙ is defined as:

```
||x||_p = ( |x₁|^p + |x₂|^p + ... + |xₙ|^p )^(1/p)
```

- The vertical bars `| |` mean absolute value.  
- The exponent p is applied to each absolute value, then the sum is taken, and finally the p‑th root is computed.  
- The vector can have any length (any number of components).

The subscript p tells you which norm you are using. Three common choices are p = 1, p = 2, and p = ∞ (infinity).

| p value | Name / Description | Formula | Notes |
|---------|-------------------|---------|-------|
| 1 | 1‑norm (Manhattan distance) | `||x||_1 = |x₁| + |x₂| + ... + |xₙ|` | Simply the sum of absolute values. |
| 2 | 2‑norm (Euclidean distance) | `||x||_2 = ( x₁² + x₂² + ... + xₙ² )^(1/2)` | Standard Euclidean distance. Absolute values are not needed because squaring already makes the value non‑negative. |
| ∞ | Infinity norm (Chebyshev distance) | `||x||_∞ = max( |x₁|, |x₂|, ..., |xₙ| )` | The maximum absolute value among all components. |

You can use any p ≥ 1. For example, you could choose p = 100 or p = 5,638,223. Each value of p gives a different way of measuring distance. The only requirement is that p is greater than or equal to 1.

When p = 1, the formula reduces to the sum of absolute values, as shown in the table. When p = 2, the absolute values become irrelevant because squaring a number already yields a positive result, so the formula matches the familiar Euclidean distance. When p = ∞, the norm is the maximum absolute component; this is equivalent to taking the limit of the p‑norm as p goes to infinity.

(Added context: The p‑norm is also called the Lᵖ norm. The infinity norm is often written as `||x||_∞`.)

### Check your understanding

1.  What is the p‑norm of the vector (3, -4) for p = 2?  
    <details><summary>Answer</summary>  
    ||(3, -4)||₂ = (3² + (-4)²)^(1/2) = (9 + 16)^(1/2) = 25^(1/2) = 5.  
    </details>

2.  For the same vector (3, -4), what is the infinity norm?  
    <details><summary>Answer</summary>  
    ||(3, -4)||_∞ = max( |3|, |-4| ) = max(3, 4) = 4.  
    </details>

3.  True or false: The p‑norm is defined for any real number p, including p = 0.5.  
    <details><summary>Answer</summary>  
    False. The p‑norm is defined only for p ≥ 1. (Values less than 1 do not satisfy the triangle inequality required for a norm.)  
    </details>
## What Different p-Norms Emphasize

This section explains how different p-norms emphasize different aspects of a dataset. You will learn how to interpret p-norm results and decide which norm is appropriate for a given practical situation.

### p-Norms: A Quick Review

A p-norm is a way to measure the size or magnitude of a vector. The general formula for a p-norm of a vector **x** with components x₁, x₂, ..., xₙ is:

||**x**||ₚ = (|x₁|^p + |x₂|^p + ... + |xₙ|^p)^(1/p)

You have already seen three specific p-norms:

- **1-norm (p = 1):** Sum of absolute values. Treats all components equally.
- **2-norm (p = 2):** Euclidean distance. Standard measure of magnitude.
- **Infinity-norm (p = ∞):** Maximum absolute value. Only the largest component matters.

### What Each p-Norm Emphasizes

The choice of p changes what the norm "cares about" most. The transcript uses two analogies to illustrate this: class grades and javelin throws.



#### Analogy 1: Class Grades

Suppose you have two classes, G1 and G2, and you want to identify which class has the single best student. You can use the infinity-norm to answer this question.

Here is the comparison:

| Class | Student 1 Grade | Student 2 Grade | Infinity-Norm Value |
|-------|-----------------|-----------------|---------------------|
| G1    | 91              | ?               | 91                  |
| G2    | 90              | ?               | 90                  |

The infinity-norm takes only the maximum value. For G1, the infinity-norm is 91. For G2, the infinity-norm is 90. Under this metric, G2 is better because 90 is larger than 89 (if G2's best student score is 90).

**Key concept:** The infinity-norm says "give me your best, that's all that I care about." It emphasizes the single largest value. The 1-norm, by contrast, takes everybody equal because it sums all absolute values. The infinity-norm ignores all other data points except the maximum.



#### Analogy 2: Javelin Throws

Now consider javelin throwing distances. Two athletes, D1 and D2, each make three throws. Their results are:

| Throw | D1 | D2 |
|-------|----|----|
| 1     | 90 | 73 |
| 2     | 90 | 90 |
| 3     | 90 | 90 |

D1 is perfectly consistent: every throw is 90 meters. D2 has one bad throw of 73 meters and two good throws of 90 meters.

If you take the average (which is equivalent to a 1-norm divided by the number of throws), the bad throw "sinks" D2. The average for D2 is (73 + 90 + 90) / 3 = 84.33, while D1's average is 90. Under the average metric, D1 is much better.

**Key concept:** The 1-norm (and the average, which is the 1-norm divided by the number of elements) is sensitive to every data point. A single low value pulls the total down significantly. The transcript compares this to "when your professor takes the average of all of your assignments, but you forgot to hand one in at the end of the year." That hurts a lot more than the professor saying "I'll just take your best assignment at the end of the year."

If you instead used the infinity-norm, you would compare only the maximum throws. Both D1 and D2 have a maximum of 90, so they would be considered equal. The infinity-norm ignores the bad throw entirely.

### How p-Norms Behave in Practice

Here is a summary of what each p-norm emphasizes:

| p-Norm | What It Emphasizes | Practical Use |
|--------|--------------------|---------------|
| 1-norm | All data points equally, no outlier is hidden | When every data point matters equally, and you want to penalize all deviations |
| 2-norm | Balanced emphasis, squares larger errors | When you want to penalize large errors more than small ones (standard least squares) |
| Infinity-norm | Only the maximum value | When you care only about the worst case or the best case |

### How to Choose the Right p-Norm

Follow this decision flow to select the appropriate p-norm for your problem:

```
Do you care about every data point?
  |
  +-- Yes: Are some errors dramatically worse than others?
  |     |
  |     +-- Yes, large errors are terrible: Use 1-norm (robust to outliers)
  |     |
  |     +-- No, all errors matter proportionally: Use 2-norm (least squares)
  |
  +-- No: Do you only care about the single worst (or best) value?
        |
        +-- Yes: Use infinity-norm
        |
        +-- No: Consider other criteria (not covered in this section)
```

### Check Your Understanding

1. **What is the infinity-norm of the vector [5, -2, 8, 3]?**

<details>
<summary>Answer</summary>
The infinity-norm is 8. It selects the maximum absolute value. The absolute values are 5, 2, 8, 3. The maximum is 8.
</details>

2. **You have three job candidates. Candidate A scores [95, 0, 0] on three tests. Candidate B scores [50, 50, 50]. Candidate C scores [90, 90, 10]. Which candidate is best under the 1-norm, and which is best under the infinity-norm?**

<details>
<summary>Answer</summary>
- **1-norm:** Candidate A: 95 + 0 + 0 = 95. Candidate B: 50 + 50 + 50 = 150. Candidate C: 90 + 90 + 10 = 190. Candidate C is best under the 1-norm because the sum is largest.
- **Infinity-norm:** Candidate A: max is 95. Candidate B: max is 50. Candidate C: max is 90. Candidate A is best under the infinity-norm because the single best test score is 95.
</details>

3. **In the javelin example, why does the average (a scaled 1-norm) make D2 look worse than D1, even though both have the same best throw?**

<details>
<summary>Answer</summary>
The 1-norm (and the average computed from it) includes every data point equally. D2's bad throw of 73 pulls the total sum down, while D1 has no low values. The infinity-norm would ignore the bad throw and show that both athletes have the same best throw of 90.
</details>

4. **You are fitting a line to sensor data. A few sensor readings are known to be faulty (outliers). Which p-norm should you use for the error function, and why?**

<details>
<summary>Answer</summary>
You should use the 1-norm (L1 regression, also called least absolute deviations). The 1-norm gives less weight to large errors compared to the 2-norm, so faulty outliers will not pull the fitted line away from the majority of good data points. (Added context: L1 regression is more robust to outliers than L2 regression.)
</details>
## Fitting a Linear Model with a p-Norm Error Function

In this section you will learn how to fit a linear model to data by minimizing a p-norm error function. The model is a discrete-time dynamical system: a straight line with slope \(m\) and intercept \(b\). You will define an error vector that measures the difference between the observed outputs and the model’s predictions, then use a p-norm to turn that vector into a single error value. The goal is to find the values of \(m\) and \(b\) that make this error as small as possible.

### Problem Setup

You have a set of \(M\) data points. Each point consists of an input \(x_i\) and an observed output \(y_i\). The data are organized as:

\[
(x_1, y_1), (x_2, y_2), \dots, (x_M, y_M)
\]

You want to find a linear function \(f(x) = m x + b\) that best matches these points. This is a line of best fit. In the language of dynamical systems, the function describes how the system evolves from one time step to the next, but here it is simply a line.

### The Error Vector

For a given choice of slope \(m\) and intercept \(b\), the model predicts the output \(m x_i + b\) for input \(x_i\). The difference between the observed output and the predicted output is:

\[
r_i = y_i - (m x_i + b)
\]

This difference is called the **residual** for data point \(i\). Collect all residuals into a vector:

\[
\mathbf{r} = \begin{pmatrix} r_1 \\ r_2 \\ \vdots \\ r_M \end{pmatrix}
\]

If the model were perfect, every residual would be zero and the vector \(\mathbf{r}\) would be the zero vector. In practice, you want to make the residuals as small as possible.

### The p-Norm Error Function

To measure the “size” of the residual vector, you use a **p-norm**. The p-norm of a vector \(\mathbf{v} = (v_1, v_2, \dots, v_M)\) is defined as:

\[
\|\mathbf{v}\|_p = \left( \sum_{i=1}^M |v_i|^p \right)^{1/p}
\]

where \(p \geq 1\). (For \(p = \infty\), the norm is \(\max_i |v_i|\).)

Apply this to the residual vector to define the **error function** \(E(m, b)\):

\[
E(m, b) = \|\mathbf{r}\|_p = \left( \sum_{i=1}^M |y_i - (m x_i + b)|^p \right)^{1/p}
\]

This function takes two inputs (\(m\) and \(b\)) and returns a single nonnegative number: the error. The table below summarizes the components of the error function.

| Component | Description |
|-----------|-------------|
| \(m\) | Slope of the linear model (unknown) |
| \(b\) | Intercept of the linear model (unknown) |
| \(x_i, y_i\) | Observed data point \(i\) (known) |
| \(y_i - (m x_i + b)\) | Residual for point \(i\) |
| \(p\) | Norm order (a positive real number, often 1, 2, or \(\infty\)) |
| \(\sum_{i=1}^M |\cdot|^p\) | Sum of absolute residuals raised to the \(p\)-th power |
| \((\cdot)^{1/p}\) | Normalization to keep the norm scale consistent |

### Goal: Minimize the Error

Your objective is to find the slope \(m\) and intercept \(b\) that make the error \(E(m, b)\) as small as possible. In mathematical terms:

\[
\min_{m, b} \; E(m, b)
\]

Because \(E\) is a function from \(\mathbb{R}^2\) (the space of \((m, b)\) pairs) to \(\mathbb{R}\) (the error value), you are performing a two-dimensional optimization.

### Special Case: \(p = \infty\)

When \(p = \infty\), the p-norm becomes the maximum absolute residual:

\[
E_\infty(m, b) = \max_{i=1,\dots,M} |y_i - (m x_i + b)|
\]

This error function measures the worst-case deviation between the model and the data. Minimizing it corresponds to finding a line that keeps the largest single error as small as possible.

### Summary of the Approach

1. Collect your data points \((x_i, y_i)\).
2. Choose a value of \(p\) (commonly 1, 2, or \(\infty\)).
3. Define the error function \(E(m, b)\) using the p-norm of the residual vector.
4. Find the \(m\) and \(b\) that minimize \(E(m, b)\).

This framework unifies many common fitting methods: \(p=2\) gives ordinary least squares, \(p=1\) gives least absolute deviations, and \(p=\infty\) gives minimax (Chebyshev) fitting.

---

### Check Your Understanding

1. **What is the residual for a single data point, and how is it used in the error function?**

   <details><summary>Answer</summary>
   The residual for data point \(i\) is \(r_i = y_i - (m x_i + b)\). It measures how far the model’s prediction is from the observed output. The error function sums the absolute residuals raised to the power \(p\) (and takes the \(p\)-th root) over all data points.
   </details>

2. **Write the explicit formula for the p-norm error function \(E(m, b)\) in terms of the data and the model parameters.**

   <details><summary>Answer</summary>
   \[
   E(m, b) = \left( \sum_{i=1}^M |y_i - (m x_i + b)|^p \right)^{1/p}
   \]
   </details>

3. **What does the error function become when \(p = \infty\)? How does this change the interpretation of “best fit”?**

   <details><summary>Answer</summary>
   When \(p = \infty\), the error function is \(E_\infty(m, b) = \max_i |y_i - (m x_i + b)|\). Instead of averaging errors, it focuses on the single largest deviation. Minimizing this error finds a line that minimizes the worst-case mismatch.
   </details>

4. **Why is the error function considered a function from \(\mathbb{R}^2\) to \(\mathbb{R}\)?**

   <details><summary>Answer</summary>
   The error function takes two inputs: the slope \(m\) and the intercept \(b\) (both real numbers). It outputs a single real number (the error). Therefore its domain is \(\mathbb{R}^2\) and its codomain is \(\mathbb{R}\).
   </details>
## Example with 13 Data Points: Similar Fits for Different p

In this section you will solve an unconstrained optimization problem to find the line of best fit for 13 data points. You will use different values of p in the p-norm error function and compare the resulting slope (m) and y-intercept (b). The key takeaway is that for this particular data set, the fits are nearly identical regardless of the p value you choose.

### The Optimization Problem



The error function you minimize is a function of two variables: the slope m and the y-intercept b. This is an unconstrained optimization problem because m and b can be any real numbers. You do not need Lagrange multipliers or other constraint techniques.

Several methods can find the minimum:

| Method | Description |
|--------|-------------|
| Calculus (closed form) | Take the derivative of the error function, set it equal to zero, and solve for m and b. This requires significant algebraic work. |
| Gradient descent | Iteratively step downhill along the gradient of the error function. |
| Newton's method | Use second derivative information to converge more quickly. |
| Direct plotting | Because the function has only two inputs (m and b) and one output (error), you can plot the error surface and estimate the minimum visually. |

(Added context: The video uses MATLAB's CVX convex optimization solver, which automates the minimization process.)

### The Data Set



The data set contains 13 input-output pairs, each representing a measurement. The video's example imagines these as observations of a yeast colony, where the input is the current amount of yeast and the output is the amount one hour later. The data set is purely expository and does not represent real experimental results.

The 13 data points (x, y pairs) are:

| Input x | Output y |
|---------|----------|
| 0.1     | 0.5      |
| 0.4     | 0.9      |
| 1.2     | 1.5      |
| 1.3     | 1.5      |
| 1.7     | 2.0      |
| 2.2     | 2.2      |
| 2.8     | 2.8      |
| 3.0     | 2.7      |
| 4.0     | 3.0      |
| 4.3     | 3.5      |
| 4.4     | 3.7      |
| 4.9     | 3.9      |

(Added context: The video mentions 11 data points at [22:28] and then corrects to 13. The complete list above contains the 13 points given in the transcript.)

### Minimization Results for Different p Values



The video uses MATLAB's CVX solver to minimize the p-norm error function for three different values of p. The solver returns the optimal m (slope) and b (y-intercept) for each case.

The results are:

| p    | Slope (m) | Y-intercept (b) |
|------|-----------|-----------------|
| 1    | 0.6873    | 0.6251          |
| 2    | 0.6713    | 0.6530          |
| 10   | 0.6470    | 0.6950          |

Notice that the slope values all share the first significant digit (0.6). The y-intercept values also share the first significant digit (0.6). The differences appear only in the hundredths place and beyond.

### Visualizing the Fits



To see how similar these lines are, plot the 13 data points on a scatter plot with x on the horizontal axis and y on the vertical axis. Then overlay the three lines:

- Line for p=1: y = 0.6873*x + 0.6251
- Line for p=2: y = 0.6713*x + 0.6530
- Line for p=10: y = 0.6470*x + 0.6950

The scatter plot should look like this:

```
y
|
|    .       .
|  .   .   .   .   .
| . . . . . . . . . . .
|. . . . . . . . . . . .
|________________________ x
```

The three lines will be nearly indistinguishable on the plot. They all pass through the same general region of points, and their slopes and intercepts are so close that the lines overlap visually.

### Why the Choice of p Does Not Matter for This Data Set



For the 13 given data points, the fitted line changes very little when you change p. The slope and y-intercept agree at the first significant digit across all three p values. This means that for this particular data set, you could use any p value and get essentially the same result.

However, this is not always true. The video hints that this property depends on the data. To demonstrate, the transcript adds two more data points: (0.5, 0.8) and (3.9, 0.3). These points would likely change the fits differently for different p values, making the choice of p more important.

### Check Your Understanding

1. Why is the optimization problem called "unconstrained" in this example?

<details>
<summary>Answer</summary>
The optimization is unconstrained because the slope m and y-intercept b can be any real numbers. There are no restrictions or constraints on their values. You do not need Lagrange multipliers or other constraint techniques.
</details>

2. For the 13 data points given, what are the slope and y-intercept when p equals 2?

<details>
<summary>Answer</summary>
When p equals 2, the slope m is 0.6713 and the y-intercept b is 0.6530.
</details>

3. How much do the three fitted lines differ from each other for the 13 data points?

<details>
<summary>Answer</summary>
The lines are very similar. The slope values all begin with 0.6, and the y-intercept values all begin with 0.6. Differences appear only in the hundredths place and beyond. On a scatter plot, the three lines are nearly indistinguishable.
</details>

4. Why does the video add two extra data points at the end, (0.5, 0.8) and (3.9, 0.3)?

<details>
<summary>Answer</summary>
The video adds these points to show that the similarity of fits for different p values is not guaranteed for all data sets. Adding outliers or points far from the general trend would likely cause the fits for different p values to diverge significantly, making the choice of p more important.
</details>
## Adding Outliers: Dramatic Effect of Larger p

In this section, we add two massive outliers to the yeast colony dataset and observe how the optimal line changes as we increase the value of p in the p-norm error function. The key takeaway: larger p values make the fitted line dramatically more sensitive to outliers, while smaller p values provide robustness.

### The Outliers

At [27:40], the speaker adds two extreme data points to the existing dataset. These are not subtle deviations. One point sits far above the main cluster, and another sits far to the right. The speaker notes that the residual for one of these points is about 0.5, while the typical residual is around 0.4. The fitted line with p = 2 previously gave a slope near 1, but with these outliers, the line will be pulled dramatically.

These outliers could represent real-world errors, such as a lab assistant's first day mistakes in a yeast colony experiment. The speaker emphasizes that even if the data seems faulty, you must work with what you are given. The outliers are not strategically chosen; they are random, and the same qualitative effect appears with many different outlier placements.

### Fitting with p = 1

At 28:23, the speaker repeats the fitting process using the CVX package, but this time with p = 1. The error function is:

```
minimize sum(|m * x_i + b - y_i|^p)
```

For p = 1, this becomes the sum of absolute errors. The resulting parameters are:

- m = 0.668
- b = 0.6333

This is remarkably close to the original fit without outliers (which had m ≈ 0.7 and b ≈ 0.6). The leading digit of each parameter is unchanged. The speaker highlights this as surprising: even with massive outliers, the p = 1 fit barely moves.

Why? Because with p = 1, the error contribution of each point grows linearly with its distance. A point that is 10 times farther away contributes 10 times the error, not 100 or 1000 times. The outliers do not dominate the error function. Every point contributes roughly equally, so the line stays close to the central trend.

### Step with p = 2

At 29:55, the speaker repeats the fit with p = 2. The results are:

- m = 0.57
- b = 0.9947

This is radically different. The first digit of m changed from 6 to 5, and b moved from 0.63 to nearly 1.0. The line is now tilted more steeply, trying to pull down to account for the low outlier and pull up to account for the high outlier. The squared error makes large residuals much more costly, so the optimizer spends more effort reducing those large distances.

### Step with p = 10

At 30:47, the speaker pushes to p = 10. The results are:

- m = 0.1340
- b = 1.9968

The line is now nearly horizontal. It is not exactly horizontal, but it is close. The slope has collapsed from 0.668 to 0.134. The intercept has risen to nearly 2. The line is essentially trying to pass through the midpoint of the two outliers, ignoring the dense cluster of points along the original trend.

### Visualizing the Effect

The speaker sketches the three lines (without the data scatter):

```
p = 1:  a line with moderate slope, close to the original fit
p = 2:  a line with a steeper tilt, pulled down and up by the outliers
p = 10: a nearly horizontal line, balancing the two outliers
```

The p = 10 line is "getting close to being horizontal" and looks like it is trying to split the difference between the two extreme points. If you took p = 100, the line would be even more horizontal.

### Why Larger p Amplifies Outliers

The mathematical reason is straightforward. Each term in the error function is:

```
|m * x_i + b - y_i|^p
```

When the absolute error is large, say 10, raising it to the power p makes it explode. For example:

| p | 10^p |
|---|------|
| 1 | 10   |
| 2 | 100  |
| 10| 10,000,000,000 |

The larger the p, the more weight is placed on points with large residuals. The optimizer, trying to minimize the total error, will focus its effort on reducing the largest terms. Those largest terms are exactly the outliers. So the line is pulled toward the outliers, and the fit to the majority of the data degrades.

### The Robustness of Small p

When p is small, especially p = 1, the outliers do not get "blown up" in the same way. Each point contributes to the error in proportion to its distance, not to a high power of its distance. The result is that the line remains close to the original fit, even with massive outliers. This is a form of robustness: the model is not unduly influenced by a few bad data points.

The speaker concludes that if the outliers were indeed mistakes, using p = 1 helps prevent those mistakes from having an outsized influence on the fitted model.

### Summary Table

| p value | m (slope) | b (intercept) | Sensitivity to outliers |
|---------|-----------|---------------|-------------------------|
| 1       | 0.668     | 0.6333        | Low, robust             |
| 2       | 0.57      | 0.9947        | Moderate                |
| 10      | 0.1340    | 1.9968        | High, nearly horizontal |

### Check your understanding

1. Why does the p = 1 fit remain close to the original line even with massive outliers?

<details><summary>Answer</summary>
With p = 1, the error contribution of each point grows linearly with its distance. Outliers do not dominate because their large distances only add a linear penalty, not an exponential one. The optimizer still cares about all points roughly equally, so the line stays close to the majority of the data.
</details>

2. What happens to the slope m as p increases from 1 to 10, and why?

<details><summary>Answer</summary>
The slope m decreases from 0.668 to 0.1340. As p increases, the error function places more weight on the largest residuals, which are the outliers. The optimizer tilts the line to reduce those large residuals, which means flattening the line to pass near the outliers, even though that ignores the original trend.
</details>

3. If you had a dataset with one extreme outlier, which p value would you choose to minimize its influence?

<details><summary>Answer</summary>
Choose p = 1. It gives the most robust fit because it does not amplify large residuals. Higher p values like 2 or 10 will pull the line toward the outlier.
</details>

4. What is the mathematical reason that 10^10 is much larger than 10^1, and why does that matter here?

<details><summary>Answer</summary>
10^10 = 10,000,000,000 while 10^1 = 10. The power operation multiplies the base by itself p times. In the error function, a large residual raised to a high power contributes a huge number to the total error, so the optimizer works hard to reduce that one term, which means it sacrifices the fit to other points.
</details>
## Practical Trade-Off and Conclusion

In this section you will learn why the choice of the norm parameter \(p\) involves a practical trade-off between robustness to outliers and mathematical convenience. You will see that \(p=1\) is theoretically optimal but computationally difficult, while \(p=2\) offers a smooth, easily differentiable function that is still reasonably robust. This is the “Goldilocks” choice used in most real-world applications.

### The Influence of the p-Norm on Outliers

Recall that the p‑norm of a vector of residuals \(\mathbf{r} = (r_1, r_2, \dots, r_n)\) is defined as

\[
\|\mathbf{r}\|_p = \left( \sum_{i=1}^{n} |r_i|^p \right)^{1/p}.
\]

The parameter \(p\) controls how much weight large residuals (outliers) receive.  

- **Large \(p\)** (e.g., \(p=10\)): Outliers are raised to a high power, so their residuals dominate the sum. A single outlier can drastically alter the fitted model.  
- **Small \(p\)** (e.g., \(p=1\)): All residuals contribute linearly, so outliers have a proportionally smaller influence.  

The speaker states: “Bigger values of P you use, the bigger influence you can have on outliers.”  

Thus, the smallest possible value of \(p\) is \(p=1\). Using \(p=1\) would give the most robust fit because outliers are not amplified. This is the **optimal setting** from a robustness standpoint.

### The Problem with \(p=1\): Absolute Values Are Hard to Differentiate

When \(p=1\), the norm becomes a sum of absolute values:

\[
\|\mathbf{r}\|_1 = \sum_{i=1}^{n} |r_i|.
\]

Fitting a linear model by minimizing this norm requires solving an optimization problem. Many widely used optimization algorithms, such as **Newton’s method** or **gradient descent**, rely on taking derivatives of the objective function. The absolute value function \(|x|\) has a derivative that is not defined at \(x=0\) (it is piecewise linear and has a “kink”).  

The speaker explains: “Absolute values are difficult to take derivatives of.”  

In practice, this means that using \(p=1\) forces you to either use specialized non‑smooth optimization techniques (like linear programming) or to accept computational complexity. Most practitioners prefer a simpler approach.

### The Compromise: \(p=2\) (The “Goldilocks” Choice)

When \(p=2\), the norm becomes:

\[
\|\mathbf{r}\|_2 = \sqrt{\sum_{i=1}^{n} r_i^2}.
\]

Minimizing the square of this norm (the sum of squared residuals) is equivalent to ordinary least squares. The function is a **quadratic function** of the model parameters.  

- **Smoothness**: A quadratic function is infinitely differentiable. “I can take derivatives of quadratic functions all day.” This makes it trivial to apply Newton’s method, gradient descent, or any calculus‑based solver.  
- **Outlier influence**: Outliers are squared, so they still have some effect, but not as drastic as with larger \(p\). The speaker notes that in the example (the “B value in particular”), outliers still shift the fit, but the shift is not “really, really, really drastically altering” the model.  

Therefore, \(p=2\) is the smallest value of \(p\) that yields a smooth, differentiable objective function. It is a “happy medium” between robustness (small \(p\)) and computational convenience (smooth function).  

The speaker calls this the “Goldilocks” choice: not too large (outliers dominate), not too small (non‑smooth), but just right.

### Summary Table: Comparison of p‑Norms

| p  | Objective function | Differentiability | Outlier influence | Practical use |
|----|-------------------|-------------------|-------------------|---------------|
| 1  | Sum of absolute values | Non‑differentiable at zero | Minimal (linear) | Theoretically optimal, but requires specialized solvers |
| 2  | Sum of squared values | Smooth (quadratic) | Moderate (squared) | Most common in practice (“Goldilocks”) |
| >2 | Sum of p‑th powers | Smooth for integer p | Large (very high powers) | Rarely used; outliers dominate |

### Conclusion and Next Steps

The practical trade-off is clear:  

- For robustness, \(p=1\) is best, but it is computationally inconvenient.  
- For ease of optimization, \(p=2\) is the smallest value that gives a smooth, differentiable function.  
- In practice, \(p=2\) is the standard choice because it balances robustness and mathematical tractability.

The video concludes with a preview of the next lecture: “I’m going to come back to these data fitting examples, and I’m going to look at fitting non‑linear functions, and in particular, we’re going to talk about the Lasso method.”

**Lasso** (Least Absolute Shrinkage and Selection Operator) is a regression method that uses an L1 penalty (absolute values), which is a return to the \(p=1\) idea but in a different context (regularization rather than pure norm minimization).

---

### Check Your Understanding

1. **Why is \(p=1\) considered the optimal setting for minimizing the influence of outliers?**  
   <details><summary>Answer</summary>  
   Because it uses the smallest possible value of \(p\) (1), which means that residuals are not raised to a higher power. Outliers therefore contribute linearly rather than being amplified, so they have the least possible effect on the fitted model.
   </details>

2. **What is the main practical difficulty with using \(p=1\)?**  
   <details><summary>Answer</summary>  
   The objective function becomes a sum of absolute values, which is not differentiable at points where a residual is zero. Many common optimization algorithms (Newton’s method, gradient descent) require derivatives, so they cannot be applied directly without special handling.
   </details>

3. **Why is \(p=2\) called the “Goldilocks” choice?**  
   <details><summary>Answer</summary>  
   It is the smallest value of \(p\) that produces a smooth, quadratic objective function (easy to differentiate), while still being small enough that outliers do not have an outsized influence on the model. It is a compromise between robustness and computational convenience.
   </details>

4. **In the context of this course, what is the next topic after this section?**  
   <details><summary>Answer</summary>  
   Fitting non‑linear functions and the Lasso method.
   </details>
## Key takeaways

- The p-norm of a vector is a general measure of its size, defined as the p-th root of the sum of the absolute values of its components raised to the power p.
- The 1-norm (sum of absolute values) treats all components equally, making it analogous to an average.
- The 2-norm (Euclidean distance) is the standard geometric distance and is the most common choice in practice due to its mathematical convenience.
- The infinity-norm (maximum absolute value) only cares about the largest component, analogous to taking the best score.
- Fitting a linear model using a p-norm involves minimizing the p-norm of the vector of residuals, which are the differences between observed and predicted values.
- Without outliers, the choice of p has little effect on the resulting linear fit.
- Larger values of p (like p=10) are highly sensitive to outliers because large residuals are magnified by the exponent, forcing the fit to prioritize reducing those errors.
- Smaller values of p (like p=1) are more robust to outliers because they do not magnify large residuals as much.
- The trade-off is that p=2 offers a smooth, differentiable error function that is easy to optimize, while p=1 is more robust but involves absolute values that are harder to work with mathematically.
- Convex optimization solvers can efficiently find the best m and b for any p-norm error function, enabling practical comparison of different fits.
## Glossary

| Term | Definition |
|---|---|
| p-norm | A mathematical function that measures the size or length of a vector, defined as the p-th root of the sum of the absolute values of its components raised to the power p, where p is any real number greater than or equal to 1. |
| 1-norm | A specific p-norm where p equals 1, computed as the sum of the absolute values of the vector's components. |
| 2-norm | A specific p-norm where p equals 2, computed as the square root of the sum of the squared components, also known as the Euclidean distance. |
| infinity-norm | A specific p-norm defined as the maximum of the absolute values of the vector's components, representing the limit of the p-norm as p approaches infinity. |
| vector | An ordered list of numbers, often representing quantities like position, grades, or measurements in a multi-dimensional space. |
| residual | The difference between an observed data point and the value predicted by a model, representing the error of the model for that specific point. |
| error function | A function that quantifies the total error or misfit between a model's predictions and the actual data, which is minimized during the fitting process. |
| linear model | A model that describes the relationship between an input variable x and an output variable y using a straight line, typically expressed as y equals m x plus b. |
| slope (m) | A parameter in a linear model that determines the steepness and direction of the line, representing the change in y for a one-unit change in x. |
| y-intercept (b) | A parameter in a linear model that represents the value of y when x is equal to zero. |
| outlier | A data point that differs significantly from other observations in a dataset, often due to measurement error or a rare event. |
| robustness | The property of a statistical method or model to be insensitive to the presence of outliers or violations of its underlying assumptions. |
| convex optimization | A subfield of optimization that deals with minimizing convex functions over convex sets, where any local minimum is also a global minimum, making the problem tractable. |
| convex optimization solver | A software tool or algorithm designed to find the optimal solution to a convex optimization problem, such as the CVX package mentioned in the lecture. |
| unconstrained optimization | An optimization problem where the variables being optimized (like m and b) can take any real value without any restrictions or constraints. |
| absolute value | The non-negative value of a real number without regard to its sign, representing its distance from zero. |
| Euclidean distance | The straight-line distance between two points in Euclidean space, computed using the 2-norm of the difference vector. |
| gradient descent | An iterative optimization algorithm that moves in the direction of the steepest descent of the error function to find a minimum. |
| Newton's method | An iterative optimization algorithm that uses second-order derivative information (the Hessian) to find the minimum of a function, often converging faster than gradient descent. |
| discrete time dynamical system | A system where the state evolves at discrete time steps, often modeled by an equation like x at the next time step equals m times x at the current time step plus b. |
## Footnotes and deeper context

1. **p-norm definition range.** The p-norm is a valid norm only for p greater than or equal to 1. For values of p between 0 and 1, the function does not satisfy the triangle inequality and is therefore not a true norm, though it is sometimes used in other contexts.
2. **infinity norm as limit.** The infinity norm is formally defined as the limit of the p-norm as p approaches infinity. This limit equals the maximum absolute value of the vector's components, which is why it is also called the max norm or Chebyshev norm.
3. **p=2 and least squares.** Minimizing the 2-norm of the residuals is equivalent to the ordinary least squares (OLS) method. This is the most common approach because the resulting error function is quadratic and differentiable, allowing for a closed-form solution using linear algebra.
4. **p=1 and absolute deviations.** Minimizing the 1-norm of the residuals is known as least absolute deviations (LAD) regression. Unlike OLS, LAD does not have a closed-form solution but can be solved efficiently using linear programming techniques.
5. **convexity of p-norm error.** For any p greater than or equal to 1, the p-norm of the residual vector is a convex function of the model parameters m and b. This guarantees that any local minimum found by an optimization solver is also the global minimum.
6. **CVX solver.** CVX is a MATLAB-based modeling system for convex optimization. It allows users to specify optimization problems in a natural mathematical syntax and automatically converts them into a form solvable by standard solvers like SeDuMi or SDPT3.
7. **outlier effect on p=10.** For very large p, the p-norm is dominated by the single largest residual. This causes the optimal fit to prioritize making that largest residual as small as possible, often at the expense of fitting the rest of the data well, which explains the nearly horizontal line in the example.
## Where to go next

- **Read about the CVX software package.** Visit the official CVX website (cvxr.com) to learn how to install and use this convex optimization solver in MATLAB. The documentation includes tutorials and examples for solving p-norm minimization problems.
- **Study least absolute deviations regression.** Search for 'least absolute deviations' or 'L1 regression' in textbooks or online resources like Wikipedia. This method uses the 1-norm and is a key alternative to ordinary least squares for robust fitting.
- **Explore the Lasso method.** The lecture mentions the Lasso method as a topic for the next lecture. Look for resources on 'Lasso regression' or 'L1 regularization' to understand how p-norms are used for feature selection in machine learning.
- **Review convex optimization theory.** Read 'Convex Optimization' by Boyd and Vandenberghe, which is freely available online. This book provides a thorough mathematical foundation for understanding why p-norm error functions are convex and how solvers like CVX work.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
