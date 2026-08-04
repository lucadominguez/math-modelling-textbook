# Constrained Modelling and Shadow Pricing: Applying Lagrange Multipliers to Production Optimization
> **Source:** [Constrained Modelling and Shadow Pricing - Math Modelling - Lecture 7](https://www.youtube.com/watch?v=SY6NvKj0fRM) by Math Modelling · 32:17 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students or professionals learning mathematical modeling and optimization who want to understand constrained optimization with Lagrange multipliers and sensitivity analysis.
## Learning objectives

After working through this document you can:

1. Set up a constrained optimization problem with multiple inequality constraints.
2. Apply Lagrange multipliers to find candidate optimal points on a binding constraint.
3. Evaluate endpoints and other constraints to determine the global optimum.
4. Perform sensitivity analysis by varying a constraint parameter and deriving linear relationships.
5. Compute the derivative of optimal profit with respect to a constraint and relate it to the Lagrange multiplier.
6. Interpret the Lagrange multiplier as a shadow price for decision making.
7. Use shadow pricing to decide whether to relax a constraint based on cost per unit.
## Prerequisites

- Basic calculus including partial derivatives and gradients.
- Single-variable optimization techniques.
- Familiarity with profit functions and linear constraints.
## Introduction and Problem Setup

This section sets up a constrained optimization problem using Lagrange multipliers. You will revisit a profit function for a television manufacturer, then add five constraints that define a feasible region. By the end, you will understand the problem you will solve in the rest of the course.

### Recap of Lagrange Multipliers

In the previous video, you learned that Lagrange multipliers provide a method to find optimum solutions for constrained optimization problems. The constraints can be linear or nonlinear. The method reduces the problem to solving a system of equations known as the Lagrange multiplier equations. (Added context: The Lagrange multiplier technique introduces an auxiliary variable, lambda, for each constraint and sets the gradient of the Lagrangian equal to zero.)

### The Profit Function

The profit function, denoted as capital P, depends on two decision variables:

*   **S**: number of 19-inch TV sets produced.
*   **T**: number of 21-inch TV sets produced.

The profit function is quadratic in S and T. It was derived in an earlier video and remains unchanged. The equation is:

```
P(S, T) = (399 - 0.01T - 0.004S) * S + (399 - 0.004S - 0.01T) * T - 400,000 - 225T
```

(Added context: The first two terms represent revenue from each TV type, with price depending on both quantities. The term 400,000 is a fixed production cost, and 225T is the per-unit production cost for 21-inch sets.)

In the unconstrained case (only requiring S and T to be positive), you found the optimum by setting the gradient of P equal to zero. Now you will add constraints.

### The Five Constraints

The problem includes five constraints. The first two are natural non-negativity constraints. The next two are material-based production limits. The fifth is a shared component limit.

| Constraint | Description | Mathematical Form |
|------------|-------------|-------------------|
| 1 | Non-negativity of 19-inch sets | S >= 0 |
| 2 | Non-negativity of 21-inch sets | T >= 0 |
| 3 | Material limit for 19-inch sets | S <= 5,000 |
| 4 | Material limit for 21-inch sets | T <= 8,000 |
| 5 | Circuit board supply limit | S + T <= 10,000 |

Constraint 5 arises because both TV models use the same internal circuit board, and the supplier can provide only 10,000 boards per year. Therefore, the total number of televisions produced (S + T) cannot exceed 10,000.

### The Feasible Region

The set of all (S, T) pairs that satisfy all five constraints is called the **feasible region**. You can visualize it as a polygon in the S-T plane.

```
ASCII diagram of the feasible region:

T
|
8000 +----+--------+
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
|    |    |        |
0----+----+--------+----> S
     0   5000     10000

Lines:
- S = 0 (vertical axis)
- T = 0 (horizontal axis)
- S = 5000 (vertical line)
- T = 8000 (horizontal line)
- S + T = 10000 (diagonal line from (0,10000) to (10000,0))

The feasible region is the area bounded by these lines, including the axes.
```

The constraints form a rectangle (from S=0 to 5000 and T=0 to 8000) that is further cut by the diagonal line S+T=10000. The feasible region is the part of that rectangle that lies below the diagonal line. This region contains all possible production plans that respect material and circuit board limits.

### Summary of the Problem

You now have a profit function P(S,T) and five inequality constraints. The goal is to find the values of S and T within the feasible region that maximize profit. In the next sections, you will apply Lagrange multipliers to handle these constraints and interpret the shadow prices.

### Check Your Understanding

1.  What are the five constraints in this production optimization problem? List them in mathematical form.

<details><summary>Answer</summary>
S >= 0, T >= 0, S <= 5000, T <= 8000, S + T <= 10000.
</details>

2.  Why is the constraint S + T <= 10000 necessary?

<details><summary>Answer</summary>
Both TV models use the same internal circuit board, and the supplier can provide only 10,000 boards per year. Therefore, the total number of televisions produced cannot exceed 10,000.
</details>

3.  Draw a rough sketch of the feasible region. Which constraints form its boundaries?

<details><summary>Answer</summary>
The feasible region is a pentagon bounded by:
- S = 0 (left edge)
- T = 0 (bottom edge)
- S = 5000 (right edge, but only up to the diagonal)
- T = 8000 (top edge, but only up to the diagonal)
- S + T = 10000 (diagonal edge connecting (2000,8000) to (5000,5000))
</details>

4.  In the unconstrained case, you found an optimum by setting the gradient of P to zero. Why is that not sufficient now?

<details><summary>Answer</summary>
The unconstrained optimum might lie outside the feasible region (e.g., require S > 5000 or T > 8000). The constraints restrict the allowable values of S and T, so you must find the optimum within the feasible region, which may occur on a boundary rather than at an interior point where the gradient is zero.
</details>
## Applying Lagrange Multipliers to the Circuit Board Constraint

In this section, you will apply the method of Lagrange multipliers to optimize a profit function subject to a linear constraint. The constraint represents a production limit on circuit boards.

### Step 1: Recall the Gradient of the Profit Function

The profit function P(s, T) depends on two variables: s (the number of standard boards) and T (the number of premium boards). You previously computed the gradient of P. The gradient is a vector of partial derivatives. It points in the direction of the steepest increase of the profit function.

The gradient of P, written as ∇P, has two components:

- The first component is the partial derivative with respect to s: ∂P/∂s = 144 − 0.02s − 0.007T
- The second component is the partial derivative with respect to T: ∂P/∂T = 174 − 0.007s − 0.02T

So the gradient vector is:

∇P = (144 − 0.02s − 0.007T, 174 − 0.007s − 0.02T)



### Step 2: Define the Constraint Function

The most interesting constraint is the one that ties the two variables together. Define the constraint function g(s, T) as:

g(s, T) = s + T

The constraint itself is the line s + T = 10,000. This means the total number of boards (standard plus premium) cannot exceed 10,000.

### Step 3: Compute the Gradient of the Constraint Function

The gradient of g is simple to compute. The partial derivative with respect to s is 1. The partial derivative with respect to T is 1. Therefore:

∇g = (1, 1)

This simplicity makes the Lagrange multiplier equation a linear system.

### Step 4: Set Up the Lagrange Multiplier Equation

The Lagrange multiplier method states that at an optimum, the gradient of the objective function (profit) is parallel to the gradient of the constraint function. This is expressed as:

∇P = λ ∇g

Here, λ (lambda) is the Lagrange multiplier. It represents the rate at which the optimal profit changes if the constraint is relaxed.

Substitute the gradients into the equation:

(144 − 0.02s − 0.007T, 174 − 0.007s − 0.02T) = λ (1, 1)

This gives you two equations:

1. 144 − 0.02s − 0.007T = λ
2. 174 − 0.007s − 0.02T = λ

### Step 5: Understand the Geometric Interpretation

The gradient of P points in the direction of steepest increase for the profit function. To maximize profit, you would follow that gradient. The gradient of g is perpendicular (orthogonal) to the level set of the constraint. The level set is the line s + T = 10,000.

When ∇P is parallel to ∇g, the only way to increase profit is to move off the constraint line. This is because the gradient of P points in a direction orthogonal to the constraint line. If you stay on the constraint line, you cannot increase profit further. This geometric intuition helps you understand why the Lagrange multiplier equation finds the optimum.

### Step 6: Use the Constraint to Reduce Unknowns

You have three unknowns: s, T, and λ. The constraint s + T = 10,000 provides a third equation. Solve for T in terms of s:

T = 10,000 − s

Substitute this into the Lagrange multiplier equations. This reduces the system to two equations with two unknowns (s and λ).

### Step 7: Solve the System

Substitute T = 10,000 − s into the first equation:

144 − 0.02s − 0.007(10,000 − s) = λ

Simplify:

144 − 0.02s − 70 + 0.007s = λ
74 − 0.013s = λ

Now substitute T = 10,000 − s into the second equation:

174 − 0.007s − 0.02(10,000 − s) = λ

Simplify:

174 − 0.007s − 200 + 0.02s = λ
−26 + 0.013s = λ

Set the two expressions for λ equal to each other:

74 − 0.013s = −26 + 0.013s

Solve for s:

74 + 26 = 0.013s + 0.013s
100 = 0.026s
s = 100 / 0.026
s = 50,000 / 13
s ≈ 3,846

Now find T using the constraint:

T = 10,000 − s
T = 10,000 − (50,000 / 13)
T = (130,000 / 13) − (50,000 / 13)
T = 80,000 / 13
T ≈ 6,154

Finally, find λ by substituting s into either expression for λ:

λ = 74 − 0.013(50,000 / 13)
λ = 74 − (650 / 13)
λ = 74 − 50
λ = 24

### Step 8: Verify the Solution

Check that s and T satisfy the constraint:

s + T = (50,000 / 13) + (80,000 / 13) = 130,000 / 13 = 10,000

The solution is valid.

### Summary of Results

| Variable | Exact Value | Approximate Value |
|----------|-------------|-------------------|
| s        | 50,000 / 13 | 3,846             |
| T        | 80,000 / 13 | 6,154             |
| λ        | 24          | 24                |

The Lagrange multiplier λ = 24 means that if the constraint were relaxed by one unit (allowing one more board total), the optimal profit would increase by approximately 24 units.

### Check Your Understanding

1. What does the Lagrange multiplier λ represent in this production optimization problem?

<details>
<summary>Answer</summary>
The Lagrange multiplier λ represents the rate of change of the optimal profit with respect to a small relaxation of the constraint. In this case, λ = 24 means that if the total board limit were increased by one unit, the optimal profit would increase by approximately 24 units.
</details>

2. Why must the gradient of the profit function be parallel to the gradient of the constraint function at the optimum?

<details>
<summary>Answer</summary>
At the optimum, you cannot increase profit by moving along the constraint line. The gradient of the profit function points in the direction of steepest increase. If it had a component along the constraint line, you could move in that direction to increase profit. Therefore, the gradient must be perpendicular to the constraint line. The gradient of the constraint function is perpendicular to the constraint line. So the two gradients must be parallel.
</details>

3. If the constraint were changed to s + T = 11,000, what would be the approximate change in optimal profit?

<details>
<summary>Answer</summary>
The Lagrange multiplier λ = 24 gives the approximate change in optimal profit per unit change in the constraint. If the constraint increases by 1,000 units, the optimal profit would increase by approximately 24 × 1,000 = 24,000 units.
</details>

4. What are the two equations you must solve when applying the Lagrange multiplier method to this problem?

<details>
<summary>Answer</summary>
The two equations are:
1. 144 − 0.02s − 0.007T = λ
2. 174 − 0.007s − 0.02T = λ
These come from setting each component of ∇P equal to the corresponding component of λ∇g.
</details>
## Checking Endpoints and Other Constraints

After finding a candidate point on the constraint \(s + t = 10{,}000\) using Lagrange multipliers, you must verify that this point is indeed a maximum along that line. Because the line is a one-dimensional object, you need to check its endpoints just as you would in a single-variable optimization problem.

The endpoints of the line \(s + t = 10{,}000\) within the feasible region occur where this line meets the other constraints \(s \le 5{,}000\) and \(t \le 8{,}000\).  
- One endpoint is where \(s = 5{,}000\), forcing \(t = 5{,}000\) (since \(5{,}000 + 5{,}000 = 10{,}000\)).  
- The other endpoint is where \(t = 8{,}000\), forcing \(s = 2{,}000\) (since \(2{,}000 + 8{,}000 = 10{,}000\)).

Evaluate the profit function at these points. The profit at the interior point \((3{,}846,\; 6{,}154)\) is \(\$532{,}308\), which is larger than the profit at either endpoint. Therefore, the maximum along the line \(s + t = 10{,}000\) is at the interior point.

But you are not done. You must also check all other constraints that define the feasible region. The full set of constraints is:

- \(s \ge 0\)  
- \(t \ge 0\)  
- \(s \le 5{,}000\)  
- \(t \le 8{,}000\)  
- \(s + t \le 10{,}000\)

You have already considered the boundary \(s + t = 10{,}000\) (the equality case). Now you need to check the boundaries where \(s = 0\), \(t = 0\), \(s = 5{,}000\), and \(t = 8{,}000\). These four constraints produce line segments that are either horizontal or vertical, so each reduces to a single-variable optimization problem.

| Constraint | Condition on the other variable | Feasible range |
|------------|--------------------------------|----------------|
| \(s = 0\) | \(t\) free, but bounded by \(0 \le t \le 8{,}000\) and \(s + t \le 10{,}000\) gives \(t \le 10{,}000\) | \(t \in [0, 8{,}000]\) |
| \(t = 0\) | \(s\) free, bounded by \(0 \le s \le 5{,}000\) and \(s + t \le 10{,}000\) gives \(s \le 10{,}000\) | \(s \in [0, 5{,}000]\) |
| \(s = 5{,}000\) | \(t\) free, bounded by \(0 \le t \le 8{,}000\) and \(s + t \le 10{,}000\) gives \(t \le 5{,}000\) | \(t \in [0, 5{,}000]\) |
| \(t = 8{,}000\) | \(s\) free, bounded by \(0 \le s \le 5{,}000\) and \(s + t \le 10{,}000\) gives \(s \le 2{,}000\) | \(s \in [0, 2{,}000]\) |

For each of these boundaries, substitute the fixed value into the profit function and maximize over the remaining variable within its range. The endpoints of these line segments (the corners of the feasible region) are also checked as part of the single-variable optimization routine. The only boundary that required a Lagrange multiplier approach was the diagonal line \(s + t = 10{,}000\) because it involves both variables in a nontrivial way. The other boundaries are parallel to the axes, so they reduce to simple one-variable calculus.

Additionally, you must check the interior of the feasible region. However, as covered in the previous video, the unconstrained optimum (where the gradient of profit is zero) lies outside the feasible region. Therefore, no interior critical point exists. All candidate maxima or minima must lie on the boundaries.

The feasible region can be visualized as the shaded polygon in the diagram below. The vertices are \((0,0)\), \((5{,}000,0)\), \((5{,}000,5{,}000)\), \((2{,}000,8{,}000)\), and \((0,8{,}000)\). The diagonal line from \((5{,}000,5{,}000)\) to \((2{,}000,8{,}000)\) is the constraint \(s + t = 10{,}000\). The other edges are the constraints \(s = 5{,}000\), \(t = 8{,}000\), \(s = 0\), and \(t = 0\).

```
t
^
8000 ----+--------+-----
         |        |
         |        |
         |  Feasible  |
         |  Region    |
         |        |
2000 ----+--------+-----
         |        |
         |        |
0 --------+--------+-----> s
         0       5000
```

After checking all boundaries, the maximum profit is found at the point \((3{,}846,\; 6{,}154)\) on the diagonal constraint, with profit \(\$532{,}308\). All other boundaries yield lower profit values.

### Check your understanding

1. **What are the endpoints of the constraint \(s + t = 10{,}000\) within the feasible region? Why must they be checked?**  
   <details><summary>Answer</summary> The endpoints are \((5{,}000, 5{,}000)\) and \((2{,}000, 8{,}000)\). They must be checked because the line is a one-dimensional object; the maximum could occur at either endpoint, just as in single-variable optimization.</details>

2. **List the four other boundary constraints that must be checked after the diagonal line.**  
   <details><summary>Answer</summary> \(s = 0\), \(t = 0\), \(s = 5{,}000\), and \(t = 8{,}000\).</details>

3. **Why is the Lagrange multiplier method necessary only for the constraint \(s + t = 10{,}000\) and not for the other boundaries?**  
   <details><summary>Answer</summary> The other boundaries are parallel to the axes (horizontal or vertical lines), so fixing one variable reduces the problem to a single-variable optimization. The diagonal constraint involves both variables together in a nontrivial way, requiring Lagrange multipliers to handle the equality condition.</details>

4. **The unconstrained optimum (gradient zero) is outside the feasible region. What does that imply about the location of the maximum?**  
   <details><summary>Answer</summary> It implies that no interior critical point exists; therefore the maximum must occur on one of the boundaries of the feasible region.</details>
## Sensitivity Analysis: Varying the Constraint

After finding the optimum for a specific constraint value, the next logical step is to perform a sensitivity analysis. This is a standard practice in mathematical modeling. You can perform sensitivity analysis on any variable in the problem. Here, we will focus on the constraint itself.

### The Constraint as a Variable

Recall the constraint for this problem: the total number of circuit boards (s plus t) must equal a constant. We previously solved this with the constant equal to 10,000. Now, we will treat that constant as a variable, which we call `c`. The constraint becomes:

g(s, t) = s + t = c

Here, `c` represents the total number of circuit boards available. By varying `c`, we can answer questions like: "If the company could produce a few more circuit boards, would that increase profit? By how much? Would it cost money?" This analysis leads to the concept of **shadow pricing**, which is the marginal value of relaxing a constraint.

### Solving the Lagrange Multiplier System with a Variable Constraint

We will solve the same Lagrange multiplier equation as before, but now with `c` as a parameter. The equation is:

∇p = λ ∇g

Where:
- `p` is the profit function.
- `g` is the constraint function.
- `λ` (lambda) is the Lagrange multiplier.

The gradient of `g` is (1, 1). The gradient of `p` was computed earlier in the course. Setting them equal gives us the same system of equations, but now the constraint equation is `s + t = c`.

From the constraint, we can express `t` in terms of `s` and `c`:

t = c - s

Substituting this into the other equations from the gradient condition and solving yields solutions that are all linear functions of `c`. The solutions are:

s = (13c - 30,000) / 26

t = (13c + 30,000) / 26

λ = (3 * (106,000 - 9c)) / 2,000

These formulas show how the optimal number of each type of circuit board (s and t) and the Lagrange multiplier (λ) change as the total number of available circuit boards (c) changes.

### Summary of the Process

To perform this sensitivity analysis, you repeat the same steps as the original problem, but you replace the fixed constraint value (10,000) with the variable `c`. The key steps are:

1.  Write the Lagrange multiplier equation: ∇p = λ ∇g.
2.  Write the constraint equation: s + t = c.
3.  Solve the system of equations for s, t, and λ in terms of c.
4.  The resulting expressions are linear functions of c, making them easy to analyze.

### Check your understanding

1.  What is the purpose of performing a sensitivity analysis on the constraint?
    <details><summary>Answer</summary>To understand how the optimal solution changes if the constraint value (the total number of circuit boards) changes. This helps determine if increasing the constraint would increase profit and by how much.</details>

2.  In the solved system, what is the expression for `t` in terms of `c`?
    <details><summary>Answer</summary>t = (13c + 30,000) / 26</details>

3.  What does the variable `c` represent in this sensitivity analysis?
    <details><summary>Answer</summary>`c` represents the total number of circuit boards available, which is the constant in the constraint equation `s + t = c`.</details>

4.  What is the mathematical form of the solutions for s, t, and λ with respect to c?
    <details><summary>Answer</summary>They are all linear functions of c.</details>
## Computing Sensitivities and the Role of Lambda

In this section you will learn how to compute the sensitivity of the optimal production quantities and the maximum profit to changes in the resource constraint \(c\).  The sensitivity is measured as an **elasticity**: the percentage change in the output (s, t, or profit) that results from a 1% change in the input \(c\).  You will also discover that the Lagrange multiplier \(\lambda\) equals the derivative of the optimal profit with respect to the constraint, a key fact that gives \(\lambda\) its interpretation as a **shadow price**.

### 1.  Derivatives of the Optimal Production Levels

Recall that the optimal number of 19-inch TVs \(s^*\) and 24-inch TVs \(t^*\) are functions of the total resource \(c\).  For the specific problem you solved earlier, the derivatives are constant:

\[
\frac{ds}{dc} = \frac{1}{2}, \qquad \frac{dt}{dc} = \frac{1}{2}.
\]

These derivatives tell you the absolute change in the optimal production for a one-unit change in \(c\).  For example, if \(c\) increases by 1 unit, both \(s^*\) and \(t^*\) increase by 0.5 units.

### 2.  Sensitivity (Elasticity) of Production Quantities

To understand the relative impact, compute the elasticity of \(s\) and \(t\) with respect to \(c\) at the point \(c = 10\,000\) (where \(s^* = 3846\) and \(t^* = 6154\)).

The elasticity formula for a variable \(x\) with respect to \(c\) is:

\[
\text{Elasticity} = \frac{dx}{dc} \cdot \frac{c}{x}.
\]

**For \(s\):**

\[
\frac{ds}{dc} \cdot \frac{c}{s^*} = \frac{1}{2} \cdot \frac{10\,000}{3846} \approx 1.3.
\]

**For \(t\):**

\[
\frac{dt}{dc} \cdot \frac{c}{t^*} = \frac{1}{2} \cdot \frac{10\,000}{6154} \approx 0.8.
\]

Interpretation:  
- A 1% increase in \(c\) (i.e., about 100 units) leads to a 1.3% increase in the optimal number of 19-inch TVs.  That is roughly 30 additional TVs.  
- The same 1% increase in \(c\) leads to a 0.8% increase in the optimal number of 24-inch TVs, or about 60 additional TVs.

### 3.  Derivative of the Optimal Profit with Respect to \(c\)

Now examine how the maximum profit \(P\) changes when \(c\) changes.  The profit function \(P(s,t)\) does **not** depend explicitly on \(c\); the constraint \(c\) enters only through the optimal values \(s^*\) and \(t^*\).  Therefore, by the chain rule:

\[
\frac{dP}{dc} = \frac{\partial P}{\partial s} \cdot \frac{ds}{dc} + \frac{\partial P}{\partial t} \cdot \frac{dt}{dc} + \frac{\partial P}{\partial c}.
\]

Because \(P\) has no explicit \(c\) term, \(\partial P/\partial c = 0\).

You can compute the partial derivatives \(\partial P/\partial s\) and \(\partial P/\partial t\) from the original profit equation (which was given at the start of the video).  Evaluating them at the optimal point and multiplying by the known derivatives \(ds/dc = dt/dc = 1/2\) yields:

\[
\frac{dP}{dc} = 24.
\]

This number **24** is not arbitrary.  It is exactly the Lagrange multiplier \(\lambda\) that you computed when solving the constrained optimization problem.  Thus the Lagrange multiplier gives the instantaneous rate of change of the optimal profit with respect to the constraint.

### 4.  Sensitivity of Profit

Finally, compute the elasticity of profit with respect to \(c\):

\[
\frac{dP}{dc} \cdot \frac{c}{P^*} = 24 \cdot \frac{10\,000}{532\,308} \approx 0.45.
\]

So a 1% increase in the resource \(c\) raises the maximum profit by about 0.45%.  This small sensitivity mirrors the fact that the production quantities themselves are not highly sensitive to small changes in the constraint.

### 5.  Summary of Key Findings

| Quantity | Derivative w.r.t. \(c\) | Sensitivity (Elasticity) | Interpretation |
|----------|--------------------------|--------------------------|----------------|
| \(s^*\) (19-inch TVs) | 1/2 | 1.3 | 1% ↑ in \(c\) → 1.3% ↑ in \(s^*\) (≈30 units) |
| \(t^*\) (24-inch TVs) | 1/2 | 0.8 | 1% ↑ in \(c\) → 0.8% ↑ in \(t^*\) (≈60 units) |
| Maximum profit \(P^*\) | \(\lambda = 24\) | 0.45 | 1% ↑ in \(c\) → 0.45% ↑ in \(P^*\) |

The Lagrange multiplier \(\lambda\) is the **shadow price** of the resource: it tells you the marginal increase in profit if you could obtain one additional unit of the resource.

---

### Check your understanding

1. **Why is the derivative of profit with respect to \(c\) equal to the Lagrange multiplier \(\lambda\)?**  
   <details><summary>Answer</summary>  
   At the optimum, the gradient of the profit function is proportional to the gradient of the constraint.  The Lagrange multiplier is the constant of proportionality.  The chain rule shows that the total derivative of the maximum profit with respect to the constraint equals that multiplier.  This is a general property of constrained optimization that holds under the standard conditions (smooth functions, active constraint).  
   </details>

2. **If the company finds it can increase \(c\) by 2% (from 10,000 to 10,200), what is the approximate percentage increase in the optimal number of 19-inch TVs?**  
   <details><summary>Answer</summary>  
   The elasticity of \(s\) with respect to \(c\) is 1.3.  A 2% increase in \(c\) therefore leads to approximately \(2\% \times 1.3 = 2.6\%\) increase in \(s^*\).  (In absolute terms, about 100 TVs if \(s^*\) is 3846.)  
   </details>

3. **What does the sensitivity of profit (0.45) tell the manager about the value of an additional unit of resource?**  
   <details><summary>Answer</summary>  
   The sensitivity 0.45 means that a 1% increase in \(c\) (100 units) raises profit by 0.45%.  The absolute change in profit per unit of \(c\) is exactly \(\lambda = 24\): each extra unit of resource adds $24 to the optimal profit.  The low elasticity reflects that profit is not extremely sensitive to the resource bound in this example.  
   </details>
## Shadow Pricing and Decision Making

The Lagrange multiplier, often denoted by the Greek letter lambda, provides a direct measure of how sensitive your optimal profit is to small changes in a binding constraint. In the video, the optimal profit changes by only about half a percentage when the constraint `c` (the maximum number of circuit boards available) is increased by 1 percent. This small sensitivity is not a coincidence: it is exactly the value of the Lagrange multiplier you computed in the constrained optimization problem.

### The Geometric Intuition Behind the Lagrange Multiplier

Recall the constrained optimization problem: maximize profit `p(x,y)` subject to the constraint `g(x,y) = c`. At the optimal point, the gradient of `p` (the vector pointing in the direction of steepest increase of profit) and the gradient of `g` (the vector perpendicular to the level set of the constraint) are parallel. The Lagrange multiplier equation ties them together:

```
gradient(p) = lambda * gradient(g)
```

This means that for every one unit you move in the direction of the gradient of `g`, you are effectively moving `lambda` units in the direction of the gradient of `p`. Moving along the gradient of `g` is exactly what happens when you change the constraint value `c` by one unit: the entire constraint line shifts perpendicular to itself (parallel to the gradient of `g`). The resulting change in profit is `lambda` units.

In the video example, the Lagrange multiplier was found to be 24. This tells you: for every one unit increase in the available circuit boards (the constraint `c`), the optimal profit increases by 24 units.

### Defining the Shadow Price

The Lagrange multiplier in a constrained optimization problem is also called the **shadow price**. It represents the marginal value of relaxing the constraint. More formally: the shadow price is the amount by which the optimal objective function (profit) would increase if the constraint were relaxed by one unit.

Key points:
- The shadow price is valid only for small changes (infinitesimal or small percentage changes) because the relationship is linear only locally.
- It applies only to binding constraints (constraints that are active at the optimal solution). If the constraint is not binding, its shadow price is zero.

### Using the Shadow Price for Decision Making

The shadow price enables you to make informed business decisions without re‑solving the entire optimization problem. In the video scenario, a circuit‑board supplier offers to produce one additional circuit board. The question is: should you accept the offer?

1. Determine the shadow price (lambda) for the circuit‑board constraint. In this case, lambda = 24.
2. Ask the supplier for the cost of producing one additional circuit board. Call that cost `m`.
3. Compare the cost to the shadow price:
   - If `m < 24`, then the additional board will increase profit by more than it costs. Accept the offer.
   - If `m > 24`, then the additional board will cost more than the profit gain. Reject the offer.
   - If `m = 24`, you are indifferent; profit remains unchanged.

This decision rule works because the shadow price is exactly the profit increase per unit of the constraint. You do not need to re‑run the optimization model; you only need to compare the marginal cost with the marginal benefit given by the shadow price.

### Summary Table: Shadow Price Decision Rule

| Condition | Decision | Effect on Profit |
|-----------|----------|------------------|
| Marginal cost < shadow price | Accept the additional unit | Profit increases |
| Marginal cost > shadow price | Reject the additional unit | Profit decreases |
| Marginal cost = shadow price | Indifferent | Profit unchanged |

### Check Your Understanding

1. **Question:** A factory has a binding constraint on machine hours. The Lagrange multiplier for that constraint is 15. The company can rent one extra machine hour for $12. Should they rent the hour? Why?

<details><summary>Answer</summary>
Yes, they should rent the hour because the cost ($12) is less than the shadow price ($15). Each additional machine hour increases profit by $15, so after paying $12, the net gain is $3.
</details>

2. **Question:** What does it mean if a constraint has a shadow price of zero?

<details><summary>Answer</summary>
A shadow price of zero means the constraint is not binding at the optimal solution. Relaxing it (or tightening it slightly) does not change the optimal profit because there is already slack in that constraint.
</details>

3. **Question:** In the video, the shadow price for circuit boards was 24. If the supplier offers to produce two more circuit boards at a total cost of $50, should you accept? (Assume the shadow price remains constant for this small change.)

<details><summary>Answer</summary>
The additional profit from two boards would be 2 * 24 = $48. The cost is $50, which is greater than $48. Therefore, you should reject the offer because it would reduce profit by $2.
</details>

4. **Question:** Why is the shadow price only valid for *small* changes in the constraint?

<details><summary>Answer</summary>
The Lagrange multiplier is a local derivative. It measures the instantaneous rate of change of the optimal profit with respect to the constraint. As the constraint changes by a large amount, the curvature of the profit function and the constraint may cause the multiplier to change. The linear relationship (profit change = lambda * change in constraint) holds only approximately for small changes.
</details>
## Conclusion and Next Steps

In this section you apply the Lagrange multiplier (shadow price) to a real production decision and preview the next topic: Newton’s method for higher-dimensional optimization.

### Using the Shadow Price in a Production Decision

The shadow price, also called the Lagrange multiplier (λ), tells you the marginal cost of relaxing a constraint. In the example, the shadow price for producing one additional TV is $23. This means that if you increase TV production by one unit, the total resource cost (e.g., labor, materials) increases by $23.

Now suppose the profit per TV is $24. The decision rule is:

- If the profit per unit exceeds the shadow price, you should increase production because the net gain is positive.
- If the profit per unit is less than the shadow price, you should decrease production because the additional cost outweighs the profit.

In the example:

| Factor                               | Value  |
|--------------------------------------|--------|
| Shadow price (marginal cost)         | $23    |
| Profit per TV                        | $24    |
| Net profit from one more TV          | $1     |

Since the net profit is $1, the decision is to accept the additional TV production. The speaker states: “If it only cost me $23 to produce another TV, then of course, I want to say yes to this because I’m making a dollar profit.”

### Preview of Newton’s Method

The next video will introduce Newton’s method as a technique for solving optimization problems in higher dimensions. Newton’s method is an iterative root-finding algorithm that can be used to find points where the gradient of a function is zero (critical points). This is useful when the system of equations from the first-order conditions (e.g., ∂L/∂x = 0, ∂L/∂y = 0) becomes too complex to solve analytically. The method updates an initial guess using the function’s gradient and Hessian matrix (second derivatives) to converge to a solution. In higher dimensions, the same principle applies: you solve a linear system at each iteration to find the step direction.

### Check Your Understanding

1. In the example, why is the decision to produce another TV justified?  
   <details><summary>Answer</summary>  
   Because the profit per TV ($24) is greater than the shadow price ($23), resulting in a net profit of $1 per additional unit.  
   </details>

2. What does the shadow price (Lagrange multiplier) represent in a production optimization problem?  
   <details><summary>Answer</summary>  
   It represents the marginal cost of relaxing a constraint, i.e., the increase in total resource cost when production is increased by one unit.  
   </details>

3. What is the purpose of Newton’s method in the context of optimization?  
   <details><summary>Answer</summary>  
   It is an iterative algorithm used to find critical points (where the gradient is zero) of a function, especially when the system of equations is large or nonlinear. It uses the gradient and Hessian matrix to update guesses and converge to a solution.  
   </details>
## Key takeaways

- A constrained optimization problem with multiple inequality constraints can be set up by defining a profit function and listing all resource limits as inequalities.
- Lagrange multipliers find candidate optimal points where the gradient of the profit function is parallel to the gradient of a binding constraint.
- After finding a candidate on a constraint, you must check endpoints and all other constraints to confirm the global optimum.
- Sensitivity analysis involves varying a constraint parameter and solving the Lagrange multiplier equations to find how optimal production levels change linearly.
- The derivative of optimal profit with respect to a constraint parameter equals the Lagrange multiplier lambda at the optimum.
- The Lagrange multiplier is interpreted as a shadow price: the amount profit increases per unit increase in the constraint limit.
- Shadow pricing helps decide whether to relax a constraint: if the cost per additional unit is less than the shadow price, it is profitable to do so.
- In the television example, each additional circuit board increases profit by $24, so you should relax the constraint if the cost to produce one more TV is less than $24.
- The unconstrained maximum of the profit function lies outside the feasible region, so the global optimum occurs on a constraint boundary.
- A 1% change in the circuit board limit leads to a 1.3% change in 19-inch TV production and a 0.8% change in 21-inch TV production.
## Glossary

| Term | Definition |
|---|---|
| Lagrange multiplier | A scalar lambda used in the equation gradient of P equals lambda times gradient of g to find optimal points on a constraint. |
| gradient | A vector of partial derivatives that points in the direction of steepest increase of a function. |
| constraint | A condition that limits the feasible values of decision variables, such as S plus T equals 10000. |
| feasible region | The set of all points that satisfy all constraints simultaneously. |
| binding constraint | A constraint that is active at the optimal solution, meaning the optimal point lies exactly on its boundary. |
| shadow price | The rate at which optimal profit changes when a constraint is relaxed by one unit, equal to the Lagrange multiplier. |
| sensitivity analysis | The study of how the optimal solution changes when a parameter of the problem is varied. |
| partial derivative | The derivative of a multivariable function with respect to one variable, holding all other variables constant. |
| chain rule | A formula for computing the derivative of a composite function, used here to relate profit change to changes in S and T. |
| optimal profit | The maximum value of the profit function given the constraints. |
| endpoint | A point at the boundary of a one-dimensional constraint line, such as where it meets another constraint. |
| global optimum | The best possible solution among all points in the feasible region. |
| unconstrained maximum | The maximum of the profit function without any constraints, found by setting the gradient to zero. |
| linear function | A function whose graph is a straight line, such as S of c equals 13c minus 30000 divided by 26. |
| derivative | A measure of how a function changes as its input changes, used to compute sensitivities. |
| percent change | The change in a quantity divided by its original value, multiplied by 100. |
| production capacity | The maximum number of units that can be produced given material or resource limits. |
| circuit board | A component used in both TV models, limiting total production to 10000 units per year. |
| profit function | A mathematical expression that calculates total profit based on the number of units produced. |
| single variable optimization | Finding the maximum or minimum of a function that depends on only one variable. |
## Footnotes and deeper context

1. **Lagrange multiplier derivation.** The Lagrange multiplier method requires that the gradient of the constraint is nonzero at the candidate point. If the gradient is zero, the method may fail to find the optimum.
2. **Shadow price interpretation.** The shadow price is valid only for small changes in the constraint limit. Large changes may cause a different constraint to become binding, changing the shadow price.
3. **Sensitivity formulas.** The derivative of optimal profit with respect to the constraint parameter equals the Lagrange multiplier only when the constraint is binding and the solution is differentiable. This is a standard result from the envelope theorem.
4. **Checking endpoints.** When optimizing along a line segment, you must evaluate the objective at the endpoints because the Lagrange multiplier method only finds interior critical points on the constraint.
5. **Multiple constraints.** With multiple inequality constraints, the optimum may lie at the intersection of several constraints. In such cases, you must use the Karush Kuhn Tucker conditions, which generalize Lagrange multipliers.
6. **Profit function form.** The profit function in the video is quadratic and concave, which guarantees that any critical point found on a linear constraint is a maximum. For non concave functions, second order conditions must be checked.
## Where to go next

- **Read about the Karush Kuhn Tucker conditions.** For problems with multiple inequality constraints, the KKT conditions generalize Lagrange multipliers. See the textbook 'Convex Optimization' by Boyd and Vandenberghe, available freely online, for a rigorous treatment.
- **Practice with sensitivity analysis in Excel Solver.** Excel Solver can compute shadow prices automatically for linear and nonlinear optimization problems. Try the built in sensitivity report to verify the Lagrange multiplier result.
- **Study the envelope theorem.** The envelope theorem explains why the derivative of the optimal value function equals the Lagrange multiplier. Read chapter 19 of 'Microeconomic Theory' by Mas Colell, Whinston, and Green for a detailed explanation.
- **Explore Newton's method for optimization.** The video mentions Newton's method as the next topic. Read the 'Numerical Optimization' book by Nocedal and Wright for a comprehensive guide to Newton and quasi Newton methods.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
