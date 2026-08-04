# Fitting Nonlinear Models with LASSO Regression: Regularization and Interpretability
> **Source:** [Fitting Nonlinear Models with LASSO Regression - Math Modelling - Lecture 22](https://www.youtube.com/watch?v=IglP4Zjhefw) by Math Modelling · 17:16 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students and practitioners of mathematical modeling who want to extend linear fitting to nonlinear systems and learn how to balance model accuracy with coefficient interpretability using LASSO regression.
## Learning objectives

After working through this document you can:

1. Formulate a nonlinear fitting problem by extending linear regression to polynomial functions of arbitrary degree.
2. Construct an error function using p-norms to measure the discrepancy between predicted and observed data points.
3. Explain the challenge of high-dimensional coefficient spaces and the need for coefficient regularization.
4. Define a regularized error function that includes a penalty term for the size of the coefficient vector.
5. Describe the role of the regularization parameter lambda and its effect on the trade-off between data fit and coefficient size.
6. Identify the LASSO method as a specific case with p=2 and q=1, and justify why q=1 treats all coefficients equally.
7. Compare the behavior of different q-norms in regularization and their impact on large versus small coefficients.
8. Evaluate the practical implications of choosing lambda, including the need for hyperparameter tuning and human decision making.
## Prerequisites

- Familiarity with basic calculus, including derivatives and absolute value functions.
- Understanding of linear regression and the concept of lines of best fit.
- Knowledge of p-norms and their properties (especially p=1 and p=2).
- Basic linear algebra: vectors, coefficients, and matrix notation.
- Experience with optimization and error functions.
## Introduction and Review of Linear Fitting

This section reviews the core concepts of linear fitting that were introduced in a previous lecture. You will revisit the idea of a "line of best fit" and the different ways to measure the distance between data points and a fitted line. These distance measures, called P norms, have different properties that make them more or less suitable for different datasets.

### Lines of Best Fit and Distance Measures

In the previous lecture, you were introduced to the concept of a line of best fit in the context of linear dynamical systems. A line of best fit is a straight line that is intended to represent the general trend of a set of data points. The goal is to find the line that minimizes the total "error" or "distance" between the line and the data points.

The way you measure this distance is crucial. You have several options, which are defined by a family of mathematical functions called **P norms**. A P norm is a way to calculate the magnitude of a vector, and in this context, it is used to calculate the distance between a predicted value (on the line) and an actual data point.

### The P Norms and Their Trade-offs

The speaker discusses two specific P norms:

1.  **P = 2 (Euclidean norm):** This is the standard, straight-line distance you are most familiar with. It is easy to work with mathematically because it is smooth and differentiable. However, it is very sensitive to **outliers** (data points that are far from the rest). A single outlier can have a very large squared distance, which can pull the line of best fit away from the majority of the data.

2.  **P = 1 (Manhattan norm):** This is the sum of the absolute values of the distances. The speaker states that this is the best norm for handling outliers. Because it does not square the distance, a single outlier has a proportionally smaller influence on the total error compared to the P=2 norm. This makes the fitted line more robust to outliers.

### The Practical Problem with P = 1

While the P=1 norm is better for handling outliers, it introduces a significant mathematical challenge. The function for the P=1 norm contains an absolute value. As you learn in basic calculus, the absolute value function has a non-continuous derivative. Specifically, its derivative is undefined at the point where the value inside the absolute value is zero.

This non-differentiability makes the P=1 norm a "hard function to differentiate." Because many standard optimization algorithms rely on calculating derivatives (gradients) to find the minimum error, the P=1 norm is more difficult to work with computationally than the P=2 norm.

### Summary of Key Concepts

| Concept | Description | Key Property |
| :--- | :--- | :--- |
| **Line of Best Fit** | A straight line that represents the general trend of data points. | Minimizes the total distance between the line and the data. |
| **P Norm** | A mathematical function used to measure the distance between a predicted value and an actual data point. | Different values of P produce different distance measures. |
| **P = 2 (Euclidean)** | Standard straight-line distance. | Easy to differentiate but very sensitive to outliers. |
| **P = 1 (Manhattan)** | Sum of absolute distances. | Best for handling outliers but hard to differentiate due to the absolute value function. |
| **Outlier** | A data point that is far away from the rest of the data. | Can disproportionately influence a line of best fit, especially when using the P=2 norm. |
| **Non-continuous derivative** | A derivative that has a "jump" or is undefined at a point. | The absolute value function has a non-continuous derivative at zero, making P=1 optimization more difficult. |

### Check your understanding

1.  Why is the P=1 norm considered better for handling outliers than the P=2 norm?
    <details><summary>Answer</summary>The P=1 norm uses absolute distances, so a single outlier does not have an exaggerated (squared) influence on the total error. The P=2 norm squares the distance, giving outliers a disproportionately large influence.</details>

2.  What is the main mathematical disadvantage of using the P=1 norm for fitting a line?
    <details><summary>Answer>The P=1 norm contains an absolute value function, which has a non-continuous derivative. This makes it a "hard function to differentiate" and more difficult to use with standard optimization algorithms that rely on derivatives.</details>

3.  In the context of this section, what is a "line of best fit"?
    <details><summary>Answer>A line of best fit is a straight line that is intended to represent the general trend of a set of data points by minimizing the total distance (error) between the line and the data points.</details>
## Extending to Polynomial Fitting

The previous section covered linear models of the form `y = c0 + c1 * x`. This section extends that approach to nonlinear relationships, specifically polynomial functions. The core process remains identical: you still fit coefficients to data by minimizing an error function. What changes is the form of the model you fit.

### The Polynomial Model

Instead of assuming a linear relationship between input `x` and output `y`, you now assume the relationship can be described by a polynomial of degree `D`. The model becomes:

```
f(x) = c0 + c1 * x + c2 * x^2 + ... + cD * x^D
```

Here:
- `D` is the polynomial degree, which you choose.
- `c0, c1, c2, ..., cD` are the coefficients you need to fit to your data.

For example, if you are modeling a logistic map (a common discrete-time dynamical system), you would use `D = 2` because the logistic map is a quadratic function, a "nice little hump function." In the previous video's context, you only went up to linear order, meaning you tuned only the y-intercept (`c0`) and the slope (`c1`). Now you have many more terms to tune.

You can think of this polynomial as a Taylor expansion of the true underlying function. (Added context: A Taylor expansion approximates a function as an infinite sum of polynomial terms; truncating it at degree `D` gives a polynomial approximation.)

### The Data Structure

The data you work with is sequential. Each data point is a pair:

```
(x_n, x_{n+1})
```

This means you know how to get from one step to the next. For example, the data could be:
- Hour 0 to hour 1
- Hour 1 to hour 2
- Hour 2 to hour 3
- ...
- Hour 100 to hour 101

Your goal is to find the function `f` that maps each `x_n` to `x_{n+1}`. In other words, you are fitting a discrete-time dynamical process:

```
x_{n+1} = f(x_n) = c0 + c1 * x_n + c2 * x_n^2 + ... + cD * x_n^D
```

The data points are assumed to be sampled from some underlying process. For simplicity, the examples use points in `R^2` (two-dimensional space), but you can extend this to higher dimensions; the math just becomes "uglier."

### The Error Function

The setup of the optimization problem is exactly the same as in the linear case. You define an error function that measures how poorly your polynomial fits the data. The error function again has a value of `p`, meaning you can use different norms (e.g., `p = 2` for squared error, which is common). The exact form of the error function is:

```
E = sum over all data points of |f(x_n) - x_{n+1}|^p
```

You then minimize this error function with respect to the coefficients `c0, c1, ..., cD`. This is the same process as before, just with more parameters to fit.

### The Complete Workflow

Here is the full process you follow:

1. **Collect sequential data points** `(x_n, x_{n+1})` from your process.
2. **Choose a polynomial degree** `D` based on what you know about the system (e.g., `D = 2` for a logistic map).
3. **Set up the polynomial model** with unknown coefficients `c0` through `cD`.
4. **Define the error function** with your chosen value of `p` (e.g., `p = 2` for squared error).
5. **Minimize the error function** to find the best coefficients.
6. **Use the fitted polynomial** to predict future values of the dynamical system.

### Visualizing the Structure

The relationship between the data and the model can be visualized as follows:

```
+------------------+     +---------------------------+
|  Input: x_n      | --> |  Polynomial model:        |
|  (current state) |     |  f(x) = c0 + c1*x + ...  |
+------------------+     |  + cD*x^D                |
                         +---------------------------+
                                      |
                                      v
                         +-----------------------+
                         |  Output: x_{n+1}      |
                         |  (next state)         |
                         +-----------------------+
```

The data is given to you as pairs `(x_n, x_{n+1})`. You are fitting the function that takes you from "what I'm doing now" to "what I'm doing next."

### Key Differences from Linear Regression

| Aspect | Linear Model | Polynomial Model |
|--------|--------------|------------------|
| Model form | `f(x) = c0 + c1*x` | `f(x) = c0 + c1*x + c2*x^2 + ... + cD*x^D` |
| Number of coefficients | 2 | `D + 1` |
| Degree | 1 | `D` (you choose) |
| Flexibility | Limited to straight lines | Can fit curves and humps |
| Typical use | Simple linear relationships | Nonlinear dynamical systems |

### Choosing the Polynomial Degree

The choice of `D` depends on your knowledge of the underlying system:
- If you know the system follows a logistic map, use `D = 2`.
- If you have no prior knowledge, you may need to try several values of `D` and compare error values.
- Higher `D` gives more flexibility but risks overfitting (fitting noise rather than the true relationship).

### Check your understanding

1. **What is the key difference between the linear model from the previous section and the polynomial model introduced here?**

<details><summary>Answer</summary>
The linear model only includes terms up to `x^1` (i.e., `c0 + c1*x`), while the polynomial model includes terms up to `x^D` (i.e., `c0 + c1*x + c2*x^2 + ... + cD*x^D`). The polynomial model has `D + 1` coefficients instead of just 2, allowing it to fit nonlinear relationships.
</details>

2. **How is the data structured for this polynomial fitting problem?**

<details><summary>Answer</summary>
The data is sequential, given as pairs `(x_n, x_{n+1})`. Each pair represents a transition from one state to the next in a discrete-time dynamical system. For example, hour 0 to hour 1, hour 1 to hour 2, and so on.
</details>

3. **If you are fitting a logistic map, what polynomial degree should you choose and why?**

<details><summary>Answer</summary>
You should choose `D = 2` because the logistic map is a quadratic function, which is a "nice little hump function." A degree-2 polynomial can exactly represent this type of relationship.
</details>

4. **What role does the error function play in this process, and what does the value of `p` control?**

<details><summary>Answer</summary>
The error function measures how poorly the fitted polynomial predicts the next state `x_{n+1}` from the current state `x_n`. The value of `p` determines the norm used in the error calculation; for example, `p = 2` gives squared error, which is the most common choice. You minimize this error function to find the best coefficients.
</details>
## Error Function for Polynomial Coefficients

In this section you will construct the error function that the LASSO regression algorithm will minimize. The error function measures how well your polynomial model fits the observed data. You will use a p-norm to quantify the difference between the predicted outputs and the actual outputs.

### The Error Function Formula

The error function takes in the coefficients of your polynomial and fits them according to a p-norm. A p-norm is a way to measure the magnitude of a vector; for a vector of errors, the p-norm raises each component to the power p, sums them, and takes the p-th root. (Added context: The most common p-norms are p=2 for Euclidean distance and p=1 for Manhattan distance.)

The error function is defined as:

```
Error = sum from i=1 to n of (y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d))^p
```

Where:
- n is the number of data points
- y_i is the actual output for the i-th data point
- x_i is the input for the i-th data point
- c_0, c_1, ..., c_d are the polynomial coefficients you are trying to find
- d is the degree of the polynomial
- p is the exponent in the p-norm

### Step by Step Construction

1. Start with the difference between the actual output and the predicted output for each data point i.

   ```
   y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d)
   ```

2. Raise this difference to the power p.

   ```
   (y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d))^p
   ```

3. Sum this quantity over all data points from i=1 to i=n.

   ```
   sum from i=1 to n of (y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d))^p
   ```

### Understanding the Goal

If each component inside the sum were zero, that would mean you perfectly matched every input to its corresponding output. In other words, if for every data point i:

```
y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d) = 0
```

Then the error would be zero, and your polynomial would pass through every data point exactly. In practice, this is rarely possible or desirable due to noise in the data and the risk of overfitting.

### Key Concepts

| Concept | Definition |
|---------|------------|
| Error function | A mathematical expression that quantifies how far your model's predictions are from the actual data |
| Polynomial coefficients | The parameters c_0, c_1, ..., c_d that define the shape of the polynomial curve |
| p-norm | A measure of vector magnitude where each component is raised to the power p, summed, and the p-th root is taken |
| Data point | A single pair of input x_i and output y_i from your dataset |
| Perfect fit | The condition where every predicted output exactly equals the actual output, making the error zero |

### Check your understanding

1. What does the error function measure in polynomial regression?

<details><summary>Answer</summary>
The error function measures how well the polynomial model fits the observed data by quantifying the difference between the predicted outputs and the actual outputs. It sums the p-norm of these differences across all data points.
</details>

2. If the error function equals zero, what does that tell you about the polynomial fit?

<details><summary>Answer</summary>
If the error function equals zero, it means the polynomial perfectly matches every data point. For each data point i, the predicted output equals the actual output, so the difference y_i minus the polynomial prediction is zero for all i.
</details>

3. What role do the polynomial coefficients play in the error function?

<details><summary>Answer</summary>
The polynomial coefficients (c_0, c_1, ..., c_d) are the parameters that the error function takes as input. The goal is to find the values of these coefficients that minimize the error function, thereby finding the best fitting polynomial for the given data.
</details>
## Challenges of High-Dimensional Fitting and the Need for Regularization



In the previous video, you worked with a model that had a two-dimensional input. You could plot the loss function (also called the error function) and find the minimum by visual inspection. That approach was possible because the input space was small enough to visualize.

Now consider what happens when you increase the complexity of your model. If you use a polynomial of degree 2 (quadratic order), the input becomes three-dimensional (features for \(x\), \(x^2\), and the bias term) with a one-dimensional output. This is already harder to visualize and optimize. In real-world applications, relationships are typically very nonlinear. To get a good fit for your data, you might need a polynomial of degree 100.

### The Dimensionality Problem

When you use a degree 100 polynomial, you have a 101-dimensional input (100 polynomial terms plus one bias term). The model becomes a single large polynomial function. This presents two immediate problems:

1. **Optimization becomes extremely difficult.** You cannot visualize the loss function in 101 dimensions to find the minimum.
2. **The coefficients become uninterpretable.** Consider what these coefficients might look like:

```
0.98632
127.629
-39.68
...
```

These numbers are arbitrary, large, and provide no insight into the relationship between inputs and outputs. The model may fit the training data well, but the coefficients have no clear meaning.

### The Role of p-Values and Regularization

Recall from the previous video that you used p equal to 1 (L1 norm) to help remove outliers and p equal to 2 (L2 norm) to make the model better behaved. These techniques help control the magnitude and behavior of coefficients. However, they alone do not solve the interpretability problem when you have a very high-dimensional polynomial.

### The Fundamental Trade-off in Data Science

You face a central trade-off in data science:

- **High accuracy:** You can get very accurate descriptions of the data by fitting a very high-degree polynomial (like degree 100). The model matches the training data closely.
- **Interpretability:** The resulting function is complicated, ugly, and difficult to work with. Throughout your mathematical career, you have likely avoided very complicated functions because they are hard to work with and take a long time to process. For example, differentiating a degree 100 polynomial requires handling all 101 terms. While differentiation itself is not that bad, the sheer volume of terms makes the computation slow and the result difficult to reason about.

The goal is to find a balance: you want a model that is accurate enough but also interpretable enough that you can understand and trust its predictions.

### Check your understanding

**Question 1:** Why can you not simply plot the loss function to find the minimum when using a degree 100 polynomial?

<details><summary>Answer</summary>
A degree 100 polynomial has 101 input dimensions. You cannot visualize a 101-dimensional loss function. You would need to optimize in a space that is too large to plot or inspect visually.
</details>

**Question 2:** What two problems do the coefficients of a high-degree polynomial create?

<details><summary>Answer</summary>
First, the coefficients are arbitrary and large (e.g., 0.98632, 127.629, -39.68), making them meaningless to interpret. Second, optimizing and differentiating a 101-term polynomial is computationally slow and the result is hard to reason about.
</details>

**Question 3:** What is the central trade-off described in this section?

<details><summary>Answer</summary>
The trade-off is between accuracy and interpretability. You can achieve high accuracy by using a very high-degree polynomial, but the resulting model becomes complicated, uninterpretable, and difficult to work with. The challenge is to find a model that is both accurate enough and interpretable enough.
</details>

**Question 4:** How did using p equal to 1 (L1 norm) help in the previous video?

<details><summary>Answer</summary>
Using p equal to 1 helped remove outliers. L1 regularization can drive some coefficients to exactly zero, which effectively removes irrelevant or outlier-influenced features from the model.
</details>
## Regularized Error Function and the Role of Lambda

When fitting a nonlinear model with many basis functions (for example, a polynomial of degree d), the coefficients can become very large. Large coefficients make the model sensitive to small changes in the input and create a heavy accounting burden to keep them balanced. To control this, we augment the original error function with a penalty term.

### The Regularized Error Function

We define a new error function, call it E_tilda, that depends on the coefficient vector c. The function has two parts:

1. The original error function (the measure of how well the model fits the data).
2. A regularization term that penalizes the size of the coefficients.

The regularized error function is written as:

```
E_tilda(c) = ( (1/N) * sum_{i=1}^{N} | y_i - (c_0 + c_1 * x_i + c_2 * x_i^2 + ... + c_d * x_i^d) |^p )^(1/p) + lambda * ||c||_q
```

Where:
- The first term is the original error function using a p-norm. The p norm describes the measure of the error. (added context: p=2 gives the standard squared error; p=1 gives absolute error.)
- The second term is lambda times the q-norm of the coefficient vector c. The q norm describes the size of the coefficients. (added context: q=1 gives LASSO regularization; q=2 gives ridge regularization.)
- lambda is the regularization parameter.

### The Role of Lambda

The regularization parameter lambda is always positive. It can be zero. If lambda equals zero, you recover the original error function with no penalty.

The regularized error function breaks into two competing components:

- **Component 1 (the data fit term):** This asks that you fit the data well. A smaller value means a better fit.
- **Component 2 (the regularization term):** This asks that you keep the coefficients small. A smaller value means smaller coefficients.

The goal is to make the entire expression E_tilda(c) as small as possible. The ideal way to make it small is to have both terms be zero, but that is not possible in practice. To minimize the sum, you must have both terms be small together. There is a tradeoff between fitting the data and keeping coefficients small.

The larger lambda is, the more preference you have for small coefficients. A large lambda forces the optimization to prioritize shrinking the coefficients, even if it means a worse fit to the data. A small lambda (close to zero) prioritizes fitting the data, allowing coefficients to grow larger.

### Summary Table: Effect of Lambda

| Lambda value | Preference | Effect on coefficients | Effect on data fit |
|---|---|---|---|
| lambda = 0 | No regularization | Coefficients can be large | Best possible fit |
| lambda > 0 (small) | Mild preference for small coefficients | Coefficients slightly shrunk | Slightly worse fit |
| lambda > 0 (large) | Strong preference for small coefficients | Coefficients heavily shrunk | Worse fit, simpler model |

### Check your understanding

1. What happens to the regularized error function if lambda is set to zero?

<details><summary>Answer</summary>
If lambda is zero, the regularization term disappears and you recover the original error function with no penalty on the coefficients.
</details>

2. What does a large value of lambda indicate about the modeler's preference?

<details><summary>Answer</summary>
A large lambda indicates a strong preference for small coefficients. The modeler is willing to accept a worse fit to the data in order to keep the coefficient values small.
</details>

3. Why can we not simply set both terms of the regularized error function to zero?

<details><summary>Answer</summary>
Setting the data fit term to zero would require a perfect fit to the data, which is rarely possible. Setting the regularization term to zero would require all coefficients to be exactly zero, which would make the model useless. In practice, we must find a compromise where both terms are small but neither is zero.
</details>
## LASSO Method: p=2, q=1 and Why q=1 Treats All Coefficients Equally

In this section you will learn how the LASSO (Least Absolute Shrinkage and Selection Operator) method balances data fit with coefficient size, why the regularization term uses a specific norm (q=1), and how that choice affects every coefficient equally.

### The Role of Lambda: Balancing Fit and Interpretability

The LASSO objective function has two competing parts: a data‑fit term and a regularization term. The regularization term is multiplied by a hyperparameter called **lambda** (λ). Lambda controls how much you penalize large coefficients.

- **Lambda = 0**: The regularization term is ignored. The model simply fits the data as well as possible, regardless of how large the coefficients become. This gives the best possible fit but often produces coefficients that are hard to interpret.
- **Lambda very large** (e.g., 1,000,000): The regularization term dominates. The best way to minimize the total objective is to make all coefficients very small, even if that means a poor fit to the data. The model sacrifices accuracy for interpretability.
- **Lambda in a “Goldilocks” zone**: A moderate lambda produces a compromise: a reasonably good fit with coefficients that are small enough to be interpretable.

 (No screenshot available; the speaker describes these three regimes.)

Lambda is a **hyperparameter**: it must be chosen *before* you solve for the coefficients. In practice, you try many different lambda values, solve the optimization for each, and then select the lambda that gives the best result according to your goal (e.g., prediction accuracy or interpretability).

| Lambda value | Effect on coefficients | Effect on data fit |
|--------------|------------------------|---------------------|
| 0            | No penalty; coefficients can be large | Best possible fit |
| Very large   | All coefficients forced toward zero | Poor fit |
| Moderate     | Coefficients are small but not zero | Good enough fit |

### LASSO: p=2, q=1

The LASSO method is a specific form of regularized regression. It uses:

- **p = 2** in the data‑fit term (the usual squared error, which is smooth and easy to differentiate).
- **q = 1** in the regularization term (the L1 norm of the coefficient vector).

The full objective is:

```
minimize  (1/2) * sum( (y_i - f(x_i))^2 )  +  lambda * ||c||_1
```

where `||c||_1` is the sum of the absolute values of the coefficients.

### Why q=1 Treats All Coefficients Equally

The choice q=1 is called the “ultimate regularizer” because it penalizes every coefficient equally, regardless of its size. To see why, compare q=1 with a larger q, say q=10.

Consider a coefficient vector `c = [1, 10]`. Compute the q‑norm:

```
||c||_q = ( |c1|^q + |c2|^q )^(1/q)
```

- **q = 1**: `(1^1 + 10^1)^(1/1) = 1 + 10 = 11`. Both coefficients contribute linearly. The optimization tries to shrink both 1 and 10 by the same relative amount.
- **q = 10**: `(1^10 + 10^10)^(1/10)`. Here `1^10 = 1` and `10^10 = 10,000,000,000`. The huge term `10^10` dominates the sum. The norm is approximately `(10^10)^(1/10) = 10`. The small coefficient (1) has almost no effect. The optimization will focus almost entirely on shrinking the large coefficient (10) and ignore the small one.

Thus, when q is larger than 1, the regularization term “prefers” to shrink the biggest coefficients first, treating them unequally. With q=1, every coefficient is treated equally: the penalty for increasing any coefficient by one unit is the same, regardless of how large that coefficient already is. This encourages all coefficients to be small together, without favoring outliers.

This is analogous to the behavior of p in the data‑fit term: larger p values give more weight to large residuals (outliers). Here, larger q gives more weight to large coefficients.

### Check your understanding

1. **What happens to the LASSO solution when lambda is set to 0?**  
   <details><summary>Answer</summary>  
   The regularization term is ignored, and the model simply fits the data as well as possible, allowing coefficients to be arbitrarily large.  
   </details>

2. **Why is lambda called a hyperparameter?**  
   <details><summary>Answer</summary>  
   Because it must be chosen before the optimization is performed; it is not learned from the data during fitting.  
   </details>

3. **Explain why q=1 treats all coefficients equally, while q=10 does not.**  
   <details><summary>Answer</summary>  
   With q=1, the norm is the sum of absolute values, so each coefficient contributes linearly. With q=10, large coefficients dominate the norm because raising them to the 10th power magnifies their influence; the optimization then focuses on shrinking those large coefficients and largely ignores small ones.  
   </details>

4. **In the LASSO objective, what is the purpose of setting p=2?**  
   <details><summary>Answer</summary>  
   p=2 makes the data‑fit term (squared error) smooth, which simplifies derivative calculations during optimization.  
   </details>
## Hyperparameter Tuning and Human Decision Making

The LASSO (Least Absolute Shrinkage and Selection Operator) penalty for nonlinear models introduces several hyperparameters that you must choose.  These hyperparameters control the complexity of the model, the degree of interaction allowed, and the strength of regularization.  The process of selecting the right values is not automatic; it requires human judgment and a deep understanding of your data and your goals.

### The Hyperparameters in Nonlinear LASSO

When fitting a nonlinear model with LASSO regularization, you typically encounter three hyperparameters (added context: these are common in polynomial or spline-based LASSO expansions):

| Hyperparameter | Role | Typical Values / Range |
|----------------|------|------------------------|
| `p` | Degree of the polynomial (or order of spline) for each feature. Controls the flexibility of individual feature transformations. | Positive integers (e.g., 1, 2, 3, ...). Higher values allow more complex curves. |
| `q` | Maximum interaction order between features. Controls how many features can be multiplied together. | Positive integers (e.g., 1 for main effects only, 2 for two-way interactions, etc.). |
| `lambda` (`λ`) | Regularization strength. Controls how much the LASSO penalty shrinks coefficients toward zero. | Non-negative real numbers (e.g., 0.01, 0.1, 1, 10). Larger values produce sparser models. |

Each combination of `p`, `q`, and `lambda` produces a different fitted model.  As the number of features grows, the number of possible combinations multiplies quickly.  The search space can become very large, especially when you consider that you may also need to tune the type of basis functions (e.g., polynomials, splines) and the number of knots for splines.

### The Role of Human Decision Making

No algorithm can automatically select the “best” hyperparameters without a clear definition of what “best” means.  You must decide:

- **What you want from the model.**  Do you need an interpretable equation that reveals the underlying relationship (e.g., a simple polynomial with few terms)?  Or do you only need predictions that are accurate on new data, even if the model is a black box?
- **What trade-offs you are willing to accept.**  A model with high `p` and `q` may fit the training data well but overfit, while a model with a very large `lambda` may be too simple and underfit.
- **What level of sparsity is acceptable.**  A larger `lambda` forces more coefficients to zero, making the model easier to interpret but potentially reducing predictive accuracy.

These choices require an intimate knowledge of your data: the domain, the measurement noise, the expected shape of relationships, and the context in which the model will be used.  For example, a biologist studying a chemical reaction might want a model that predicts rates accurately, even if the model has many terms.  A physicist, on the other hand, might prefer a simple, mathematically tractable expression that can be manipulated analytically.

### Example: Two Different Goals

Consider the same dataset with two different users:

- **User A (the mathematician)** wants a model that is “something I can do math on.”  They will likely choose small `p` and `q` (e.g., `p=2`, `q=1`) and a moderate `lambda` to keep only the most important terms.  The resulting equation is short and interpretable.
- **User B (the biologist or chemist)** wants a model that “gives them predictions into the future.”  They may allow larger `p` and `q` (e.g., `p=3`, `q=2`) and select `lambda` via cross-validation to minimize prediction error.  The final model may be complex, but it maximizes forecast accuracy.

### Practical Guidance

When tuning hyperparameters for nonlinear LASSO:

1. **Start with a grid search** over a small set of `p`, `q`, and `lambda` values.  For each combination, fit the model and evaluate a metric (e.g., mean squared error, AIC, or BIC).
2. **Visualize the results** using validation curves or heatmaps to see how the model complexity changes with each hyperparameter.
3. **Incorporate domain knowledge** to narrow the search.  For example, if you know that interactions above order 2 are physically impossible, set `q=2`.
4. **Decide on your primary objective** (interpretability vs. prediction) before finalizing the hyperparameters.  There is no single “correct” answer; the choice is yours.

The diagram below shows how the hyperparameters interact to produce different model families:

```
                    Hyperparameter Space
                    ┌─────────────────────────┐
                    │   p = 1, q = 1          │  ← linear model (no interactions)
                    │   p = 2, q = 1          │  ← quadratic, main effects only
                    │   p = 2, q = 2          │  ← quadratic, two-way interactions
                    │   p = 3, q = 2          │  ← cubic, two-way interactions
                    │      ...                │
                    └─────────────────────────┘
                    For each (p,q), lambda varies
                    lambda = 0   → no regularization (overfitting)
                    lambda = ∞   → all coefficients zero (underfitting)
                    lambda chosen → trade-off between fit and sparsity
```

### Check Your Understanding

1. **What are the three hyperparameters mentioned in the video for nonlinear LASSO, and what does each control?**

<details><summary>Answer</summary>
`p` controls the degree of polynomial (or flexibility of the feature transformation), `q` controls the maximum interaction order between features, and `lambda` controls the strength of regularization (how much coefficients are shrunk toward zero).
</details>

2. **Why is human decision making required in hyperparameter tuning, according to the video?**

<details><summary>Answer</summary>
Because the best choice depends on the user’s goal: some users want an interpretable model they can “do math on,” while others want accurate predictions.  The algorithm cannot automatically decide which trade-off is correct without a clear definition of the objective.
</details>

3. **Explain the difference between the goal of a mathematician and the goal of a biologist or chemist when fitting a nonlinear LASSO model.**

<details><summary>Answer</summary>
A mathematician prefers a model that is simple and mathematically tractable (e.g., low `p` and `q`, moderate `lambda`).  A biologist or chemist often wants a model that gives reliable predictions for future observations, even if the model is complex (e.g., higher `p` and `q`, `lambda` tuned for prediction accuracy).
</details>

4. **True or False: Increasing `lambda` always makes the model more interpretable because it forces more coefficients to zero.**

<details><summary>Answer</summary>
True.  A larger `lambda` increases the penalty, shrinking more coefficients to exactly zero, which results in a sparser model.  Sparser models are generally easier to interpret because they include fewer terms.  However, if `lambda` is too large, the model may be too simple to capture the underlying relationship, so interpretability should be balanced with adequate fit.
</details>
## Key takeaways

- Polynomial fitting extends linear regression by using a polynomial of degree D to model nonlinear relationships between input and output.
- The error function for polynomial fitting uses a p-norm of the residuals, where p=1 is robust to outliers but hard to differentiate and p=2 is smooth and commonly used.
- High-degree polynomials lead to high-dimensional coefficient spaces, making coefficients large, uninterpretable, and computationally expensive.
- Regularization adds a penalty term lambda times the q-norm of the coefficient vector to the error function to encourage small coefficients.
- The regularization parameter lambda controls the trade-off between data fit and coefficient size: lambda=0 prioritizes fit, large lambda prioritizes small coefficients.
- LASSO (Least Absolute Shrinkage and Selection Operator) uses p=2 for the error norm and q=1 for the penalty norm, treating all coefficients equally.
- Using q=1 penalizes all coefficients uniformly, while higher q-norms (e.g., q=10) disproportionately penalize larger coefficients, similar to how larger p-norms favor outliers.
- Lambda is a hyperparameter that must be chosen before optimization, often by testing multiple values and selecting based on the goal (e.g., prediction accuracy vs. interpretability).
- Choosing lambda requires intimate knowledge of the data and the desired outcome, involving human decision making and domain expertise.
## Glossary

| Term | Definition |
|---|---|
| p-norm | A measure of vector magnitude defined as the p-th root of the sum of absolute values raised to the power p; used to quantify the error between predicted and observed values. |
| q-norm | A norm applied to the coefficient vector in the regularization term; the choice of q determines how coefficients are penalized (e.g., q=1 treats all equally, q>1 favors shrinking large coefficients more). |
| polynomial degree D | The highest exponent in a polynomial function; a degree D polynomial has D+1 coefficients (c0 through cD). |
| residual | The difference between an observed output and the predicted output from the model. |
| regularization | A technique that adds a penalty term to the error function to discourage large coefficients, improving model interpretability and preventing overfitting. |
| regularization parameter lambda | A positive scalar that controls the strength of the penalty term; larger lambda forces smaller coefficients, smaller lambda emphasizes fitting the data. |
| hyperparameter | A parameter set before the optimization process (e.g., lambda, polynomial degree) that is not learned from data but chosen by the practitioner. |
| LASSO (Least Absolute Shrinkage and Selection Operator) | A regularization method that uses p=2 for the error norm and q=1 for the penalty norm, encouraging sparsity and equal treatment of all coefficients. |
| coefficient vector | A vector containing all the parameters (c0, c1, ..., cD) of the polynomial model that are optimized to fit the data. |
| outlier | A data point that deviates significantly from the majority of the data; p=1 norm is robust to outliers, while p=2 norm is sensitive to them. |
| discrete dynamical system | A system where the state at the next time step is a function of the current state; here modeled as x_{n+1} = f(x_n). |
| error function | A function that measures the discrepancy between model predictions and actual data; minimized during fitting. |
| regularized error function E_tilde | The sum of the original error function and lambda times the q-norm of the coefficient vector; the objective to minimize in regularized fitting. |
| Goldilocks zone | A colloquial term for the range of lambda values that balances data fit and coefficient size, avoiding extremes of overfitting or underfitting. |
| interpretability | The degree to which a model's parameters and predictions can be understood and analyzed by humans; small coefficients aid interpretability. |
| Taylor expansion | A representation of a function as an infinite sum of terms calculated from its derivatives; polynomial fitting can be seen as a truncated Taylor series. |
| input space | The set of all possible input vectors; for polynomial fitting of degree D, the input space has D+1 dimensions (the coefficients). |
| optimization | The process of finding the coefficient values that minimize the error function (or regularized error function). |
| smooth derivative | A derivative that is continuous and well-behaved; p=2 norm yields smooth derivatives, making optimization easier compared to p=1. |
| sparsity | A property of a coefficient vector where many entries are zero or very small; LASSO with q=1 encourages sparsity. |
## Footnotes and deeper context

1. **LASSO name origin.** LASSO stands for Least Absolute Shrinkage and Selection Operator, introduced by Robert Tibshirani in 1996. It is a specific case of regularized regression with an L1 penalty (q=1).
2. **p=2 and q=1 in LASSO.** In the LASSO method, p=2 corresponds to the standard least squares error (Euclidean norm), and q=1 corresponds to the L1 norm of the coefficients. This combination is widely used because it yields a convex optimization problem and encourages sparse solutions.
3. **q=1 treats all coefficients equally.** The L1 norm sums the absolute values of coefficients, so each coefficient contributes linearly to the penalty regardless of its magnitude relative to others. In contrast, higher q-norms (e.g., L2) square larger coefficients, giving them disproportionate influence.
4. **Hyperparameter tuning in practice.** Common practice is to evaluate the model's performance (e.g., via cross-validation) over a grid of lambda values and select the lambda that minimizes validation error. This is a standard step in machine learning pipelines.
5. **Polynomial degree and overfitting.** Using a very high polynomial degree (e.g., 100) can lead to overfitting, where the model fits noise in the training data but generalizes poorly. Regularization helps mitigate this by penalizing large coefficients.
6. **p=1 vs p=2 for error norm.** The p=1 error norm (sum of absolute residuals) is also known as least absolute deviations (LAD) and is more robust to outliers but has a non-differentiable point at zero. The p=2 norm (sum of squared residuals) is differentiable everywhere and corresponds to ordinary least squares.
7. **Lambda=0 and lambda very large limits.** When lambda=0, the regularized error reduces to the original error, and the solution is the unregularized polynomial fit. When lambda approaches infinity, the optimal coefficient vector approaches zero, ignoring the data entirely.
## Where to go next

- **Scikit-learn documentation on LASSO.** The official scikit-learn documentation provides a practical guide to using LASSO regression in Python, including parameter tuning and examples. See sklearn.linear_model.Lasso.
- **Original LASSO paper by Tibshirani (1996).** Read the seminal paper 'Regression Shrinkage and Selection via the Lasso' by Robert Tibshirani (Journal of the Royal Statistical Society, Series B) for the theoretical foundation and motivation.
- **Elements of Statistical Learning by Hastie, Tibshirani, and Friedman.** This textbook covers regularization methods including LASSO and ridge regression in depth, with mathematical derivations and practical advice. Chapters 3 and 6 are especially relevant.
- **Cross-validation for hyperparameter tuning.** To learn how to choose lambda in practice, study k-fold cross-validation. The scikit-learn documentation on cross-validation and GridSearchCV is a good starting point.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
