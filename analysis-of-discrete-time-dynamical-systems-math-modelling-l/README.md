# Analysis of Discrete-Time Dynamical Systems - Math Modelling - Lecture 19
> **Source:** [Analysis of Discrete-Time Dynamical Systems - Math Modelling - Lecture 19](https://www.youtube.com/watch?v=6It02qpjHQ8) by Math Modelling · 08:14 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
## Analysis of Discrete-Time Dynamical Systems - Math Modelling - Lecture 19

### Introduction to Discrete-Time Dynamical Systems

This section covers the analysis of discrete-time dynamical systems, which are systems where state variables change at discrete time steps rather than continuously. The key difference from continuous-time systems lies in the stability criterion, but the overall analytical framework remains remarkably similar.

### Representing Discrete-Time Systems

A discrete-time dynamical system is written as the change in a state variable \(X\) being equal to a function of that state variable:

\[
\Delta X = F(X)
\]


![The whiteboard displays three equations related to numerical methods, including Delta X equals F of X, Delta X equals X of n plus one minus X of...](frames/frame_01_60s.jpg)
*[01:00](https://www.youtube.com/watch?v=6It02qpjHQ8&t=60s) The whiteboard displays three equations related to numerical methods, including Delta X equals F of X, Delta X equals X of n plus one minus X of n, and X of n plus one equals X of n plus F of X of n.*


The change \(\Delta X\) represents the difference between the next state and the current state:

\[
\Delta X = X(n+1) - X(n)
\]

This expands into a difference equation that tells us what happens next given the current state:

\[
X(n+1) = X(n) + F(X(n))
\]

This form is called an **update equation** or **difference equation**. Common examples include Newton's method, gradient descent, and population models (such as yeast populations). The update equation form is the standard notation you will encounter because numerical methods like Newton's method, gradient descent, and Euler's method all use this structure.

### Defining the Update Function G

Define a function \(G(X)\) that represents the entire right-hand side of the update equation:

\[
G(X) = X + F(X)
\]

This allows us to write the system compactly as:

\[
X(n+1) = G(X(n))
\]

### Equilibrium Points


![The whiteboard displays equations for delta X, X(n+1), G(x), and the conditions for equilibrium.](frames/frame_02_160s.jpg)
*[02:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=160s) The whiteboard displays equations for delta X, X(n+1), G(x), and the conditions for equilibrium.*


An **equilibrium point** (also called a **fixed point** or **steady state**) is a value \(X^*\) where the system does not change from one step to the next. There are two equivalent interpretations:

1. **No change interpretation**: \(F(X^*) = 0\) means there is zero change from step to step.
2. **Fixed point interpretation**: \(G(X^*) = X^*\) means that if you are at the equilibrium, you stay at the equilibrium.

Both conditions are equivalent:

\[
F(X^*) = 0 \quad \text{or} \quad G(X^*) = X^*
\]

### Linearization Around Equilibrium


![Mathematical equations for linearization and equilibrium are written on a whiteboard.](frames/frame_04_220s.jpg)
*[03:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=220s) Mathematical equations for linearization and equilibrium are written on a whiteboard.*


Just as with continuous-time systems, we can linearize a discrete-time system around an equilibrium point. Linearization means computing the **Jacobian matrix** of the update function \(G\) evaluated at the equilibrium point.

The linearized system becomes:

\[
X(n+1) = DG(X^*) X(n)
\]

where \(DG(X^*)\) is the Jacobian matrix of \(G\) evaluated at \(X^*\). This is a completely linear dynamical system whose behavior determines the local dynamics of the original nonlinear system.

### Stability Criterion for Discrete-Time Systems


![This frame displays mathematical equations and definitions related to linearization and stability of systems, including expressions for ΔX, G(x)...](frames/frame_05_260s.jpg)
*[04:20](https://www.youtube.com/watch?v=6It02qpjHQ8&t=260s) This frame displays mathematical equations and definitions related to linearization and stability of systems, including expressions for ΔX, G(x), and conditions for stability.*


All dynamics of the linearized system are determined by the eigenvalues of the Jacobian matrix \(DG(X^*)\). The stability condition for discrete-time systems differs from continuous-time systems:

**Stability condition**: The equilibrium point \(X^*\) is stable if **every eigenvalue** of \(DG(X^*)\) has **modulus less than 1**.

The **modulus** (also called absolute value or magnitude) of a complex eigenvalue \(\lambda = a + bi\) is:

\[
|\lambda| = \sqrt{a^2 + b^2}
\]

This represents the Euclidean distance from the origin in the complex plane. The condition \(|\lambda| < 1\) means all eigenvalues lie inside the **unit circle** (the circle of radius 1 centered at the origin in the complex plane).

**Why this works**: When all eigenvalues have modulus less than 1, the Jacobian matrix becomes a **contraction**. After each iteration \(n\), the state contracts toward zero:

\[
\lim_{n \to \infty} \|X(n)\| = 0
\]

### Instability Criterion


![The whiteboard shows equations for linearizing a system, defining equilibrium, and conditions for stability and instability based on eigenvalues.](frames/frame_06_380s.jpg)
*[06:20](https://www.youtube.com/watch?v=6It02qpjHQ8&t=380s) The whiteboard shows equations for linearizing a system, defining equilibrium, and conditions for stability and instability based on eigenvalues.*


The equilibrium point is **unstable** if there exists **at least one eigenvalue** of \(DG(X^*)\) with **modulus greater than 1**.

**Why this works**: When even one eigenvalue has modulus greater than 1, successive powers of that eigenvalue grow larger. This creates at least one **expanding direction** in the state space. The system no longer contracts; it has an unstable direction that pushes trajectories away from the equilibrium.

### Summary Table: Stability Conditions

| System Type | Stability Criterion | Region in Complex Plane |
|-------------|-------------------|------------------------|
| Discrete-time | All eigenvalues have modulus \(< 1\) | Inside the unit circle |
| Continuous-time | All eigenvalues have real part \(< 0\) | Left half-plane |

### The Stable Manifold Theorem for Discrete Systems

The **Stable Manifold Theorem** for discrete-time systems states the same principle as for continuous-time systems: if the linearized system is stable (a contraction), then locally the fully nonlinear system is also stable. The "local" qualification comes from the Taylor expansion used in linearization: if you start close enough to the equilibrium, the nonlinear terms are small enough that the linear approximation dominates.

### The Hartman-Grobman Theorem for Discrete Systems

The **Hartman-Grobman Theorem** also applies to discrete-time systems. It states that near an equilibrium point, the nonlinear difference equation looks more and more like the linearized system as you zoom in closer. The nonlinear system may be bent or deformed, but it has the same basic topological structure. Specifically, it is **homeomorphic** (topologically equivalent) to the linearized discrete-time system.

### Key Difference to Remember


![This whiteboard displays mathematical equations for linearization, including definitions for delta X, G(x), equilibrium conditions, and stability...](frames/frame_08_460s.jpg)
*[07:40](https://www.youtube.com/watch?v=6It02qpjHQ8&t=460s) This whiteboard displays mathematical equations for linearization, including definitions for delta X, G(x), equilibrium conditions, and stability criteria based on the modulus of eigenvalues.*


The most common source of confusion is the different stability regions:

- **Discrete-time**: eigenvalues must be inside the **unit circle** (modulus \(< 1\))
- **Continuous-time**: eigenvalues must be in the **left half-plane** (real part \(< 0\))

If you remember this distinction, everything else follows the same analytical process as continuous-time systems.

### Check Your Understanding

1. **Question**: A discrete-time system has Jacobian matrix \(DG(X^*)\) with eigenvalues \(\lambda_1 = 0.5\), \(\lambda_2 = -0.8\), and \(\lambda_3 = 1.2\). Is the equilibrium stable or unstable? Why?

<details><summary>Answer</summary>
The equilibrium is unstable because eigenvalue \(\lambda_3 = 1.2\) has modulus \(1.2 > 1\). Even though two eigenvalues satisfy the stability condition, the presence of any eigenvalue with modulus greater than 1 creates an unstable direction.
</details>

2. **Question**: What is the difference between the stability condition for discrete-time systems and continuous-time systems?

<details><summary>Answer</summary>
For discrete-time systems, stability requires all eigenvalues to have modulus less than 1 (inside the unit circle in the complex plane). For continuous-time systems, stability requires all eigenvalues to have real part less than 0 (in the left half-plane of the complex plane).
</details>

3. **Question**: Explain why the conditions \(F(X^*) = 0\) and \(G(X^*) = X^*\) are equivalent for an equilibrium point.

<details><summary>Answer</summary>
Since \(G(X) = X + F(X)\), evaluating at \(X^*\) gives \(G(X^*) = X^* + F(X^*)\). If \(F(X^*) = 0\), then \(G(X^*) = X^*\). Conversely, if \(G(X^*) = X^*\), then \(X^* + F(X^*) = X^*\), which implies \(F(X^*) = 0\). Both conditions describe the same situation: no change from one time step to the next.
</details>

4. **Question**: A discrete-time system has Jacobian eigenvalues \(\lambda_1 = 0.9 + 0.3i\) and \(\lambda_2 = 0.9 - 0.3i\). Is the equilibrium stable?

<details><summary>Answer</summary>
Yes, the equilibrium is stable. Compute the modulus: \(|\lambda| = \sqrt{0.9^2 + 0.3^2} = \sqrt{0.81 + 0.09} = \sqrt{0.90} \approx 0.949\). Since \(0.949 < 1\), both eigenvalues lie inside the unit circle, satisfying the stability condition.
</details>
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
