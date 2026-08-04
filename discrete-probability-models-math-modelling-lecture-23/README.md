# Discrete Probability Models: From Basics to Optimization in a Diode Testing Problem
> **Source:** [Discrete Probability Models - Math Modelling - Lecture 23](https://www.youtube.com/watch?v=7c43WFHCRac) by Math Modelling · 29:50 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for learners who have a basic understanding of probability and want to apply discrete probability models to practical optimization problems in manufacturing.
## Learning objectives

After working through this document you can:

1. Define discrete probability models and their key components (random variable, probability distribution, expected value, independence)
2. Calculate expected values for discrete random variables using weighted sums
3. Model a real-world scenario (diode testing) using a discrete probability distribution
4. Construct an expected cost function and optimize it to find the minimum average cost
5. Interpret the optimal batch size in the context of the problem
6. Perform sensitivity analysis on model parameters and interpret the results
7. Explain the importance of sensitivity in probabilistic models for robustness
8. Distinguish between discrete and continuous probability models in the context of the lecture series
## Prerequisites

- Basic understanding of probability (random variables, probability distributions, expected value, independence)
- Familiarity with calculus (derivatives) for optimization
- Experience with mathematical modeling or optimization problems (helpful but not required)
## Introduction and Course Context

This section marks the beginning of the third major unit in your study of mathematical modeling. You have concluded your discussion of dynamic systems, which remains an open area of investigation, and now you will transition into probability models. Probability models incorporate many ideas from optimization and dynamical systems, and you will carry those concepts forward into stochastic (random) models.


![A mathematical expression X ∈ {x1, ..., xn}, n ≥ 1 is written on a dark background.](frames/frame_01_140s.jpg)
*[02:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=140s) A mathematical expression X ∈ {x1, ..., xn}, n ≥ 1 is written on a dark background.*


### The Cascading Structure of Mathematical Modeling

This transition mirrors what you did in the previous lecture on data fitting. In that lecture, you saw that all ideas developed for optimization could be carried over into data fitting. Now you will see a similar cascading effect: optimization ideas flow into dynamical systems, and those ideas then flow into probability models. This cascading structure is the unifying idea of applied mathematics: you use whatever tool is necessary for the job.

### Course Focus on Modeling

This is a course on mathematical modeling, not on dynamical systems. Therefore, you will discuss another aspect of mathematical modeling: discrete probability models. The course assumes you have some basic idea of how probabilities work from a mathematical perspective. However, this does not mean the instructor will skip introducing topics. Every piece you need will be explained, but the course will not go into full detail about certain aspects of probability theory because basic familiarity is assumed. As with everything in this class, the focus bends toward the modeling aspect. Probability here is the tool, but the goal is to do modeling.

### Review of Discrete Probability Basics

A random variable, denoted as X, is a variable whose possible values are numerical outcomes of a random phenomenon. A discrete probability distribution means that X can take on one of only finitely many states.

The on-screen text at 02:20 shows the mathematical expression:

```
X ∈ {x1, ..., xn}, n ≥ 1
```

This expression means:
- X is a random variable.
- X can take on values from the set {x1, x2, ..., xn}.
- The set contains n possible values, where n is greater than or equal to 1.
- Each xi represents a distinct possible outcome or state that X can assume.

(Added context: In a discrete probability model, each possible value xi has an associated probability P(X = xi) that is greater than or equal to 0, and the sum of all probabilities equals 1.)

### Check your understanding

1. What is the relationship between optimization, dynamical systems, and probability models in this course?

<details><summary>Answer</summary>Ideas from optimization flow into dynamical systems, and those ideas then flow into probability models. This cascading structure is a unifying theme of applied mathematics.</details>

2. What does the expression X ∈ {x1, ..., xn}, n ≥ 1 tell you about the random variable X?

<details><summary>Answer</summary>X is a discrete random variable that can take on one of n possible values (x1 through xn), where n is at least 1. The set of possible values is finite.</details>

3. Why does the course assume basic familiarity with probability rather than teaching probability theory from scratch?

<details><summary>Answer</summary>The course focuses on mathematical modeling, not on probability theory itself. Probability is treated as a tool for modeling. The instructor will explain every piece needed but will not go into full detail about probability theory because basic familiarity is assumed.</details>
## Review of Discrete Probability Basics

This section reviews the fundamental concepts of discrete probability: random variables, probability distributions, expected value, and independence. These concepts are the foundation for modeling and optimizing a diode testing problem later in the course.

### Discrete Random Variables and Probability

A **discrete random variable** is a variable that can take only a finite number of distinct values. Each possible value is called a **state**.


![The frame shows the definition of a random variable X as a set of values x1 to xn, where n is greater than 1, and the probability P(X=xi) is equal...](frames/frame_02_200s.jpg)
*[03:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=200s) The frame shows the definition of a random variable X as a set of values x1 to xn, where n is greater than 1, and the probability P(X=xi) is equal to pi.*


The frame shows the definition of a random variable \(X\) as a set of values \(x_1\) to \(x_n\), where \(n > 1\), and the probability \(P(X = x_i)\) is equal to \(p_i\).

On-screen text:

```
X ∈ {x1, ..., xn}, n > 1
P(X=xi) = pi
```

For example, rolling a standard six-sided die gives six possible states: the numbers 1 through 6. Here, \(n = 6\). The random variable \(X\) is the number shown on the die after rolling.

Each probability \(p_i\) (the probability that \(X\) takes the value \(x_i\)) must satisfy:

- \(0 \leq p_i \leq 1\). A probability of 1 means the outcome is certain. A probability of 0 means it is impossible. Values in between (e.g., 0.5, 0.75) correspond to percentages.


![The frame shows mathematical notation for a discrete random variable X, its probability P(X=xi)=pi, and the sum of probabilities p1+p2+...+pn=1.](frames/frame_03_240s.jpg)
*[04:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=240s) The frame shows mathematical notation for a discrete random variable X, its probability P(X=xi)=pi, and the sum of probabilities p1+p2+...+pn=1.*


The frame shows the mathematical notation for a discrete random variable \(X\) and the condition that the sum of all probabilities equals 1.

On-screen text:

```
X∈{x1...,xn}, n≥1
P(X=xi) = pi
p1+p2+...+pn=1
```

The sum of all probabilities must equal 1. This is the **completeness of information** assumption. It means that every possible outcome the random variable can take is accounted for. If you only listed states 1 through 5 for a die, but a 6 could appear, then the information would be incomplete. The sum would be less than 1, and the model would be wrong.

States with probability zero, such as rolling a 7 on a standard die, are not included in the set of possible states. Only states with positive probability (or potentially positive) are listed.

### Expected Value (Mean)

The **expected value** (also called the mean) of a discrete random variable \(X\) is a weighted average of its possible values, where the weights are the probabilities. It is denoted \(E(X)\).


![Mathematical formulas for probability and expected value are written on a dark background.](frames/frame_04_320s.jpg)
*[05:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=320s) Mathematical formulas for probability and expected value are written on a dark background.*


The frame shows the formula for expected value.

On-screen text:

```
X ∈ {x₁, ..., xₙ}, n ≥ 1
P(X=xᵢ) = pᵢ
p₁ + p₂ + ... + pₙ = 1
E(X) = Σᵢ₌₁ⁿ pᵢxᵢ
```

The formula is:

\[
E(X) = \sum_{i=1}^{n} p_i x_i
\]

For a fair six-sided die, each outcome has probability \(p_i = \frac{1}{6}\). The expected value is:

\[
E(X) = \frac{1}{6} \times 1 + \frac{1}{6} \times 2 + \frac{1}{6} \times 3 + \frac{1}{6} \times 4 + \frac{1}{6} \times 5 + \frac{1}{6} \times 6 = 3.5
\]

Because all outcomes are equally likely, the expected value is simply the midpoint between 1 and 6. The expected value does not have to be a possible outcome.

### Probability Distribution

The collection of probabilities \(p_1, p_2, \dots, p_n\) is called the **probability distribution** of the random variable \(X\).


![Mathematical equations for probability and expected value are written on a dark background.](frames/frame_05_380s.jpg)
*[06:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=380s) Mathematical equations for probability and expected value are written on a dark background.*


The frame adds the label "prob. distribution" to the list of probabilities.

On-screen text:

```
X∈{x1...,xn}, n>1
P(X=xi)=pi
p1+p2+...+pn=1
E(X)=∑_{i=1}^{n} pixi
p1,p2...,pn - prob. distribution
```

The probability distribution completely describes the behavior of the discrete random variable.

### Independence of Random Variables

Two random variables are **independent** if the outcome of one does not affect the outcome of the other. For discrete random variables, independence means that the probability of both events occurring together equals the product of their individual probabilities.


![A whiteboard displays mathematical equations for probability distributions, expected value, and the probability of independent events.](frames/frame_06_480s.jpg)
*[08:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=480s) A whiteboard displays mathematical equations for probability distributions, expected value, and the probability of independent events.*


The frame shows the definition of independence for two random variables \(Y\) and \(Z\).

On-screen text:

```
X∈{x1...,xn}, n≥1
IP(X=xi) = Pi
P1+P2+...+pn=1
E(X) = Σ(i=1 to n) Pixi
P1,P2...,Pn - prob. distribution
Y∈{y1,y2...}, Z∈{z1,z2...}
IP(Y=yi and Z=zj) = P(Y=yi)IP(Z=zj)
```

Let \(Y\) and \(Z\) be two discrete random variables, each with a finite set of possible states. They are independent if and only if for every possible value \(y_i\) of \(Y\) and every possible value \(z_j\) of \(Z\):

\[
P(Y = y_i \text{ and } Z = z_j) = P(Y = y_i) \times P(Z = z_j)
\]

For example, consider two independent six-sided dice. Let \(Y\) be the result of the first die and \(Z\) be the result of the second die. The probability that \(Y\) shows a 2 is \(\frac{1}{6}\). The probability that \(Z\) shows a 1 is \(\frac{1}{6}\). Because they are independent, the probability of both happening (a 2 on the first die and a 1 on the second) is \(\frac{1}{6} \times \frac{1}{6} = \frac{1}{36}\).

The random variables \(Y\) and \(Z\) may have different numbers of possible states. For instance, one could be a six-sided die and the other a twelve-sided die. The independence condition still applies: the joint probability is the product of the marginal probabilities.

### Check Your Understanding

1.  A discrete random variable \(X\) has possible values \(x_1 = 2\) with \(p_1 = 0.3\), \(x_2 = 5\) with \(p_2 = 0.5\), and \(x_3 = 8\) with \(p_3 = 0.2\). What is the expected value \(E(X)\)?

    <details><summary>Answer</summary>
    \(E(X) = 0.3 \times 2 + 0.5 \times 5 + 0.2 \times 8 = 0.6 + 2.5 + 1.6 = 4.7\)
    </details>

2.  Why must the sum of the probabilities \(p_1 + p_2 + \dots + p_n\) equal 1?

    <details><summary>Answer</summary>
    The sum of probabilities must equal 1 because the random variable must take one of the listed values. This ensures that 100% of possible outcomes are accounted for, which is the completeness of information assumption.
    </details>

3.  Two fair dice are rolled: one red and one blue. Let \(Y\) be the number on the red die and \(Z\) be the number on the blue die. Are \(Y\) and \(Z\) independent? What is \(P(Y = 3 \text{ and } Z = 4)\)?

    <details><summary>Answer</summary>
    Yes, the dice are independent. The outcome of one die does not affect the other. \(P(Y = 3) = \frac{1}{6}\), \(P(Z = 4) = \frac{1}{6}\). Therefore \(P(Y = 3 \text{ and } Z = 4) = \frac{1}{6} \times \frac{1}{6} = \frac{1}{36}\).
    </details>

4.  A random variable \(X\) has possible values \(\{0, 1\}\) with probabilities \(p_0 = 0.4\) and \(p_1 = 0.6\). What is the name of the collection \(\{0.4, 0.6\}\)?

    <details><summary>Answer</summary>
    The collection \(\{0.4, 0.6\}\) is the probability distribution of the random variable \(X\).
    </details>
## Diode Testing Problem Setup

This section introduces a practical optimization problem from electronics manufacturing. You will learn how to model a quality control process using discrete probability, define random variables for testing costs, and set up the foundation for finding the optimal batch size.

### The Manufacturing Scenario

Imagine you work at an electronics manufacturing firm that produces diodes. Quality control engineers want to detect faulty diodes before they are shipped to customers. The problem is that testing every diode individually is expensive, but you cannot simply skip testing because faulty products damage the company's reputation.

**Key facts about the production process:**

- Approximately 0.3 percent of all diodes produced are faulty.
- Faulty diodes appear completely at random in the production stream. There is no pattern that lets you predict where they will show up.
- You have two testing options: test every diode individually, or test batches of diodes together.

### Testing Costs

The video defines two cost structures:

**Individual testing:** Testing one diode costs 5 cents. If you test every diode individually, you pay 5 cents per diode.

**Batch testing:** Testing a batch of n diodes costs 4 cents plus 1 cent for every diode in the batch. So the batch test cost is (4 + n) cents. However, the batch test only tells you whether the batch contains at least one faulty diode. It does not tell you which diode is faulty.

If the batch test reveals that the batch contains one or more faulty diodes, you must then test each diode in the batch individually at 5 cents per diode. This means the total cost for a batch that fails the group test becomes (4 + n) + 5n cents, which simplifies to (4 + 6n) cents.

### Defining the Variables


![A whiteboard displays mathematical formulas for probability distribution, expected value, and an example problem defining variables for diodes...](frames/frame_09_740s.jpg)
*[12:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=740s) A whiteboard displays mathematical formulas for probability distribution, expected value, and an example problem defining variables for diodes, testing cost, and average testing cost.*


The video defines three key variables for this problem:

- **n** = the number of diodes per test group. This is the decision variable. You get to choose this number.
- **C** = the testing cost for a group. This is a random outcome because it depends on whether the group contains any faulty diodes.
- **A** = the average testing cost in cents per diode. This is not random. It is an expected value.

### Understanding the Random Variable C

The testing cost for a group, C, depends on whether the group contains any faulty diodes.

**Case 1: n = 1**

If you test each diode individually, the cost is always 5 cents per diode. There is no randomness in this case. The average testing cost A equals 5 cents per diode.


![The whiteboard shows mathematical formulas for probability distribution and expected value, along with an example problem defining variables for...](frames/frame_11_840s.jpg)
*[14:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=840s) The whiteboard shows mathematical formulas for probability distribution and expected value, along with an example problem defining variables for testing cost.*


**Case 2: n > 1**

If you test in batches larger than one, the cost C has two possible values:

- If the group contains no faulty diodes, the cost is C = 4 + n. You pay only for the batch test.
- If the group contains one or more faulty diodes, the cost is C = (4 + n) + 5n. You pay for the batch test plus individual testing of every diode in the group.


![The whiteboard shows mathematical formulas for probability distribution and expected value, along with an example problem about testing costs for...](frames/frame_13_940s.jpg)
*[15:40](https://www.youtube.com/watch?v=7c43WFHCRac&t=940s) The whiteboard shows mathematical formulas for probability distribution and expected value, along with an example problem about testing costs for diodes.*


### The Average Testing Cost A

The average testing cost A is defined as the expected value of C divided by n, the number of diodes in the group.

A = E(C) / n

This gives the expected cost per diode when using batches of size n. Your goal is to choose n to minimize A.

### Summary of the Setup

| Variable | Definition | Type |
|----------|------------|------|
| n | Number of diodes per test group | Decision variable (you choose) |
| C | Testing cost for a group | Random variable |
| A | Average testing cost in cents per diode | Expected value (not random) |

**Cost structure for n = 1:**
- A = 5 cents per diode

**Cost structure for n > 1:**
- If the group has no faulty diodes: C = 4 + n
- If the group has at least one faulty diode: C = (4 + n) + 5n = 4 + 6n

**Objective:** Choose n to minimize A = E(C) / n.

### Check Your Understanding

1. Why is C a random variable when n > 1, but not when n = 1?

<details><summary>Answer</summary>When n = 1, you always test the single diode individually at a cost of 5 cents. There is no uncertainty. When n > 1, the cost depends on whether the batch contains any faulty diodes, which is a random event. If the batch is all good, you pay only the batch test cost. If the batch contains at least one faulty diode, you pay the batch test cost plus individual testing for every diode in the batch.</details>

2. What is the total cost for testing a batch of 20 diodes if the batch contains no faulty diodes? What is the total cost if the batch contains at least one faulty diode?

<details><summary>Answer</summary>If the batch contains no faulty diodes, the cost is 4 + 20 = 24 cents. If the batch contains at least one faulty diode, the cost is (4 + 20) + (5 x 20) = 24 + 100 = 124 cents.</details>

3. What does the variable A represent, and why is it not a random variable?

<details><summary>Answer</summary>A represents the average testing cost in cents per diode. It is not a random variable because it is defined as the expected value of C divided by n. An expected value is a single number that summarizes the long-run average outcome, not a random outcome itself.</details>

4. What is the decision variable in this optimization problem, and what is the objective?

<details><summary>Answer</summary>The decision variable is n, the number of diodes per test group. The objective is to choose n to minimize A, the average testing cost per diode.</details>
## Model Construction and Expected Cost Calculation

This section builds a discrete probability model for the diode testing problem.  
You will define the random variable, compute the probability of each outcome,  
derive the expected cost for a group, and then obtain the average cost per diode.  
All steps follow the five‑step method for constructing a probability model:  
(1) identify the random variable and its possible values, (2) decide to model it as a discrete probability model, (3) assign probabilities to each outcome, (4) compute the expected value, (5) interpret the result.

The problem is introduced on the whiteboard at the start of this section.


![A whiteboard displays mathematical formulas for probability distributions and an example problem about testing costs for diodes.](frames/frame_14_1020s.jpg)
*[17:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=1020s) A whiteboard displays mathematical formulas for probability distributions and an example problem about testing costs for diodes.*

```
X ∈ {x1, ..., xn}, n > 1
P(X = xi) = pi
p1 + p2 + ... + pn = 1
E(X) = Σ_{i=1}^n pi xi
p1, p2, ..., pn - prob. distribution
Y ∈ {y1, y2, ...}, Z ∈ {z1, z2, ...}
P(Y = yj and Z = zj) = P(Y = yj) P(Z = zj)
Ex: n = # of diodes per test group
C = testing cost for a group
A = average testing cost (cents/diode)
• If n = 1, then A = 5
• If n > 1, we have C = 4 + n if the group contains no faulty diodes, C = (4 + n) + 5n otherwise
• A = (Average value of C) / n
E(C)
```

The whiteboard shows the general definition of a discrete probability distribution and the formula for expected value.  
It also states the specific diode testing problem:  
- For a group of size \(n\) (number of diodes per test group), the testing cost \(C\) is a random variable.  
- If \(n = 1\), the average cost is already known to be 5 cents per diode.  
- For \(n > 1\), the cost depends on whether the group contains any faulty diodes.

### Defining the Random Variable and Possible Outcomes

For a group of \(n\) diodes (with \(n > 1\)), there are exactly two possible outcomes:

| Outcome | Cost \(C\) (cents) | Probability |
|---------|-------------------|-------------|
| No faulty diodes in the group | \(4 + n\) | \(p\) |
| At least one faulty diode in the group | \((4 + n) + 5n = 4 + 6n\) | \(1 - p\) |

The two outcomes are **mutually exclusive** and **exhaustive**: the group either has no faults or it has at least one fault.  
Therefore the probabilities sum to 1: \(p + (1-p) = 1\).

### Computing the Probability \(p\) (No Faults)

The failure rate of a single diode is given as 0.3%, which means:

- Probability a diode is faulty: \(0.003\)  
- Probability a diode is good: \(0.997\)

The whiteboard shows these values at frame 19:00.


![This frame shows a whiteboard with mathematical equations and an example problem related to probability distributions and expected value...](frames/frame_15_1140s.jpg)
*[19:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=1140s) This frame shows a whiteboard with mathematical equations and an example problem related to probability distributions and expected value, specifically calculating the average testing cost for diodes.*

```
...
0.003 - diodes faulty
=> 0.997 - diode is good
```

Each diode is **independent** of the others; the condition of one diode does not affect the condition of another.  
For independent events, the probability that all \(n\) diodes are good is the product of the individual probabilities:

\[
p = (0.997)^n
\]

This is recorded on the whiteboard at frame 20:00.


![This frame displays mathematical formulas and definitions related to probability distribution and an example problem involving diode testing costs.](frames/frame_16_1200s.jpg)
*[20:00](https://www.youtube.com/watch?v=7c43WFHCRac&t=1200s) This frame displays mathematical formulas and definitions related to probability distribution and an example problem involving diode testing costs.*

```
...
=> p = (0.997)^n
```

### Expected Cost of a Group

The expected value of \(C\) is the weighted average of the two possible costs:

\[
E(C) = (4 + n) \cdot p + (4 + 6n) \cdot (1 - p)
\]

Substitute \(p = (0.997)^n\):

\[
E(C) = (4 + n) \cdot (0.997)^n + (4 + 6n) \cdot \left(1 - (0.997)^n\right)
\]

The speaker then simplifies this expression.  
First expand the second term:

\[
E(C) = (4 + n)(0.997)^n + (4 + 6n) - (4 + 6n)(0.997)^n
\]

Combine the terms that contain \((0.997)^n\):

\[
E(C) = (4 + 6n) + \left[(4 + n) - (4 + 6n)\right] (0.997)^n
\]

The bracket simplifies to \(-5n\):

\[
E(C) = (4 + 6n) - 5n \cdot (0.997)^n
\]

Thus the cleaned‑up formula is:

\[
E(C) = 4 + 6n - 5n (0.997)^n
\]


![A person writes the letter 'E' on a dark background, likely a whiteboard or similar surface.](frames/frame_17_1240s.jpg)
*[20:40](https://www.youtube.com/watch?v=7c43WFHCRac&t=1240s) A person writes the letter 'E' on a dark background, likely a whiteboard or similar surface.*
 shows the speaker writing “E” during this simplification step.

### Average Cost per Diode

The average cost per diode, denoted \(A\), is the expected cost per group divided by the group size \(n\):

\[
A = \frac{E(C)}{n} = \frac{4 + 6n - 5n (0.997)^n}{n}
\]

Divide each term in the numerator by \(n\):

\[
A = \frac{4}{n} + 6 - 5 (0.997)^n
\]

The final formulas are displayed on the whiteboard at frame 21:40.


![A whiteboard shows the equations for E(C) and A, which is E(C) divided by n.](frames/frame_18_1300s.jpg)
*[21:40](https://www.youtube.com/watch?v=7c43WFHCRac&t=1300s) A whiteboard shows the equations for E(C) and A, which is E(C) divided by n.*

```
E(C) = 4 + 6n - 5n(0.997)^n
A = E(C)/n = 4/n + 6 - 5(0.997)^n
```

Now you have a complete expression for the average testing cost per diode as a function of the group size \(n\).  
The next step, covered in the following section of the course, is to find the value of \(n\) that minimizes \(A\) (the optimizer).

---

### Check your understanding

1.  Why is the probability that a group of \(n\) diodes contains no faulty diodes equal to \((0.997)^n\)?  
    <details><summary>Answer</summary>  
    Each diode has a 99.7% chance of being good (0.997). Because the diodes are independent, the probability that all \(n\) are good is the product of the individual probabilities: \(0.997 \times 0.997 \times \dots \times 0.997 = (0.997)^n\).  
    </details>

2.  For \(n = 10\), what is the expected cost per diode \(A\)? (Compute to three decimal places.)  
    <details><summary>Answer</summary>  
    \(A = \frac{4}{10} + 6 - 5(0.997)^{10}\)  
    First, \((0.997)^{10} \approx 0.97041\).  
    Then \(A = 0.4 + 6 - 5 \times 0.97041 = 6.4 - 4.85205 \approx 1.548\) cents per diode.  
    </details>

3.  What are the two possible values of the testing cost \(C\) for a group of \(n > 1\) diodes, and under what conditions does each occur?  
    <details><summary>Answer</summary>  
    - If the group contains **no faulty diodes**, the cost is \(4 + n\) cents.  
    - If the group contains **at least one faulty diode**, the cost is \(4 + 6n\) cents.  
    These are the only two possibilities because the group either has zero faults or one or more faults.  
    </details>

4.  Why can we use the formula \(E(C) = (4+n)p + (4+6n)(1-p)\) as the expected value?  
    <details><summary>Answer</summary>  
    The expected value of a discrete random variable is the sum of each outcome’s value multiplied by its probability. Here there are two outcomes, so we multiply the cost of the “no faults” outcome by its probability \(p\) and the cost of the “at least one fault” outcome by its probability \(1-p\), then add them.  
    </details>
## Optimization and Sensitivity Analysis

You now have a deterministic function for the average cost per diode, \(A(n)\). This function is an expected value that removed the randomness from the original problem. The goal is to find the batch size \(n\) that minimizes \(A(n)\). The problem is identical in structure to the pig‑holding problem from the beginning of the lecture series: you have a single‑variable function, and you find its minimum by taking the derivative and setting it equal to zero.


![A whiteboard shows equations for E(C) and A, and the minimum value of A at n=17.](frames/frame_19_1360s.jpg)
*[22:40](https://www.youtube.com/watch?v=7c43WFHCRac&t=1360s) A whiteboard shows equations for E(C) and A, and the minimum value of A at n=17.*


The whiteboard shows the cost expressions:

```
E(C) = 4 + 6n - 5n (0.997)
A = E(C)/n = 4/n + 6 - 5(0.997)
```

(Note: the correct expression for \(E(C)\) includes the exponent \(n\) on 0.997, as shown in later frames. The video corrects this at timestamp 26:20.)

The minimum of \(A\) occurs at \(n = 17\) and equals 1.48 cents per diode.


![The whiteboard shows the equations for E(C) and A, and the minimum value of A at n=17.](frames/frame_20_1400s.jpg)
*[23:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=1400s) The whiteboard shows the equations for E(C) and A, and the minimum value of A at n=17.*


The same values are displayed again. The minimum means that as the manager or owner of the factory, you should organize the diodes into batches of exactly 17. Each batch is tested together: the machine costs 21 cents (4 cent base price plus 1 cent per diode for the 17 diodes), and most diodes are good. In the low‑probability event that a batch contains a faulty diode, the cost per diode increases to 5 cents because each diode in that batch must be tested individually.

### Sensitivity to Batch Size

The factory may not be able to produce batches of exactly 17. For example, diodes might come in sets of 5, forcing you to choose 15 or 20. You can examine the shape of \(A(n)\) around the minimum. If you plot the function in a tool like Desmos, you will see that the curve is flat near \(n = 17\). This flatness gives you “wiggle room”: moving to 15 or 20 does not increase the average cost significantly. That observation is itself a sensitivity computation: the model is not very sensitive to small deviations from the optimal batch size.


![Mathematical equations for E(C) and A are displayed, along with the minimum value of A.](frames/frame_21_1520s.jpg)
*[25:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=1520s) Mathematical equations for E(C) and A are displayed, along with the minimum value of A.*


The same minimum is shown again. The flatness is a qualitative check, but the more important sensitivity analysis concerns the probability of a faulty diode. Let \(q\) be that probability. The video initially estimated \(q = 0.003\) (0.3%). The correct expression for \(A\) in terms of \(q\) is

\[
A = \frac{4}{n} + 6 - 5(1 - q)^n.
\]


![The whiteboard shows the equations for E(C) and A, the minimum value of A, and a new equation for A with q=0.003.](frames/frame_22_1580s.jpg)
*[26:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=1580s) The whiteboard shows the equations for E(C) and A, the minimum value of A, and a new equation for A with q=0.003.*


The whiteboard now shows the correct formula with the exponent:

```
A = 4/n + 6 - 5(1 - q)^n
```

If \(q = 0.003\), then \((1 - q) = 0.997\), and the formula matches the earlier numeric expression.

### Sensitivity of \(A\) with Respect to \(q\)

The sensitivity of \(A\) to a parameter like \(q\) is measured by the dimensionless quantity

\[
S(A, q) = \frac{dA}{dq} \cdot \frac{q}{A}.
\]

This is the relative change in \(A\) for a given relative change in \(q\). At the optimum \(n = 17\), you compute the derivative of \(A\) with respect to \(q\), multiply by \(q/A\), and obtain a value.


![A whiteboard shows mathematical equations for E(C), A, and S(A,q) with specific values for q and n.](frames/frame_23_1640s.jpg)
*[27:20](https://www.youtube.com/watch?v=7c43WFHCRac&t=1640s) A whiteboard shows mathematical equations for E(C), A, and S(A,q) with specific values for q and n.*


The whiteboard shows the result:

```
At n=17: S(A,q) = dA/dq * q/A = 0.16
```

The value 0.16 is very small. It means that for every 1% change in \(q\) (the probability of a faulty diode), the average cost \(A\) changes by only about 0.16% (roughly 0.1% as stated in the video). This is a “fantastic robustness computation”: the model is extremely insensitive to the exact value of \(q\). Even if your estimate of \(q\) is off by a modest amount, the optimal batch size and the resulting cost per diode are hardly affected.

### Why Sensitivity Matters

The probability \(q\) is always an estimate. You might obtain it from historical data, for example, “of all the diodes we sent out last year, 0.2997% were faulty.” But last year’s data could be skewed by unusual conditions, such as humidity in the factory that temporarily increased the fault rate. Sensitivity analysis tells you how much you can trust your model’s conclusions when the inputs are uncertain. In this case, the model is very robust: the estimated \(q\) does not need to be exact.

The next lecture in the series will move to continuous probability models, where the random variable can take any value within a range. For now, the discrete model has given you an optimal batch size of 17 and a highly insensitive relationship to the fault probability.

### Check Your Understanding

1.  What is the minimum average cost per diode and at what batch size does it occur?
    <details><summary>Answer</summary>The minimum average cost is 1.48 cents per diode, achieved at a batch size of 17.</details>

2.  Why is the sensitivity \(S(A, q)\) a useful quantity to compute?
    <details><summary>Answer</summary>It tells you how much the output (average cost) changes relative to a change in the input parameter (fault probability). A small value (like 0.16) indicates the model is robust: even if the estimate of \(q\) is off by a few percent, the cost changes very little.</details>

3.  If the factory can only test batches in multiples of 5, what batch size (15 or 20) would you choose and why?
    <details><summary>Answer</summary>You would choose 15 or 20. Because the function \(A(n)\) is flat near the minimum, either choice will result in an average cost only slightly above 1.48 cents per diode. The exact choice depends on convenience; the sensitivity to batch size is low.</details>

4.  The video states that the model is “insensitive” to \(q\). What does that mean in practical terms for the factory manager?
    <details><summary>Answer</summary>It means the manager does not need a perfectly accurate estimate of the fault probability. Even if the true fault rate differs from 0.3%, the optimal batch size remains 17 and the average cost per diode stays close to 1.48 cents. The manager can be confident in the decision without worrying about small errors in the probability estimate.</details>
## Key takeaways

- Discrete probability models describe random variables that can take only a finite number of distinct values, each with an assigned probability.
- The expected value of a discrete random variable is calculated as the weighted sum of each outcome multiplied by its probability.
- Independence between random variables means the probability of their joint occurrence equals the product of their individual probabilities.
- In the diode testing problem, the optimal batch size of 17 minimizes the expected average cost per diode to 1.48 cents.
- The average cost function is flat near its minimum, so small deviations from the optimal batch size do not significantly increase cost.
- Sensitivity analysis measures how changes in an input parameter, such as the fault probability, affect the model output.
- The sensitivity coefficient of 0.16 for the fault probability indicates the model is very robust to estimation errors in that parameter.
- Discrete probability models use sums over finite outcomes, while continuous probability models use integrals over intervals of outcomes.
## Glossary

| Term | Definition |
|---|---|
| random variable | A variable whose possible values are numerical outcomes of a random phenomenon. |
| discrete probability distribution | A list of all possible values a discrete random variable can take, together with the probability of each value. |
| expected value | The long-run average value of a random variable, computed as the sum of each outcome multiplied by its probability. |
| independence | Two random variables are independent if the probability that both take specific values equals the product of their individual probabilities. |
| probability | A number between 0 and 1 that measures the likelihood of a specific event occurring. |
| weighted sum | A sum in which each term is multiplied by a coefficient that reflects its relative importance, such as probability. |
| batch size | The number of diodes tested together as a single group in the testing procedure. |
| expected cost function | A mathematical expression that gives the average cost for a given decision variable, derived from the probabilities of different outcomes. |
| optimization | The process of finding the input value that minimizes or maximizes a given objective function. |
| sensitivity analysis | The study of how the output of a model changes in response to changes in its input parameters. |
| sensitivity coefficient | A dimensionless number that measures the relative change in the output for a given relative change in an input parameter. |
| robustness | The property of a model or solution to remain effective even when input parameters deviate from their assumed values. |
| decision variable | A variable whose value can be chosen by the decision maker to influence the outcome of the model. |
| fault probability | The probability that a single diode is defective, estimated as 0.3 percent in the problem. |
| average cost per diode | The total expected testing cost for a batch divided by the number of diodes in that batch. |
| deterministic function | A function that produces the same output for a given input every time, with no randomness involved. |
| derivative | A measure of how a function changes as its input changes, used in calculus to find minima and maxima. |
| continuous probability model | A probability model where the random variable can take any value within a continuous range, described by a probability density function. |
| finite states | A countable set of distinct possible outcomes for a random variable, such as the numbers 1 through 6 on a die. |
| probability distribution | The complete assignment of probabilities to all possible outcomes of a random variable. |
## Footnotes and deeper context

1. **Expected value interpretation.** The expected value is not necessarily a value the random variable can actually take. For a fair six-sided die, the expected value is 3.5, which is not a possible outcome of a single roll.
2. **Independence assumption in diode testing.** The model assumes each diode's fault status is independent of every other diode. In real manufacturing, defects can cluster due to machine wear or material batches, which would violate this assumption and require a more complex model.
3. **Sensitivity coefficient formula.** The sensitivity coefficient S(A, q) is defined as (dA/dq) * (q/A). It expresses the percentage change in A for a one percent change in q, making it unitless and comparable across different parameters.
4. **Optimization method used.** The lecturer found the minimum by taking the derivative of A with respect to n and setting it to zero. Because n must be an integer, the exact minimum is found by checking integer values near the continuous optimum, which in this case is 17.
5. **Practical batch size constraints.** The lecturer notes that factories may only handle batches in multiples of 5. Because the cost function is flat near the minimum, using 15 or 20 instead of 17 increases the average cost only slightly, demonstrating practical robustness.
6. **Distinction between discrete and continuous models.** Discrete probability models use sums over a finite set of outcomes, while continuous models use integrals over an interval. The diode problem is discrete because the batch size n is a whole number and the outcomes are two distinct events.
## Where to go next

- **Review the five step method for mathematical modeling.** The lecturer references a five step method for building models. To deepen your understanding, consult the textbook 'A First Course in Mathematical Modeling' by Giordano, Fox, Horton, and Weir, which introduces and applies this method across many examples.
- **Practice sensitivity analysis with other parameters.** Try computing the sensitivity of the optimal batch size n to changes in the base testing cost (4 cents) or the individual testing cost (5 cents). This will reinforce how sensitivity coefficients are calculated and interpreted.
- **Explore continuous probability models.** The next lecture in this series covers continuous probability models. To prepare, review the concept of a probability density function and how expected values are computed using integrals. The open textbook 'Introductory Statistics' by OpenStax provides a clear introduction.
- **Use computational tools to verify the optimization.** Plot the function A(n) = 4/n + 6 - 5*(0.997)^n in a graphing tool like Desmos or Python with Matplotlib. Verify that the minimum occurs near n=17 and observe how flat the curve is around that point.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
