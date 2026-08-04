# Stability of Discrete-Time Dynamical Systems: Linearization and Eigenvalue Analysis
> **Source:** [Analysis of Discrete-Time Dynamical Systems - Math Modelling - Lecture 19](https://www.youtube.com/watch?v=6It02qpjHQ8) by Math Modelling · 08:14 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students of mathematical modeling who have already studied continuous-time dynamical systems and want to understand the analogous theory for discrete-time systems.
## Learning objectives

After working through this document you can:

1. Define a discrete-time dynamical system in both difference equation form (X_{n+1} = X_n + f(X_n)) and update form (X_{n+1} = g(X_n)).
2. Identify equilibrium points of a discrete-time system using the conditions f(X*) = 0 or g(X*) = X*.
3. Linearize a discrete-time system around an equilibrium by computing the Jacobian matrix of the update function g.
4. State the stability condition for a discrete-time linear system: all eigenvalues of the Jacobian must have modulus less than 1.
5. Explain why eigenvalues with modulus less than 1 cause contraction and convergence to the equilibrium.
6. Determine instability when at least one eigenvalue has modulus greater than 1, leading to expansion and divergence.
7. Compare the discrete-time stability condition (unit circle) with the continuous-time condition (left half-plane) and highlight the key difference.
8. Apply the stable manifold theorem and Hartman-Grobman theorem to conclude that linear stability implies local nonlinear stability.
## Prerequisites

- Basic calculus and linear algebra, including eigenvalues and Jacobian matrices.
- Familiarity with continuous-time dynamical systems, fixed points, and stability conditions (real part of eigenvalues less than zero).
- Understanding of difference equations and iterative maps.
## Introduction and Motivation for Discrete-Time Systems

This section introduces discrete-time dynamical systems and explains why they deserve separate attention after studying continuous-time systems. You will learn how discrete-time systems relate to continuous-time theory and how they are typically written.

### What Are Discrete-Time Dynamical Systems?

In previous videos, the course focused on continuous-time dynamical systems. That focus was not because the theory applies only to continuous-time systems. In fact, every concept discussed for continuous-time systems has an analog in discrete-time systems. (Added context: A discrete-time system updates its state at distinct time steps, such as every second or every iteration, rather than continuously.)

The purpose of this short lecture video is to catch up on the discrete-time concepts that might have been overlooked while walking through the general theory of dynamical systems.

### How Discrete-Time Systems Are Written

A discrete-time dynamical system is written as the change in some state variable X equals a function of that state variable. The standard form is:

```
X_{k+1} = f(X_k)
```

Here:
- X is the state variable (a vector or scalar that describes the system at a given time).
- k is the current time step (an integer index).
- X_{k+1} is the state at the next time step.
- f is a function that maps the current state to the next state.

Typically, we like to open this representation a little bit. (Added context: "Open this up" means expanding the notation to show the iterative nature more clearly.) For example, you might write:

```
X_1 = f(X_0)
X_2 = f(X_1) = f(f(X_0))
X_3 = f(X_2) = f(f(f(X_0)))
```

This shows that the system evolves by repeatedly applying the function f to the current state.

### Key Concepts

| Concept | Definition |
|---------|------------|
| Discrete-time dynamical system | A system where state updates occur at distinct, separate time steps (e.g., k = 0, 1, 2, ...) |
| State variable X | The variable (scalar or vector) that describes the system at a given time step |
| Update function f | The rule that maps the current state X_k to the next state X_{k+1} |
| Continuous-time analog | Every concept from continuous-time systems (stability, equilibrium, linearization) has a corresponding version in discrete-time |

### Why This Matters

Understanding discrete-time systems is essential because many real-world systems are inherently discrete: digital controllers, economic models, population dynamics with non-overlapping generations, and computer simulations of continuous systems. The eigenvalue analysis you will learn later applies directly to these systems.

### Check Your Understanding

1. What is the standard form for writing a discrete-time dynamical system?

<details>
<summary>Answer</summary>
The standard form is X_{k+1} = f(X_k), where X_k is the state at time step k, and f is the function that maps the current state to the next state.
</details>

2. How does a discrete-time system differ from a continuous-time system in terms of when state updates occur?

<details>
<summary>Answer</summary>
A discrete-time system updates its state at distinct, separate time steps (e.g., k = 0, 1, 2, ...), while a continuous-time system updates its state continuously over time.
</details>

3. True or False: The theory of continuous-time dynamical systems has no relationship to discrete-time systems.

<details>
<summary>Answer</summary>
False. Every concept discussed for continuous-time systems has an analog in discrete-time systems.
</details>

4. What does the notation X_{k+1} represent in a discrete-time system?

<details>
<summary>Answer</summary>
X_{k+1} represents the state of the system at the next time step (one step after the current time step k).
</details>
## Difference Equations and Equilibrium Definitions

This section introduces difference equations as a way to model discrete-time dynamical systems and defines what it means for a point to be an equilibrium (or fixed point) of such a system.

### From Change to Difference Equations

In a discrete-time dynamical system, the change from one step to the next is given by the function F. Specifically, if X is the current state, then the change is F(X). This change is the difference between the next state and the current state.

The relationship is:

X_next minus X_current equals F(X_current)

This is a difference equation. It tells you that if you know the current state X_current, then you can compute the next state X_next by adding the change F(X_current) to the current state.

X_next equals X_current plus F(X_current)

(Added context: A difference equation is a discrete analog of a differential equation. Instead of describing a continuous rate of change, it describes the change from one discrete time step to the next.)

### Examples of Difference Equations

Two common examples of systems that use difference equations are:

1.  Newton's method: An iterative algorithm for finding roots of a function.
2.  Gradient descent: An optimization algorithm that iteratively moves toward a minimum of a function.

These are both iterative processes where the next value depends on the current value plus some computed change.

Another example, which you have seen in this course, is modeling yeast populations. In such a model, the population size at the next time step depends on the current population size plus a change term (often representing growth or decay).

### Defining G(X) and the Equilibrium Condition

To analyze the system, we can define a new function G. G of X is equal to X plus F of X.

G(X) equals X plus F(X)

This function G directly gives the next state from the current state. So the difference equation can be rewritten as:

X_next equals G(X_current)

Now, we can analyze this discrete-time system using a process similar to what we have done with continuous dynamical systems. That process is linearization around a fixed point or an equilibrium.

### What is an Equilibrium?

Let X star (written as X*) be an equilibrium point. For a discrete-time system, an equilibrium has two equivalent definitions:

1.  F of X star is equal to zero. This means there is no change from one step to the next.
2.  G of X star is equal to X star. This means the next state is the same as the current state.

These two definitions are two different interpretations of the same condition.

If F of X star is zero, then the change is zero. This directly implies that what you are doing next (X_next) is the same as what you are doing now (X_current). Therefore, the system stays at X star once it reaches that point.

### Summary of Key Concepts

| Concept | Definition | Mathematical Expression |
| :--- | :--- | :--- |
| Difference Equation | A rule that gives the next state based on the current state. | X_next equals X_current plus F(X_current) |
| Change Function F | The function that computes the change from one step to the next. | F(X_current) equals X_next minus X_current |
| Next-State Function G | The function that directly gives the next state. | G(X) equals X plus F(X) |
| Equilibrium X* | A state where the system does not change from one step to the next. | F(X*) equals 0, or equivalently, G(X*) equals X* |

### Check your understanding

1.  What is the relationship between the change function F and the next-state function G?

    <details>
    <summary>Answer</summary>
    G(X) equals X plus F(X). G gives the next state directly, while F gives the change from the current state to the next state.
    </details>

2.  A population model is given by X_next equals 2 times X_current. What is the change function F(X)?

    <details>
    <summary>Answer</summary>
    Since X_next equals X_current plus F(X_current), we have 2X equals X plus F(X). Therefore, F(X) equals X.
    </details>

3.  For the same model, X_next equals 2X, is X equals 0 an equilibrium? Explain.

    <details>
    <summary>Answer</summary>
    Yes. At X equals 0, the next state is 2 times 0 equals 0. So the state does not change. This satisfies the equilibrium condition G(0) equals 0.
    </details>

4.  State the two equivalent conditions for a point X* to be an equilibrium of a discrete-time dynamical system.

    <details>
    <summary>Answer</summary>
    The two conditions are: (1) F(X*) equals 0, and (2) G(X*) equals X*.
    </details>
## Linearization Around an Equilibrium

This section explains how to linearize a discrete-time dynamical system around an equilibrium point. The process is analogous to linearization in continuous-time systems, but it is applied to an update equation rather than a differential equation.

### The Equilibrium Condition in a Difference Equation

A discrete-time dynamical system is often written as an update equation:

\[
x_{k+1} = f(x_k)
\]

Here, \(x_k\) is the state at time step \(k\), and \(f\) is a function that maps the current state to the next state. (Added context: This is called a "difference equation" because it describes how the state changes from one discrete time step to the next.)

An **equilibrium point** (also called a steady state or fixed point) is a state \(x^*\) such that if the system starts at \(x^*\), it stays there forever. Mathematically, this means:

\[
x^* = f(x^*)
\]

If you are currently at the equilibrium, you will stay at the equilibrium. This is the same condition as saying that the state does not change from one step to the next. These two views (the definition of equilibrium and the condition \(x^* = f(x^*)\)) are equivalent.

### Why the Update Equation Notation is Standard

The update equation form \(x_{k+1} = f(x_k)\) is the standard notation you will encounter in many numerical methods. Examples include:

- **Newton's method** for finding roots of a function.
- **Gradient descent** for optimization.
- **Euler's method** for numerically solving differential equations (explained in a later video).

All of these methods are expressed as update equations, making the linearization technique broadly applicable.

### Linearizing the Update Equation

Just as we linearized continuous-time dynamics by taking the Jacobian matrix about the steady state, we can do the same for discrete-time dynamics.

The linearization of the update equation \(x_{k+1} = f(x_k)\) around an equilibrium point \(x^*\) is:

\[
x_{k+1} - x^* \approx A (x_k - x^*)
\]

where \(A\) is the **Jacobian matrix** of \(f\) evaluated at \(x^*\). The Jacobian matrix contains all first-order partial derivatives of \(f\) with respect to the state variables. (Added context: For a system with \(n\) state variables, \(A\) is an \(n \times n\) matrix.)

The linearized system describes how small deviations from the equilibrium evolve over time. The stability of the original nonlinear system near the equilibrium is determined by the eigenvalues of \(A\).

### Summary of the Linearization Process

1. Identify the equilibrium point \(x^*\) by solving \(x^* = f(x^*)\).
2. Compute the Jacobian matrix \(A = \frac{\partial f}{\partial x}\) evaluated at \(x = x^*\).
3. The linearized dynamics are given by \(x_{k+1} - x^* = A (x_k - x^*)\).

### Check your understanding

1.  What is the condition for a point \(x^*\) to be an equilibrium of the discrete-time system \(x_{k+1} = f(x_k)\)?

    <details>
    <summary>Answer</summary>
    The condition is \(x^* = f(x^*)\). If the system starts at \(x^*\), it stays at \(x^*\).
    </details>

2.  Name two numerical methods that are commonly written as update equations of the form \(x_{k+1} = f(x_k)\).

    <details>
    <summary>Answer</summary>
    Newton's method and gradient descent. (Euler's method is also mentioned in the transcript.)
    </details>

3.  What matrix is used to linearize the update equation \(x_{k+1} = f(x_k)\) around an equilibrium point?

    <details>
    <summary>Answer</summary>
    The Jacobian matrix of \(f\) evaluated at the equilibrium point.
    </details>
## Stability Condition: Eigenvalues with Modulus Less Than One

After linearizing the system around an equilibrium point, you obtain a linear dynamical system. The linearization process means you compute the Jacobian matrix of the function g at the equilibrium point x star. The resulting updating scheme is governed entirely by this Jacobian matrix, denoted dg(x star). This is a completely linear dynamical system.

The stability of this linearized system follows results similar to those in continuous time. All of the dynamics are determined by the eigenvalues of the matrix dg. Specifically, the system is stable if every eigenvalue of dg(x star) has a modulus less than 1.

### Eigenvalue Modulus and the Unit Circle

The modulus of an eigenvalue refers to its absolute value in the complex plane. Because eigenvalues can be complex conjugates of each other, you must consider the full complex number. The modulus of a complex number is the Euclidean norm: the square root of (real part squared plus imaginary part squared). This modulus must be smaller than 1 for every eigenvalue.

The condition "modulus less than 1" means that all eigenvalues lie inside the unit circle in the complex plane. The unit circle is the set of all complex numbers with modulus exactly 1.

### Why This Condition Works

When every eigenvalue has modulus less than 1, the Jacobian matrix dg(x star) becomes a contraction. A contraction is a mapping that reduces distances between points with each application. In this context, after each iteration n, the state vector contracts toward the equilibrium point. This contraction property ensures that the original equilibrium point is stable.

### Summary of the Stability Condition

| Component | Description |
|-----------|-------------|
| System type | Linearized discrete-time dynamical system |
| Governing matrix | Jacobian matrix dg(x star) evaluated at equilibrium x star |
| Stability condition | Every eigenvalue of dg(x star) has modulus less than 1 |
| Modulus definition | sqrt(real part^2 + imaginary part^2) for complex eigenvalues |
| Geometric interpretation | All eigenvalues lie inside the unit circle in the complex plane |
| Underlying mechanism | The Jacobian matrix acts as a contraction, reducing distance to equilibrium each iteration |

### Check your understanding

1. What is the modulus of a complex eigenvalue with real part 0.5 and imaginary part 0.5?

<details><summary>Answer</summary>
The modulus is sqrt(0.5^2 + 0.5^2) = sqrt(0.25 + 0.25) = sqrt(0.5) approximately 0.707. Since 0.707 is less than 1, this eigenvalue satisfies the stability condition.
</details>

2. If a Jacobian matrix has eigenvalues 0.9, -0.8, and 1.1, is the equilibrium point stable?

<details><summary>Answer</summary>
No. The eigenvalue 1.1 has modulus 1.1, which is greater than 1. For stability, every eigenvalue must have modulus less than 1. The presence of any eigenvalue with modulus greater than or equal to 1 means the system is not stable.
</details>

3. What does it mean for a Jacobian matrix to be a contraction in the context of discrete-time dynamical systems?

<details><summary>Answer</summary>
A contraction means that with each iteration of the system, the distance between the current state and the equilibrium point decreases. When the Jacobian matrix has all eigenvalues with modulus less than 1, the mapping it defines shrinks distances, causing the state to converge toward the equilibrium point over successive time steps.
</details>

4. Why must you consider the modulus of complex eigenvalues rather than just the real part?

<details><summary>Answer</summary>
Complex eigenvalues can have real parts that are less than 1 but imaginary parts that cause the overall modulus to exceed 1. For example, an eigenvalue with real part 0 and imaginary part 1.1 has modulus 1.1, which violates the stability condition even though the real part is less than 1. The modulus captures the full magnitude of the eigenvalue in the complex plane, which determines the contraction or expansion behavior of the system.
</details>
## Instability Condition: At Least One Eigenvalue with Modulus Greater Than One

  
At this point in the analysis, you have already established the stability condition for a discrete-time dynamical system. The stable manifold theorem, which you learned for continuous dynamics, applies identically to discrete-time dynamics. If the linearized discrete system is a contraction, meaning it pulls points closer together, then the fully nonlinear system also behaves as a contraction locally. The word "locally" is critical because the linearization comes from a Taylor expansion around the equilibrium point. That Taylor expansion is only accurate near the equilibrium, so the contraction guarantee only holds for starting points sufficiently close to that equilibrium.

The stability result is: if you start close to the equilibrium, you converge to it when the Jacobian matrix, denoted as dg(x*), has all eigenvalues with modulus less than 1. Here, "modulus" means the absolute value for real eigenvalues, or the magnitude (distance from the origin in the complex plane) for complex eigenvalues. The Jacobian matrix dg(x*) is the matrix of first partial derivatives of the system function g evaluated at the equilibrium point x*.

### The Instability Condition

You can reverse the stability logic to obtain an instability condition. The system is unstable if there exists at least one eigenvalue of the matrix dg(x*) with modulus greater than 1. The phrase "at least one" is essential: even a single eigenvalue outside the unit circle is sufficient to declare the system unstable. The unit circle is the set of all complex numbers with modulus exactly 1. Eigenvalues with modulus less than 1 lie inside the unit circle, eigenvalues with modulus greater than 1 lie outside it.

| Condition on eigenvalues of dg(x*) | System behavior |
|------------------------------------|-----------------|
| All eigenvalues have modulus < 1 | Locally asymptotically stable (contraction) |
| At least one eigenvalue has modulus > 1 | Unstable (expansion in at least one direction) |
| All eigenvalues have modulus ≤ 1, at least one has modulus = 1 | Marginal case, requires further analysis (added context) |

### Why One Eigenvalue Outside the Unit Circle Causes Instability

The reason is straightforward when you consider what happens when you take successive powers of that eigenvalue. For a linear system, the state at step n is computed by applying the matrix dg(x*) repeatedly, n times. If an eigenvalue λ has modulus greater than 1, then λ^n grows without bound as n increases. The magnitude of λ^n is |λ|^n, and since |λ| > 1, this quantity tends to infinity as n goes to infinity.

That single expanding eigenvalue means that at least one dimension of the state space is expanding. Even if all other eigenvalues are contracting (modulus less than 1), the expanding direction dominates. Starting from any initial condition that has a nonzero component along that expanding eigenvector, the trajectory will move away from the equilibrium. The system is therefore unstable.

```
State space diagram (added context):

        Unit circle (|λ| = 1)
        ┌─────────────────┐
        │                 │
        │   Stable region │   Unstable region
        │   (|λ| < 1)     │   (|λ| > 1)
        │                 │
        │    ● λ = 0.5    │    ● λ = 1.2
        │                 │
        └─────────────────┘
        All eigenvalues   At least one eigenvalue
        inside circle     outside circle
        → stable          → unstable
```

The practical consequence is that you do not need to check every eigenvalue for stability. You only need to find one eigenvalue with modulus greater than 1 to conclude the system is unstable. Conversely, to prove stability, you must verify that every eigenvalue has modulus less than 1.

### Check your understanding

1. **Question:** A discrete-time system has a Jacobian matrix dg(x*) with eigenvalues 0.8, 0.5, and 1.1. Is the system stable or unstable at x*?

<details><summary>Answer</summary>
Unstable. The eigenvalue 1.1 has modulus greater than 1, so at least one eigenvalue lies outside the unit circle. The system is unstable even though the other two eigenvalues are contracting.

</details>

2. **Question:** What does the phrase "at least one eigenvalue with modulus greater than 1" mean for the behavior of successive powers of that eigenvalue?

<details><summary>Answer</summary>
If an eigenvalue λ has |λ| > 1, then |λ|^n grows without bound as n increases. The successive powers λ^n become larger in magnitude, which means the state component along that eigenvector expands over time, driving the trajectory away from the equilibrium.

</details>

3. **Question:** Why is the instability condition only valid locally for a nonlinear system?

<details><summary>Answer</summary>
The Jacobian matrix dg(x*) comes from a Taylor expansion of the nonlinear function g around the equilibrium x*. The Taylor expansion is only an accurate approximation near x*. Therefore, the eigenvalue analysis guarantees instability only for initial conditions sufficiently close to the equilibrium. Far from the equilibrium, nonlinear effects may dominate and the linear prediction may not hold.

</details>

4. **Question:** If a Jacobian matrix has eigenvalues 0.9, 0.9, and 0.9, is the system stable?

<details><summary>Answer</summary>
Yes. All three eigenvalues have modulus 0.9, which is less than 1. Every eigenvalue lies inside the unit circle, so the system is locally asymptotically stable. Starting close to the equilibrium, the trajectory converges to it.

</details>
## Comparison with Continuous-Time Systems and Key Theorems

The analysis of discrete-time nonlinear systems follows the same fundamental process as continuous-time dynamical systems. In both cases, the stability of a nonlinear system near an equilibrium point is determined by analyzing the eigenvalues of the linearized system's matrix.

### The Core Principle: Linearization Carries Over

If the linearized system is stable, then the nonlinear system is also stable near the equilibrium point. Conversely, if the linearized system has an unstable direction (meaning at least one eigenvalue indicates instability), that instability carries over to the nonlinear system. If you start close to the equilibrium point in an unstable direction, you will be pushed away from it.

This principle is formalized by two key theorems that apply to both continuous-time and discrete-time systems.

### The Stable Manifold Theorem

The stable manifold theorem tells you the same thing for discrete-time systems as it does for continuous-time systems: if you have stability for the linear system, then it carries over to stability for the nonlinear system. This means that near the equilibrium point, the set of points that approach the equilibrium (the stable manifold) has the same dimension and structure as the stable subspace of the linearized system.

### The Critical Difference: Stability Region

The only thing you must be very careful about is that the meaning of "stable eigenvalues" is slightly different between the two types of systems. This is typically the thing that messes people up the most.

| System Type | Stability Condition | Region in Complex Plane |
|-------------|---------------------|-------------------------|
| Continuous-time | Real part of eigenvalue is less than zero | Left half of the complex plane |
| Discrete-time | Magnitude of eigenvalue is less than one | Inside the unit circle in the complex plane |

For continuous-time systems, stability requires that all eigenvalues have a real part less than zero. This places them in the left half of the complex plane.

For discrete-time systems, stability requires that all eigenvalues have a magnitude less than one. This places them inside the unit circle in the complex plane.

If you can remember this single difference, everything else about the analysis is the same.

### The Hartman-Grobman Theorem

The Hartman-Grobman theorem also applies to discrete-time systems. It tells you that if you zoom in closer and closer to an equilibrium value for a nonlinear difference equation, the system looks more and more like the linearized system.

Specifically, the nonlinear system near the equilibrium point is homeomorphic to the linearized system. A homeomorphism is a continuous, invertible mapping with a continuous inverse (added context: it preserves the topological structure but can bend or deform the shape). This means the nonlinear system might be bent or deformed a little bit compared to the linear system, but it has the same basic structure. The trajectories near the equilibrium point are topologically equivalent to those of the linearized system.

### Summary of Key Concepts

1.  Both continuous-time and discrete-time nonlinear systems are analyzed by linearizing around an equilibrium point.
2.  The stable manifold theorem guarantees that linear stability implies nonlinear stability.
3.  The Hartman-Grobman theorem guarantees that the nonlinear system is topologically equivalent to the linear system near the equilibrium point.
4.  The only difference is the stability region: eigenvalues must be inside the unit circle for discrete-time systems, not in the left half-plane as for continuous-time systems.

### Check Your Understanding

1.  What is the stability condition for a discrete-time linear system?

<details><summary>Answer</summary>
All eigenvalues must have a magnitude less than one (they must lie inside the unit circle in the complex plane).
</details>

2.  How does the stability condition for discrete-time systems differ from that for continuous-time systems?

<details><summary>Answer</summary>
For continuous-time systems, eigenvalues must have a real part less than zero (they must lie in the left half of the complex plane). For discrete-time systems, eigenvalues must have a magnitude less than one (they must lie inside the unit circle).
</details>

3.  What does the Hartman-Grobman theorem tell us about the relationship between a nonlinear system and its linearization near an equilibrium point?

<details><summary>Answer</summary>
It tells us that the nonlinear system is homeomorphic to the linearized system near the equilibrium point. This means they have the same basic topological structure, even if the nonlinear system is slightly bent or deformed.
</details>

4.  If a linearized discrete-time system has one eigenvalue with magnitude 1.2 and all others with magnitude less than 1, what can you conclude about the nonlinear system near the equilibrium point?

<details><summary>Answer</summary>
The nonlinear system will be unstable near the equilibrium point. The eigenvalue with magnitude greater than 1 indicates an unstable direction, and this instability carries over from the linear system to the nonlinear system. Starting close to the equilibrium point in that direction will push you away from it.
</details>
## Key takeaways

- A discrete-time dynamical system can be written as a difference equation X_{n+1} = X_n + f(X_n) or as an update equation X_{n+1} = g(X_n).
- An equilibrium point X* satisfies f(X*) = 0 (no change) or equivalently g(X*) = X* (stays at the same point).
- Linearization around an equilibrium is performed by computing the Jacobian matrix of the update function g at X*.
- The linearized system is X_{n+1} = dg(X*) X_n, and its dynamics are determined by the eigenvalues of dg(X*).
- For stability, every eigenvalue of dg(X*) must have modulus (absolute value) less than 1.
- If at least one eigenvalue has modulus greater than 1, the linear system has an expanding direction and the equilibrium is unstable.
- The stable manifold theorem guarantees that linear stability (all eigenvalues inside the unit circle) implies local nonlinear stability.
- The Hartman-Grobman theorem states that near a hyperbolic equilibrium, the nonlinear system is homeomorphic to its linearization.
- The discrete-time stability condition (eigenvalues inside the unit circle) differs from the continuous-time condition (eigenvalues in the left half-plane, real part less than 0).
- A common mistake is confusing the two stability regions; always check whether the system is discrete or continuous.
## Glossary

| Term | Definition |
|---|---|
| discrete-time dynamical system | A system where the state evolves at discrete time steps, typically described by a difference equation X_{n+1} = g(X_n). |
| difference equation | An equation that relates the value of a variable at one time step to its value at the next time step. |
| update equation | Another name for the difference equation, emphasizing the rule that computes the next state from the current state. |
| equilibrium point | A state X* such that the system remains at X* if started there; for discrete systems, g(X*) = X* or f(X*) = 0. |
| fixed point | Synonym for equilibrium point in discrete-time systems. |
| Jacobian matrix | A matrix of all first-order partial derivatives of a vector-valued function; used for linearization. |
| linearization | Approximating a nonlinear system near an equilibrium by a linear system using the Jacobian matrix. |
| eigenvalue | A scalar λ such that for a matrix A, A v = λ v for some nonzero vector v; determines the behavior of linear systems. |
| modulus | The absolute value or magnitude of a complex number, computed as sqrt(real^2 + imaginary^2). |
| unit circle | The set of complex numbers with modulus equal to 1; the boundary of the stability region for discrete-time systems. |
| contraction | A mapping that reduces distances; in linear discrete systems, all eigenvalues with modulus less than 1 cause contraction toward zero. |
| expansion | A mapping that increases distances; an eigenvalue with modulus greater than 1 leads to expansion away from the equilibrium. |
| stable manifold theorem | A theorem stating that if a linearization is a contraction (all eigenvalues inside unit circle), then the nonlinear system is locally stable near the equilibrium. |
| Hartman-Grobman theorem | A theorem stating that near a hyperbolic equilibrium (no eigenvalue on the unit circle), the nonlinear system is topologically conjugate to its linearization. |
| homeomorphism | A continuous bijection with a continuous inverse; used in the Hartman-Grobman theorem to describe the equivalence of dynamics. |
| local stability | Stability that holds only for initial conditions sufficiently close to the equilibrium. |
| instability | A property where small perturbations from equilibrium grow over time, causing the system to move away. |
| continuous-time dynamical system | A system where the state evolves continuously in time, typically described by a differential equation dx/dt = f(x). |
| left half-plane | The set of complex numbers with negative real part; the stability region for continuous-time linear systems. |
| hyperbolic equilibrium | An equilibrium where the linearization has no eigenvalues on the imaginary axis (continuous) or on the unit circle (discrete). |
## Footnotes and deeper context

1. **Common misconception: modulus vs. real part.** A frequent error is applying the continuous-time condition (real part less than 0) to discrete-time systems. For discrete systems, the condition is on the modulus, not the real part. An eigenvalue with real part negative but modulus greater than 1 would be unstable in discrete time.
2. **Jacobian of g, not f.** When linearizing a discrete system written as X_{n+1} = g(X_n), the Jacobian is taken of g, not of f. If the system is given as X_{n+1} = X_n + f(X_n), then dg = I + df, where I is the identity matrix.
3. **Strict inequality and marginal stability.** The stability condition requires all eigenvalues to have modulus strictly less than 1. If any eigenvalue has modulus exactly 1, the linear analysis is inconclusive; the system may be marginally stable, and nonlinear terms determine the outcome.
4. **Hyperbolicity requirement for Hartman-Grobman.** The Hartman-Grobman theorem applies only when the equilibrium is hyperbolic, meaning no eigenvalue lies on the unit circle. If eigenvalues are on the unit circle, the linearization does not fully capture the local dynamics.
5. **Stable manifold theorem for discrete systems.** The stable manifold theorem for discrete maps guarantees that the local stable manifold of a hyperbolic equilibrium has the same dimension as the stable eigenspace of the linearization. This is the discrete analog of the continuous-time theorem.
6. **Complex eigenvalues and oscillations.** Complex eigenvalues with modulus less than 1 produce spiral convergence toward the equilibrium, with oscillations determined by the imaginary part. The modulus still controls the contraction rate.
## Where to go next

- **Strogatz, 'Nonlinear Dynamics and Chaos' (2nd edition).** Chapters on discrete maps and linearization provide clear explanations and examples. The book is a canonical resource for both continuous and discrete dynamical systems.
- **Hirsch, Smale, and Devaney, 'Differential Equations, Dynamical Systems, and an Introduction to Chaos' (3rd edition).** Covers the stable manifold theorem and Hartman-Grobman theorem for both continuous and discrete systems with rigorous proofs. Recommended for deeper theoretical understanding.
- **MATLAB or Octave documentation for 'eig' function.** To compute eigenvalues of a Jacobian matrix numerically, use the eig function. Official documentation explains how to interpret complex eigenvalues and compute their modulus.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
