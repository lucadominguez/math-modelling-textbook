# Discrete-Time Dynamical Systems: Stability via Eigenvalue Modulus Condition
> **Source:** [Analysis of Discrete-Time Dynamical Systems - Math Modelling - Lecture 19](https://www.youtube.com/watch?v=6It02qpjHQ8) by Math Modelling · 08:14 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students in mathematical modeling or dynamical systems who have studied continuous-time systems and want to understand the analogous theory for discrete-time systems.
## Learning objectives

After working through this document you can:

1. Define discrete-time dynamical systems using difference equations and the update function G(x).
2. Identify equilibrium conditions for discrete systems: F(x*) = 0 or G(x*) = x*.
3. Linearize a discrete-time system around an equilibrium by computing the Jacobian matrix DG(x*).
4. Determine stability of an equilibrium by checking if every eigenvalue of DG(x*) has modulus less than 1.
5. Determine instability when at least one eigenvalue has modulus greater than 1.
6. Apply the stable manifold theorem to conclude local stability or instability of the nonlinear system from the linearized system.
7. Contrast the stability criterion for discrete systems (unit circle) with that for continuous systems (left half-plane).
8. Explain the Hartman-Grobman theorem for discrete systems and its implication that the nonlinear system is locally homeomorphic to the linearized system.
## Prerequisites

- Basic calculus and linear algebra, including eigenvalues and Jacobian matrices.
- Familiarity with continuous-time dynamical systems, fixed points, and stability concepts.
## Introduction to Discrete-Time Dynamical Systems and Difference Equations

This section introduces discrete-time dynamical systems and the difference equations that describe them. You will learn how to express the change in a state variable from one time step to the next, and how this leads to an iterative formula for predicting future states.

### From Continuous to Discrete Time

In previous lessons you studied continuous-time dynamical systems, where time flows continuously and the system is described by differential equations. Every concept from continuous-time theory has a direct analog in discrete-time systems. This section covers the discrete-time formulation so that you can apply the same stability analysis (via eigenvalue modulus) to systems that evolve in distinct steps.

### Defining a Discrete-Time Dynamical System

A **discrete-time dynamical system** is a system whose state changes at discrete time steps (e.g., \(n = 0, 1, 2, \dots\)). The state is represented by a **state variable** \(X\). The change in the state variable from one step to the next is written as:

\[
\Delta X = F(X)
\]

Here, \(\Delta X\) is the difference between the next state and the current state. The function \(F\) describes how the current state influences that change.

### From Change to a Difference Equation

Because the system evolves in discrete steps, we can expand \(\Delta X\) as:

\[
\Delta X = X(n+1) - X(n)
\]

where \(X(n)\) is the state at time step \(n\) and \(X(n+1)\) is the state at the next step. Substituting this into the definition gives:

\[
X(n+1) - X(n) = F(X(n))
\]

Rearranging yields the **difference equation** (also called an **iterative map**):

\[
X(n+1) = X(n) + F(X(n))
\]

This equation tells you: if you know the current state \(X(n)\), you can compute the next state \(X(n+1)\) by adding the change \(F(X(n))\).


![The whiteboard displays mathematical equations for Delta X and an iterative formula for X(n+1).](frames/frame_01_60s.jpg)
*[01:00](https://www.youtube.com/watch?v=6It02qpjHQ8&t=60s) The whiteboard displays mathematical equations for Delta X and an iterative formula for X(n+1).*


The whiteboard at this timestamp shows the three equations above:

```
ΔX = F(x)
ΔX = X(n+1) - X(n)
X(n+1) = X(n) + F(X(n))
```

### Examples of Discrete-Time Systems

Many real-world processes and algorithms are naturally discrete-time. The video mentions:

- **Newton’s method** for finding roots of a function: each iteration updates an estimate using the derivative.
- **Gradient descent** for optimization: each step moves the parameters in the direction of the negative gradient.
- **Yeast population models**: population size at one time step determines the size at the next step (e.g., logistic map).

All of these can be written in the form \(X(n+1) = X(n) + F(X(n))\).

### Introducing the Map Function \(G(X)\)

Often it is convenient to define a single function that directly gives the next state:

\[
G(X) = X + F(X)
\]

Then the difference equation becomes simply:

\[
X(n+1) = G(X(n))
\]

This is the **discrete-time map**. The function \(G\) takes the current state and returns the next state. This form is directly analogous to the flow map in continuous-time systems, and it will be used later to analyze stability by examining the eigenvalues of the Jacobian of \(G\).

### Key Concepts Summary

| Term | Definition |
|------|------------|
| Discrete-time dynamical system | A system where the state changes at distinct time steps. |
| State variable \(X\) | A quantity that describes the system at a given time. |
| Change \(\Delta X\) | The difference between the next state and the current state. |
| Difference equation | An equation of the form \(X(n+1) = X(n) + F(X(n))\) that predicts the next state. |
| Map function \(G(X)\) | \(G(X) = X + F(X)\), so that \(X(n+1) = G(X(n))\). |

### Check your understanding

1. What is the relationship between the change \(\Delta X\) and the function \(F(X)\) in a discrete-time dynamical system?

<details><summary>Answer</summary>
The change \(\Delta X\) is defined to be equal to \(F(X)\). That is, \(\Delta X = F(X)\).
</details>

2. Write the difference equation that expresses \(X(n+1)\) in terms of \(X(n)\) and \(F(X(n))\).

<details><summary>Answer</summary>
\(X(n+1) = X(n) + F(X(n))\)
</details>

3. How is the map function \(G(X)\) defined, and why is it useful?

<details><summary>Answer</summary>
\(G(X) = X + F(X)\). It is useful because it directly gives the next state: \(X(n+1) = G(X(n))\), simplifying the analysis of the system’s dynamics.
</details>

4. Name two examples of discrete-time systems mentioned in the video.

<details><summary>Answer</summary>
Newton’s method and gradient descent. (Also yeast population models.)
</details>
## Equilibrium Conditions and Notation

In discrete-time dynamical systems, we study how a state evolves step by step. The core concept is an **equilibrium point** (also called a fixed point or steady state), where the system does not change from one time step to the next.

### Defining the System

We represent a discrete-time system using a **difference equation**:

\[
X_{n+1} = G(X_n)
\]

Here:
- \(X_n\) is the state at time step \(n\)
- \(X_{n+1}\) is the state at the next time step
- \(G\) is the **update function** that maps the current state to the next state

Alternatively, we can write the change in state as:

\[
\Delta X = X_{n+1} - X_n = F(X_n)
\]

where \(F(X_n) = G(X_n) - X_n\) is the **increment function**.

### Equilibrium Condition

An **equilibrium point** \(X^*\) satisfies the condition that the system remains at that point forever. This gives two equivalent definitions:

1. **Using the increment function**: \(F(X^*) = 0\)  
   (No change from one step to the next)

2. **Using the update function**: \(G(X^*) = X^*\)  
   (The next state equals the current state)

Both statements mean the same thing: at an equilibrium, the state does not move.

### Visualizing the Relationship

The whiteboard shows these equations clearly:


![The whiteboard displays equations for delta X, X(n+1), G(x), and the conditions for equilibrium.](frames/frame_02_160s.jpg)
*[02:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=160s) The whiteboard displays equations for delta X, X(n+1), G(x), and the conditions for equilibrium.*


```
ΔX = F(x)
ΔX = X(n+1) - X(n)
X(n+1) = X(n) + F(X(n))
G(x) = X + F(x)
Suppose X* equilibrium: F(X*) = 0
or G(X*) = X*
```

The key insight: **F(X*) = 0** is equivalent to **G(X*) = X***. If the increment is zero, the next state equals the current state.

### Why This Matters

This notation is standard because many important algorithms fit this form:
- **Newton's method** for finding roots
- **Gradient descent** for optimization
- **Euler's method** for numerical integration of differential equations

All of these can be written as \(X_{n+1} = G(X_n)\), making equilibrium analysis directly applicable.

### Linearization Around Equilibrium

Just as with continuous systems, we can **linearize** a discrete-time system near an equilibrium point. This involves computing the **Jacobian matrix** of \(G\) evaluated at \(X^*\):

\[
J = \frac{\partial G}{\partial X}\bigg|_{X=X^*}
\]

The eigenvalues of this Jacobian determine the **stability** of the equilibrium:
- If all eigenvalues have magnitude less than 1, the equilibrium is **stable** (attracting)
- If any eigenvalue has magnitude greater than 1, the equilibrium is **unstable** (repelling)
- If eigenvalues have magnitude exactly 1, the stability is **marginal** (requires further analysis)

### Summary Table

| Concept | Continuous System | Discrete System |
|---------|------------------|-----------------|
| State equation | \(\dot{x} = f(x)\) | \(X_{n+1} = G(X_n)\) |
| Equilibrium condition | \(f(x^*) = 0\) | \(G(X^*) = X^*\) or \(F(X^*) = 0\) |
| Linearization tool | Jacobian of \(f\) | Jacobian of \(G\) |
| Stability criterion | Real parts of eigenvalues < 0 | Magnitudes of eigenvalues < 1 |

---

### Check Your Understanding

1. **What are the two equivalent conditions for a point \(X^*\) to be an equilibrium of the discrete system \(X_{n+1} = G(X_n)\)?**

<details><summary>Answer</summary>
The two equivalent conditions are:
- \(F(X^*) = 0\) (the increment is zero)
- \(G(X^*) = X^*\) (the update function returns the same point)

Both mean the state does not change from one step to the next.
</details>

2. **If a discrete system has update function \(G(x) = 2x(1-x)\), find all equilibrium points.**

<details><summary>Answer</summary>
Set \(G(x^*) = x^*\):
\(2x^*(1-x^*) = x^*\)
\(2x^* - 2x^{*2} = x^*\)
\(x^* - 2x^{*2} = 0\)
\(x^*(1 - 2x^*) = 0\)

So the equilibria are \(x^* = 0\) and \(x^* = 0.5\).
</details>

3. **Why is the condition \(F(X^*) = 0\) equivalent to \(G(X^*) = X^*\)?**

<details><summary>Answer</summary>
Because \(F(X) = G(X) - X\). If \(F(X^*) = 0\), then \(G(X^*) - X^* = 0\), so \(G(X^*) = X^*\). Conversely, if \(G(X^*) = X^*\), then \(F(X^*) = X^* - X^* = 0\). They are algebraically identical statements.
</details>

4. **What is the stability criterion for a discrete-time equilibrium, and how does it differ from the continuous-time criterion?**

<details><summary>Answer</summary>
For discrete-time systems, an equilibrium is stable if all eigenvalues of the Jacobian of \(G\) have magnitude less than 1. For continuous-time systems, stability requires all eigenvalues of the Jacobian of \(f\) have negative real parts. The difference arises because discrete updates multiply by the Jacobian each step, while continuous dynamics involve exponential growth/decay.
</details>
## Linearization and Stability Condition (Modulus Less Than 1)


![Mathematical equations for linearization, including definitions for \(\Delta X\), \(G(x)\), and the linearized form \(X(n+1)=DG(x_*)X(n)\).](frames/frame_04_220s.jpg)
*[03:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=220s) Mathematical equations for linearization, including definitions for \(\Delta X\), \(G(x)\), and the linearized form \(X(n+1)=DG(x_*)X(n)\).*


### Linearizing the System

To analyze stability near an equilibrium point, we must first linearize the nonlinear system. Linearization means computing the Jacobian matrix of the function \(G(x)\) at the equilibrium point \(x_*\).

Recall the original system definitions from the whiteboard:

- \(\Delta X = F(x)\) represents the change in state
- \(\Delta X = X(n+1) - X(n)\) is the discrete difference
- \(X(n+1) = X(n) + F(X(n))\) is the update equation
- \(G(x) = X + F(x)\) is the function that maps current state to next state

An equilibrium point \(x_*\) satisfies either:
- \(F(x_*) = 0\) (no change in state)
- or equivalently \(G(x_*) = x_*\) (state maps to itself)

To linearize, we compute the Jacobian matrix \(DG(x_*)\) of \(G\) evaluated at the equilibrium. This gives us the linearized dynamical system:

\[
X(n+1) = DG(x_*) X(n)
\]

This is now a completely linear dynamical system. The Jacobian matrix \(DG(x_*)\) is a matrix of partial derivatives (added context: each entry \((i,j)\) is \(\frac{\partial G_i}{\partial x_j}\) evaluated at \(x_*\)).


![A whiteboard shows mathematical equations for linearization and stability, including definitions for ΔX, G(x), and conditions for equilibrium and...](frames/frame_05_260s.jpg)
*[04:20](https://www.youtube.com/watch?v=6It02qpjHQ8&t=260s) A whiteboard shows mathematical equations for linearization and stability, including definitions for ΔX, G(x), and conditions for equilibrium and stability.*


### Stability Condition: Eigenvalue Modulus Less Than 1

For this linearized system, all dynamics are determined by the eigenvalues of the matrix \(DG(x_*)\). This is analogous to results from continuous-time systems.

**The stability condition is:** The equilibrium point \(x_*\) is stable if every eigenvalue of \(DG(x_*)\) has modulus less than 1.

The term "modulus" refers to the absolute value of a complex number. Some eigenvalues may be complex conjugates of each other. For a complex eigenvalue \(\lambda = a + bi\) (where \(a\) is the real part and \(b\) is the imaginary part), the modulus is:

\[
|\lambda| = \sqrt{a^2 + b^2}
\]

This is the Euclidean norm of the complex number. The condition \(|\lambda| < 1\) means every eigenvalue lies inside the unit circle in the complex plane.

### Why This Condition Works

The Jacobian matrix \(DG(x_*)\) becomes what is called a contraction. A contraction means that after each iteration (each time step \(n\)), the state is contracting toward the equilibrium point. When all eigenvalues have modulus less than 1, repeated multiplication by the Jacobian matrix shrinks any initial perturbation, causing the system to converge to the equilibrium.

### Summary Table

| Concept | Definition | Condition for Stability |
|---------|------------|------------------------|
| Linearization | Computing Jacobian \(DG(x_*)\) at equilibrium | Required for local analysis |
| Eigenvalue modulus | \(\sqrt{(\text{real part})^2 + (\text{imaginary part})^2}\) | Must be less than 1 |
| Contraction | State shrinks toward equilibrium each iteration | Guaranteed when all eigenvalues have modulus < 1 |
| Unit circle | Circle of radius 1 in complex plane | All eigenvalues must lie inside |

### Check Your Understanding

1. What is the mathematical condition for stability of a discrete-time dynamical system at an equilibrium point?

<details><summary>Answer</summary>
Every eigenvalue of the Jacobian matrix \(DG(x_*)\) must have modulus less than 1. That is, \(|\lambda| < 1\) for all eigenvalues \(\lambda\).
</details>

2. How do you compute the modulus of a complex eigenvalue \(\lambda = 3 + 4i\)?

<details><summary>Answer</summary>
The modulus is \(\sqrt{3^2 + 4^2} = \sqrt{9 + 16} = \sqrt{25} = 5\). Since 5 is greater than 1, this eigenvalue would indicate instability.
</details>

3. Why does the condition \(|\lambda| < 1\) ensure stability in the linearized system?

<details><summary>Answer</summary>
When all eigenvalues have modulus less than 1, the Jacobian matrix acts as a contraction. Each iteration multiplies the state by the Jacobian, and because all eigenvalues are inside the unit circle, repeated multiplication shrinks any perturbation toward zero, causing convergence to the equilibrium.
</details>

4. What is the relationship between the functions \(F(x)\) and \(G(x)\) in the linearization process?

<details><summary>Answer</summary>
\(G(x) = x + F(x)\). The function \(F\) represents the change in state, while \(G\) maps the current state to the next state. At equilibrium, both \(F(x_*) = 0\) and \(G(x_*) = x_*\) hold. The Jacobian of \(G\) is used for linearization because the update equation is \(X(n+1) = G(X(n))\).
</details>
## Instability Condition and the Stable Manifold Theorem

In the previous part of the video you learned that when all eigenvalues of the linearized matrix have modulus less than 1, the discrete-time system is locally stable. Now we examine the opposite case: instability. The same linearization approach tells you when small perturbations grow instead of shrink.

### Linearization Recap

For a discrete-time dynamical system defined by

\[
X(n+1) = G(X(n))
\]

an equilibrium point \(X^*\) satisfies \(G(X^*) = X^*\) (or equivalently \(F(X^*) = 0\) if you write the system as \(\Delta X = F(X)\)). To study behavior near \(X^*\), you linearize:

\[
X(n+1) = DG(X^*) \, X(n)
\]

where \(DG(X^*)\) is the Jacobian matrix of \(G\) evaluated at \(X^*\). The eigenvalues of this matrix determine the local dynamics.


![The whiteboard displays equations for linearization, equilibrium, and conditions for stability and instability based on eigenvalues.](frames/frame_06_380s.jpg)
*[06:20](https://www.youtube.com/watch?v=6It02qpjHQ8&t=380s) The whiteboard displays equations for linearization, equilibrium, and conditions for stability and instability based on eigenvalues.*


The whiteboard shows the full set of equations:

```
ΔX = F(x)
ΔX = X(n+1) - X(n)
↳ X(n+1) = X(n) + F(x(n))
G(x) = X + F(x)
Suppose X* equilibrium: F(x*) = 0
or G(x*) = X*
Linearize:
X(n+1) = DG(x*) X(n)
Stable: every eig. of DG(x*)
has modulus < 1
: ∃ at least one eig. of
DG(x*) with modulus > 1
```

### Stable Manifold Theorem for Discrete Time

The stable manifold theorem, which you may have seen for continuous dynamics, applies equally to discrete-time systems. It states:

> If the linearized system is a contraction (all eigenvalues have modulus less than 1), then the fully nonlinear system is locally a contraction near the equilibrium.

The word “local” comes from the Taylor expansion used in linearization: the approximation is accurate only close to \(X^*\). So if you start sufficiently near \(X^*\), the nonlinear dynamics will converge to \(X^*\) when the linearized Jacobian has all eigenvalues with modulus less than 1.

### Instability Condition

Now consider the opposite scenario. The system is **unstable** if there exists **at least one** eigenvalue of \(DG(X^*)\) with modulus greater than 1. Even a single expanding direction is enough to cause instability.

Why does one eigenvalue with modulus > 1 cause instability? When you take successive powers of that eigenvalue (as you do when iterating the linearized map), its magnitude grows without bound. That means in at least one dimension the map is expanding. Any initial perturbation along that eigenvector will be amplified, driving the trajectory away from the equilibrium.

The table below summarizes the two conditions:

| Condition | Eigenvalue Moduli | Local Behavior |
|-----------|-------------------|----------------|
| Stable    | All eigenvalues have modulus < 1 | Contraction: nearby points converge to equilibrium |
| Unstable  | At least one eigenvalue has modulus > 1 | Expansion: nearby points diverge from equilibrium |

Note: If an eigenvalue has modulus exactly equal to 1, the linearization is inconclusive; higher-order terms determine stability. This case is not covered in this section.

### Visualizing the Unit Circle

The unit circle in the complex plane is the boundary between stability and instability. Eigenvalues inside the circle (modulus < 1) are contracting; eigenvalues outside (modulus > 1) are expanding.

```
          Im
          ^
          |   (outside: unstable)
          |    x
          |   / \
          |  /   \
          | /     \
          |/       \
   <------+---------> Re
          |\       /
          | \     /
          |  \   /
          |   \ /
          |    x
          |   (inside: stable)
          v
```

### Check Your Understanding

1. **Question:** What is the instability condition for a discrete-time dynamical system near an equilibrium point \(X^*\)?

<details><summary>Answer</summary>
The system is unstable if the Jacobian matrix \(DG(X^*)\) has at least one eigenvalue with modulus greater than 1.
</details>

2. **Question:** Why does a single eigenvalue with modulus > 1 cause instability, even if all other eigenvalues are stable?

<details><summary>Answer</summary>
When you iterate the linearized map, that eigenvalue is raised to successive powers. Its magnitude grows without bound, so any perturbation along its eigenvector expands. This expansion dominates the dynamics in that direction, driving the trajectory away from the equilibrium.
</details>

3. **Question:** How does the stable manifold theorem for discrete-time dynamics relate to the linearized system?

<details><summary>Answer</summary>
The theorem states that if the linearized system is a contraction (all eigenvalues have modulus < 1), then the fully nonlinear system is locally a contraction near the equilibrium. “Locally” means the result holds only for initial conditions sufficiently close to \(X^*\), because the linearization is a Taylor approximation valid only in a small neighborhood.
</details>

4. **Question:** In the whiteboard screenshot, what two conditions are listed for the eigenvalues of \(DG(x^*)\)?

<details><summary>Answer</summary>
Stable: every eigenvalue has modulus < 1. Unstable: there exists at least one eigenvalue with modulus > 1.
</details>
## Comparison with Continuous Systems and the Hartman-Grobman Theorem

This section connects the stability analysis of discrete-time dynamical systems to the more familiar continuous-time case. It introduces the Hartman-Grobman theorem and highlights the single critical difference between the two settings.

### Stability: Carrying Instability from Linear to Nonlinear Systems

When a linearized system has an unstable direction (an eigenvector associated with an eigenvalue whose modulus is greater than 1), the nonlinear system also exhibits instability in that region. If you start a trajectory close to an equilibrium point in an unstable direction, the dynamics push that trajectory away from the equilibrium.


![This frame shows mathematical equations for linearizing a system, defining stable and unstable conditions based on the modulus of eigenvalues.](frames/frame_07_400s.jpg)
*[06:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=400s) This frame shows mathematical equations for linearizing a system, defining stable and unstable conditions based on the modulus of eigenvalues.*


The process for determining stability is the same as for continuous-time systems. In both cases, the analysis reduces to examining the eigenvalues of a matrix. Specifically, you linearize the system around an equilibrium point to obtain a Jacobian matrix. The stability of the linearized system determines the stability of the original nonlinear system near that equilibrium.

The stable manifold theorem supports this claim. If the linear system is stable (all trajectories converge to the equilibrium), then the nonlinear system is stable near that equilibrium as well.

### The Critical Difference: The Stability Region

The single critical difference between discrete and continuous systems is the location of the stability region in the complex plane.

| System Type | Stability Condition | Region in Complex Plane |
|-------------|---------------------|-------------------------|
| Continuous-time | All eigenvalues have real part less than 0 (Re(lambda) < 0) | Left half of the complex plane |
| Discrete-time | All eigenvalues have a modulus less than 1 (|lambda| < 1) | Inside the unit circle centered at the origin |


![The whiteboard shows equations for linearizing a system, defining equilibrium, and conditions for stability and instability based on the modulus...](frames/frame_08_460s.jpg)
*[07:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=460s) The whiteboard shows equations for linearizing a system, defining equilibrium, and conditions for stability and instability based on the modulus of eigenvalues.*


For discrete-time systems, every eigenvalue of the linearized Jacobian matrix DG(X*) must have a modulus (absolute value) less than 1 for stability. If at least one eigenvalue has a modulus greater than 1, the system is unstable.

For continuous-time systems, every eigenvalue must have a real part less than 0. This places them in the left half of the complex plane.

This difference in stability region is the most common source of confusion when moving between continuous and discrete-time systems. If you remember this distinction, the rest of the analysis follows the same structure.

### The Hartman-Grobman Theorem

The Hartman-Grobman theorem applies to discrete-time systems in the same way it applies to continuous-time systems. The theorem states that near a hyperbolic equilibrium point (one where no eigenvalue has a modulus exactly equal to 1), the nonlinear system is topologically conjugate to its linearization.

Topological conjugacy means there exists a homeomorphism (a continuous, invertible mapping with a continuous inverse) that transforms trajectories of the nonlinear system into trajectories of the linearized system. As you zoom in closer and closer to the equilibrium point of a nonlinear difference equation, the system looks more and more like the linearized system. The nonlinear system may be slightly bent or deformed compared to the linear version, but it has the same basic structure. The mapping between the two systems is homeomorphic.

### Check your understanding

1.  For a discrete-time dynamical system, what condition must the eigenvalues of the linearized Jacobian matrix satisfy for the system to be stable at an equilibrium point?

<details>
<summary>Answer</summary>
Every eigenvalue must have a modulus (absolute value) less than 1.
</details>

2.  What is the key difference between the stability condition for discrete-time systems and the stability condition for continuous-time systems?

<details>
<summary>Answer</summary>
Discrete-time systems require eigenvalues inside the unit circle (modulus less than 1) in the complex plane. Continuous-time systems require eigenvalues in the left half-plane (real part less than 0).
</details>

3.  According to the Hartman-Grobman theorem, what is the relationship between a nonlinear discrete-time system and its linearization near a hyperbolic equilibrium point?

<details>
<summary>Answer</summary>
The nonlinear system is topologically conjugate to its linearization. There exists a homeomorphism that maps trajectories of the nonlinear system to trajectories of the linearized system. The nonlinear system has the same basic structure but may be slightly bent or deformed.
</details>

4.  If a linearized discrete-time system is stable, what does the stable manifold theorem tell you about the original nonlinear system?

<details>
<summary>Answer</summary>
The stable manifold theorem states that stability of the linear system carries over to stability of the nonlinear system near the equilibrium point. If the linear system is stable, the nonlinear system is also stable near that equilibrium.
</details>
## Key takeaways

- Discrete-time dynamical systems are modeled by difference equations of the form X(n+1) = X(n) + F(X(n)), where the update function G(x) = x + F(x) defines the next state from the current state.
- An equilibrium point x* satisfies F(x*) = 0, meaning no change occurs between steps, which is equivalent to G(x*) = x*, meaning the system stays at that point.
- To analyze stability near an equilibrium, linearize the system by computing the Jacobian matrix DG(x*) of the update function G at the equilibrium.
- The linearized system is X(n+1) = DG(x*) X(n), and its behavior is determined entirely by the eigenvalues of DG(x*).
- An equilibrium is stable if every eigenvalue of DG(x*) has modulus (absolute value) less than 1, because the linear system is a contraction that shrinks perturbations to zero.
- An equilibrium is unstable if at least one eigenvalue of DG(x*) has modulus greater than 1, because that eigenvalue creates an expanding direction that pushes perturbations away.
- The stable manifold theorem guarantees that stability or instability of the linearized system carries over to local stability or instability of the original nonlinear system.
- The Hartman-Grobman theorem for discrete systems states that near an equilibrium, the nonlinear system is homeomorphic to its linearization, so linear analysis accurately describes local behavior.
- The key difference from continuous systems is the stability criterion: discrete systems require eigenvalues inside the unit circle (modulus less than 1), while continuous systems require eigenvalues in the left half-plane (real part less than 0).
- Examples of discrete-time systems include Newton's method, gradient descent, and yeast population models, all of which can be analyzed using the same eigenvalue-based stability framework.
## Glossary

| Term | Definition |
|---|---|
| discrete-time dynamical system | A system where the state evolves in distinct steps, modeled by a difference equation X(n+1) = G(X(n)), where n is an integer time index. |
| difference equation | An equation that relates the value of a variable at one time step to its value at the next time step, such as X(n+1) = X(n) + F(X(n)). |
| update function G(x) | A function that maps the current state x to the next state, defined as G(x) = x + F(x) for a system with change function F. |
| equilibrium point | A state x* where the system does not change over time, satisfying F(x*) = 0 or equivalently G(x*) = x*. |
| linearization | The process of approximating a nonlinear system near an equilibrium by a linear system, typically using a Taylor expansion and computing the Jacobian matrix. |
| Jacobian matrix | A matrix of all first-order partial derivatives of a vector-valued function. For the update function G, DG(x*) is the Jacobian evaluated at the equilibrium x*. |
| eigenvalue | A scalar lambda such that for a matrix A, there exists a nonzero vector v satisfying A v = lambda v. Eigenvalues determine the behavior of linear systems. |
| modulus | The absolute value or magnitude of a complex number, computed as the square root of the sum of the squares of its real and imaginary parts. |
| unit circle | The set of all complex numbers with modulus equal to 1. For discrete system stability, all eigenvalues must lie inside this circle (modulus less than 1). |
| contraction | A linear map that reduces distances between points with each iteration, occurring when all eigenvalues have modulus less than 1. |
| stable manifold theorem | A theorem stating that if the linearization of a system at an equilibrium is a contraction (all eigenvalues inside the unit circle), then the nonlinear system is locally stable near that equilibrium. |
| Hartman-Grobman theorem | A theorem stating that near a hyperbolic equilibrium (no eigenvalues on the unit circle), the nonlinear system is topologically conjugate to its linearization, meaning local dynamics are equivalent up to a continuous deformation. |
| homeomorphic | A relationship between two spaces where there exists a continuous bijection with a continuous inverse, indicating they have the same topological structure. |
| left half-plane | The set of complex numbers with negative real part. This is the stability region for continuous-time systems, contrasting with the unit circle for discrete systems. |
| Newton's method | An iterative root-finding algorithm that can be expressed as a discrete-time dynamical system X(n+1) = X(n) - f(X(n))/f'(X(n)). |
| gradient descent | An optimization algorithm that iteratively moves in the direction of the negative gradient, modeled as a discrete-time system X(n+1) = X(n) - alpha * gradient(f)(X(n)). |
| Taylor expansion | A mathematical approximation of a function near a point using its derivatives, used in linearization to approximate G(x) near x* as G(x*) + DG(x*)(x - x*). |
| complex conjugate | A pair of complex numbers a + bi and a - bi. Eigenvalues of real matrices often appear as complex conjugate pairs. |
| Euclidean norm | The standard distance metric in Euclidean space, computed as the square root of the sum of squared components. For a complex number, it is the same as the modulus. |
| hyperbolic equilibrium | An equilibrium point where the Jacobian matrix has no eigenvalues on the unit circle (for discrete systems) or on the imaginary axis (for continuous systems). |
## Footnotes and deeper context

1. **Stable manifold theorem scope.** The stable manifold theorem for discrete systems applies only to hyperbolic equilibria, where no eigenvalue of DG(x*) has modulus exactly 1. If any eigenvalue lies on the unit circle, linearization alone cannot determine stability, and higher-order analysis is required.
2. **Hartman-Grobman theorem requirement.** The Hartman-Grobman theorem for discrete systems also requires the equilibrium to be hyperbolic. If eigenvalues have modulus exactly 1, the linear and nonlinear systems may not be topologically conjugate, and local behavior can differ significantly.
3. **Modulus versus magnitude.** The term modulus is used interchangeably with absolute value or magnitude for complex numbers. For a real eigenvalue, the modulus is simply its absolute value. For a complex eigenvalue a + bi, the modulus is sqrt(a^2 + b^2).
4. **Common misconception about instability.** A common mistake is to think that if all eigenvalues have modulus less than or equal to 1, the system is stable. However, if any eigenvalue has modulus exactly 1, the system is not hyperbolic, and stability cannot be determined from linearization alone. The system may be stable, unstable, or exhibit more complex behavior like oscillations.
5. **Continuous versus discrete stability regions.** The stability region for continuous systems is the open left half-plane (real part less than 0), while for discrete systems it is the open unit disk (modulus less than 1). These are fundamentally different geometric regions, and confusing them is a common error.
6. **Jacobian of G versus Jacobian of F.** When linearizing a discrete system, the Jacobian is computed for the update function G(x) = x + F(x), not for F alone. This means DG(x*) = I + DF(x*), where I is the identity matrix. The eigenvalues of DG(x*) determine stability, not those of DF(x*).
## Where to go next

- **Read Strogatz's Nonlinear Dynamics and Chaos, Chapter 10.** This textbook provides a clear, intuitive introduction to discrete-time dynamical systems, including logistic maps, bifurcations, and stability analysis. It is a canonical resource for understanding the concepts in this course.
- **Explore the MATLAB or Python Control Systems Library documentation.** These tools allow you to compute eigenvalues of Jacobian matrices and simulate discrete-time systems numerically. The documentation for 'damp' in MATLAB or 'control.damp' in Python shows how to compute eigenvalues and check stability conditions.
- **Review the Hartman-Grobman theorem in Hirsch, Smale, and Devaney's Differential Equations, Dynamical Systems, and an Introduction to Chaos.** This book offers a rigorous treatment of the theorem for both continuous and discrete systems, including proofs and examples. It is a standard reference for advanced study.
- **Practice with the logistic map X(n+1) = r X(n) (1 - X(n)).** This classic discrete system demonstrates stability, bifurcations, and chaos. Compute its fixed points, linearize, and check the eigenvalue condition for different values of r to see how stability changes.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
