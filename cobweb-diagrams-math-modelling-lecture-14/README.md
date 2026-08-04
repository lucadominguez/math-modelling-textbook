# Cobweb Diagrams for Discrete Time Dynamical Systems: A Graphical Method for Analyzing One Dimensional Difference Equations
> **Source:** [Cobweb Diagrams - Math Modelling - Lecture 14](https://www.youtube.com/watch?v=1hCX5Gbeo0E) by Math Modelling · 31:04 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students who have been introduced to discrete time dynamical systems and want to learn a graphical method for analyzing one dimensional difference equations when explicit solutions are not available.
## Learning objectives

After working through this document you can:

1. Define a one dimensional difference equation and its components using a yeast population growth model.
2. Calculate explicit solutions for linear difference equations with constant growth rates.
3. Formulate a logistic growth model for a population with a carrying capacity.
4. Construct a cobweb diagram by plotting the function F of X and the line Y equal to X.
5. Identify equilibrium points from the intersections of F of X and Y equal to X on a cobweb diagram.
6. Interpret the dynamics of a system by tracing iterations on a cobweb diagram for monotonic convergence.
7. Analyze the effect of increasing the growth rate parameter R on the behavior of the cobweb diagram, including overshooting and oscillations.
8. Recognize chaotic behavior in a cobweb diagram when the growth rate is very large.
## Prerequisites

- Familiarity with discrete time dynamical systems or difference equations as introduced in a previous lecture.
- Basic understanding of exponential growth and logarithms.
- Knowledge of equilibrium points and phase line diagrams for continuous time systems.
## Introduction to One Dimensional Difference Equations and a Simple Yeast Model

In this section you will learn about one dimensional difference equations, also called discrete time dynamical systems. You will model a growing yeast population, derive the difference equation, solve it, and answer questions about the population at specific times. This method forms the foundation for the graphical cobweb diagrams you will study later.

### What Is a One Dimensional Difference Equation?

A **difference equation** describes how a quantity changes from one discrete time step to the next. When the state of the system is described by a single variable, it is a **one dimensional** difference equation. For example, the population of yeast at hour `n` is a single number `x_n`. The equation relates the future value `x_{n+1}` to the current value `x_n`.

This is analogous to the phase line diagrams you may have seen for continuous dynamical systems, but here time advances in discrete steps (e.g., every hour). There is no assumption about what happens between steps; you only observe the system at integer times.

### Modeling a Yeast Population

Suppose you have a colony of yeast that grows at a constant rate of 10% per hour. You start counting at time zero, and the initial population is 100,000 (units of individuals). You check the population every hour.

**Relative growth rate** is defined as the change in population divided by the current population:

\[
\text{relative growth rate} = \frac{x_{n+1} - x_n}{x_n}
\]

In this problem the relative growth rate is fixed at 0.1 (10% per hour). So:

\[
\frac{x_{n+1} - x_n}{x_n} = 0.1
\]

Rearrange to solve for `x_{n+1}`:

\[
x_{n+1} - x_n = 0.1 \, x_n
\]
\[
x_{n+1} = x_n + 0.1 \, x_n = 1.1 \, x_n
\]

This is the **difference equation** for the yeast population. The factor 1.1 is the **growth multiplier** per hour.

### Initial Condition

The initial population at hour 0 is:

\[
x_0 = 100{,}000
\]

### Explicit Solution

Because the difference equation is a simple geometric progression, you can write an explicit formula. Starting from `x_0`, after one hour you have `x_1 = 1.1 x_0`, after two hours `x_2 = 1.1 x_1 = 1.1^2 x_0`, and in general:

\[
x_n = 1.1^n \cdot x_0
\]

Substituting `x_0 = 100{,}000`:

\[
x_n = 1.1^n \cdot 100{,}000
\]

This is the solution for any hour `n`.

### Example: Population After 4 Hours

To find the population after 4 hours, set `n = 4`:

\[
x_4 = 1.1^4 \cdot 100{,}000
\]

Compute `1.1^4`:

```
1.1^2 = 1.21
1.1^4 = (1.21)^2 = 1.4641
```

Then multiply by 100,000:

\[
x_4 = 1.4641 \times 100{,}000 = 146{,}410
\]

So after 4 hours the yeast population is 146,410. The increase is 46,410.

### Question: When Does the Population Double?

You want to know the hour `n` when the population reaches 200,000 (double the initial 100,000). Set `x_n = 200{,}000`:

\[
1.1^n \cdot 100{,}000 = 200{,}000
\]

Divide both sides by 100,000:

\[
1.1^n = 2
\]

To solve for `n`, take the natural logarithm of both sides:

\[
\ln(1.1^n) = \ln(2)
\]
\[
n \cdot \ln(1.1) = \ln(2)
\]
\[
n = \frac{\ln(2)}{\ln(1.1)}
\]

Compute the values (using a calculator or approximate):

- `ln(2) ≈ 0.6931`
- `ln(1.1) ≈ 0.09531`

\[
n ≈ \frac{0.6931}{0.09531} ≈ 7.27
\]

Since `n` must be an integer hour (you check at discrete hours), the population doubles between hour 7 and hour 8. At hour 7, `x_7 = 1.1^7 * 100,000 ≈ 194,872`; at hour 8, `x_8 ≈ 214,359`. So the doubling time is just over 7 hours.

### Summary of Key Concepts

| Concept | Definition or Formula |
|---------|----------------------|
| One dimensional difference equation | `x_{n+1} = f(x_n)` with a single state variable |
| Relative growth rate | `(x_{n+1} - x_n) / x_n` |
| Growth multiplier | 1 + relative growth rate |
| Explicit solution for constant multiplier | `x_n = r^n * x_0`, where `r` is the multiplier |
| Doubling time | Solve `r^n = 2` for `n` |

### Check Your Understanding

1. **Derive the difference equation.** A bacteria population grows at 5% per hour, starting with 50,000. Write the difference equation and the explicit solution.

<details><summary>Answer</summary>
Relative growth rate = 0.05. Difference equation: `x_{n+1} = 1.05 x_n`. Initial condition: `x_0 = 50{,}000`. Explicit solution: `x_n = 1.05^n * 50{,}000`.
</details>

2. **Compute a specific value.** Using the yeast model in this section, what is the population after 10 hours?

<details><summary>Answer</summary>
`x_10 = 1.1^10 * 100{,}000`. `1.1^10 ≈ 2.5937`. Multiply: 259,370.
</details>

3. **Find the doubling time for a different growth rate.** If the yeast grew at 8% per hour instead of 10%, how many hours (to two decimal places) would it take to double?

<details><summary>Answer</summary>
Growth multiplier `r = 1.08`. Solve `1.08^n = 2`. `n = ln(2) / ln(1.08) ≈ 0.6931 / 0.07696 ≈ 9.01` hours.
</details>

4. **Interpret the relative growth rate.** Why is the relative growth rate defined as `(x_{n+1} - x_n)/x_n` rather than just `x_{n+1} - x_n`?

<details><summary>Answer</summary>
The relative growth rate normalizes the absolute change by the current population. This allows comparison across different population sizes. A fixed absolute change of 10,000 means very different things if the population is 100,000 (10% growth) versus 1,000,000 (1% growth). The relative rate captures the proportional change.
</details>
## Formulating a More Complex Logistic Growth Model

In the previous section, you solved the exponential growth model \( x_{n+1} = 1.1 \, x_n \) explicitly. You found that the population doubles after approximately 7.27 hours. Because the system is discrete, you must check at integer time steps: at hour 7 the population has not yet doubled, but at hour 8 it has more than doubled.



That explicit solution was possible because the model was linear. Many realistic models are nonlinear and cannot be solved explicitly. For continuous time systems, you have graphical methods like the phase line (one dimension) and the phase plane (two dimensions). These methods rely on derivatives. For discrete time systems, there are no derivatives, but a different graphical method exists: the cobweb diagram.

### The Need for a More Realistic Model

The exponential growth model \( x_{n+1} = 1.1 \, x_n \) predicts unbounded growth. After enough hours, the yeast population would reach a million, a billion, or even a trillion. This is not feasible. In reality, yeast in a petri dish face limited space and resources. As the population grows, competition for these resources increases.

### Introducing Carrying Capacity

To account for competition, you must modify the growth rate. Instead of a constant 10 percent growth rate, the growth rate should decrease as the population increases. When the population is very large, overcrowding occurs: individuals compete for resources, reproduction slows, and eventually the population may decline.

The revised model uses a **carrying capacity** \( K \). The carrying capacity is the maximum population that the environment (for example, the petri dish) can support. The growth rate is now adjusted by the factor \( 1 - \frac{x_n}{K} \).

- If the current population \( x_n \) is below \( K \), the factor \( 1 - \frac{x_n}{K} \) is positive. The population grows.
- If \( x_n \) is above \( K \), the factor is negative. The population shrinks.

### The Logistic Growth Equation

The new model is:

\[
x_{n+1} = r \, x_n \left(1 - \frac{x_n}{K}\right)
\]

Where:
- \( x_n \) is the population at time step \( n \).
- \( r \) is the intrinsic growth rate (the constant rate when the population is very small).
- \( K \) is the carrying capacity.

This equation is quadratic in \( x_n \). It is a nonlinear difference equation. You cannot solve it explicitly for all \( n \), but you can analyze it graphically using a cobweb diagram.

### Key Concepts Summary

| Concept | Definition |
|---------|------------|
| Carrying capacity \( K \) | The maximum population the environment can sustain. |
| Intrinsic growth rate \( r \) | The growth rate when the population is near zero. |
| Logistic growth equation | \( x_{n+1} = r x_n (1 - x_n / K) \), a quadratic nonlinear model. |
| Nonlinear difference equation | An equation where the next value depends nonlinearly on the current value; cannot be solved explicitly. |

### ASCII Diagram: Logistic Growth Behavior

```
Population x_{n+1}
    ^
    |     /
    |    /   (growth when x_n < K)
    |   /
    |  /
    | / 
    |/____________________> Population x_n
    K
```

When \( x_n \) is less than \( K \), the next population \( x_{n+1} \) is larger than \( x_n \). When \( x_n \) exceeds \( K \), \( x_{n+1} \) is smaller than \( x_n \). The population tends to stabilize near \( K \).

### Check Your Understanding

1. Why can't you solve the logistic growth equation \( x_{n+1} = r x_n (1 - x_n / K) \) explicitly for all \( n \)?

<details><summary>Answer</summary>
The equation is quadratic and nonlinear. Unlike the linear exponential model, there is no closed-form formula that gives \( x_n \) directly for any \( n \). You must iterate step by step or use graphical methods.
</details>

2. What does the factor \( 1 - x_n / K \) represent in the logistic model?

<details><summary>Answer</summary>
It represents the reduction in growth rate due to crowding. When \( x_n \) is small, the factor is close to 1, so growth is nearly exponential. When \( x_n \) approaches \( K \), the factor approaches 0, slowing growth. When \( x_n \) exceeds \( K \), the factor becomes negative, causing the population to shrink.
</details>

3. If the carrying capacity \( K = 1000 \) and the current population \( x_n = 1200 \), will the population increase or decrease at the next time step?

<details><summary>Answer</summary>
Decrease. Because \( x_n > K \), the factor \( 1 - 1200/1000 = -0.2 \) is negative. Multiplying by the positive growth rate \( r \) and the positive population gives a negative change, so \( x_{n+1} < x_n \).
</details>

4. How does the logistic model differ from the exponential model in terms of long-term behavior?

<details><summary>Answer</summary>
The exponential model predicts unbounded growth forever. The logistic model predicts that the population will approach the carrying capacity \( K \) and stabilize there, because growth slows as the population nears \( K \) and becomes negative if it exceeds \( K \).
</details>
## Constructing a Cobweb Diagram and Identifying Equilibrium Points

A cobweb diagram is a graphical tool for analyzing the long-term behavior of a one-dimensional discrete time dynamical system. It is especially useful when the difference equation is nonlinear and cannot be solved exactly. For example, a logistic-type model for a yeast population with parameters R > 0 and K > 0 has no closed-form solution like `X_n = 1.1^n * 100,000`. The cobweb diagram lets you see the dynamics without solving the equation.

### Step 1: Plot the function and the diagonal line

To build a cobweb diagram, start with a set of axes. The horizontal axis represents the current state `X_n`. The vertical axis represents the next state `X_{n+1}`.

1. Plot the function `F(x)` that defines the difference equation: `X_{n+1} = F(X_n)`. This curve is the right-hand side of your model. For a logistic model, `F(x)` is a concave down curve that starts at the origin, rises to a maximum, and then decreases toward zero as `x` increases.
2. On the same axes, plot the line `y = x`. This is a straight diagonal line through the origin with slope 1.

```
    X_{n+1}
      ^
      |   / F(x)
      |  /
      | /
      |/
      |\
      | \
      |  \
      |   \
      +----+-----> X_n
           x0
```

### Step 2: Identify equilibrium points

The intersection points of the curve `F(x)` and the line `y = x` are the **equilibrium points** (also called fixed points) of the system. At an equilibrium, `F(x) = x`, so `X_{n+1} = X_n`. The population does not change from one time step to the next.

In a logistic model with positive parameters, there are two equilibrium points:

- **Zero (0):** If the population is zero, it cannot reproduce, so it stays at zero. This is a trivial equilibrium.
- **The carrying capacity K:** This is the unique positive equilibrium. If the population equals K, the growth rate is zero and the population remains at K.

The speaker notes: “If your population is exactly at the carrying capacity, then your population doesn’t want to increase or decrease. It’s very happy being there.”

### Step 3: Start the cobweb iteration

Choose an initial condition `X_0` (a point on the x-axis). The cobweb diagram shows successive iterates `X_1, X_2, X_3, ...` by following a simple geometric procedure:

1. **Vertical step:** From `X_0` on the x-axis, draw a vertical line upward until it meets the curve `F(x)`. The y-coordinate of this intersection is `F(X_0)`, which equals `X_1`. Mark this point as `(X_0, X_1)`.
2. **Horizontal step:** From that point, draw a horizontal line to the right (or left) until it meets the diagonal line `y = x`. Because the horizontal line has constant y-value equal to `X_1`, the intersection with `y = x` occurs at `(X_1, X_1)`. This step effectively “reflects” the y-value back onto the x-axis.
3. **Vertical step again:** From `(X_1, X_1)`, draw a vertical line downward to the x-axis. This lands on `X_1`.
4. **Repeat:** Now you have `X_1` on the x-axis. From there, draw a vertical line up to the curve to find `X_2 = F(X_1)`. Then draw a horizontal line to the diagonal, then a vertical line down to the x-axis to get `X_2`. Continue this process.

The pattern of vertical and horizontal lines that forms is called a **cobweb** (or “tic-tac-toe” pattern). Each complete “square” of the cobweb corresponds to one iteration.

```
    X_{n+1}
      ^
      |   (x0, F(x0)) ---- (x1, F(x0)) on y=x
      |   |               |
      |   |   (x1, F(x1)) ---- (x2, F(x1))
      |   |   |               |
      |   |   |   (x2, F(x2)) ---- ...
      |   |   |   |
      +---+---+---+---> X_n
      x0  x1  x2
```

### Step 4: Observe convergence

If the initial condition is below the carrying capacity `K`, the cobweb will spiral inward toward the equilibrium point `K`. The population increases, then decreases, and gradually approaches K. If the initial condition is above K, the population decreases, then may overshoot, and again converges to K. The cobweb shows that the system “wedges itself” into the equilibrium.

The speaker demonstrates this: “In this case, you can see that you are pushing yourself into the equilibrium point. X_n is converging to the equilibrium point K.” The same behavior occurs when starting from a population above K: “you trace yourself up to your curve ... your growth rate is negative now ... you’re going to sort of wed yourself in.”

### Key takeaways

- The cobweb diagram is a graphical method for one-dimensional difference equations that cannot be solved analytically.
- Equilibrium points are the intersections of `F(x)` and `y = x`.
- The cobweb construction uses the diagonal line to map the output of the function back onto the input axis.
- Convergence to a stable equilibrium is visible as a tightening cobweb pattern.

### Check your understanding

1. **Question:** What are the two equilibrium points in a logistic model with positive parameters, and how do you find them on a cobweb diagram?
   <details><summary>Answer</summary>They are zero and the carrying capacity K. They are found at the intersections of the curve F(x) and the line y = x.</details>

2. **Question:** Describe the steps to obtain X_2 from X_0 using a cobweb diagram.
   <details><summary>Answer</summary>From X_0, go vertically up to F(x) to get X_1. Then go horizontally to the y=x line, then vertically down to the x-axis to mark X_1. From X_1, go vertically up to F(x) to get X_2.</details>

3. **Question:** Why is the diagonal line y = x essential in the cobweb construction?
   <details><summary>Answer</summary>It allows you to “reflect” the output value (vertical coordinate) back to the horizontal axis so that you can use it as the next input. Without it, you would not be able to continue the iteration graphically.</details>

4. **Question:** If the cobweb pattern shows a tightening spiral that ends at the intersection of F(x) and y=x, what does that indicate about the long-term behavior of the system?
   <details><summary>Answer</summary>The population converges to the equilibrium point at that intersection. The system is stable at that equilibrium.</details>
## Interpreting Cobweb Diagrams: Monotonic Convergence and Overshooting

A cobweb diagram is a graphical tool for analyzing the behavior of a one‑dimensional discrete time dynamical system, such as a population model. The diagram plots the update function \(f(x)\) (the right‑hand side of the difference equation) together with the line \(y = x\). The equilibrium points of the system occur where \(f(x) = x\). In a logistic growth model, the carrying capacity \(K\) is one such equilibrium.

### Monotonic Convergence (Small Growth Rate)

When the relative growth rate \(R\) is small, the function \(f(x)\) rises gently from the origin and crosses the line \(y = x\) at \(K\). Starting from a small initial population \(x_0\) (for example, a tiny amount of yeast), the cobweb construction proceeds as follows:

1. From \(x_0\) on the horizontal axis, draw a vertical line upward to the curve \(f(x)\). The height of this intersection is the next population \(x_1 = f(x_0)\).
2. From that point on the curve, draw a horizontal line to the right until it meets the line \(y = x\). This step “reflects” the population value back to the horizontal axis.
3. From the intersection with \(y = x\), draw a vertical line upward to the curve again. This gives \(x_2 = f(x_1)\).
4. Repeat: vertical to the curve, horizontal to \(y = x\), vertical to the curve, and so on.

In this case, every step stays **below** the carrying capacity \(K\). The population increases each time but by a smaller amount, and the cobweb “staircase” approaches \(K\) from below without ever crossing it. This pattern is called **monotonic convergence**: the sequence \(x_n\) increases steadily toward \(K\).

The diagram below illustrates the monotonic case. The curve \(f(x)\) is drawn with a moderate slope at the origin. The line \(y = x\) is the diagonal. The cobweb steps (vertical and horizontal lines) form a staircase that converges to the intersection point at \(K\).

```
        f(x)
        ^
        |          / 
        |         /  
        |        /   
        |       /    
        |      /     
        |     /      
        |    /       
        |   /        
        |  /         
        | /          
        |/___________> x
        |            K
```

(Added context: The vertical and horizontal lines are not drawn in this simple ASCII sketch, but the staircase would appear as a series of steps climbing the curve from left to right toward \(K\).)

### Overshooting and Spiraling Convergence (Larger Growth Rate)

If the growth rate \(R\) is increased, the function \(f(x)\) becomes steeper at the origin and reaches a higher peak before descending to cross the line \(y = x\) at the same carrying capacity \(K\). The equilibrium \(K\) does **not** change with \(R\); it is a fixed point of the system regardless of the growth rate. However, the dynamics change dramatically.

Starting again from a small initial population, the cobweb construction follows the same vertical‑horizontal procedure. Because the function is steeper, each step produces a much larger jump in population. The population may now **overshoot** the carrying capacity: after a few steps, the vertical line from the curve lands above \(K\) instead of below it.

The sequence of steps becomes:

- \(x_0\) small → \(x_1\) larger but still below \(K\).
- \(x_1\) → \(x_2\) even larger, still below \(K\).
- \(x_2\) → \(x_3\) now **above** \(K\) (overshoot).
- Because the population is above \(K\), the next update \(x_4 = f(x_3)\) is smaller (crowding reduces the population). This brings the value back below \(K\).
- Then \(x_5\) overshoots again, and so on.

The cobweb diagram now shows a pattern of alternating above and below \(K\), with the steps gradually shrinking in amplitude. This is called **overshooting convergence** or **spiraling convergence**: the population oscillates around \(K\) while approaching it.

The following ASCII diagram sketches the overshooting case. The curve \(f(x)\) has a higher peak. The cobweb steps cross the line \(y = x\) multiple times, creating a spiral pattern around \(K\).

```
        f(x)
        ^
        |       /\
        |      /  \
        |     /    \
        |    /      \
        |   /        \
        |  /          \
        | /            \
        |/______________\___> x
        |               K
```

(Added context: The actual cobweb would show vertical and horizontal lines that zigzag across the diagonal, forming a spiral that tightens around \(K\).)

The key claim from the video is that the value of \(R\) determines whether convergence is monotonic or overshooting. A larger \(R\) means a steeper initial slope and a higher peak in \(f(x)\), which causes larger jumps from one time step to the next. This overshooting behavior is analogous to the case of a linear difference equation where the eigenvalue \(\lambda\) lies between 1 and 2: each step multiplies the deviation from equilibrium by a negative factor, producing alternating signs and convergence.

### Summary of the Two Convergence Patterns

| Feature | Monotonic Convergence | Overshooting (Spiraling) Convergence |
|---------|-----------------------|--------------------------------------|
| Growth rate \(R\) | Small | Large |
| Shape of \(f(x)\) | Gentle rise, low peak | Steep rise, high peak |
| Cobweb pattern | Staircase below \(K\) | Zigzag crossing \(K\) |
| Population behavior | Increases steadily toward \(K\) | Oscillates above and below \(K\) |
| Equilibrium \(K\) | Attracts from below | Attracts with alternating steps |

### Check your understanding

1. **What determines whether a cobweb diagram shows monotonic convergence or overshooting?**  
   <details><summary>Answer</summary> The growth rate parameter \(R\). A small \(R\) leads to monotonic convergence; a larger \(R\) leads to overshooting and spiraling convergence.</details>

2. **In the overshooting case, why does the population sometimes decrease even though it is below the carrying capacity?**  
   <details><summary>Answer</summary> It does not decrease when below \(K\); it decreases only after overshooting above \(K\). The overshoot causes crowding, which reduces the population in the next step.</details>

3. **What is the role of the line \(y = x\) in constructing a cobweb diagram?**  
   <details><summary>Answer</summary> The line \(y = x\) is used to “reflect” the population value from the vertical axis back to the horizontal axis after each update. It allows the next vertical step to start from the correct horizontal coordinate.</details>

4. **True or false: The carrying capacity \(K\) changes when \(R\) is increased.**  
   <details><summary>Answer</summary> False. \(K\) is an equilibrium of the system and does not depend on \(R\). Only the dynamics (how the population approaches \(K\)) change with \(R\).</details>
## Chaotic Behavior in Cobweb Diagrams with Very Large Growth Rates

When the growth rate \(R\) becomes very large, the discrete time dynamical system no longer settles into a fixed point or a periodic cycle. Instead, the population jumps erratically between high and low values, never repeating in a predictable pattern. This behavior is called **chaos**. In a cobweb diagram, chaos appears as a dense tangle of lines that never converge to a single point or a small set of points.

### How Chaos Arises from Large Growth Rates

Recall the general form of the one-dimensional difference equation (the logistic map):

\[
x_{n+1} = R \, x_n \left(1 - \frac{x_n}{K}\right)
\]

where \(R\) is the growth rate and \(K\) is the carrying capacity. For small \(R\) (e.g., \(R < 2\)), the cobweb diagram shows monotone convergence or damped oscillations toward the carrying capacity. As \(R\) increases past 2, you see period-doubling (jumping between two values). When \(R\) becomes very large (e.g., \(R > 3.57\) for the standard logistic map, or even larger depending on \(K\)), the system enters chaos.

In the video, the speaker sketches a cobweb diagram for a very large \(R\). The key steps are:

1. Start with a very small initial population \(x_0\) (near zero).
2. Apply the function \(f(x) = R x (1 - x/K)\). Because \(R\) is huge, the population jumps massively upward in one step.
3. The new population is now far above the carrying capacity \(K\). The next step brings it way down, often below \(K\).
4. The population overshoots downward, so the following step shoots back up.
5. This overshoot pattern continues indefinitely. The population never settles into a steady state or a simple cycle.

The speaker emphasizes that the cobweb diagram for chaos “would start to fill in” with so many lines that you cannot read it. The equilibrium points (the fixed points at \(x=0\) and \(x=K\)) no longer attract the trajectory. Instead, the population wanders seemingly at random.

### Visualizing Chaos with an ASCII Cobweb Diagram

Since no screenshots are available, the following ASCII diagram illustrates the chaotic cobweb pattern for a very large \(R\). The dashed line is the diagonal \(y = x\). The curve is the function \(f(x)\). The cobweb path bounces erratically.

```
Population x_{n+1}
^
|                     f(x) curve (steep)
|                    /
|                   /
|                  /
|                 /
|                /
|               /
|              /
|             /
|            /
|           /
|          /
|         /
|        /
|       /
|      /
|     /
|    /
|   /
|  /
| /
|/________________________> Population x_n
```

In a real chaotic cobweb, the lines cross the diagonal many times, never settling into a small region. The path appears to fill the space between the curve and the diagonal.

### Interactive Exploration

The video provides a link to a website that lets you sketch cobweb diagrams interactively. To see chaos for yourself:

- Set the carrying capacity \(K = 1\) (or any fixed value).
- Choose a very small initial condition, such as \(x_0 = 0.01\).
- Systematically increase \(R\) from small values (e.g., 0.5, 1.0, 2.0, 3.0, 3.5, 4.0, 6.0).
- Observe the transition from monotone convergence to damped oscillations, then to period-doubling, and finally to chaos.

The speaker notes that for very large \(R\) (e.g., \(R = 4\) or \(R = 6\), depending on \(K\)), the cobweb diagram becomes chaotic.

### A Real-World Example: Carlson’s Yeast Data

In 1913, the German researcher Carlson collected data on yeast populations. The video mentions that the original exponential growth model (10% per hour) came from that data. When you fit Carlson’s data to a model of the form \(x_{n+1} = a x_n - b x_n^2\), you obtain the specific equation:

\[
x_{n+1} = 1.56 \, x_n - 0.00861 \, x_n^2
\]

This is a logistic map with \(R = 1.56\) and \(K = 1.56 / 0.00861 \approx 181.2\). For this value of \(R\), the system is not chaotic; it converges to a stable equilibrium. The example illustrates that real yeast populations typically have moderate growth rates, not the extreme values that produce chaos.

### Summary of Behaviors for Different Growth Rates

The following table summarizes the typical behavior of the logistic map as \(R\) increases (with \(K\) fixed).

| Growth Rate \(R\) | Cobweb Behavior | Description |
|-------------------|-----------------|-------------|
| \(0 < R \leq 1\) | Monotone convergence to zero | Population dies out. |
| \(1 < R < 2\) | Monotone convergence to \(K\) | Population grows smoothly to carrying capacity. |
| \(2 \leq R < 3\) | Damped oscillations to \(K\) | Population overshoots and then settles. |
| \(3 \leq R < 3.57\) (approx.) | Period-doubling (2-cycle, 4-cycle, etc.) | Population alternates between two or more values. |
| \(R \geq 3.57\) (approx.) | Chaos | Population never settles; cobweb fills the diagram. |

The exact thresholds depend on the specific form of the equation and the value of \(K\). The video’s sketches for very large \(R\) (e.g., \(R = 4\) or \(R = 6\)) fall into the chaotic regime.

### Check Your Understanding

1. **What is the defining characteristic of a chaotic cobweb diagram?**  
   <details><summary>Answer</summary> The cobweb never converges to a fixed point or a periodic cycle. The lines fill the diagram, and the population jumps erratically between high and low values in a seemingly random manner.</details>

2. **Why does a very large growth rate \(R\) cause chaos?**  
   <details><summary>Answer</summary> A large \(R\) makes the function \(f(x)\) very steep. A small change in population leads to a huge change in the next step. This causes the population to overshoot the carrying capacity massively in both directions, and the overshoots never dampen out.</details>

3. **In the video, the speaker mentions a specific equation from Carlson’s yeast data: \(x_{n+1} = 1.56 x_n - 0.00861 x_n^2\). Is this equation chaotic? Why or why not?**  
   <details><summary>Answer</summary> No, it is not chaotic. The growth rate \(R = 1.56\) is less than 2, so the system converges monotonically to the carrying capacity. The equation is an example of a real-world population model that does not exhibit chaos.</details>

4. **What happens to the equilibrium points (fixed points) when the system becomes chaotic?**  
   <details><summary>Answer</summary> The equilibrium points (at \(x=0\) and \(x=K\)) become unstable. They no longer attract the trajectory. The population wanders away from them and never settles.</details>
## Real World Application: Carlson's Yeast Data and Model Fitting

After fitting the logistic map to Carlson’s 1913 yeast data, the model parameters are determined to be:

- \( R = 0.56 \)
- \( K = 650.4 \) (approximately)

(Added context) The logistic map is a discrete-time population model: \( x_{n+1} = R \, x_n \left(1 - \frac{x_n}{K}\right) \).  
\( R \) is the intrinsic growth rate; \( K \) is the carrying capacity of the environment.

Now you are asked to draw a cobweb diagram for this specific logistic map. A cobweb diagram is a graphical method for iterating a one-dimensional map: you plot the function curve and the line \( y = x \), then step vertically to the curve and horizontally to the diagonal to obtain successive values.

Follow these steps:

1. Define the function: \( f(x) = 0.56 \cdot x \cdot \left(1 - \frac{x}{650.4}\right) \).
2. Choose a plotting range for \( x \). Since \( K \) is the carrying capacity, plot \( x \) from 0 to, for example, 700.
3. Plot the curve \( y = f(x) \) over this range.
4. Plot the diagonal line \( y = x \).
5. Choose an initial condition \( x_0 \). (Consider the initial yeast population from Carlson’s experiment, or simply pick a small value like 10 to start.)
6. Locate \( x_0 \) on the \( x \)-axis. Draw a vertical line from \( (x_0, 0) \) up to the curve at \( (x_0, f(x_0)) \). This point gives \( x_1 = f(x_0) \).
7. From that point, draw a horizontal line to the diagonal line \( y = x \). This lands at \( (x_1, x_1) \).
8. From \( (x_1, x_1) \), draw a vertical line to the curve at \( (x_1, f(x_1)) \).
9. Repeat steps 7 and 8 for several iterations, tracing the cobweb path.

Examine the resulting cobweb. Does the population converge to a fixed point? If so, what is its value? (Added context) The fixed points satisfy \( x = f(x) \). Solving \( x = 0.56 x \left(1 - \frac{x}{650.4}\right) \) gives \( x = 0 \) or \( x = 650.4 \left(1 - \frac{1}{0.56}\right) \approx -511 \). The negative fixed point is not biologically meaningful. The only non‑negative fixed point is 0. Because \( R < 1 \), the population is expected to decline to extinction.

Now consider the question posed by the instructor: “If you are T. Carlson actually observing this back in 1913, what would your yeast population do if it was governed by this model?”

Draw the cobweb diagram and interpret the result. You tell me: what does the cobweb diagram show? Go ahead and let me know what you come up with.

### Check your understanding

1. What are the values of \( R \) and \( K \) obtained from Carlson’s yeast data?
2. For the logistic map with \( R = 0.56 \) and \( K = 650.4 \), what is the biologically relevant fixed point?
3. What does the cobweb diagram predict about the long‑term behavior of the yeast population?
4. Why does the cobweb diagram show a decline to zero rather than a stable non‑zero population?

<details>
<summary>Answer</summary>
1. \( R = 0.56 \), \( K \approx 650.4 \).  
2. The only non‑negative fixed point is \( x = 0 \). (The other fixed point is negative and not biologically meaningful.)  
3. The cobweb diagram shows the population decreasing toward zero, i.e., extinction.  
4. Because \( R < 1 \), the growth rate is too low to sustain the population. The logistic map model predicts that the population will decline to zero.
</details>
## Key takeaways

- A one-dimensional difference equation relates the next state to the current state using a function F of X, often derived from a relative growth rate.
- For linear difference equations with constant growth, explicit solutions are geometric sequences like Xn = R^n * X0.
- The logistic growth model adds a carrying capacity K, making the growth rate decrease as population increases, resulting in the equation Xn+1 = R*Xn*(1 - Xn/K).
- A cobweb diagram is constructed by plotting the function F of X and the line Y = X, then tracing vertical and horizontal lines to visualize iterations.
- Equilibrium points are found at the intersections of F of X and Y = X, representing populations that do not change over time.
- For small growth rates R, the cobweb diagram shows monotonic convergence toward the carrying capacity without overshooting.
- Larger R causes overshooting and oscillations as the population jumps above and then below the equilibrium, eventually spiraling in.
- Very large growth rates R lead to chaotic behavior where the population never settles, jumping seemingly at random between high and low values.
- Real data from Carlson's yeast experiment (1913) can be fitted to the logistic model, yielding specific R and K values for practical analysis.
- The cobweb diagram provides a powerful graphical method to analyze nonlinear difference equations that cannot be solved explicitly.
## Glossary

| Term | Definition |
|---|---|
| one-dimensional difference equation | An equation that describes how a single variable changes from one discrete time step to the next, written as Xn+1 = F(Xn). |
| discrete time dynamical system | A system where time advances in fixed steps and the state is updated at each step using a rule or function. |
| state space | The set of all possible values of the variable that describes the system; for one-dimensional systems, it is a subset of the real numbers. |
| relative growth rate | The change in population per unit time divided by the current population, often expressed as a percentage. |
| carrying capacity | The maximum population size that an environment can sustain indefinitely, denoted by K. |
| logistic growth model | A model where the growth rate decreases linearly with population size, leading to the equation Xn+1 = R*Xn*(1 - Xn/K). |
| cobweb diagram | A graphical method for analyzing one-dimensional difference equations by plotting F(X) and Y = X, then tracing iterations to visualize dynamics. |
| equilibrium point | A value of X such that F(X) = X, meaning the population does not change at that point. |
| iteration | The process of repeatedly applying the difference equation to move from one state to the next. |
| monotonic convergence | A behavior where the population steadily approaches the equilibrium without crossing it, moving consistently upward or downward. |
| overshooting | A situation where the population jumps past the equilibrium in one time step, leading to oscillations around it. |
| oscillation | A pattern where the population alternates between values above and below the equilibrium over successive time steps. |
| chaotic behavior | A dynamical regime where the population evolves in a seemingly random, aperiodic manner, highly sensitive to initial conditions. |
| explicit solution | A closed-form formula that gives the state at any time step directly, without needing to iterate. |
| nonlinear function | A function that is not a straight line; for example, the quadratic function in the logistic model. |
| parameter R | A constant in the logistic model that controls the intrinsic growth rate; larger R leads to more complex dynamics. |
| parameter K | The carrying capacity in the logistic model, representing the maximum sustainable population. |
| initial condition | The value of the variable at time zero, from which the iteration begins. |
| phase line | A graphical tool for one-dimensional continuous-time dynamical systems that shows the sign of the derivative; the cobweb diagram is its discrete-time analog. |
| relative growth rate adjustment | The modification of the growth rate in the logistic model so that it decreases as the population approaches the carrying capacity. |
## Footnotes and deeper context

1. **Discrete vs continuous time.** In discrete-time models, the state is updated only at integer time steps, unlike continuous-time models where derivatives describe instantaneous change. The cobweb diagram is the discrete analog of the phase line for continuous systems.
2. **Chaos in the logistic map.** The logistic map with R > 3.56995 (approximately) exhibits chaos, but the exact threshold depends on the parameter. For R > 4, the population can become negative or exceed the carrying capacity in ways that lead to divergence, so the model is usually restricted to R ≤ 4.
3. **Carlson's yeast data.** The values R = 0.56 and K ≈ 650.4 come from fitting the logistic model to actual yeast growth data collected by Carlson in 1913. These values are well within the range that produces monotonic convergence, so the real yeast population likely approached K smoothly.
4. **Common misconception about overshooting.** Overshooting is not caused by the discrete nature alone; it occurs when the growth rate is high enough that the next iterate exceeds the equilibrium. In continuous-time logistic models, overshooting does not happen because the growth rate is smoothly adjusted.
5. **Explicit solutions for nonlinear equations.** Most nonlinear difference equations, including the logistic map, do not have closed-form explicit solutions. The cobweb diagram is one of the few general methods to analyze their behavior without solving them.
## Where to go next

- **Interactive logistic map applet.** Use online applets such as 'Logistic Map' by Geogebra or the one at 'math.bu.edu/DYSYS/applets/Logistic.html' to visually explore cobweb diagrams for different R values. This hands-on practice helps solidify the connection between R and dynamics.
- **Strogatz, Nonlinear Dynamics and Chaos.** Chapters 10 and 11 of Strogatz's textbook provide a rigorous introduction to one-dimensional maps, including the logistic map, period-doubling route to chaos, and the cobweb method. It is the canonical resource for understanding discrete dynamical systems.
- **May, R. M. (1976). Simple mathematical models with very complicated dynamics.** This classic paper by Robert May explains how simple logistic equations can produce complex dynamics and chaos. It is a foundational reference for the ecological application of cobweb diagrams.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
