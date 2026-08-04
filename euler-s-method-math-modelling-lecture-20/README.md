# Euler's Method for Approximating Solutions to Continuous-Time Dynamical Systems
> **Source:** [Euler's Method - Math Modelling - Lecture 20](https://www.youtube.com/watch?v=203GsVI7fpU) by Math Modelling · 19:58 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students in a mathematical modelling or differential equations course who want to learn how to numerically approximate solutions to continuous-time dynamical systems.
## Learning objectives

After working through this document you can:

1. Derive Euler's method by approximating the derivative with a finite difference quotient.
2. Explain how Euler's method converts a continuous-time dynamical system into a discrete-time system.
3. Implement Euler's method in a for-loop to approximate solutions step by step.
4. Analyze the trade-off between step size h and accuracy, including the accumulation of error over multiple steps.
5. Visualize the geometric interpretation of Euler's method using tangent lines and error accumulation.
6. Apply Euler's method to a specific dynamical system, such as the RLC circuit model, to observe a limit cycle.
7. Perform sensitivity analysis by decreasing h to verify that observed phenomena are not numerical artifacts.
8. Interpret the output of Euler's method in terms of phase plane plots and time series signals.
## Prerequisites

- Basic calculus, including the definition of a derivative as a limit.
- Familiarity with differential equations and dynamical systems, at least qualitatively.
- Understanding of discrete-time dynamical systems and update rules.
- Basic programming concepts, especially loops and iteration.
- Linear algebra, including vectors and vector-valued functions.
## Introduction: From Qualitative Analysis to Computational Methods

In earlier lectures you studied the **theory of dynamical systems**. You began with **qualitative analysis**: drawing phase portraits and sketches to understand the long‑term behavior of a system without solving it exactly. Then you moved to **quantitative analysis** using **linearization methods**: you computed eigenvalues and eigenvectors of a linearized system near equilibrium points to determine stability and the nature of trajectories.

Now you will shift from theory to **computational methods**. The goal is to approximate the behavior of dynamical systems using a computer, which cannot handle continuous mathematics directly. This section explains why one type of dynamical system is easy to simulate on a computer and why another type requires special approximation schemes.

### Discrete‑Time Systems: Easy to Implement

A **discrete‑time dynamical system** is defined by an **update rule**:

\[
x_{n+1} = f(x_n)
\]

If you know the current state \(x_n\), you can compute the next state \(x_{n+1}\) by applying the function \(f\). This is a direct, one‑step calculation.

To simulate a discrete‑time system on a computer you use a **looping process**:

1. Start with an initial state \(x_0\).
2. For each step \(n = 0, 1, 2, \dots\):
   - Compute \(x_{n+1} = f(x_n)\).
   - Store or use the new state.
   - Set \(x_n = x_{n+1}\) and repeat.

Because the computer can evaluate the function \(f\) exactly (as a formula or algorithm), every step is straightforward. The loop can run for as many steps as needed.

### Continuous‑Time Systems: The Problem of Derivatives

A **continuous‑time dynamical system** is described by a differential equation:

\[
\frac{dx}{dt} = g(x(t))
\]

The rate of change is given by a derivative, which is a limit of differences. A computer cannot store a continuous derivative or evaluate it directly for an arbitrary time interval. Instead, it works with discrete numbers at discrete times.

The key difficulty: you cannot simply “put the derivative into a computer” and get the next state. You need an **approximation scheme** that replaces the continuous derivative with a discrete step. The simplest such scheme is **Euler’s method**, which you will implement in the next sections.

### Comparison: Discrete vs. Continuous Implementation

| Aspect | Discrete‑Time System | Continuous‑Time System |
|--------|----------------------|------------------------|
| Defining equation | \(x_{n+1} = f(x_n)\) (update rule) | \(\displaystyle \frac{dx}{dt} = g(x)\) (differential equation) |
| Computer implementation | Direct loop: evaluate \(f\) at each step | Requires approximation of the derivative |
| Exactness | The update rule is exact for the discrete dynamics | Any algorithm produces an approximate solution |
| Complexity | Simple, no numerical error from the step itself | Introduces step‑size dependent error |

### ASCII Diagram: Discrete‑Time Loop

```
Start with x0
    |
    v
  +-------------------+
  | Compute x_{n+1}   |
  | = f(x_n)          |
  +-------------------+
    |
    v
  +-------------------+
  | Is this the final |
  | step?             | ---> Yes → Stop
  +-------------------+
    |
    No
    |
    v
  Set x_n = x_{n+1}
  Go back to "Compute"
```

For continuous‑time systems, this simple loop does not work because you cannot directly compute \(x_{n+1}\) from \(x_n\) without an approximation.

### Check Your Understanding

1.  **Why is a discrete‑time dynamical system easier to simulate on a computer than a continuous‑time system?**

    <details><summary>Answer</summary>
    A discrete‑time system is defined by an update rule \(x_{n+1} = f(x_n)\) that can be evaluated directly on a computer. A continuous‑time system involves a derivative, which cannot be computed exactly by a computer; it must be approximated.
    </details>

2.  **What is the main limitation of a computer when dealing with continuous‑time dynamical systems?**

    <details><summary>Answer</summary>
    A computer cannot store or evaluate a continuous derivative. It works with discrete numbers, so it must approximate the derivative using a finite‑difference scheme (e.g., Euler’s method).
    </details>

3.  **Describe the looping process used to simulate a discrete‑time system. Mention the two steps that repeat.**

    <details><summary>Answer</summary>
    Start with an initial state \(x_0\). Then, for each step: (1) compute the next state using the update rule; (2) set the current state to the newly computed state and repeat until the desired number of steps is reached.
    </details>
## Derivative Approximation and the Basic Idea of Euler's Method

This section explains how to approximate the solution of a continuous-time dynamical system by turning it into a discrete-time dynamical system. The method is called **Euler's method** (sometimes *forward Euler method*), named after the mathematician Leonhard Euler. It is one of the simplest numerical schemes for solving differential equations.

### Continuous-Time Dynamical Systems

A continuous-time dynamical system is described by a differential equation of the form

\[
x'(t) = f(x(t))
\]

Here, \(x(t)\) is a vector function of time (it could be multi-dimensional, for example, \(n\)-dimensional). The function \(f\) is also vector-valued, matching the dimension of \(x\). The prime denotes the derivative with respect to time: \(x'(t) = \frac{dx}{dt}\).

The goal is to find \(x(t)\) for future times, given an initial condition \(x(0)\). Computers cannot directly handle continuous time, so we need a way to simulate the system step by step.

### The Definition of the Derivative

Recall from calculus: the derivative of \(x\) at time \(t\) is defined as the limit

\[
x'(t) = \lim_{h \to 0} \frac{x(t+h) - x(t)}{h}
\]

The quantity \(h\) is a small step in time. The limit says that as \(h\) becomes arbitrarily small, the difference quotient approaches the derivative exactly.

### Approximating the Derivative with a Small Step

If we choose a very small but nonzero \(h > 0\), the limit tells us that the quotient is close to the derivative. For a fixed small \(h\), we can write the approximation

\[
x'(t) \approx \frac{x(t+h) - x(t)}{h}
\]

The approximation becomes more accurate as \(h\) gets smaller. (We will discuss how to choose \(h\) later; the important point now is that the limit exists, so for sufficiently small \(h\) the equality is nearly exact.)

### Replacing the Derivative in the Differential Equation

Now substitute this approximation into the original differential equation \(x'(t) = f(x(t))\). We obtain

\[
\frac{x(t+h) - x(t)}{h} \approx f(x(t))
\]

The right-hand side is evaluated at the same moment in time \(t\). This equation relates the current state \(x(t)\) to the state one step \(h\) into the future \(x(t+h)\).

### Rearranging to Get an Update Rule

To solve for the future state, multiply both sides by \(h\):

\[
x(t+h) - x(t) \approx h \, f(x(t))
\]

Then add \(x(t)\) to both sides:

\[
x(t+h) \approx x(t) + h \, f(x(t))
\]

This is the core of Euler's method. It turns the continuous-time system into a **discrete-time dynamical system** (a difference equation). Starting from a known state \(x(t)\), we can compute an approximation for the state at time \(t+h\). Then we can repeat the process to step forward in time.

### Why It Is Called "Forward Euler"

Because we use information at the current time \(t\) to move forward to \(t+h\), the method is often called the *forward Euler method*. It is a simple, explicit scheme: the next state depends only on the current state and the derivative function \(f\).

### Summary of the Euler Method Steps

1. Choose a small step size \(h > 0\).
2. At the current time \(t\), evaluate \(f(x(t))\).
3. Compute the next state: \(x(t+h) = x(t) + h \cdot f(x(t))\).
4. Set \(t \leftarrow t + h\) and repeat.

The approximation will have errors that depend on the size of \(h\) and the behavior of \(f\). Smaller \(h\) generally gives better accuracy but requires more steps.

### Check Your Understanding

1. **Why does Euler's method replace the derivative with a difference quotient?**  
   <details><summary>Answer</summary>  
   The exact derivative is defined as a limit of that quotient. By choosing a small but nonzero \(h\), we approximate the derivative, which allows us to rewrite the differential equation as an algebraic equation that can be stepped forward in time on a computer.  
   </details>

2. **What is the approximate update equation for Euler's method?**  
   <details><summary>Answer</summary>  
   \(x(t+h) \approx x(t) + h \, f(x(t))\)  
   </details>

3. **Why is this method called "forward Euler"?**  
   <details><summary>Answer</summary>  
   It uses the current state and derivative to compute the state at a future time \(t+h\), moving forward in time.  
   </details>

4. **What does the approximation become as \(h\) approaches zero?**  
   <details><summary>Answer</summary>  
   As \(h \to 0\), the difference quotient approaches the exact derivative, and the Euler update becomes the exact differential equation. In practice, we cannot use \(h = 0\) because we would never move forward in time.  
   </details>
## The Euler Update Formula and Iterative Procedure

The Euler method uses a fixed time step, denoted by `h`, to move forward in time. The value `h` represents a small, constant increment of time. The core idea is that if you know the exact state of the system at one instant, you can use the derivative at that instant to approximate the state a short time `h` later.

### The Euler Update Formula

The formula for a single Euler step is:

`x(t + h) = x(t) + h * f(x(t), t)`

Where:
- `x(t)` is the current state at time `t`.
- `h` is the fixed time step size.
- `f(x(t), t)` is the derivative of `x` with respect to time, evaluated at the current state and time. This derivative tells you the instantaneous rate of change.
- `x(t + h)` is the approximate state at the next time step.

This formula is the fundamental building block. It pushes the system forward by one step of size `h`.

### The Iterative Procedure

You can repeat this procedure to approximate the solution over many time steps. The process starts with a known initial condition.

**Step 1: The Initial Condition**

You are given an initial condition. This is the exact state of the system at time `t = 0`. We denote this as `x(0)`.

**Step 2: The First Euler Step**

To find the approximate state at time `t = h`, you apply the Euler update formula using the initial condition:

`x(h) = x(0) + h * f(x(0), 0)`

This gives you an approximation for `x(h)`.

**Step 3: The Second Euler Step**

To find the approximate state at time `t = 2h`, you apply the formula again. This time, you use the approximation you just computed, `x(h)`, as your starting point:

`x(2h) = x(h) + h * f(x(h), h)`

Notice that the derivative `f` is now evaluated at the approximate state `x(h)` and the new time `t = h`.

**Step 4: Repeating the Process**

You can continue this process indefinitely. Each step uses the result of the previous step to compute the next one.

- To get `x(3h)`, you use `x(2h)`:
  `x(3h) = x(2h) + h * f(x(2h), 2h)`

This creates a chain of approximations. Every single time you use what you were given, it approximates where you are going. Then you know where you are going, and you use that to approximate further.

### The General Formula for the Nth Step

This iterative process can be expressed as a general formula. If you want to go `(n + 1) * h` time units into the future, you use the state at `n * h` time units:

`x((n + 1) * h) = x(n * h) + h * f(x(n * h), n * h)`

This formula defines a looping procedure. You know where you start (`x(0)`). You put it into the formula to get `x(h)`. Then you put `x(h)` into the formula to get `x(2h)`. You keep going, using the output of each step as the input for the next.

### The Procedure as a Loop

This repeated application is a classic "for loop" in programming. The structure is:

```
Initialize:  t = 0,  x = x(0)
For each step from 1 to N:
    Compute the derivative:  dx = f(x, t)
    Update the state:        x = x + h * dx
    Advance the time:        t = t + h
```

Each iteration of the loop performs one Euler step. The loop continues until you have reached your desired final time.

### Check your understanding

1.  What is the purpose of the variable `h` in the Euler method?
    <details><summary>Answer</summary> `h` is the fixed time step size. It determines how far forward in time the method moves with each iteration. A smaller `h` generally leads to a more accurate approximation but requires more steps.</details>

2.  If you know `x(2h)`, how do you compute `x(3h)` using the Euler update formula?
    <details><summary>Answer</summary> You compute `x(3h) = x(2h) + h * f(x(2h), 2h)`. You use the state at `2h` and the derivative evaluated at that state and time to step forward by `h`.</details>

3.  Why is the Euler method described as an "iterative procedure"?
    <details><summary>Answer</summary> It is iterative because the output of one step (the approximate state at the next time) becomes the input for the following step. This process is repeated, or iterated, many times to march the solution forward in time.</details>

4.  In the general formula `x((n + 1) * h) = x(n * h) + h * f(x(n * h), n * h)`, what does the term `f(x(n * h), n * h)` represent?
    <details><summary>Answer</summary> It represents the derivative of the state `x` with respect to time, evaluated at the approximate state `x(n * h)` and the time `n * h`. This is the instantaneous rate of change that is used to estimate the next state.</details>
## Error Accumulation and the Trade-Off with Step Size

Euler’s method replaces the exact derivative with an approximation. The exact derivative requires a limit, but the method uses a finite difference:

\[
\frac{dy}{dt} \approx \frac{y(t+h) - y(t)}{h}
\]

The “approximately equal” sign is the key. Because this is not the exact derivative, every step you take with Euler’s method will be off by a small amount. You will not get the exact solution to the differential equation; you will get a solution that contains a little error at each step.

### How error accumulates

You know exactly where you started (the initial condition). After the first step, you have a small error in approximating where the system is \(h\) time units into the future. You then take that slightly incorrect point and use it to approximate the next step, \(2h\) units into the future. This second step adds its own approximation error on top of the error already present from the first step. The pattern continues: each new step inherits the error from all previous steps and adds a new approximation error. This is a cascading error. The further you go into the future, the more error accumulates.

### The trade-off with step size

You clearly want the step size \(h\) to be very small so that each individual approximation is extremely accurate. However, if \(h\) is very small, the method requires many steps to advance a given distance. For example, if \(h = 1/1000\), you need to perform the Euler update 1000 times just to move one time unit forward. The course often discusses behavior as \(t\) goes to infinity; one time unit is a very short distance compared to infinity, yet even that requires a thousand iterations. A computer program could run for a very long time. If you were doing the calculations by hand, you would certainly not want to run a thousand iterations just to go one unit into the future.

On the other hand, you might want \(h\) to be as large as possible so that you can cover a long time interval quickly. But if \(h\) is too large, the error at each step becomes large, and the accumulation of that error can become so severe that the results have nothing to do with the original differential equation.

This is the fundamental computational trade-off in Euler’s method: a small step size gives accuracy at the cost of many steps (slow computation), while a large step size gives speed at the cost of potentially unacceptable error.

### Key terms defined

- **Step size \(h\)**: the fixed time interval between successive approximations in Euler’s method.
- **Local truncation error**: the error introduced by a single step of Euler’s method. It is proportional to \(h^2\) (added context: for a smooth function, the local error is \(O(h^2)\)).
- **Global error**: the total accumulated error after many steps. For Euler’s method, the global error is proportional to \(h\) (added context: \(O(h)\)), meaning it grows as the number of steps increases.

### Check your understanding

1. Why does Euler’s method introduce error at every step?

<details><summary>Answer</summary>
Euler’s method uses an approximation of the derivative (a finite difference) instead of the exact derivative, which requires a limit. This approximation is not exact, so each step produces a small error.
</details>

2. Describe how error accumulates over multiple steps.

<details><summary>Answer</summary>
After the first step, the approximated point contains a small error. That point is used as the starting point for the next step, so the second step inherits the previous error and adds its own approximation error. This cascading process continues, and the total error grows as you move further into the future.
</details>

3. What is the trade-off when choosing the step size \(h\)?

<details><summary>Answer</summary>
A small \(h\) makes each step more accurate but requires many steps to cover a given time interval, which can be computationally slow. A large \(h\) reduces the number of steps (faster computation) but increases the error per step, and the accumulated error may become so large that the results are meaningless.
</details>

4. If \(h = 0.001\), how many Euler steps are needed to advance from \(t=0\) to \(t=1\)?

<details><summary>Answer</summary>
1000 steps. Because \(1 / 0.001 = 1000\).
</details>
## Geometric Visualization of Error Accumulation

This section builds a geometric intuition for how errors in Euler’s method grow from one step to the next. You will see why the method is only an approximation and why the error does not stay constant but instead compounds.

### Setup: The Exact Solution

Imagine a graph with horizontal axis `t` (time) and vertical axis `x(t)` (the state). Starting at the initial condition `(t₀, x₀)`, the exact solution of the differential equation `dx/dt = f(x)` is a smooth curve that passes through that point. The existence and uniqueness theorem guarantees that as long as `f` is continuous, a solution exists locally and can be extended. We draw this curve as a gently curving line.

### The First Step: Tangent Line Approximation

Euler’s method replaces the exact curve with its tangent line at the starting point. The slope of that tangent line is `f(x₀)`. We step forward by a fixed amount `h` (the step size) along the tangent line to obtain the first approximate value `x₁ = x₀ + h·f(x₀)`.

In the geometric picture (exaggerated for clarity):

- The tangent line touches the exact curve only at `(t₀, x₀)`.
- After moving `h` units to the right, the vertical distance between the tangent line and the exact curve is the **local truncation error**.
- This error arises because we are approximating a (possibly curved) function by a straight line. This is exactly the same linearization that appears in Taylor’s theorem, the stable manifold theorem, and the Hartman-Grobman theorem: approximating a nonlinear object with a linear one.

### The Second Step: Double Whammy of Errors

Now we must compute the next step. The tangent line we use now is **not** the tangent to the exact curve. Instead, we use the tangent to the approximation at `(t₁, x₁)`. Its slope is `f(x₁)`, where `x₁` is already an approximate value.

The geometric consequence:

- The exact tangent at the true point on the curve would have a different slope.
- The approximate tangent at `(t₁, x₁)` points in a slightly wrong direction.
- When we step forward another `h` units, we combine two sources of error:
  1. The error carried forward from the previous step (the approximation `x₁` is not the true value).
  2. A new error from using an incorrect slope (`f(x₁)` instead of the true slope at the true point).

This is the “double whammy.”

### Accumulation Pattern

Each subsequent step repeats the same pattern:

1. Use the current approximate value to compute the slope.
2. Step forward along that slope.
3. The new approximation inherits all previous errors and adds a new local error.

The effect is a cascading divergence: the approximate points drift further and further from the true curve. The error does not average out; it rolls up like a snowball, as the speaker says: “every time you push that thing forward you take all of the errors that you had before and you just roll them up and you put another piece of error on top of that.”

### ASCII Diagram of the Process

The diagram below shows an exaggerated view of the first two steps. The exact curve is a smooth arc. The tangent lines are straight segments. The errors are the vertical gaps between the approximate points and the true curve.

```
x(t)
^
|               exact curve
|              .   .
|            .       .
|          .           .
|        .               .
|      .   *               .
|    .       *               .
|  .           *               .
|.               *               .
|                  *               .
|                     *               .
|                        *               .
|                           *               .
|                              *               .
|                                 *               .
|                                    
+-----------------------------------------------> t
t₀                t₁                t₂

Legend:
  .  = exact solution
  *  = Euler approximation points
  --- = tangent lines (not drawn to scale)
```

- At `t₀`: the first tangent line (not shown) follows the curve exactly at the start and then diverges.
- At `t₁`: the first approximate point `*` lies above the curve. The second tangent line (not shown) is drawn from that `*` and points further away from the curve.
- At `t₂`: the second approximate point `*` is even farther from the true curve.

### Key Concepts Defined

| Term | Definition |
|------|------------|
| Euler’s method | A numerical algorithm that approximates the solution of an ODE by stepping forward along tangent lines. |
| Tangent line | The straight line that best approximates a curve at a given point; its slope equals the derivative. |
| Step size `h` | The fixed increment in `t` between successive approximations. |
| Local truncation error | The error incurred in a single step by using a linear approximation instead of the true curve. |
| Error accumulation | The process by which errors from previous steps are carried forward and combined with new errors, leading to a growing total error. |
| Taylor approximation | Approximating a function by a polynomial; the linear (first‑order) Taylor approximation is the tangent line. (added context) |
| Linearization | Replacing a nonlinear function by its linear approximation near a point. (added context) |

### Check Your Understanding

1. **Why is the error in the second step called a “double whammy”?**

<details><summary>Answer</summary>
The second step suffers from two sources of error: (1) the error from the first step, which makes the starting point `x₁` inexact, and (2) a new error because the slope `f(x₁)` is computed from an approximate value and therefore differs from the true slope of the exact curve at that time.
</details>

2. **In the geometric picture, what does the vertical distance between the approximate point and the exact curve represent?**

<details><summary>Answer</summary>
It represents the accumulated global error at that time step. It includes the local truncation errors from all previous steps plus the current step.
</details>

3. **How does the existence and uniqueness theorem relate to the geometric visualization?**

<details><summary>Answer</summary>
The theorem guarantees that an exact solution curve exists locally (as long as `f` is continuous). Without that guarantee, there would be no “true curve” to compare the approximation against, and the geometric picture of error accumulation would have no reference.
</details>

4. **Why is Euler’s method equivalent to a first‑order Taylor approximation?**

<details><summary>Answer</summary>
Euler’s method uses the formula `x_{n+1} = x_n + h·f(x_n)`. This is exactly the first‑order Taylor expansion of the true solution around `t_n`, truncated after the linear term. The error is the remainder of the Taylor series, which depends on the curvature of the solution.
</details>
## Application to the RLC Circuit Model and Detection of a Limit Cycle

### The RLC Circuit Model

The RLC circuit model is a continuous-time dynamical system described by two coupled ordinary differential equations:

- `x1' = x1 - x1^3 - x2`
- `x2' = x1`

The system has a single equilibrium point at `(0,0)`. An equilibrium point is a state where all derivatives are zero. At `(0,0)`, the equilibrium is unstable: small perturbations cause trajectories to spiral outward.

By examining the vector field, you can see two opposing forces:

- Near the origin, trajectories are pushed outward.
- Far away from the origin, trajectories are pulled inward.

This combination suggests that somewhere in between, a balance exists: a closed periodic orbit called a **limit cycle**. A limit cycle is an isolated, closed trajectory in the phase plane that represents a periodic solution. Unlike a family of nested periodic orbits (which you might see in a conservative system), a limit cycle is unique: nearby trajectories either spiral toward it or away from it.

### Euler’s Method Applied to the Model

Euler’s method is a numerical technique for approximating solutions of ordinary differential equations. It iterates forward in time using a fixed step size `h`. The method is simple to implement but has a trade-off:

- If `h` is too large, the approximation accumulates error.
- If `h` is too small, the computation takes too long.

For the RLC circuit model, the Euler update steps are:

```
x1_new = x1 + h * (x1 - x1^3 - x2)
x2_new = x2 + h * x1
```

The speaker implemented this scheme with `h = 0.1`. By starting from an initial condition near the origin, the simulation produces a spiral outward that eventually settles onto a closed orbit. That closed orbit is the limit cycle.

### Detecting the Limit Cycle

The limit cycle appears as a “big beautiful” closed circle in the `(x1, x2)` phase plane. It is the balance point where the outward push from the unstable equilibrium and the inward pull from infinity cancel out. Trajectories get “stuck” on this ring.

### Sensitivity Analysis: Checking Your Own Work

Because Euler’s method can introduce numerical artifacts (features that appear only because of the step size), you must verify that the observed limit cycle is real. Perform a **sensitivity analysis**:

1. Decrease the step size `h` (for example, to `0.05` or `0.01`).
2. Run the simulation again with the same initial conditions.
3. Compare the results.

If the same periodic orbit persists with a similar shape and location, the limit cycle is a genuine dynamical phenomenon, not a numerical artifact. This is a robustness computation: you are checking your own work to ensure that the observed behavior is not caused by the numerical method.

The following table summarizes the trade-offs for step size:

| Step Size `h` | Advantage | Disadvantage |
|---------------|-----------|--------------|
| Large (e.g., 0.1) | Faster computation | Increased error, may miss fine details |
| Small (e.g., 0.01) | Higher accuracy, fewer artifacts | Slower computation, may take too long |

### Phase Plane Diagram

The ASCII diagram below shows the qualitative flow in the phase plane. The equilibrium at the origin is unstable (arrows pointing outward). Far away, arrows point inward. The limit cycle is the closed curve where the two forces balance.

```
        x2
        ^
        |       / \
        |      /   \   (limit cycle)
        |     /     \
        |    /       \
        |   /         \
        |  /           \
        | /             \
        |/               \
        +-------------------> x1
        \                /
         \              /
          \            /
           \          /
            \        /
             \      /
              \    /
               \  /
                \/
```

### Check Your Understanding

1. Why is it important to perform a sensitivity analysis on the step size `h` when using Euler’s method to detect a limit cycle?

2. Describe the behavior of the RLC circuit model near the equilibrium point `(0,0)` and far away from it.

3. What is a limit cycle? How does it differ from a family of nested periodic orbits?

<details><summary>Answer</summary>1. To ensure that the observed limit cycle is not a numerical artifact caused by a large step size. Decreasing `h` and rerunning the simulation should produce the same qualitative behavior; if the limit cycle disappears or changes drastically, it may be spurious.</details>
<details><summary>Answer</summary>2. Near `(0,0)`, trajectories spiral outward because the equilibrium is unstable. Far away, the vector field pulls trajectories inward. This creates a region where trajectories converge to a periodic orbit, the limit cycle.</details>
<details><summary>Answer</summary>3. A limit cycle is an isolated closed trajectory in the phase plane that represents a periodic orbit. Unlike a family of nested periodic orbits (e.g., in a conservative system), a limit cycle is unique: nearby trajectories either spiral toward it or away from it, depending on stability.</details>
## Sensitivity Analysis and Conclusion: Verifying Numerical Results

In this section you will examine how the choice of step size `h` affects the accuracy and computational cost of Euler’s method, and then verify your implementation by observing a periodic orbit.

### Understanding the Trade-Off: Accuracy vs. Computation Time

The core idea of Euler’s method is to approximate the continuous-time system by taking discrete steps of size `h`. As you make `h` smaller, the approximation becomes more accurate because each step covers a shorter interval, so the local error (the error introduced in a single step) is reduced. Over many steps, less error accumulates, and the overall trajectory stays closer to the true solution.

**Key claim:**  
- Smaller `h` → more accurate solution, less accumulated error.  
- The only drawback is that more steps are required to cover the same time span, which can increase the computation time. You may “be stuck at our computer waiting for a little bit longer” as you take shorter steps.

The following table summarizes the trade-off:

| Step size `h` | Accuracy | Error accumulation | Computation time |
|---------------|----------|-------------------|------------------|
| Large         | Lower    | Higher            | Shorter          |
| Small         | Higher   | Lower             | Longer           |

This sensitivity analysis shows that the step size is a parameter you must balance: you want a small enough `h` to obtain a trustworthy result, but not so small that the simulation becomes impractical.

### Implementing Euler’s Method with a For Loop

Now you will put the theory into practice. Implement Euler’s method using a simple `for` loop. The generic structure is:

```
h = 0.01          # step size (choose a small value)
T = 100           # total simulation time
N = int(T/h)      # number of steps

# initial conditions
x1 = initial_value_1
x2 = initial_value_2

for i in range(N):
    # compute derivatives (right-hand side of your system)
    dx1 = f1(x1, x2)
    dx2 = f2(x1, x2)
    # Euler update
    x1 = x1 + h * dx1
    x2 = x2 + h * dx2
    # (optional) store or plot x1, x2 at each step
```

Replace `f1` and `f2` with the specific equations of your dynamical system. Run the loop and record the values of `x1` and `x2` over time.

### Observing the Periodic Orbit

The system you are simulating lives in a two‑dimensional space called the **phase space**, where the axes are `x1` and `x2`. In this space, a **periodic orbit** is a closed curve that the trajectory traces repeatedly. The values of `x1` and `x2` repeat over time, meaning the system returns to the same state after a fixed period.

Below is a simplified ASCII diagram of a periodic orbit (a limit cycle) in the `x1`‑`x2` plane:

```
          x2
          ^
          |      . . . . . . . . .
          |    .                   .
          |   .                     .
          |  .                       .
          | .                         .
          |.                           .
          .                            .
          |.                           .
          | .                         .
          |  .                       .
          |   .                     .
          |    .                   .
          |      . . . . . . . . .
          +---------------------------> x1
```

Time is not directly shown on the axes; it is embedded in the motion of the trajectory. As you run the simulation, the point `(x1(t), x2(t))` moves along this closed curve. If you plot `x1(t)` and `x2(t)` separately against time, you will see that they converge to periodic signals that resemble sine or cosine waves.

**Claim from the transcript:**  
“If you actually plot it out what x1(t) and x2(t) look like they would converge into something some periodic signal … they would look like a sine or a cosine type thing.”

### Verifying Your Numerical Results

To confirm that your implementation is correct, check that the trajectory in phase space indeed forms a closed loop (or visually approaches one). You can also compute the period by detecting when the system returns to the starting state. A successful verification means your choice of `h` was small enough to capture the periodic behavior without excessive error.

### Check Your Understanding

1. **Why does a smaller step size `h` reduce the accumulated error in Euler’s method?**  
   <details><summary>Answer</summary>  
   A smaller `h` means each step covers a shorter interval, so the local truncation error at each step is smaller. Over many steps, these smaller errors accumulate less, resulting in a more accurate overall trajectory.  
   </details>

2. **What is the main drawback of using a very small `h`?**  
   <details><summary>Answer</summary>  
   The number of steps increases proportionally, which increases the computation time.  
   </details>

3. **In the phase space `(x1, x2)`, what does a periodic orbit look like?**  
   <details><summary>Answer</summary>  
   It appears as a closed curve (a loop). The trajectory repeats the same sequence of states indefinitely.  
   </details>

4. **How can you verify that your Euler simulation has produced a periodic orbit?**  
   <details><summary>Answer</summary>  
   Plot the trajectory in `(x1, x2)` space and look for a closed loop. Alternatively, plot `x1(t)` and `x2(t)` separately and check that they become periodic signals (e.g., resembling sine or cosine waves). You can also compute the time it takes for the system to return to the initial state.  
   </details>
## Key takeaways

- Euler's method approximates the derivative in a continuous-time dynamical system using a finite difference quotient with a small, fixed step size h.
- The method converts a continuous-time system into a discrete-time system by producing the update rule x(t+h) = x(t) + h f(x(t)).
- Starting from an initial condition, Euler's method iteratively applies the update rule in a for-loop to step forward in time.
- Each step introduces a local truncation error because the derivative is approximated, not computed exactly.
- Errors accumulate over multiple steps, causing the approximate solution to diverge from the true solution, especially for large step sizes.
- There is a trade-off between step size h and accuracy: smaller h reduces error but increases the number of steps and computation time.
- Geometrically, Euler's method follows the tangent line at the current point for a distance h, landing off the true curve, and then uses the tangent of the approximated point for the next step.
- Applying Euler's method to the RLC circuit model x1' = x1 - x1^3 - x2, x2' = x1 with h=0.1 can reveal a limit cycle, a periodic orbit in the phase plane.
- Sensitivity analysis by decreasing h (e.g., to 0.01) and rerunning the simulation helps verify that observed phenomena like limit cycles are not numerical artifacts.
- The output of Euler's method can be interpreted in phase plane plots (x1 vs x2) and time series signals (x1 vs t or x2 vs t) to analyze system behavior.
## Glossary

| Term | Definition |
|---|---|
| Continuous-time dynamical system | A system described by differential equations where the state evolves continuously with time, typically written as x' = f(x). |
| Discrete-time dynamical system | A system described by update rules where the state is defined only at discrete time steps, typically written as x_{n+1} = g(x_n). |
| Derivative | The instantaneous rate of change of a function, defined as the limit of (x(t+h) - x(t))/h as h approaches zero. |
| Finite difference quotient | An approximation of the derivative using a small but nonzero h: (x(t+h) - x(t))/h. |
| Euler's method | A numerical technique that approximates solutions to differential equations by iterating the update rule x(t+h) = x(t) + h f(x(t)). |
| Forward Euler method | Another name for Euler's method, emphasizing that it uses the derivative at the current time to step forward to the next time. |
| Step size h | The fixed time increment used in Euler's method between successive approximations. |
| Initial condition | The known state of the system at the starting time, typically t=0, used to begin the iterative process. |
| For-loop | A programming construct that repeats a block of code a specified number of times, used here to apply the Euler update repeatedly. |
| Local truncation error | The error introduced in a single step of Euler's method due to approximating the derivative with a finite difference. |
| Error accumulation | The process by which errors from each step compound over multiple iterations, causing the approximate solution to drift from the true solution. |
| Tangent line | A straight line that touches a curve at a point and has the same slope as the curve at that point, used geometrically in Euler's method to approximate the next point. |
| Phase plane | A two-dimensional plot where each axis represents one state variable of a dynamical system, used to visualize trajectories. |
| Limit cycle | A closed, isolated periodic orbit in the phase plane that attracts or repels nearby trajectories. |
| Periodic orbit | A trajectory that repeats itself exactly after a fixed period of time, appearing as a closed curve in the phase plane. |
| RLC circuit model | A specific dynamical system with equations x1' = x1 - x1^3 - x2 and x2' = x1, used as an example to demonstrate limit cycles. |
| Sensitivity analysis | The process of varying parameters (here, step size h) to check whether observed results are robust or are numerical artifacts. |
| Numerical artifact | A feature in a computed result that arises from the numerical method itself rather than from the true behavior of the system. |
| Time series signal | A plot of a state variable against time, showing how it evolves over the simulation. |
| Linearization | Approximating a nonlinear function by a linear one near a point, often using the tangent line or Taylor expansion. |
## Footnotes and deeper context

1. **Euler method accuracy order.** Euler's method is a first-order method, meaning the local truncation error is proportional to h^2, and the global error after many steps is proportional to h. This is a standard result from numerical analysis textbooks such as 'Numerical Analysis' by Burden and Faires.
2. **Stability condition for Euler method.** For stiff differential equations, Euler's method can become unstable unless h is extremely small. A common misconception is that smaller h always improves accuracy, but for stiff systems, stability constraints may force h to be smaller than accuracy requirements alone would suggest. This is documented in 'Solving Ordinary Differential Equations I' by Hairer, Norsett, and Wanner.
3. **RLC circuit model origin.** The specific RLC circuit model x1' = x1 - x1^3 - x2, x2' = x1 is a classic example of a system with a stable limit cycle, often used to illustrate the van der Pol oscillator behavior. It is not a literal RLC circuit but a simplified model of nonlinear oscillation.
4. **Alternative numerical methods.** Higher-order methods like Runge-Kutta (e.g., RK4) provide better accuracy per step than Euler's method for the same h. These are standard in scientific computing and are implemented in libraries such as SciPy's 'solve_ivp' function.
5. **Convergence of Euler method.** Under mild smoothness conditions on f, Euler's method converges to the true solution as h approaches zero. This is guaranteed by the Lax equivalence theorem for consistent and stable numerical methods, as covered in 'Finite Difference Methods for Ordinary and Partial Differential Equations' by LeVeque.
## Where to go next

- **Implement Euler's method in Python or MATLAB.** Write a simple for-loop script to simulate the RLC circuit model. Use the equations x1' = x1 - x1^3 - x2 and x2' = x1. Start with h=0.1 and run for 1000 steps. Plot the phase plane (x1 vs x2) and time series. Then repeat with h=0.01 to verify the limit cycle persists. This hands-on practice solidifies the concepts from the lecture.
- **Read about higher-order methods in 'Numerical Recipes' by Press et al..** Chapter 17 of 'Numerical Recipes: The Art of Scientific Computing' covers Euler's method and introduces Runge-Kutta methods. It explains why higher-order methods reduce error without requiring extremely small step sizes, which is the natural next step after mastering Euler's method.
- **Explore the van der Pol oscillator in the SciPy documentation.** The SciPy library's 'integrate' module includes 'solve_ivp' which implements adaptive Runge-Kutta methods. The documentation provides examples of simulating the van der Pol oscillator, a system closely related to the RLC circuit model. This shows how professional tools handle numerical integration.
- **Study error analysis in 'Differential Equations and Their Applications' by Braun.** Chapter 6 of Braun's textbook provides a clear, example-driven explanation of local and global truncation errors for Euler's method. It includes worked problems that quantify how error grows with step size and number of steps, directly supporting the trade-off discussion in the lecture.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
