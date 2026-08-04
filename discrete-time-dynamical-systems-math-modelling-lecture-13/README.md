# Introduction to Discrete-Time Dynamical Systems
> **Source:** [Discrete-Time Dynamical Systems - Math Modelling - Lecture 13](https://www.youtube.com/watch?v=wnYe8KK4qJg) by Math Modelling · 26:38 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** Undergraduate students in mathematics, engineering, or related fields who have completed a course in differential equations and linear algebra.
## Learning objectives

After working through this document you can:

1. Define a discrete-time dynamical system and contrast it with a continuous-time system.
2. Write a discrete-time system in both difference form (Δx = F(x)) and update form (x_{n+1} = G(x_n)).
3. Identify steady states of a discrete-time system by solving F(x) = 0.
4. Explain the concept of stability for a steady state in discrete time.
5. Convert a recurrence relation (e.g., Fibonacci numbers) into a first-order vector system.
6. Analyze a linear two-dimensional discrete system and derive conditions for stability of the origin.
7. Interpret the behavior of iterates based on the parameter λ: convergence, divergence, oscillation, and one-step decay.
8. Apply the stability criterion to determine whether a given steady state attracts nearby initial conditions.
## Prerequisites

- Basic calculus (derivatives, limits)
- Ordinary differential equations (continuous-time dynamical systems)
- Linear algebra (vectors, matrices, eigenvalues)
- Familiarity with Newton's method for root finding
## Introduction to Discrete-Time Dynamical Systems

This section introduces discrete-time dynamical systems, also called difference equations. Unlike continuous-time systems where time flows smoothly, discrete-time systems move from one time step to the next in distinct jumps.

### What is a Discrete-Time Dynamical System?

A discrete-time dynamical system models how a set of variables changes from one time instant to the next. The "discrete" aspect means time advances in steps (day to day, week to week, season to season, year to year) rather than flowing continuously.



In continuous-time dynamical systems, you think about flowing from one moment to the next. In discrete-time systems, you think about hopping from one instance to the next. This makes discrete-time models appropriate when you only observe data at discrete time intervals, such as:

- Day to day
- Week to week
- Month to month
- Season to season
- Year to year

Any scenario where there is a gap between sampling your population or whatever you are trying to model.

### State Space

Just like with continuous-time dynamical systems, we define a **state space** (denoted as **s**). This state space can be an n-dimensional space. Elements in this space look like:

```
x1, x2, x3, ..., xn
```



A typical state space used in examples is one where all elements are positive. This is common when working with populations, because a negative population makes no sense.

### Difference Equations

Instead of having a time derivative on one side of the equation, discrete-time systems use a **difference** (change) from one time step to the next. The equations look like this:

For the first variable:
```
Δx1 = f1(x1, x2, ..., xn)
```

For the second variable:
```
Δx2 = f2(x1, x2, ..., xn)
```

This pattern repeats for all variables down to the last one:
```
Δxn = fn(x1, x2, ..., xn)
```



Compare this to continuous-time systems. In continuous time, you let the interval over which you measure change shrink down to zero (the same way you define a derivative by letting the time interval go to zero, using t + h and t). In discrete-time systems, you keep these changes discrete. The delta (Δ) represents a discrete change to move from one time to the next.

### Vector Notation

Instead of writing all these equations separately, we use vector notation:

```
Δx = F(x)
```

Where:
- **Δx** is the vector of changes for each variable
- **F(x)** is the vector of all functions: f1, f2, f3, ..., fn



The vector Δx represents the value at the next time step minus the value at the current time step:

```
Δx = x(n+1) - x(n)
```

Here, **n** is a natural number representing the current time instance. The units of time are scaled to be natural numbers (0, 1, 2, 3, ...). So:
- **x(n)** is the value at the nth time instance
- **x(n+1)** is the value at the next time instance

### Key Concepts Summary

| Concept | Definition |
|---------|------------|
| Discrete-time dynamical system | A model where time advances in distinct steps rather than continuously |
| Difference equation | The equation describing change from one time step to the next |
| State space (s) | The n-dimensional space containing all possible states of the system |
| Δx | The change vector: x(n+1) minus x(n) |
| F(x) | The vector of functions describing how each variable changes |
| n | A natural number representing the current time instance |

### Check your understanding

1. What is the key difference between a continuous-time dynamical system and a discrete-time dynamical system?

<details><summary>Answer</summary>
In continuous-time systems, time flows smoothly from one moment to the next. In discrete-time systems, time advances in distinct steps (hops) from one instance to the next, with gaps between observations.
</details>

2. In the equation Δx = F(x), what does Δx represent?

<details><summary>Answer</summary>
Δx represents the change vector, which equals x(n+1) minus x(n). It is the value at the next time step minus the value at the current time step.
</details>

3. Why might a discrete-time model be more appropriate than a continuous-time model for studying a population?

<details><summary>Answer</summary>
A discrete-time model is appropriate when you only observe data at discrete time intervals (such as day to day, week to week, or year to year). If you sample a population at regular intervals rather than continuously, a discrete-time model matches the data collection pattern.
</details>

4. In the vector notation Δx = F(x), what does F(x) contain?

<details><summary>Answer</summary>
F(x) is the vector of all functions: f1, f2, f3, ..., fn. Each function describes how one variable changes from one time step to the next.
</details>
## Steady States in Discrete-Time Systems

In a discrete-time dynamical system, time advances in discrete steps. These steps could represent seconds, days, weeks, or any other fixed interval. The key idea is that each moment in time is indexed by a natural number (0, 1, 2, 3, ...). This indexing lets you describe how the system evolves from one moment to the next.



### The Update Formulation

The core equation for a discrete-time dynamical system is written in terms of the change in the system from one time step to the next. Let `x` represent the state of the system at the current time step. The change in the system, denoted `Δx` (delta x), is the difference between the next state and the current state. The equation is:

`Δx = f(x)`

Here, `f(x)` is a function that describes how the system changes based only on the current state. Everything on the right-hand side of the equation depends only on what is happening right now. This means that if you know the current state, you can find the next state. The next state equals the current state plus the change:

`next state = current state + Δx`

This formulation is directly analogous to Newton iteration (also called the Newton-Raphson method). In Newton iteration, you have a current guess for a root of a function, and you apply an update rule to get a better guess. That update rule is a discrete-time dynamical system. (Added context: Newton iteration uses the formula `x_{n+1} = x_n - f(x_n)/f'(x_n)`, which fits the pattern of "current state plus a change computed from the current state.")

### Initial Conditions

Just like with differential equations, a discrete-time dynamical system requires an initial condition. The initial condition specifies the state of the system at time zero. You must know what happens at the start. You set the state at time `n = 0` to a specific value. For example, if the system represents Newton's method, the initial condition is your first guess at the root.

### Steady States

A steady state (also called a fixed point or equilibrium) is a value of the state variable `x` for which there is no change in the system from one time step to the next. In continuous-time differential equations, a steady state is a value where the derivative is zero. In discrete-time systems, the concept is simpler because the equation directly describes the change.

For a steady state, the change `Δx` must be zero. This means:

`Δx_1 = 0, Δx_2 = 0, ..., Δx_n = 0`

When `Δx = 0`, nothing changes from one time step to the next. Whatever you observe today will be the same tomorrow, the same the next day, and so on. Mathematically, you find steady states by solving the equation:

`f(x) = 0`

This is because `Δx = f(x)`, and setting `Δx = 0` gives `f(x) = 0`. Finding steady states in a discrete-time dynamical system is therefore equivalent to finding the roots of the function `f` that describes the change.

### Alternative Formulation

You may have seen discrete-time dynamical systems written in a different, more common form:

`x_{next} = g(x)`

Here, `g(x)` is a function that directly gives the next state from the current state. The two formulations are related. If `Δx = f(x)`, then:

`x_{next} = x + Δx = x + f(x)`

So `g(x) = x + f(x)`. The steady-state condition `Δx = 0` is equivalent to `x_{next} = x`. In the `x_{next} = g(x)` formulation, a steady state satisfies `x = g(x)`. This is called a fixed point of the function `g`.

The transcript uses the `Δx = f(x)` form because it makes the concept of steady states more intuitive: a steady state is simply a point where there is no change. The course will move back and forth between these two ways of looking at the system.

### Check your understanding

1.  What is the mathematical condition for a steady state in a discrete-time dynamical system written as `Δx = f(x)`?

    <details><summary>Answer</summary>
    The condition is `f(x) = 0`. Since `Δx = f(x)`, a steady state requires no change, so `Δx = 0`, which implies `f(x) = 0`.
    </details>

2.  How does the concept of a steady state in a discrete-time system compare to a steady state in a continuous-time differential equation?

    <details><summary>Answer</summary>
    In both cases, a steady state is a value of the state variable where there is no change. In continuous-time systems, this means the derivative is zero. In discrete-time systems, this means the change from one step to the next is zero (`Δx = 0`). The discrete-time condition is often easier to see directly because the equation explicitly describes the change.
    </details>

3.  If a discrete-time system is given as `x_{next} = g(x)`, what equation must a steady state `x*` satisfy?

    <details><summary>Answer</summary>
    A steady state `x*` must satisfy `x* = g(x*)`. This is because at a steady state, the next state equals the current state.
    </details>

4.  Why is an initial condition necessary for a discrete-time dynamical system?

    <details><summary>Answer</summary>
    An initial condition is necessary because the update rule `Δx = f(x)` or `x_{next} = g(x)` tells you how to go from one state to the next, but it does not tell you where to start. You must specify the state at time zero (n = 0) to begin the sequence of states.
    </details>
## Stability of Steady States

In this section, you will learn what it means for a steady state to be *stable*. Stability is a property that tells you whether a system will return to a steady state after a small disturbance.

### Defining a Steady State

First, recall that a steady state is a point where the system does not change. In a discrete-time dynamical system, the update rule is given by:

x_{n+1} = x_n + f(x_n)

Here, f is the *change function*. A steady state x0 satisfies:

f(x0) = 0

This means that if you start exactly at x0, the system stays there forever. (added context: This is equivalent to finding a root of the change function f.)

### Defining Stability



Let x0 be a steady state. We say that **x0 is stable** if the following condition holds:

For all initial conditions that are *close enough* to x0, the sequence x_n generated by the update rule converges to x0.

In other words, if you start near x0, you will eventually end up at x0.

The speaker is deliberately vague about what "close enough" means. This is because the required distance depends on the specific system. For example, in Newton's method (a common way to find roots), the quality of the initial guess needed to guarantee convergence varies from function to function. A more complicated function may require a much better (closer) initial guess.

### What Stability Does and Does Not Tell You

The stability criterion does not tell you exactly how close you must start. It only guarantees that *there exists* some distance (a "neighborhood") around x0 such that if you start within that distance, you will converge to x0.

Think of it this way: stability says there is a possibility of success if your guess is good enough. It does not guarantee success for any arbitrary starting point.

### Example: Fibonacci Numbers

The Fibonacci numbers are a classic example of a discrete dynamical system. Let F_n be the nth Fibonacci number. The update rule is:

F_{n+2} = F_{n+1} + F_n

This is a second-order linear recurrence. (added context: It can be rewritten as a first-order system of two variables, but the key point is that it is a discrete-time dynamical system with a known update rule.)

### Summary of Key Concepts

| Concept | Definition |
| :--- | :--- |
| Steady state x0 | A point where f(x0) = 0, so the system does not change. |
| Stability | A steady state is stable if starting close enough to it guarantees convergence to it. |
| "Close enough" | The required distance is system-dependent and not specified by the definition. |
| Guarantee | Stability guarantees existence of a neighborhood of convergence, not a specific distance. |

### Check your understanding

1.  What is the mathematical condition for a point x0 to be a steady state of the system x_{n+1} = x_n + f(x_n)?

    <details><summary>Answer</summary>f(x0) = 0. This means the change function has a root at x0.</details>

2.  Does stability tell you exactly how close to a steady state you need to start in order to converge?

    <details><summary>Answer</summary>No. Stability only guarantees that there is some distance (a neighborhood) within which convergence is guaranteed. The exact distance depends on the system.</details>

3.  True or False: If a steady state is stable, then starting from *any* initial condition will cause the system to converge to that steady state.

    <details><summary>Answer</summary>False. Stability only guarantees convergence for initial conditions that are *close enough* to the steady state. Starting far away may lead to divergence or convergence to a different steady state.</details>

4.  Give one example of a discrete dynamical system mentioned in this section besides Newton's method.

    <details><summary>Answer</summary>The Fibonacci numbers, where F_{n+2} = F_{n+1} + F_n.</details>
## Example: Fibonacci Numbers as a Discrete Dynamical System

The Fibonacci sequence is a classic example of a discrete dynamical system. A discrete dynamical system is a rule that describes how a state changes from one time step to the next, where time takes integer values (like n = 0, 1, 2, ...). The Fibonacci sequence is defined by the recurrence relation:

F(n+1) = F(n) + F(n-1)

with initial conditions F(0) = 0 and F(1) = 1. This means each new Fibonacci number is the sum of the two previous numbers. The first few terms are: 0, 1, 1, 2, 3, 5, 8, 13, and so on.

This recurrence relation is already an update rule, just like Newton's method from earlier in the course. However, it does not fit the standard form of a discrete dynamical system, which typically uses a state vector. A state vector is a collection of variables that fully describes the system at a given time step. We need to reformulate the Fibonacci recurrence into this standard form.

### Reformulating the Fibonacci Sequence as a State Vector

Define a state vector with two components at time step n:

- x₁(n) = F(n-1), which is the previous Fibonacci number.
- x₂(n) = F(n), which is the current Fibonacci number.

Now, we derive the update rule for the next time step, n+1.

For the first component, x₁(n+1), substitute n+1 into the definition:

x₁(n+1) = F(n)

Since F(n) = x₂(n), we get:

x₁(n+1) = x₂(n)

For the second component, x₂(n+1), substitute n+1 into the definition:

x₂(n+1) = F(n+1)

Using the Fibonacci recurrence relation, F(n+1) = F(n) + F(n-1). Since F(n) = x₂(n) and F(n-1) = x₁(n), we get:

x₂(n+1) = x₂(n) + x₁(n)

So the full discrete dynamical system in standard form is:

x₁(n+1) = x₂(n)
x₂(n+1) = x₁(n) + x₂(n)

This is a linear system, meaning each new state is a linear combination of the previous state components.

### Writing the System in Delta Notation

Delta notation expresses the change in each variable from one step to the next. The change in a variable x is defined as Δx(n) = x(n+1) - x(n).

For x₁, subtract x₁(n) from both sides of the first update equation:

x₁(n+1) - x₁(n) = x₂(n) - x₁(n)

This gives:

Δx₁(n) = x₂(n) - x₁(n)

For x₂, subtract x₂(n) from both sides of the second update equation:

x₂(n+1) - x₂(n) = x₁(n) + x₂(n) - x₂(n)

This simplifies to:

Δx₂(n) = x₁(n)

So the delta form of the system is:

Δx₁(n) = x₂(n) - x₁(n)
Δx₂(n) = x₁(n)

This tells us that the change in x₁ comes from the difference between x₂ and x₁ at the current step, and the change in x₂ is simply equal to the current value of x₁.

### Initial Conditions

The standard Fibonacci sequence uses the initial conditions F(0) = 0 and F(1) = 1. In terms of the state vector:

x₁(0) = F(-1) is not defined by the standard Fibonacci definition, but we can use the recurrence to find it. Since F(1) = F(0) + F(-1), we have 1 = 0 + F(-1), so F(-1) = 1. However, the video uses the convention that x₁(0) = 0 and x₂(0) = 1. This is a valid choice because the state vector at n = 0 is defined as:

x₁(0) = F(-1) = 0 (by convention for this example)
x₂(0) = F(0) = 1

(added context: The video sets x₁(0) = 0 to match the first Fibonacci number, even though strictly F(-1) would be 1. This is a common simplification in textbook treatments.)

You can also create your own Fibonacci-like sequence by choosing any two initial values. For example, you could start with x₁(0) = 5 and x₂(0) = 10, or x₁(0) = -2 and x₂(0) = 3. These are perfectly valid initial conditions that fit into the same framework. The only requirement is that you use the update rule or the delta rule to generate subsequent states.

### Summary of the System

The following table summarizes the two equivalent forms of the Fibonacci discrete dynamical system:

| Form | Equation for x₁ | Equation for x₂ |
|------|-----------------|-----------------|
| Standard update | x₁(n+1) = x₂(n) | x₂(n+1) = x₁(n) + x₂(n) |
| Delta form | Δx₁(n) = x₂(n) - x₁(n) | Δx₂(n) = x₁(n) |

The relationship between the state variables and the Fibonacci numbers is:

| State variable | Definition | Value at n = 0 |
|----------------|------------|----------------|
| x₁(n) | F(n-1) | 0 |
| x₂(n) | F(n) | 1 |

The flow of computation for the first few steps is shown in this ASCII diagram:

```
n = 0:  x₁ = 0,  x₂ = 1
        |
        v
n = 1:  x₁ = 1,  x₂ = 1   (x₁ becomes old x₂, x₂ becomes old x₁ + old x₂)
        |
        v
n = 2:  x₁ = 1,  x₂ = 2
        |
        v
n = 3:  x₁ = 2,  x₂ = 3
        |
        v
n = 4:  x₁ = 3,  x₂ = 5
```

This reformulation shows that the Fibonacci sequence, which appears to be a single scalar recurrence, can be expressed as a two-dimensional discrete dynamical system. This is a powerful technique because it allows us to apply all the tools of linear systems theory, such as eigenvalue analysis, to study the long-term behavior of the sequence.

### Check your understanding

1. Given the state vector x₁(n) = 2 and x₂(n) = 5, what are x₁(n+1) and x₂(n+1)?

<details><summary>Answer</summary>
Using the standard update rule: x₁(n+1) = x₂(n) = 5, and x₂(n+1) = x₁(n) + x₂(n) = 2 + 5 = 7.
</details>

2. Write the delta form equation for Δx₁(n) in words.

<details><summary>Answer</summary>
The change in x₁ from step n to step n+1 is equal to the current value of x₂ minus the current value of x₁.
</details>

3. If you choose initial conditions x₁(0) = 3 and x₂(0) = 4, what is x₂(2)?

<details><summary>Answer</summary>
Step 1: x₁(1) = x₂(0) = 4, x₂(1) = x₁(0) + x₂(0) = 3 + 4 = 7.
Step 2: x₁(2) = x₂(1) = 7, x₂(2) = x₁(1) + x₂(1) = 4 + 7 = 11.
</details>

4. Why is the Fibonacci sequence considered a discrete dynamical system even before reformulation?

<details><summary>Answer</summary>
Because it has an update rule, F(n+1) = F(n) + F(n-1), that determines the next value from previous values at discrete time steps. This is exactly the structure of a discrete dynamical system.
</details>
## A Simple Two-Dimensional Linear System

This section introduces a two-dimensional linear discrete-time dynamical system. The system is deliberately simple so that you can see exactly how the analysis works. You will learn how to find the steady state, how the two coordinates evolve independently, and how to determine whether the origin is stable.

### Defining the System

Let the state be a two-dimensional vector **X** = (X₁, X₂). The change in the state from one time step to the next is given by

Δ**X** = **X**(n+1): **X**(n) = -λ **X**(n)

where λ is a positive number (λ > 0). This is the same form as the general discrete dynamical system **X**(n+1) = **F**(**X**(n)) with **F**(**X**) = **X** + Δ**X**. Here **F**(**X**) = **X**: λ **X** = (1: λ) **X**.

### Steady State

A steady state (or fixed point) satisfies **F**(**X**) = **X**, which is equivalent to Δ**X** = 0. For our system:

**F**(**X**) = (1: λ) **X** = **X**   ⇒   -λ **X** = 0

Since λ > 0, the only solution is **X** = (0, 0). The origin is the unique steady state.

### Update Equations and Decoupling

Write the update rule in component form. Starting from the change equation:

X₁(n+1): X₁(n) = -λ X₁(n)   ⇒   X₁(n+1) = X₁(n): λ X₁(n) = (1: λ) X₁(n)

X₂(n+1): X₂(n) = -λ X₂(n)   ⇒   X₂(n+1) = (1: λ) X₂(n)

The two equations are completely decoupled: each coordinate evolves independently according to the same one-dimensional linear map. To understand the whole system, you only need to analyze one coordinate.

### Iterating the Map

Let the initial condition be **X**(0) = (X₁(0), X₂(0)). Apply the update repeatedly:

| Step | X₁(n) | X₂(n) |
|------|-------|-------|
| n = 0 | X₁(0) | X₂(0) |
| n = 1 | (1: λ) X₁(0) | (1: λ) X₂(0) |
| n = 2 | (1: λ)² X₁(0) | (1: λ)² X₂(0) |
| n = 3 | (1: λ)³ X₁(0) | (1: λ)³ X₂(0) |
| … | … | … |
| n = k | (1: λ)ᵏ X₁(0) | (1: λ)ᵏ X₂(0) |

In general, after n iterations:

X₁(n) = (1: λ)ⁿ X₁(0)  
X₂(n) = (1: λ)ⁿ X₂(0)

### Stability of the Origin

We want to know what happens as n → ∞. The limit of (1: λ)ⁿ depends on the magnitude of the factor (1: λ).

- If |1: λ| < 1, then (1: λ)ⁿ → 0 as n → ∞. Consequently, X₁(n) → 0 and X₂(n) → 0 for any initial condition. The origin is **stable** (an attractor).
- If |1: λ| = 1, the iterates either stay constant (λ = 0, but λ > 0) or oscillate between two values (λ = 2). The origin is not attracting.
- If |1: λ| > 1, then (1: λ)ⁿ grows without bound (or oscillates with increasing magnitude). The origin is **unstable**.

Because λ > 0, the condition |1: λ| < 1 is equivalent to 0 < λ < 2. For λ ≥ 2, the origin is not stable.

### Summary

- The system **X**(n+1) = (1: λ) **X**(n) with λ > 0 has a single steady state at the origin.
- The coordinates evolve independently with the same multiplicative factor (1: λ).
- The origin is stable (attracts nearby points) if and only if 0 < λ < 2.

---

### Check your understanding

1. **What is the steady state of the system?**  
   <details><summary>Answer</summary>  
   The steady state is the origin (0, 0).  
   </details>

2. **Write the update equation for X₁(n+1) in terms of X₁(n).**  
   <details><summary>Answer</summary>  
   X₁(n+1) = (1: λ) X₁(n)  
   </details>

3. **If λ = 0.5 and X₁(0) = 4, what is X₁(3)?**  
   <details><summary>Answer</summary>  
   (1 to 0.5) = 0.5. X₁(3) = (0.5)³ × 4 = 0.125 × 4 = 0.5  
   </details>

4. **Under what condition on λ does the origin attract all initial conditions?**  
   <details><summary>Answer</summary>  
   The origin attracts all initial conditions when |1: λ| < 1, i.e., 0 < λ < 2.  
   </details>
## Stability Analysis of the Linear System

In this section we analyze the stability of the equilibrium point at the origin for a simple discrete-time linear system. The system is given by the scalar iteration

\[
x_{n+1} = (1 - \lambda) x_n,
\]

where \( \lambda \) is a real parameter with \( \lambda > 0 \) (the speaker assumes \( \lambda > 0 \) for the entire analysis) and \( n = 0, 1, 2, \dots \). This is a one-dimensional linear system, but the same factor \( (1 - \lambda) \) applies to each component in a multi-dimensional system if the system is diagonal. In the transcript, the speaker refers to two components \( x_1(n) \) and \( x_2(n) \), both governed by the same factor, so we can treat the system as having the same scalar dynamics for each coordinate.

The solution to the recurrence is

\[
x_n = (1 - \lambda)^n x_0,
\]

with \( x_0 \) the initial condition. The origin (\( x = 0 \)) is an equilibrium point because if \( x_0 = 0 \), then \( x_n = 0 \) for all \( n \).

### Stability Condition

Stability of the origin means that for any initial condition, the sequence \( x_n \) converges to 0 as \( n \to \infty \). Convergence occurs if and only if

\[
\lim_{n \to \infty} (1 - \lambda)^n = 0.
\]

This limit equals zero exactly when the base \( (1 - \lambda) \) has absolute value less than 1:

\[
|1 - \lambda| < 1.
\]

Solve this inequality:

\[
-1 < 1 - \lambda < 1.
\]

Subtract 1 from all parts:

\[
-2 < -\lambda < 0.
\]

Multiply by -1 (reversing inequality signs):

\[
0 < \lambda < 2.
\]

Thus, **the origin is stable (attractive) for all initial conditions** whenever \( \lambda \) lies in the open interval \( (0, 2) \). This is the key result.

### Behavior Outside the Stable Region

#### \( \lambda > 2 \)

If \( \lambda > 2 \), then \( 1 - \lambda \) is a number whose absolute value is greater than 1. For example, if \( \lambda = 3 \), then \( 1 - \lambda = -2 \), and raising \( -2 \) to increasing powers gives \( -2, 4, -8, 16, -32, 64, \dots \), which diverges in magnitude. Consequently, for any initial condition (even arbitrarily close to 0, but not exactly 0), the iterates \( x_n \) grow without bound. The origin is **unstable**: no matter how close you start, you are pushed away.

#### \( \lambda = 2 \)

At \( \lambda = 2 \), we have \( 1 - \lambda = -1 \). Then

\[
x_n = (-1)^n x_0.
\]

The sequence does not converge to 0 (unless \( x_0 = 0 \)). Instead, it simply alternates between \( x_0 \) and \( -x_0 \) forever. The origin is neither stable nor unstable in the usual sense: the state does not approach the origin, but it also does not blow up. This is a neutral, purely oscillatory case.

### Subcases Within the Stable Region: Monotonic vs. Oscillatory Convergence

Even when \( 0 < \lambda < 2 \), the sign of \( (1 - \lambda) \) affects the sign of successive iterates.

#### \( 0 < \lambda < 1 \)

Here \( 1 - \lambda > 0 \). Every iterate multiplies the previous value by a positive number. Therefore, the sign of \( x_n \) never changes: if \( x_0 > 0 \), all \( x_n \) are positive and converge to 0 from above; if \( x_0 < 0 \), all \( x_n \) are negative and converge to 0 from below. The convergence is **monotonic** (no sign flips).

#### \( 1 < \lambda < 2 \)

Here \( 1 - \lambda < 0 \). The factor is negative, so each iteration flips the sign of the state. The absolute value shrinks because \( |1 - \lambda| < 1 \), but the sequence alternates between positive and negative values as it approaches 0. The convergence is **oscillatory**: the iterates hop back and forth across the origin while getting closer.

The following table summarizes the behavior for all relevant \( \lambda \) values:

| \( \lambda \) range | \( |1 - \lambda| \) | Behavior of \( x_n \) | Stability of origin |
|---------------------|----------------------|-----------------------|---------------------|
| \( 0 < \lambda < 1 \) | \( < 1 \) | Monotonic convergence to 0 | Stable (attractive) |
| \( \lambda = 1 \) | \( 0 \) | Convergence to 0 in one step (since \( 1 - \lambda = 0 \)) | Stable (attractive): included in (0,2) |
| \( 1 < \lambda < 2 \) | \( < 1 \) | Oscillatory convergence to 0 | Stable (attractive) |
| \( \lambda = 2 \) | \( 1 \) | Pure oscillation between \( x_0 \) and \( -x_0 \) | Neither stable nor unstable |
| \( \lambda > 2 \) | \( > 1 \) | Divergence (magnitude grows) | Unstable |

### Key Concepts Defined

- **Discrete-time dynamical system**: A system that evolves in discrete steps (iterations) according to a rule.
- **Equilibrium point**: A point that, if chosen as the initial condition, remains unchanged for all future times.
- **Stability (asymptotic)**: The property that all trajectories starting sufficiently close to the equilibrium converge to it. In this linear system, the condition \( |1 - \lambda| < 1 \) guarantees global convergence (from any initial condition).
- **Exponentiation of a number**: Repeated multiplication of the number by itself; here \( (1 - \lambda)^n \) is the factor applied to the initial condition after \( n \) steps.

### Check Your Understanding

1. **Question**: For which values of \( \lambda \) does the origin become unstable?  
   <details><summary>Answer</summary>  
   \( \lambda > 2 \) (and also \( \lambda < 0 \) if we did not assume \( \lambda > 0 \); but the video assumes \( \lambda > 0 \) so the unstable region is \( \lambda > 2 \)).  
   </details>

2. **Question**: If \( \lambda = 1.5 \) and \( x_0 = 3 \), what is the sign of \( x_1 \) and \( x_2 \)?  
   <details><summary>Answer</summary>  
   \( 1 - \lambda = -0.5 \). \( x_1 = -0.5 \times 3 = -1.5 \) (negative). \( x_2 = -0.5 \times (-1.5) = 0.75 \) (positive). The signs alternate.  
   </details>

3. **Question**: Explain why the condition \( |1 - \lambda| < 1 \) is equivalent to \( 0 < \lambda < 2 \).  
   <details><summary>Answer</summary>  
   \( |1 - \lambda| < 1 \) means \( -1 < 1 - \lambda < 1 \). Subtract 1: \( -2 < -\lambda < 0 \). Multiply by -1: \( 2 > \lambda > 0 \), i.e., \( 0 < \lambda < 2 \).  
   </details>

4. **Question**: What happens at \( \lambda = 2 \)? Is the origin stable?  
   <details><summary>Answer</summary>  
   At \( \lambda = 2 \), \( 1 - \lambda = -1 \), so \( x_n = (-1)^n x_0 \). The sequence does not converge to 0 (unless \( x_0 = 0 \)). It merely oscillates between \( x_0 \) and \( -x_0 \). The origin is not stable because nearby points do not approach the origin; they stay at a constant distance.  
   </details>
## Conclusion and Preview of Upcoming Lectures

The final case to consider is when the parameter lambda equals 1. In this situation, the system behaves in a special way: the next point becomes 0 regardless of the initial condition. This means the equilibrium is reached in a single step. Because the value of lambda minus 1 is 0 (added context: the difference between lambda and 1 is zero, which causes the iterative map to collapse to zero immediately), the dynamics are trivial. No further interesting behavior occurs.

This concludes a brief, rough introduction to discrete-time dynamical systems. The key ideas covered include the role of the parameter lambda in determining the behavior of solutions, the concept of equilibrium points, and the classification of stability based on the value of lambda.

In the upcoming lectures, the course will move into more hands-on work. You will get your hands dirtier by analyzing and interpreting discrete-time dynamical systems using graphical methods and other rough, intuitive approaches. After building comfort with these techniques, the course will zoom out to examine dynamical systems as a whole. At that point, you will learn analytical (pencil-and-paper) methods for determining:

- What the equilibrium points are.
- Whether each equilibrium point is stable or unstable.
- How solutions behave over time.

The immediate next step is to develop intuition through extensive graphical work. This will prepare you for the more formal analytical methods that follow.

### Check your understanding

1. What happens to the system when lambda equals 1, according to the lecture?

<details><summary>Answer</summary>
When lambda equals 1, the next point becomes 0 regardless of the initial condition. The equilibrium is reached in one step, and no further interesting dynamics occur.
</details>

2. List two types of methods that will be used in upcoming lectures to study discrete-time dynamical systems.

<details><summary>Answer</summary>
Graphical methods (intuitive, rough approaches) and analytical methods (pencil-and-paper techniques for determining equilibrium points, stability, and solution behavior).
</details>

3. What is the purpose of the graphical methods that will be introduced first?

<details><summary>Answer</summary>
The graphical methods are intended to build intuition and comfort with analyzing and interpreting discrete-time dynamical systems before moving on to more formal analytical methods.
</details>

4. Name three things that analytical methods will help determine.

<details><summary>Answer</summary>
Equilibrium points, stability of those equilibrium points, and how solutions behave.
</details>
## Key takeaways

- Discrete-time dynamical systems, also called difference equations, model situations where time advances in discrete steps such as days or years, unlike continuous-time systems where time flows continuously.
- A discrete-time system can be written in difference form as Δx = F(x) (change from one step to the next) or in update form as x_{n+1} = G(x_n) (next state as a function of the current state).
- Steady states (equilibrium points) occur when Δx = 0, which means solving F(x) = 0; at these points the state does not change from one time step to the next.
- A steady state x0 is stable if all initial conditions sufficiently close to x0 generate sequences that converge to x0; the required closeness depends on the system.
- The Fibonacci sequence can be rewritten as a first-order vector discrete dynamical system by defining x1(n) = F(n-1) and x2(n) = F(n), leading to update rules x1(n+1) = x2(n) and x2(n+1) = x1(n) + x2(n).
- For the linear two-dimensional system Δx = -λ x (with λ > 0), the origin is the only steady state; the update form x(n+1) = (1-λ)x(n) decouples the components, each evolving independently.
- The behavior of iterates depends on the parameter λ: stable for 0 < λ < 2 (convergence to origin), unstable for λ > 2 (divergence), oscillatory at λ = 2 (alternating between ±x(0) without converging), and one-step decay at λ = 1 (reaching zero in one step).
- For 0 < λ < 1, iterates retain the same sign and converge monotonically to zero; for 1 < λ < 2, iterates oscillate while converging to zero.
## Glossary

| Term | Definition |
|---|---|
| discrete-time dynamical system | A system in which time advances in discrete steps (e.g., days, years) and the state evolves according to a rule that uses the current state to compute the next state. |
| continuous-time dynamical system | A system in which time flows continuously and the state evolves according to a differential equation, typically written as dx/dt = f(x). |
| state space | The set of all possible states of a dynamical system, often denoted S, which can be an n-dimensional space where each coordinate corresponds to a variable of interest. |
| difference equation | Another name for a discrete-time dynamical system, where the change in state from one time step to the next is given by a function of the current state. |
| Δx (delta x) | The change in the state vector from time step n to n+1, defined as x(n+1) minus x(n). |
| update form | The representation of a discrete dynamical system as x_{n+1} = G(x_n), where G is a function that gives the next state directly from the current state. |
| difference form | The representation of a discrete dynamical system as Δx = F(x), where F is the function that gives the change from one time step to the next. |
| steady state (equilibrium point) | A state x0 such that Δx = 0, i.e., F(x0) = 0; at this state the system does not change from one time step to the next. |
| stability | A property of a steady state x0 such that all initial conditions sufficiently close to x0 produce sequences that converge to x0 as n increases. |
| initial condition | The value of the state at time n = 0, denoted x(0), which is required to start iterating the discrete dynamical system. |
| Newton's method (Newton iteration) | An iterative root-finding algorithm that can be viewed as a discrete dynamical system where the update rule is x_{n+1} = x_n - f(x_n)/f'(x_n). |
| Fibonacci numbers | A sequence defined by F(n+1) = F(n) + F(n-1) with F(0)=0 and F(1)=1; it can be expressed as a first-order vector discrete dynamical system. |
| linear system | A dynamical system in which the update or change function is a linear function of the state, such as Δx = -λ x. |
| decoupled system | A system in which the equations for each state variable are independent of the others, so each variable evolves according to its own separate rule. |
| multiplier (1-λ) | In the linear system Δx = -λ x, the factor (1-λ) appears in the update form x(n+1) = (1-λ)x(n) and determines the growth or decay of iterates. |
| convergence | The property of a sequence of states that approaches a limit (e.g., a steady state) as n tends to infinity. |
| divergence | The property of a sequence of states that grows without bound or does not approach a limit as n tends to infinity. |
| oscillation | A pattern of iterates that alternate between positive and negative values (or between two or more values) without settling to a single value. |
| monotonic convergence | A sequence that approaches a limit from one side (either all positive or all negative) without changing sign, and with each step moving closer to the limit. |
| one-step decay | The special case where the multiplier (1-λ) equals zero, so that from any initial condition the system reaches zero in exactly one time step. |
## Footnotes and deeper context

1. **Stability criterion in general.** For a linear discrete system x_{n+1} = A x_n, the origin is stable if and only if all eigenvalues of A have magnitude less than 1. The condition |1-λ| < 1 for the scalar case is a special case of this eigenvalue criterion.
2. **Newton's method as a dynamical system.** Newton's method is a specific discrete dynamical system where the update function G(x) = x - f(x)/f'(x). Its steady states are roots of f, and stability depends on the derivative of G at the root being less than 1 in absolute value.
3. **Fibonacci vector formulation.** The vector form of the Fibonacci recurrence uses the companion matrix [[0,1],[1,1]]; the eigenvalues of this matrix are the golden ratio φ and its conjugate, both of magnitude greater than 1, so the origin is unstable.
4. **Periodic behavior at λ=2.** When λ = 2, the multiplier is -1, leading to a period-2 cycle: x(n+2) = x(n). This is a borderline case between stability and instability; in nonlinear systems, such points often lead to bifurcations.
5. **Difference form vs. update form equivalence.** The two forms are equivalent: given Δx = F(x), the update form is x_{n+1} = x_n + F(x_n). Conversely, given x_{n+1} = G(x_n), the difference form is Δx = G(x_n) - x_n.
## Where to go next

- **Nonlinear Dynamics and Chaos by Steven H. Strogatz.** Chapters on discrete maps (logistic map, bifurcations) provide a deeper understanding of stability, period-doubling, and chaos. This is a standard textbook for dynamical systems at the undergraduate level.
- **An Introduction to Difference Equations by Saber Elaydi.** A comprehensive resource on difference equations covering linear systems, stability theory, and applications. It is a canonical reference for discrete-time dynamical systems.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
