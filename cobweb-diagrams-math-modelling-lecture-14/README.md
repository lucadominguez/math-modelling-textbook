# Cobweb Diagrams and Discrete Dynamical Systems: A Graphical Approach to Population Models
> **Source:** [Cobweb Diagrams - Math Modelling - Lecture 14](https://www.youtube.com/watch?v=1hCX5Gbeo0E) by Math Modelling · 31:04 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students in mathematical modeling, ecology, or dynamical systems who want to understand iterative maps and their graphical analysis.
## Learning objectives

After working through this document you can:

1. Define discrete time dynamical systems and difference equations for one-dimensional state spaces.
2. Construct and solve simple exponential growth models using explicit iteration and logarithms.
3. Formulate logistic growth models that incorporate carrying capacity and nonlinearity.
4. Explain the need for graphical methods when explicit solutions are unavailable.
5. Build and interpret cobweb diagrams by plotting the update function $F(x)$ and the line $y = x$.
6. Identify equilibria as intersections of $F(x)$ and $y = x$ and classify their stability.
7. Analyze the effect of the growth rate parameter $r$ on dynamics: monotonic convergence, oscillatory convergence, and chaos.
8. Apply cobweb analysis to real data, such as Carlson's yeast population model.
## Prerequisites

- Basic algebra and logarithms
- Familiarity with functions and graphs
- Introductory calculus (derivatives, continuous time dynamical systems)
## Exponential Growth Model and Explicit Solution

This section introduces one-dimensional discrete time dynamical systems. A discrete time dynamical system is a rule that gives the next value of a variable from its current value at separate, evenly spaced time steps. The state space is the set of all possible values that the variable can take. In a one-dimensional system, the state space contains only one variable, so each state is a single number. The rule that describes the change from one step to the next is called a difference equation.

| Symbol | Meaning |
|---|---|
| $n$ | the time step, measured in hours |
| $X_n$ | the yeast population at hour $n$ |
| $\Delta X_n$ | the change in population from hour $n$ to hour $n+1$, so $\Delta X_n = X_{n+1} - X_n$ |
| $r_n$ | the relative growth rate at hour $n$ |

### Modeling the yeast population

We model a yeast colony that grows at 10% per hour. When the clock starts, the population is 100,000. We check the population once every hour. This is the discrete part of the model: we move from hour 0 to hour 1, from hour 1 to hour 2, and so on. We make no assumption about what happens between checks.

The relative growth rate is the change in population divided by the current population. It measures how much the population grows per unit of current population over one time step. The video also notes that relative rates appeared earlier in the course, for example in sensitivity analysis during the optimization unit.


![A whiteboard shows the example equation r(n) = ΔX(n) / X.](frames/frame_01_120s.jpg)
*[02:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=120s) A whiteboard shows the example equation r(n) = ΔX(n) / X.*


The relative growth rate is

$$
r_n = \frac{\Delta X_n}{X_n}.
$$

In this model, the relative growth rate is constant. Since 10% per hour means 0.1 in decimal form, we set

$$
r_n = 0.1.
$$

Therefore,

$$
\Delta X_n = 0.1 X_n.
$$


![A whiteboard shows an example equation for r(n) and its derived form for ΔX(n).](frames/frame_02_180s.jpg)
*[03:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=180s) A whiteboard shows an example equation for r(n) and its derived form for ΔX(n).*


To step forward one hour, we add the change to the current population:

$$
X_{n+1} = X_n + \Delta X_n = X_n + 0.1 X_n = 1.1 X_n.
$$

The initial condition is the state at time zero:

$$
X_0 = 100{,}000.
$$

So the complete model is

$$
X_{n+1} = 1.1 X_n, \qquad X_0 = 100{,}000.
$$


![An example problem is shown on a whiteboard, defining r(n) as the change in X(n) over X(n) equals 0.1, leading to X(n+1) = 1.1 X(n) with an...](frames/frame_03_220s.jpg)
*[03:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=220s) An example problem is shown on a whiteboard, defining r(n) as the change in X(n) over X(n) equals 0.1, leading to X(n+1) = 1.1 X(n) with an initial value of X(0) = 100,000.*


### Explicit solution

Because the rule multiplies the current population by the same constant 1.1 at every step, we can write the solution directly for any hour $n$. After one hour, $X_1 = 1.1 X_0$. After two hours, $X_2 = 1.1 X_1 = 1.1^2 X_0$. Continuing this pattern gives the explicit solution:

$$
X_n = (1.1)^n \cdot 100{,}000.
$$

An explicit solution gives the state at any time step directly, without iterating one step at a time. The factor $1.1$ is the growth multiplier and plays the same role as the fixed multiplier in the general linear difference equation from the previous lecture.

Now we can answer concrete questions.

How much yeast is present after four hours?


![A whiteboard shows an example calculation for exponential growth, starting with r(n) = ΔX(n)/X(n) = 0.1 and leading to X(n) = (1.1)^n * 100,000...](frames/frame_04_280s.jpg)
*[04:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=280s) A whiteboard shows an example calculation for exponential growth, starting with r(n) = ΔX(n)/X(n) = 0.1 and leading to X(n) = (1.1)^n * 100,000, with a prompt to calculate X(4).*


After four hours,

$$
X_4 = (1.1)^4 \cdot 100{,}000.
$$

Since $(1.1)^4 = 1.4641$, we get

$$
X_4 = 146{,}410.
$$

The population increased by

$$
X_4 - X_0 = 146{,}410 - 100{,}000 = 46{,}410.
$$

### When does the population double?

We want the hour $n$ at which the population reaches 200,000. Set the explicit solution equal to 200,000:

$$
(1.1)^n \cdot 100{,}000 = 200{,}000.
$$

Divide both sides by 100,000:

$$
(1.1)^n = 2.
$$

Take the natural logarithm of both sides:

$$
n \ln(1.1) = \ln(2).
$$

Therefore,

$$
n = \frac{\ln(2)}{\ln(1.1)} \approx 7.27.
$$


![The whiteboard shows an example problem calculating population growth and the time it takes for a population to double.](frames/frame_05_380s.jpg)
*[06:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=380s) The whiteboard shows an example problem calculating population growth and the time it takes for a population to double.*


In a continuous time model, we could report the doubling time as about 7.27 hours. In this discrete model, however, we only check the population at integer hours. At hour 7, the population is still below 200,000. At hour 8, the population is above 200,000. So the model tells us to check at the 8th hour to observe at least a full doubling from the initial population.

### When an explicit solution is not available

The yeast model has a simple explicit solution because the updating rule is linear and constant. Many difference equations do not have such a simple closed form. In those cases, we need a graphical method to understand the behavior of solutions.

For one-dimensional continuous time systems, the phase line method summarizes how the state changes for different values of the state. The graphical method for discrete difference equations extends that idea. The method is called a cobweb diagram, and it lets us visualize the sequence of states produced by iterating a difference equation without requiring an explicit solution.
## Logistic Growth Model and the Need for Graphical Methods

In a continuous-time dynamical system, the phase plane method uses derivatives to describe how a state changes over time. A discrete dynamical system updates a state by a rule such as $X_{n+1} = f(X_n)$ at separate time steps. In the discrete case, there is no derivative with respect to time, so the usual calculus language of increasing or decreasing cannot be applied directly. A graphical method can still be used: plot the update rule $f$ together with the line $y=x$.

### Exponential growth for yeast

Begin with a yeast population that grows at a constant rate. Let $X_n$ be the population at hour $n$, and let

$$
\Delta X_n = X_{n+1} - X_n
$$

be the change in population during one hour. The per-hour growth rate is

$$
\frac{\Delta X_n}{X_n} = 0.1.
$$

Therefore,

$$
\Delta X_n = 0.1 X_n,
$$

so

$$
X_{n+1} = 1.1 X_n.
$$

If the initial population is $X_0 = 100{,}000$, then the exact solution is

$$
X_n = (1.1)^n \cdot 100{,}000.
$$


![A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n) = (1.1)^n * 100,000.](frames/frame_06_500s.jpg)
*[08:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=500s) A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n) = (1.1)^n * 100,000.*


After 4 hours,

$$
X_4 = (1.1)^4 \cdot 100{,}000 = 146{,}410.
$$

To find when the population doubles, solve

$$
X_n = 200{,}000,
$$

which gives

$$
(1.1)^n = 2,
$$

so

$$
n = \frac{\ln 2}{\ln 1.1} \approx 7.27.
$$

The doubling time is about 7.27 hours.

### Why exponential growth is not realistic

This model has no upper bound. It predicts that the yeast population could grow to a million, a billion, a trillion, or even take over the entire universe. That is not feasible. Real yeast in a petri dish compete for a finite amount of resources and space. The exponential model does not include that competition.


![A whiteboard shows an example problem calculating population growth and doubling time using the formula r(n) = ΔX(n)/X(n) = 0.1.](frames/frame_07_560s.jpg)
*[09:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=560s) A whiteboard shows an example problem calculating population growth and doubling time using the formula r(n) = ΔX(n)/X(n) = 0.1.*


To improve the model, return to the growth-rate equation. The original assumption was that the growth rate stays at 10% no matter how many yeast are present. Instead, allow the growth rate to decrease as the population increases.

If the population becomes crowded, there is less room and fewer resources for new yeast. Reproduction slows. If the population becomes extremely overcrowded, competition for resources is so intense that the population stops growing and may shrink.


![A whiteboard shows an example problem calculating population growth and doubling time using mathematical equations.](frames/frame_08_600s.jpg)
*[10:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=600s) A whiteboard shows an example problem calculating population growth and doubling time using mathematical equations.*


Let $r$ be the growth rate when the population is small. This is the maximum possible per-step growth rate. Let $K$ be the carrying capacity, which is the maximum population that the environment can support. The adjusted growth rate is

$$
R_n
## Constructing Cobweb Diagrams and Monotonic Convergence

A cobweb diagram is a graphical tool for visualizing the iterates of a discrete dynamical system $X_{n+1} = F(X_n)$. It plots the function $F(x)$ and the line $y=x$ on the same axes. The intersections of these two curves are the equilibrium points of the system.

### Equilibrium Points from Intersections


![A whiteboard shows mathematical equations for population growth and a graph of F(x) versus x, with a line y=x.](frames/frame_11_840s.jpg)
*[14:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=840s) A whiteboard shows mathematical equations for population growth and a graph of F(x) versus x, with a line y=x.*


At any equilibrium point, the population does not change from one time step to the next: $\Delta X_n = 0$. For the logistic model

$$
X_{n+1} = X_n + r X_n \left(1 - \frac{X_n}{K}\right) = F(X_n),
$$

the condition $X_{n+1} = X_n$ gives $F(X_n) = X_n$. Graphically, this occurs where the curve $y=F(x)$ crosses the line $y=x$. There are two such intersections:

- $X=0$ (the trivial equilibrium, no population).
- $X=K$ (the carrying capacity, the unique positive equilibrium).

At $X=K$, the growth rate is zero: the population is stable. At $X=0$, no reproduction is possible, so the system remains at zero. Identifying these steady states is an immediate advantage of the graphical approach.

### Constructing the Cobweb Diagram

The cobweb diagram works like a phase line diagram but provides a step-by-step picture of the dynamics. To construct it, follow these steps for a given initial condition $X_0$.

| Step | Action | Resulting Point |
|------|--------|----------------|
| 1 | Locate $X_0$ on the x-axis. | $(X_0, 0)$ |
| 2 | Draw a vertical line from $(X_0,0)$ up to the curve $y=F(x)$. | $(X_0, F(X_0)) = (X_0, X_1)$ |
| 3 | Draw a horizontal line from $(X_0, X_1)$ to the line $y=x$. | $(X_1, X_1)$ |
| 4 | Draw a vertical line from $(X_1, X_1)$ up (or down) to the curve $y=F(x)$. | $(X_1, F(X_1)) = (X_1, X_2)$ |
| 5 | Repeat steps 3 and 4 to generate $X_3, X_4, \dots$ | Sequence $X_0, X_1, X_2, \dots$ |

The line $y=x$ acts as a mirror: it transfers the output value $X_1$ from the y-axis back to the x-axis so that it can be used as the next input. The resulting path of alternating vertical and horizontal segments is called a cobweb (or “tic-tac-toe” pattern).


![A whiteboard shows an example calculation for when a value doubles, and a graph illustrating a function F(x) and the line y=x.](frames/frame_12_920s.jpg)
*[15:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=920s) A whiteboard shows an example calculation for when a value doubles, and a graph illustrating a function F(x) and the line y=x.*


### Monotonic Convergence to the Equilibrium

In the logistic model with $0 < r \le 2$ and $K>0$, the cobweb diagram shows monotonic convergence to $K$ for initial conditions between $0$ and $K$ or above $K$.

- **Starting below $K$** (e.g., $X_0 < K$): The vertical segment from $X_0$ to the curve gives $X_1 > X_0$. The horizontal segment to the line $y=x$ then leads to a vertical segment that gives $X_2 > X_1$. Each iterate increases, and the cobweb “wedges” into the equilibrium point $K$ from below. The sequence $X_n$ increases monotonically toward $K$.

- **Starting above $K$** (e.g., $X_0 > K$): The first vertical segment gives $X_1 < X_0$ (because the curve lies below the line $y=x$ for $x>K$). The subsequent steps produce decreasing iterates, and the cobweb wedges into $K$ from above. The sequence $X_n$ decreases monotonically toward $K$.

In both cases, the population approaches the carrying capacity without oscillating. This behavior is called **monotonic convergence**. The cobweb diagram makes the direction and stability of the equilibrium visually obvious.

### Summary of Key Concepts

- **Equilibrium point**: A value $X^*$ such that $F(X^*) = X^*$. For the logistic map, $X^* = 0$ and $X^* = K$.
- **Cobweb diagram**: A graphical iteration method that alternates vertical moves to the function curve and horizontal moves to the line $y=x$.
- **Monotonic convergence**: The sequence $X_n$ steadily increases or decreases toward an equilibrium, never crossing it.

### Check Your Understanding

1. **What are the two equilibrium points of the logistic map $X_{n+1} = X_n + r X_n (1 - X_n/K)$?**  
   <details><summary>Answer</summary>  
   $X=0$ and $X=K$ (the carrying capacity).  
   </details>

2. **Describe the first two steps of constructing a cobweb diagram starting from an initial condition $X_0$.**  
   <details><summary>Answer</summary>  
   Step 1: From $X_0$ on the x-axis, draw a vertical line up to the curve $y=F(x)$ to obtain $X_1 = F(X_0)$.  
   Step 2: From that point, draw a horizontal line to the line $y=x$ to obtain the point $(X_1, X_1)$.  
   </details>

3. **What is the role of the line $y=x$ in a cobweb diagram?**  
   <details><summary>Answer</summary>  
   The line $y=x$ allows you to transfer the output value $X_{n+1}$ from the y-axis back to the x-axis so that it can be used as the next input. It acts as a mirror for the iteration.  
   </details>

4. **If the initial population $X_0$ is below the carrying capacity $K$, what does the cobweb diagram show about the population’s long-term behavior?**  
   <details><summary>Answer</summary>  
   The cobweb diagram shows that the population increases monotonically and converges to $K$ from below. Each iterate is larger than the previous one, and the path wedges into the equilibrium point $K$.  
   </details>
## Oscillatory Convergence and Overshooting

In the previous section, you saw a cobweb diagram where the population converged smoothly to the carrying capacity $K$ from below. The population always stayed below $K$ as it approached. This section shows that this smooth approach is not the only possible behavior. When the growth rate $r$ is larger, the population can overshoot the carrying capacity and then oscillate as it converges.

### The Role of the Growth Rate $r$

The key parameter that determines the behavior of the discrete logistic map is the growth rate $r$. The carrying capacity $K$ remains an equilibrium point regardless of the value of $r$. However, $r$ controls the slope of the function $F(x)$ at the origin and determines where the equilibrium point $K$ lies on the curve.


![A whiteboard shows an example of population growth calculation and a graph illustrating a function F(x) and its iteration.](frames/frame_13_1120s.jpg)
*[18:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1120s) A whiteboard shows an example of population growth calculation and a graph illustrating a function F(x) and its iteration.*


The function you are iterating is:

$$F(x) = x + r x \left(1 - \frac{x}{K}\right)$$

This is the discrete logistic map. The equilibrium point $x = K$ satisfies $F(K) = K$.

### Constructing the Cobweb Diagram for a Larger $r$

When $r$ is larger, the function $F(x)$ rises higher before curving back down to cross the line $y = x$ at $x = K$.


![This frame shows a whiteboard with mathematical equations and a graph illustrating population growth and doubling time, along with a diagram of a...](frames/frame_14_1160s.jpg)
*[19:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1160s) This frame shows a whiteboard with mathematical equations and a graph illustrating population growth and doubling time, along with a diagram of a cobweb plot.*


To construct the cobweb diagram, follow these steps:

1.  **Start with an initial population** $x_0$ that is small (a "little bit of yeast").
2.  **Move vertically** from $(x_0, x_0)$ up to the curve $F(x)$. This gives you the point $(x_0, F(x_0)) = (x_0, x_1)$.
3.  **Move horizontally** from $(x_0, x_1)$ to the line $y = x$. This gives you the point $(x_1, x_1)$.
4.  **Move vertically** from $(x_1, x_1)$ up to the curve $F(x)$. This gives you the point $(x_1, F(x_1)) = (x_1, x_2)$.
5.  **Repeat**: Continue alternating between vertical moves to the curve and horizontal moves to the line $y = x$.


![A whiteboard shows mathematical equations for population growth and a graphical representation of a function F(x) and y=x.](frames/frame_15_1200s.jpg)
*[20:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1200s) A whiteboard shows mathematical equations for population growth and a graphical representation of a function F(x) and y=x.*


This process traces out the cobweb diagram. Each vertical move computes the next population value, and each horizontal move prepares the next iteration.

### Observing Overshooting

With a larger $r$, the steps between successive population values become larger. The population grows so quickly that it overshoots the carrying capacity $K$.

Here is the sequence of events as shown in the cobweb diagram:

1.  Starting from a small $x_0$, the population grows toward $K$.
2.  At some step, the population value crosses above $K$. This is the overshoot.
3.  Because the population is now above $K$, the growth rate becomes negative (crowding). The population contracts.
4.  The contraction brings the population back below $K$.
5.  Because the population is below $K$, growth resumes, and the population overshoots again.


![This frame shows mathematical equations for population growth and two graphs illustrating the behavior of a function F(x) and its relation to y=x...](frames/frame_16_1360s.jpg)
*[22:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1360s) This frame shows mathematical equations for population growth and two graphs illustrating the behavior of a function F(x) and its relation to y=x, with a cobweb plot.*


This creates a pattern where the population alternates between being above and below $K$ at each time step. The cobweb diagram shows a "spiraling" motion around the equilibrium point $K$.

### Oscillatory Convergence

The population does not diverge. Instead, it converges to $K$ through a series of oscillations. Each oscillation is smaller than the previous one, so the population gradually settles into the equilibrium.

This behavior is analogous to the case of a linear difference equation $x_{n+1} = \lambda x_n$ when $\lambda$ is between -1 and 0. In that case, the population alternates sign (positive to negative) while converging to zero. Here, the population alternates between being above and below $K$ while converging to $K$.

The process can be summarized as:

- **Too many**: Population above $K$ causes contraction.
- **Room to grow**: Population below $K$ causes expansion.
- **Overshoot**: Expansion is so strong that it pushes the population above $K$ again.
- **Repeat**: The cycle continues until the population settles at $K$.

The growth rate $r$ is the controlling factor. A larger $r$ leads to larger overshoots and more pronounced oscillations. The specific value of $r$ in this example is not given; the purpose is to show the qualitative behavior of oscillatory convergence.

### Check Your Understanding

1.  What is the key difference between the smooth convergence shown earlier and the oscillatory convergence shown in this section?

<details><summary>Answer</summary>
In smooth convergence, the population always stays below the carrying capacity $K$ as it approaches. In oscillatory convergence, the population overshoots $K$ and then alternates between being above and below $K$ while converging.
</details>

2.  What parameter controls whether the population overshoots the carrying capacity?

<details><summary>Answer</summary>
The growth rate $r$. A larger $r$ causes the population to take larger steps from one time point to the next, leading to overshooting.
</details>

3.  In the cobweb diagram, what does a horizontal move represent?

<details><summary>Answer</summary>
A horizontal move from the curve $F(x)$ to the line $y = x$ represents setting the current population value as the input for the next iteration. It moves from $(x_n, x_{n+1})$ to $(x_{n+1}, x_{n+1})$.
</details>

4.  Does the carrying capacity $K$ change when $r$ is increased?

<details><summary>Answer</summary>
No. The carrying capacity $K$ remains an equilibrium point regardless of the value of $r$. Changing $r$ changes the dynamics (how the population approaches $K$), but not the equilibrium value itself.
</details>
## Chaos and Complex Dynamics at High Growth Rates

As the growth rate $r$ increases, the behavior of the discrete logistic model changes dramatically. For moderate $r$ values, the population settles into a stable equilibrium or a periodic cycle. When $r$ becomes very large, the dynamics become **chaotic**: the population never settles, and its future values appear random even though the rule is deterministic.

### The Logistic Map Equation

The discrete logistic model is given by

$$
X_{n+1} = X_n + r X_n \left(1 - \frac{X_n}{K}\right)
$$

where $X_n$ is the population at time step $n$, $r$ is the intrinsic growth rate, and $K$ is the carrying capacity. This equation is the function $f(x)$ used to construct cobweb diagrams.


![This frame shows mathematical equations and graphs related to population growth models, including an example calculation for population doubling...](frames/frame_17_1480s.jpg)
*[24:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1480s) This frame shows mathematical equations and graphs related to population growth models, including an example calculation for population doubling time and two graphical representations of logistic growth.*


The whiteboard shows this equation alongside an exponential growth example. The logistic map is the core of the cobweb construction.

### Cobweb Diagram for Very Large $r$

When $r$ is huge (e.g., $r = 4$ or $6$, depending on $K$), the cobweb diagram reveals chaotic behavior. The steps are:

1. Start with a small initial population $X_0$.
2. Move vertically to the curve $f(x)$ to find $X_1 = f(X_0)$.
3. Move horizontally to the diagonal line $y = x$ to set the next input.
4. Repeat.

Because $r$ is large, the population makes enormous jumps from one step to the next. It overshoots the carrying capacity, then crashes far below it, then overshoots again, and so on. The cobweb never converges to a fixed point or a cycle; it fills the diagram with a seemingly random tangle of lines.


![This frame shows mathematical equations for population growth and two cobweb diagrams illustrating the behavior of functions.](frames/frame_18_1580s.jpg)
*[26:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1580s) This frame shows mathematical equations for population growth and two cobweb diagrams illustrating the behavior of functions.*


The whiteboard shows the same logistic equation and two cobweb diagrams. The right diagram illustrates the chaotic regime: the lines crisscross without settling.

### Characteristics of Chaos in This Model

- **No stable equilibrium**: The fixed points (e.g., $X = K$) no longer attract the population. The cobweb does not spiral into them.
- **Sensitive dependence**: Tiny changes in initial conditions lead to completely different future sequences.
- **Bounded but aperiodic**: The population stays between 0 and $K$ but never repeats exactly.
- **Seemingly random**: The sequence of population values appears unpredictable, even though it is generated by a simple deterministic rule.


![This frame shows mathematical equations and graphs related to population growth models, including an example calculation for when a population...](frames/frame_19_1640s.jpg)
*[27:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1640s) This frame shows mathematical equations and graphs related to population growth models, including an example calculation for when a population doubles.*


The whiteboard repeats the logistic equation. The chaotic cobweb diagram (right) shows the population bouncing between high and low values without settling.

### Interactive Exploration

The video provides a link to a website that draws cobweb diagrams interactively. To explore the transition to chaos:

- Set $K = 1$ (or any fixed carrying capacity).
- Start with a small $r$ (e.g., $r = 0.1$) and observe monotonic convergence to $K$.
- Gradually increase $r$. Notice the **tipping point** where the dynamics change from monotonic to oscillatory (overcompensatory growth) and eventually to chaos.
- For very large $r$ (e.g., $r = 4$), the cobweb fills the diagram with no pattern.


![A whiteboard shows mathematical equations for population growth and a graphical representation of the logistic map.](frames/frame_20_1680s.jpg)
*[28:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1680s) A whiteboard shows mathematical equations for population growth and a graphical representation of the logistic map.*


The whiteboard again shows the logistic equation. The chaotic cobweb diagram (right) demonstrates that the equilibrium points no longer absorb the population.

### Why Chaos Occurs

The growth rate $r$ controls the steepness of the logistic curve. When $r$ is large, the curve rises steeply near $X=0$ and then drops sharply near $X=K$. This steepness causes the population to overshoot the carrying capacity by a wide margin. The subsequent correction is also extreme, leading to a perpetual cycle of overshoot and crash. The system never settles because the jumps are too large to be damped.


![This frame shows a whiteboard with mathematical equations for population growth and related graphs, including a logistic map diagram.](frames/frame_21_1720s.jpg)
*[28:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1720s) This frame shows a whiteboard with mathematical equations for population growth and related graphs, including a logistic map diagram.*


The whiteboard shows the logistic equation and a chaotic cobweb diagram. The population wanders between large and small values, never repeating.

### Mermaid Diagram: Cobweb Iteration Process

The following flowchart summarizes the iterative process used to draw a cobweb diagram:

```mermaid
flowchart TD
    A[Start with X_n] --> B[Compute X_{n+1} = f(X_n)]
    B --> C[Draw vertical line from (X_n, X_n) to (X_n, X_{n+1})]
    C --> D[Draw horizontal line from (X_n, X_{n+1}) to (X_{n+1}, X_{n+1})]
    D --> E[Set X_n = X_{n+1}]
    E --> B
```

This process is repeated for many steps. In the chaotic regime, the lines never converge to a single point.

### Check Your Understanding

1. What is the key difference between the cobweb diagram for a stable equilibrium and the cobweb diagram for chaos?

<details><summary>Answer</summary>
For a stable equilibrium, the cobweb spirals inward toward a fixed point. For chaos, the cobweb never settles; it fills the diagram with a tangle of lines that do not converge.
</details>

2. Why does a very large growth rate $r$ lead to chaotic behavior in the logistic model?

<details><summary>Answer</summary>
A large $r$ makes the logistic curve very steep. This causes the population to overshoot the carrying capacity by a large amount, then crash far below it, then overshoot again. The jumps are too large to be damped, so the system never settles into a fixed point or cycle.
</details>

3. In the interactive website described, what parameter should you fix and what parameter should you vary to observe the transition to chaos?

<details><summary>Answer</summary>
Fix the carrying capacity $K$ (e.g., set $K = 1$). Vary the growth rate $r$ from small values (e.g., 0.1) to large values (e.g., 4 or 6) and observe the changes in the cobweb diagram.
</details>

4. True or False: In a chaotic dynamical system, the future population is completely unpredictable because the rule is random.

<details><summary>Answer</summary>
False. The rule is deterministic (the logistic map equation). The unpredictability arises from sensitive dependence on initial conditions, not from randomness.
</details>
## Real Data Application and Course Conclusion

In 1913, the German researcher Carlson collected data on yeast populations. That data was the original source for the simple exponential growth model you saw earlier in the course, where the population grew by 10% each hour. The 10% growth rate per time step (hour to hour) came directly from Carlson’s observations.

However, a pure exponential model does not account for limited resources. When Carlson’s data is fitted to a **logistic growth model** (a model that includes a carrying capacity), a more accurate iteration scheme emerges. The logistic model is written as:

$$
X_{n+1} = X_n + r X_n \left(1 - \frac{X_n}{K}\right)
$$

where $r$ is the intrinsic growth rate and $K$ is the carrying capacity. Fitting Carlson’s data to this form gives the specific iteration scheme:

$$
X_{n+1} = 1.56\,X_n - 0.000861\,X_n^2
$$


![This frame shows a whiteboard with mathematical equations and graphs related to population growth models, including an example calculation for...](frames/frame_22_1800s.jpg)
*[30:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1800s) This frame shows a whiteboard with mathematical equations and graphs related to population growth models, including an example calculation for when a population doubles and a logistic growth model.*


The whiteboard at this timestamp shows the derivation from the general logistic equation to this numerical scheme. Compare the fitted equation with the standard logistic form:

$$
X_{n+1} = (1+r) X_n - \frac{r}{K} X_n^2
$$

By matching coefficients, you obtain:

- $1 + r = 1.56$  →  $r = 0.56$
- $\frac{r}{K} = 0.000861$  →  $K = \frac{0.56}{0.000861} \approx 650.4$

Thus, the intrinsic growth rate $r$ is 0.56 (56% per hour) and the carrying capacity $K$ is approximately 650.4 (in the same units as the population count). These are explicit, real-world values derived from actual data.

Now you can use these values to construct a **cobweb diagram** for the logistic map $F(x) = 1.56x - 0.000861x^2$. A cobweb diagram is a graphical tool that shows the iteration of a discrete dynamical system: you plot the function $F(x)$ and the line $y=x$, then start from an initial population $X_0$, draw a vertical line to the curve, then a horizontal line to the diagonal, and repeat. This visualizes the population’s trajectory over time.

The following flowchart summarizes the process from data to cobweb analysis:

```mermaid
flowchart TD
    A[Carlson's 1913 yeast data] --> B[Fit logistic model]
    B --> C[Obtain X_{n+1} = 1.56 X_n - 0.000861 X_n^2]
    C --> D[Identify r = 0.56, K ≈ 650.4]
    D --> E[Construct cobweb diagram for F(x)]
    E --> F[Iterate and observe population behavior]
```

As a final exercise, draw the cobweb diagram for this map using the values of $r$ and $K$ above. Ask yourself: if you were Carlson observing the yeast population in 1913, what would the population do over time according to this model? Would it approach a stable equilibrium, oscillate, or behave chaotically? The answer depends on the value of $r$ (0.56) relative to the known thresholds for the logistic map. (Recall that for $0 < r \leq 2$, the population tends to a stable fixed point; for $2 < r < \sqrt{5} \approx 2.236$, it may exhibit period-doubling; for larger $r$, chaos can appear. Here $r=0.56$ is well within the stable regime, so the population should converge to the carrying capacity $K$.)

This concludes the course. You now have the tools to analyze discrete dynamical systems graphically using cobweb diagrams and to connect them to real-world data.

### Check your understanding

1. What are the values of $r$ and $K$ obtained from fitting Carlson’s yeast data to the logistic model?  
   <details><summary>Answer</summary>  
   $r = 0.56$, $K \approx 650.4$  
   </details>

2. Write the iteration scheme for the yeast population in the form $X_{n+1} = (1+r)X_n - \frac{r}{K}X_n^2$ using the fitted values.  
   <details><summary>Answer</summary>  
   $X_{n+1} = 1.56 X_n - 0.000861 X_n^2$  
   </details>

3. If you draw a cobweb diagram for this map starting from a small initial population, what long-term behavior do you expect? Explain briefly.  
   <details><summary>Answer</summary>  
   The population should converge to the stable fixed point at $X = K \approx 650.4$ because $r = 0.56$ is less than 2, which is the threshold for stability in the logistic map.  
   </details>

4. Why is the logistic model more realistic than the simple exponential model for Carlson’s yeast data?  
   <details><summary>Answer</summary>  
   The exponential model assumes unlimited growth, but real populations are limited by resources. The logistic model includes a carrying capacity $K$, which caps the population size and better matches observed data.  
   </details>
## Key takeaways

- Discrete time dynamical systems model populations at discrete time steps using difference equations like $X_{n+1} = F(X_n)$.
- Exponential growth models assume a constant relative growth rate, leading to explicit solutions $X_n = (1+r)^n X_0$ but are unrealistic because they allow unbounded growth.
- Logistic growth models incorporate a carrying capacity $K$, making the growth rate density dependent and the difference equation nonlinear: $X_{n+1} = X_n + r X_n (1 - X_n/K)$.
- Cobweb diagrams graphically iterate a one-dimensional map by plotting $F(x)$ and the line $y=x$, then tracing vertical and horizontal lines to visualize the sequence of states.
- Equilibria of a discrete dynamical system are found where $F(x)=x$; for the logistic model these are $x=0$ and $x=K$.
- The stability of an equilibrium depends on the growth rate $r$: small $r$ yields monotonic convergence, moderate $r$ yields oscillatory convergence, and large $r$ can lead to chaos.
- Chaotic dynamics in the logistic map produce aperiodic, seemingly random behavior that is sensitive to initial conditions, visible as a dense cobweb that never settles.
- Real data, such as Carlson's 1913 yeast experiment, can be fitted to a logistic model, allowing students to apply cobweb analysis to actual population measurements.
- Graphical methods like cobweb diagrams are essential when explicit solutions are unavailable, providing qualitative insight into nonlinear discrete systems.
## Glossary

| Term | Definition |
|---|---|
| discrete time dynamical system | A system where the state evolves at discrete time steps according to a rule $X_{n+1} = F(X_n)$, where $n$ is an integer index. |
| difference equation | An equation that relates the value of a variable at one time step to its value at the previous step, e.g., $X_{n+1} = 1.1 X_n$. |
| state space | The set of all possible values of the system variable; for one-dimensional systems it is a subset of $\mathbb{R}$. |
| relative growth rate | The change in population per unit time divided by the current population, $r(n) = \frac{\Delta X_n}{X_n}$. |
| carrying capacity | The maximum population size that the environment can sustain indefinitely, denoted $K$. |
| logistic map | A nonlinear difference equation of the form $X_{n+1} = X_n + r X_n (1 - X_n/K)$ or its scaled version $x_{n+1} = r x_n (1 - x_n)$. |
| cobweb diagram | A graphical tool for iterating a one-dimensional map: plot $y=F(x)$ and $y=x$, then draw vertical and horizontal lines to trace the sequence $X_0, X_1, X_2, \dots$. |
| equilibrium (fixed point) | A state $X^*$ such that $F(X^*) = X^*$; if the system reaches this state it remains there forever. |
| stability | A property of an equilibrium: if nearby initial conditions converge to it, the equilibrium is stable (attracting); if they move away, it is unstable. |
| monotonic convergence | A sequence that approaches an equilibrium from one side without crossing it, typical for small growth rates in the logistic model. |
| oscillatory convergence | A sequence that alternates above and below an equilibrium while gradually approaching it, typical for moderate growth rates. |
| chaos | Aperiodic, bounded dynamics that are sensitive to initial conditions, occurring in the logistic map for sufficiently large $r$. |
| sensitive dependence on initial conditions | A hallmark of chaos where arbitrarily small differences in initial state lead to exponentially diverging trajectories. |
| iteration | Repeated application of the update function $F$ to generate the sequence $X_0, X_1 = F(X_0), X_2 = F(X_1), \dots$. |
| explicit solution | A closed-form formula for $X_n$ as a function of $n$ and initial condition, possible only for simple linear difference equations. |
| nonlinear | A function or equation that is not linear; the logistic map is nonlinear because it contains $X_n^2$. |
| phase line | A graphical method for one-dimensional continuous dynamical systems; the cobweb diagram is its discrete analog. |
| update function | The function $F(x)$ that maps the current state to the next state in a discrete dynamical system. |
| doubling time | The time required for a population to double in size under exponential growth, computed as $\frac{\ln 2}{\ln(1+r)}$. |
| Carlson's yeast model | A logistic model fitted to 1913 yeast data: $X_{n+1} = 1.56 X_n - 0.00086 X_n^2$, giving $r=0.56$ and $K \approx 650.4$. |
## Footnotes and deeper context

1. **Logistic map parameterization.** The video uses $X_{n+1} = X_n + r X_n (1 - X_n/K)$, which is equivalent to the standard logistic map $x_{n+1} = R x_n (1 - x_n)$ after scaling $x = X/K$ and setting $R = 1+r$. In the standard form, chaos occurs for $R > 3.57$; in the video's form, chaos appears for $r$ roughly above 2.57 (since $R = 1+r$).
2. **Explicit solution for exponential growth.** The explicit solution $X_n = (1+r)^n X_0$ is derived by repeated multiplication. The doubling time formula $n = \ln 2 / \ln(1+r)$ is exact for continuous $n$; for discrete steps the population doubles at the first integer $n$ where $(1+r)^n \ge 2$.
3. **Cobweb diagram construction.** The cobweb diagram works for any one-dimensional map $F$. Starting at $(X_0, X_0)$ on the line $y=x$, move vertically to $(X_0, F(X_0))$, then horizontally to $(F(X_0), F(X_0))$ on $y=x$, then vertically again. This process generates the sequence $X_1, X_2, \dots$.
4. **Stability condition for logistic map.** For the map $F(x) = x + r x (1 - x/K)$, the derivative at $x=K$ is $F'(K) = 1 - r$. The equilibrium $K$ is stable when $|1 - r| < 1$, i.e., $0 < r < 2$. Monotonic convergence occurs for $0 < r < 1$, oscillatory convergence for $1 < r < 2$, and instability (leading to cycles or chaos) for $r > 2$.
5. **Carlson's 1913 data.** The German researcher T. Carlson published yeast population measurements in 1913. The fitted model $X_{n+1} = 1.56 X_n - 0.00086 X_n^2$ yields $r=0.56$ and $K \approx 650.4$. With $r < 1$, the dynamics are monotonic convergence to $K$, consistent with the data.
6. **Sensitive dependence in chaos.** In chaotic regimes, tiny rounding errors in initial conditions or in the iteration process lead to completely different long-term trajectories. This makes long-term prediction impossible even though the model is deterministic.
## Where to go next

- **Logistic map on Wikipedia.** A comprehensive article covering the standard logistic map, bifurcation diagram, period-doubling route to chaos, and Lyapunov exponents. Useful for connecting the video's parameterization to the more common form.
- **Online cobweb diagram applet.** Interactive tools like 'Cobweb Plotter' (e.g., from Geogebra or Desmos) allow you to adjust $r$ and $K$ and see the cobweb in real time. The video mentions a link in its description; searching for 'cobweb diagram logistic map' will yield similar resources.
- **Strogatz, Nonlinear Dynamics and Chaos (Chapter 10).** This textbook provides a clear introduction to one-dimensional maps, cobweb diagrams, and the logistic map. It includes exercises on stability analysis and the period-doubling cascade.
- **Carlson's original paper.** T. Carlson, 'Uber Geschwindigkeit und Grösse der Hefevermehrung in Würze', Biochemische Zeitschrift 57 (1913), 313-334. The original data source for the yeast model discussed in the video.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
