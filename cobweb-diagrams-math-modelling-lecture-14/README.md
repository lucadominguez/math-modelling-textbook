# Cobweb Diagrams - Math Modelling - Lecture 14
> **Source:** [Cobweb Diagrams - Math Modelling - Lecture 14](https://www.youtube.com/watch?v=1hCX5Gbeo0E) by Math Modelling · 31:04 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
## Cobweb Diagrams - Math Modelling - Lecture 14

### 1. Introduction: One-Dimensional Difference Equations

This lecture focuses on **one-dimensional difference equations**, also called discrete time dynamical systems. In these systems, the state space contains only one variable. The goal is to understand how this variable evolves over discrete time steps.

The key graphical tool introduced here is the **cobweb diagram**, which serves a similar purpose for difference equations as the **phase line diagram** does for continuous time systems. Both methods help visualize the behavior of solutions without solving the equations explicitly.


![A mathematical example showing the formula for r(n) as the ratio of delta X(n) to X.](frames/frame_01_120s.jpg)
*[02:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=120s) A mathematical example showing the formula for r(n) as the ratio of delta X(n) to X.*


### 2. Example 1: Exponential Growth of Yeast

#### 2.1 Setting Up the Model

Consider a population of yeast growing at 10% per hour. The initial population is 100,000 cells when the clock starts. We check the population every hour, making this a discrete time system.

The **relative growth rate** \( r(n) \) is defined as the change in population divided by the current population:

\[
r(n) = \frac{\Delta X(n)}{X(n)}
\]

For this example, the relative growth rate is constant at 10%:

\[
r(n) = \frac{\Delta X(n)}{X(n)} = 0.1
\]

Rearranging gives:

\[
\Delta X(n) = 0.1 X(n)
\]


![A whiteboard shows an example equation for r(n) and its derived form for ΔX(n).](frames/frame_02_180s.jpg)
*[03:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=180s) A whiteboard shows an example equation for r(n) and its derived form for ΔX(n).*


#### 2.2 The Difference Equation

Since \(\Delta X(n) = X(n+1) - X(n)\), we can write:

\[
X(n+1) - X(n) = 0.1 X(n)
\]

\[
X(n+1) = 1.1 X(n)
\]

With the initial condition:

\[
X(0) = 100{,}000
\]


![An example problem is shown on a whiteboard, defining r(n) as the change in X(n) over X(n) which equals 0.1, leading to X(n+1) = 1.1 X(n) with an...](frames/frame_03_220s.jpg)
*[03:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=220s) An example problem is shown on a whiteboard, defining r(n) as the change in X(n) over X(n) which equals 0.1, leading to X(n+1) = 1.1 X(n) with an initial value of X(0) = 100,000.*


#### 2.3 Explicit Solution

This simple linear difference equation has an explicit solution:

\[
X(n) = (1.1)^n \cdot 100{,}000
\]

Here, 1.1 plays the role of the growth factor per time step.


![A whiteboard shows an example calculation for exponential growth, starting with r(n) = ΔX(n)/X(n) = 0.1 and leading to X(n) = (1.1)^n * 100,000...](frames/frame_04_280s.jpg)
*[04:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=280s) A whiteboard shows an example calculation for exponential growth, starting with r(n) = ΔX(n)/X(n) = 0.1 and leading to X(n) = (1.1)^n * 100,000, with a prompt to calculate X(4).*


#### 2.4 Population After 4 Hours

To find the population after 4 hours:

\[
X(4) = (1.1)^4 \cdot 100{,}000 = 146{,}410
\]

The population increased by 46,410 cells over 4 hours.


![A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n+1) = 1.1x(n).](frames/frame_05_380s.jpg)
*[06:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=380s) A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n+1) = 1.1x(n).*


#### 2.5 Doubling Time

To find when the population doubles, solve:

\[
X(n) = 200{,}000
\]

\[
(1.1)^n \cdot 100{,}000 = 200{,}000
\]

\[
(1.1)^n = 2
\]

Using natural logarithms:

\[
n = \frac{\ln(2)}{\ln(1.1)} \approx 7.27
\]

Since we only check at discrete hourly intervals, we must wait until the 8th hour. At hour 7, the population has not yet doubled; at hour 8, it has exceeded double the initial population.

**Key point:** In a discrete time system, the answer must be an integer number of time steps. The continuous time answer of 7.27 hours does not apply here.


![A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n) = (1.1)^n * 100,000.](frames/frame_06_500s.jpg)
*[08:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=500s) A whiteboard shows an example problem calculating population growth and doubling time using the formula x(n) = (1.1)^n * 100,000.*


### 3. A More Realistic Model: Logistic Growth

#### 3.1 Limitations of Exponential Growth

The exponential model predicts unbounded growth. According to this model, the yeast population could reach a million, a billion, or even a trillion cells. This is unrealistic because there is internal competition for resources and space.

#### 3.2 Introducing Carrying Capacity

We modify the growth rate so that it decreases as the population increases. The **carrying capacity** \( K \) represents the maximum population that can be supported in the environment (for example, in a petri dish).

The modified relative growth rate becomes:

\[
\frac{\Delta X(n)}{X(n)} = r \left(1 - \frac{X(n)}{K}\right)
\]

When \( X(n) < K \), the growth rate is positive and the population grows. When \( X(n) > K \), the growth rate is negative and the population shrinks.


![A whiteboard shows an example calculation for population growth and doubling time using the formula r(n) = Δx(n)/x(n) = 0.1.](frames/frame_09_640s.jpg)
*[10:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=640s) A whiteboard shows an example calculation for population growth and doubling time using the formula r(n) = Δx(n)/x(n) = 0.1.*


#### 3.3 The Logistic Difference Equation

Rearranging gives the **logistic difference equation**:

\[
X(n+1) = X(n) + r X(n) \left(1 - \frac{X(n)}{K}\right)
\]

This is a quadratic function in \( X(n) \), making it nonlinear. Unlike the exponential model, this equation cannot be solved explicitly. We need graphical methods to understand its behavior.


![A whiteboard shows an example of population growth calculation, including solving for when the population doubles.](frames/frame_10_700s.jpg)
*[11:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=700s) A whiteboard shows an example of population growth calculation, including solving for when the population doubles.*


### 4. The Cobweb Diagram Method

#### 4.1 Setting Up the Graph

To create a cobweb diagram, we plot two functions on the same axes:

1. The function \( F(X) = X + rX\left(1 - \frac{X}{K}\right) \), which represents the right-hand side of the difference equation
2. The line \( Y = X \), which serves as a reference


![A whiteboard shows mathematical equations for population growth and a graph of F(x) versus x.](frames/frame_11_840s.jpg)
*[14:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=840s) A whiteboard shows mathematical equations for population growth and a graph of F(x) versus x.*


#### 4.2 Finding Equilibrium Points

The **equilibrium points** occur where the two curves intersect, that is, where \( F(X) = X \). At these points, there is no change in the system: \(\Delta X = 0\).

For the logistic equation, there are two equilibrium points:
- \( X = 0 \) (the trivial equilibrium, no population)
- \( X = K \) (the carrying capacity)

If the population is exactly at the carrying capacity, it neither increases nor decreases. If there is no population, reproduction cannot occur.


![The whiteboard shows an example calculation for when a value doubles, and a graph illustrating a function F(x) and the line y=x.](frames/frame_12_920s.jpg)
*[15:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=920s) The whiteboard shows an example calculation for when a value doubles, and a graph illustrating a function F(x) and the line y=x.*


#### 4.3 Constructing the Cobweb

The cobweb diagram is constructed by an iterative process:

1. Start at the initial condition \( X(0) \) on the x-axis
2. Trace vertically up to the curve \( F(X) \). The y-coordinate at this point is \( X(1) \)
3. Trace horizontally to the line \( Y = X \). This transfers the value \( X(1) \) to the x-axis
4. Trace vertically up to the curve \( F(X) \) again. The y-coordinate is now \( X(2) \)
5. Repeat steps 3 and 4 to generate successive iterates

The resulting pattern of horizontal and vertical lines resembles a cobweb, giving the method its name.


![A whiteboard shows an example of population growth calculation and a graph illustrating the logistic map, with a student pointing to the graph.](frames/frame_13_1120s.jpg)
*[18:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1120s) A whiteboard shows an example of population growth calculation and a graph illustrating the logistic map, with a student pointing to the graph.*


### 5. Behavior for Different Growth Rates

#### 5.1 Small Growth Rate: Monotone Convergence

When \( r \) is small, the curve \( F(X) \) has a gentle slope. Starting from a small initial population:

- The population increases each step
- It approaches the carrying capacity from below
- It never overshoots \( K \)

Similarly, starting from a population above \( K \):
- The population decreases each step
- It approaches \( K \) from above

In both cases, \( X(n) \) converges monotonically to \( K \).


![This frame shows a whiteboard with mathematical equations and a graph related to population dynamics, including an example calculation for...](frames/frame_14_1160s.jpg)
*[19:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1160s) This frame shows a whiteboard with mathematical equations and a graph related to population dynamics, including an example calculation for population doubling time and a diagram illustrating a cobweb plot.*


#### 5.2 Moderate Growth Rate: Oscillatory Convergence

When \( r \) is larger, the curve rises higher before falling. Starting from a small population:

- The population grows rapidly
- It overshoots the carrying capacity
- The next step, the population contracts below \( K \)
- Then it grows again, overshooting again

This creates an oscillation around \( K \). The population alternates between being above and below the carrying capacity, but the oscillations decrease in amplitude. Eventually, \( X(n) \) converges to \( K \), but through a damped oscillation rather than monotone approach.


![This frame shows mathematical equations and graphs related to population growth and logistic models, including calculations for population...](frames/frame_15_1200s.jpg)
*[20:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1200s) This frame shows mathematical equations and graphs related to population growth and logistic models, including calculations for population doubling time.*


#### 5.3 Large Growth Rate: Chaos

When \( r \) is very large, the behavior becomes chaotic:

- The population makes enormous jumps from step to step
- It constantly overshoots and then contracts
- The system never settles into a stable equilibrium
- The population appears to wander randomly between large and small values

In this regime, the cobweb diagram becomes so dense with lines that it fills in completely. The system is said to exhibit **chaos**: deterministic behavior that appears random because of extreme sensitivity to initial conditions.


![This frame shows mathematical equations for population growth and two graphs illustrating the behavior of X(n) approaching K.](frames/frame_16_1360s.jpg)
*[22:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1360s) This frame shows mathematical equations for population growth and two graphs illustrating the behavior of X(n) approaching K.*


### 6. Summary of Cobweb Behaviors

| Growth Rate \( r \) | Behavior | Cobweb Pattern |
|---------------------|----------|----------------|
| Small | Monotone convergence to \( K \) | Spirals inward from one side |
| Moderate | Oscillatory convergence to \( K \) | Alternates above and below \( K \), amplitude decreases |
| Large | Chaos, no convergence | Lines fill the diagram, no pattern |


![This frame displays mathematical equations and graphs related to population growth models, including an example calculation for population...](frames/frame_17_1480s.jpg)
*[24:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1480s) This frame displays mathematical equations and graphs related to population growth models, including an example calculation for population doubling time and a graphical representation of logistic growth.*


### 7. Real Data: Carlson's Yeast Experiment

In 1913, the German researcher Carlson collected data on yeast populations. This data motivated the exponential growth model with 10% growth per hour.

Fitting Carlson's data to the logistic model gives specific parameter values:

\[
X(n+1) = 1.56 X(n) - 0.000861 X(n)^2
\]

From this equation, we can identify:
- \( r = 0.56 \) (the intrinsic growth rate)
- \( K \approx 650.4 \) (the carrying capacity)


![This frame shows mathematical equations for population growth and two diagrams illustrating cobweb plots for analyzing the stability of fixed...](frames/frame_18_1580s.jpg)
*[26:20](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1580s) This frame shows mathematical equations for population growth and two diagrams illustrating cobweb plots for analyzing the stability of fixed points in discrete dynamical systems.*


You can use these values to construct a cobweb diagram and observe what the model predicts for Carlson's yeast population. The behavior will depend on whether \( r = 0.56 \) falls in the monotone convergence, oscillatory convergence, or chaotic regime.


![A whiteboard shows mathematical equations for population growth and related graphs, including a cobweb plot.](frames/frame_20_1680s.jpg)
*[28:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1680s) A whiteboard shows mathematical equations for population growth and related graphs, including a cobweb plot.*


### 8. Interactive Exploration

To explore cobweb diagrams yourself, use an online cobweb diagram generator. Set \( K = 1 \) and systematically increase \( r \):

1. For small \( r \), observe monotone convergence
2. Find the tipping point where oscillations begin
3. Continue increasing \( r \) to see chaotic behavior

Try different initial conditions, including values very close to zero, and observe how the long-term behavior changes.


![This frame shows a whiteboard with mathematical equations and graphs related to population dynamics, including examples of exponential growth and...](frames/frame_21_1720s.jpg)
*[28:40](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1720s) This frame shows a whiteboard with mathematical equations and graphs related to population dynamics, including examples of exponential growth and logistic growth models.*


### 9. Key Takeaways

1. **Cobweb diagrams** provide a graphical method to analyze one-dimensional difference equations without solving them explicitly
2. **Equilibrium points** are found where \( F(X) = X \), that is, where the update function crosses the line \( Y = X \)
3. The **growth rate \( r \)** determines the qualitative behavior: monotone convergence, oscillatory convergence, or chaos
4. The **carrying capacity \( K \)** always remains an equilibrium point regardless of \( r \)
5. The logistic difference equation \( X(n+1) = X(n) + rX(n)(1 - X(n)/K) \) models population growth with limited resources


![This frame shows a whiteboard with mathematical equations and graphs related to population growth models, including an example calculation for...](frames/frame_22_1800s.jpg)
*[30:00](https://www.youtube.com/watch?v=1hCX5Gbeo0E&t=1800s) This frame shows a whiteboard with mathematical equations and graphs related to population growth models, including an example calculation for when a population doubles and a logistic growth model.*


### Check Your Understanding

**Question 1:** For the exponential growth model \( X(n+1) = 1.1 X(n) \) with \( X(0) = 100{,}000 \), why must we wait until hour 8 for the population to double, even though the calculation gives \( n \approx 7.27 \)?

<details>
<summary>Answer</summary>
The system is discrete: we only observe the population at integer hours. At hour 7, the population is \( (1.1)^7 \cdot 100{,}000 \approx 194{,}872 \), which is less than 200,000. At hour 8, the population is \( (1.1)^8 \cdot 100{,}000 \approx 214{,}359 \), which exceeds 200,000. Since we cannot check at fractional hours, the first time we observe doubling is hour 8.
</details>

**Question 2:** In the logistic model \( X(n+1) = X(n) + rX(n)(1 - X(n)/K) \), what are the two equilibrium points and why?

<details>
<summary>Answer</summary>
The equilibrium points occur where \( X(n+1) = X(n) \), which means \( rX(n)(1 - X(n)/K) = 0 \). This gives \( X = 0 \) (no population, no reproduction possible) and \( X = K \) (population at carrying capacity, growth rate is zero). Both points are intersections of the curve \( F(X) \) with the line \( Y = X \).
</details>

**Question 3:** How does increasing the growth rate \( r \) change the behavior of the logistic map?

<details>
<summary>Answer</summary>
For small \( r \), the population converges monotonically to \( K \) from below or above. For moderate \( r \), the population overshoots \( K \) and oscillates around it with decreasing amplitude, eventually converging. For large \( r \), the system becomes chaotic: the population never settles, constantly jumping between values above and below \( K \) in a seemingly random pattern.
</details>

**Question 4:** What is the role of the line \( Y = X \) in constructing a cobweb diagram?

<details>
<summary>Answer</summary>
The line \( Y = X \) serves as a transfer mechanism. After computing \( X(n+1) = F(X(n)) \) on the y-axis, we trace horizontally to the line \( Y = X \). Since every point on this line has equal x and y coordinates, this transfers the value \( X(n+1) \) back to the x-axis, allowing us to continue the iteration process.
</details>
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
