# Discrete Probability Models in Mathematical Modeling: A Self Contained Video Based Course
> **Source:** [Discrete Probability Models - Math Modelling - Lecture 23](https://www.youtube.com/watch?v=7c43WFHCRac) by Math Modelling · 29:50 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students who have completed studies in optimization and dynamical systems and are ready to learn how probability models integrate with those topics.
## Learning objectives

After working through this document you can:

1. Define a discrete probability distribution and explain the completeness of information assumption.
2. Calculate the expected value of a discrete random variable using a weighted sum of probabilities and outcomes.
3. State the condition for independence between two discrete random variables.
4. Formulate a real world quality control problem as a discrete probability model using the five step method.
5. Derive the expected testing cost per diode for a given batch size using probabilities of faulty and non faulty diodes.
6. Optimize the batch size to minimize the average testing cost per diode by taking a derivative and setting it to zero.
7. Analyze the sensitivity of the optimal average cost to changes in the estimated probability of a faulty diode.
8. Interpret the results of sensitivity analysis to determine the robustness of the model against estimation errors.
## Prerequisites

- Basic familiarity with probability theory, including random variables, discrete probability distributions, expected value, and independence.
- Understanding of optimization techniques, including finding minima of functions using derivatives.
- Familiarity with the five step method for mathematical modeling as used in previous lectures of this series.
- Ability to interpret sensitivity analysis using relative change formulas.
## Introduction to Probability Models and Review of Discrete Probability

This section marks the transition from deterministic dynamical systems to stochastic (random) models. Probability models incorporate ideas from optimization and dynamical systems, but now the outcomes are uncertain. We assume you have a basic familiarity with probability; we will review the essential concepts and then apply them to a manufacturing quality control problem.

### 1. Review of Discrete Probability

A **random variable** \(X\) is a quantity whose value is determined by the outcome of a random experiment. In a **discrete probability distribution**, \(X\) can take on only a finite number of distinct values (states). For example, rolling a fair six‑sided die gives six possible states: 1, 2, 3, 4, 5, 6.

Let the possible values of \(X\) be \(x_1, x_2, \dots, x_N\). For each state \(x_i\) we assign a **probability** \(p_i = P(X = x_i)\). Each probability satisfies \(0 \le p_i \le 1\). Because we assume we know all possible states, the probabilities must sum to 1:

\[
\sum_{i=1}^{N} p_i = 1
\]

This is the **completeness of information** assumption: every possible outcome is accounted for, and any outcome not in the list has probability zero.

#### Expected Value (Mean)

The **expected value** (or mean) of a discrete random variable \(X\) is the weighted average of its possible values, weighted by their probabilities:

\[
E[X] = \sum_{i=1}^{N} p_i \, x_i
\]

For a fair die, each \(p_i = \frac{1}{6}\) and \(x_i = i\). Then

\[
E[X] = \frac{1}{6}(1+2+3+4+5+6) = 3.5
\]

The set \(\{p_1, p_2, \dots, p_N\}\) is called the **probability distribution** of \(X\).

#### Independence

Two random variables \(Y\) and \(Z\) (each with a finite number of states) are **independent** if the probability that \(Y\) takes a particular value \(y\) and \(Z\) takes a particular value \(z\) equals the product of their individual probabilities:

\[
P(Y = y \text{ and } Z = z) = P(Y = y) \cdot P(Z = z)
\]

For example, rolling two separate fair dice: the probability of a 2 on the first die and a 1 on the second die is \(\frac{1}{6} \times \frac{1}{6} = \frac{1}{36}\). The outcome of one die does not affect the other.

### 2. A Discrete Probability Model: Quality Control for Diodes

We now apply these ideas to a real‑world optimization problem.

#### Problem Setup

You work at an electronics manufacturing firm that produces diodes. Quality control engineers want to detect faulty diodes before shipping. It is estimated that **0.3%** of all diodes produced are faulty (probability \(p = 0.003\)). The faults appear completely at random; there is no pattern.

Testing every diode individually is expensive: it costs **5 cents per diode**. To reduce cost, you can test diodes in **batches** (groups). The testing procedure is:

- Test a batch of \(n\) diodes together as a group. The cost for this group test is **4 cents plus 1 cent per diode** in the batch, i.e., \(4 + n\) cents.
- If the group test passes (no faulty diodes in the batch), the entire batch is shipped. No further testing is needed.
- If the group test fails (at least one faulty diode in the batch), you must then test each diode in the batch individually at **5 cents per diode**. This individual testing cost is added **on top of** the group test cost.

#### Decision Variable and Random Outcome

Let  

- \(n\) = number of diodes per test group (the decision variable you can choose).  
- \(c\) = testing cost for a group (a random variable, because it depends on whether the group contains a faulty diode).  
- \(a\) = **average testing cost per diode** (in cents). This is an expected value, not a random quantity.

#### Cost Structure

| Scenario | Cost for a group of \(n\) diodes |
|----------|----------------------------------|
| No faulty diodes in the group | \(4 + n\) cents |
| At least one faulty diode in the group | \((4 + n) + 5n = 4 + 6n\) cents |

#### Expected Cost per Diode

If \(n = 1\), you are testing each diode individually. The cost per diode is always 5 cents, so the average cost per diode is \(a = 5\) cents.

For \(n > 1\), we need to compute the expected cost for a group and then divide by \(n\) to get the average cost per diode.

Let \(X\) be the number of faulty diodes in a group of \(n\). Because faults occur independently with probability \(p = 0.003\), \(X\) follows a binomial distribution. The probability that the group contains **no faulty diodes** is

\[
P(\text{no faulty}) = (1 - p)^n
\]

The probability that the group contains **at least one faulty diode** is

\[
P(\text{at least one faulty}) = 1 - (1 - p)^n
\]

The expected cost for a group is therefore

\[
E[c] = (4 + n) \cdot (1 - p)^n + (4 + 6n) \cdot \left(1 - (1 - p)^n\right)
\]

The average testing cost per diode is

\[
a = \frac{E[c]}{n}
\]

This expression is a function of \(n\). The goal is to choose \(n\) (the batch size) that minimizes \(a\). (The actual optimization and solution will be developed later in the course.)

#### Diagram: Decision Tree for One Group

```
                    ┌─ No faulty diodes ── Cost = 4 + n
                    │   (probability (1-p)^n)
Start group test ──┤
                    │
                    └─ At least one faulty ── Cost = 4 + 6n
                        (probability 1 - (1-p)^n)
```

### Check Your Understanding

1. **Define a discrete random variable and give an example not from the video.**  
   <details><summary>Answer</summary> A discrete random variable takes on a finite number of distinct values. Example: the number of heads when flipping a coin three times (possible values 0, 1, 2, 3).</details>

2. **Why must the probabilities of all possible outcomes of a discrete random variable sum to 1?**  
   <details><summary>Answer</summary> Because the set of all possible outcomes is assumed to be complete; the total probability of all outcomes must account for 100% of the possibilities.</details>

3. **In the diode example, what is the expected cost per diode when \(n = 2\)? (Use \(p = 0.003\).)**  
   <details><summary>Answer</summary>  
   \((1-p)^2 = (0.997)^2 \approx 0.994009\).  
   Expected group cost = \((4+2)\times 0.994009 + (4+12)\times (1-0.994009) = 6\times 0.994009 + 16\times 0.005991 \approx 5.964054 + 0.095856 = 6.05991\) cents.  
   Average per diode = \(6.05991 / 2 \approx 3.02996\) cents.  
   (This is lower than the 5 cents per diode for individual testing, illustrating the potential benefit of batch testing.)</details>

4. **If two random variables are independent, what does that imply about the probability of both taking specific values?**  
   <details><summary>Answer</summary> The probability that both take those specific values equals the product of their individual probabilities: \(P(Y=y \text{ and } Z=z) = P(Y=y) \cdot P(Z=z)\).</details>
## Modeling a Quality Control Problem for Diode Testing

In this section you will build a discrete probability model to minimize the average testing cost per diode in a factory. The problem is to decide how many diodes to test together as a single batch. You will compute the expected cost, simplify the expression, and then find the optimal batch size.

### Problem Setup

You are the manager of a diode assembly line. Each diode has a 0.3% chance of being faulty (0.003 probability of fault). Diodes are independent: the condition of one diode does not affect the condition of any other. You have a testing machine that can test a batch of diodes all at once. The costs are:

- Base cost to run the machine: 4 cents per batch (regardless of batch size).
- Per‑diode testing cost: 1 cent per diode in the batch.
- If a batch contains at least one faulty diode, you must replace every diode in that batch. Replacement costs 5 cents per diode.

Let \(N\) be the number of diodes in a batch. Let \(C\) be the total testing cost for one batch (in cents). The quantity you want to minimize is the average cost per diode:

\[
A = \frac{\text{average value of } C}{N} = \frac{E[C]}{N}
\]

where \(E[C]\) is the expected value (average) of \(C\).

### Step 1: Identify the Two Possible Outcomes

A batch can be in one of two states:

1. **No faulty diodes**: all \(N\) diodes are good.
2. **At least one faulty diode**: the batch contains one or more faults.

These two outcomes cover all possibilities. Let \(P\) be the probability that the batch has no faulty diodes. Then the probability that the batch has at least one faulty diode is \(1 - P\).

### Step 2: Compute the Probability \(P\)

Because each diode is independent and has a 99.7% chance of being good (0.997), the probability that all \(N\) diodes are good is:

\[
P = 0.997^N
\]

This follows from the multiplication rule for independent events: the probability that all \(N\) independent events occur is the product of their individual probabilities.

### Step 3: Write the Expected Value \(E[C]\)

The cost \(C\) depends on the outcome:

- If the batch has no faults: cost = base cost + per‑diode testing cost = \(4 + N\) cents.
- If the batch has at least one fault: cost = base cost + per‑diode testing cost + replacement cost for all diodes = \(4 + N + 5N = 4 + 6N\) cents.

The expected value is the sum of each cost multiplied by its probability:

\[
E[C] = (4 + N) \cdot P + (4 + 6N) \cdot (1 - P)
\]

Substitute \(P = 0.997^N\):

\[
E[C] = (4 + N) \cdot 0.997^N + (4 + 6N) \cdot (1 - 0.997^N)
\]

### Step 4: Simplify the Expression

Expand and combine like terms:

\[
\begin{aligned}
E[C] &= (4 + N)0.997^N + (4 + 6N) - (4 + 6N)0.997^N \\
&= (4 + 6N) + \left[(4 + N) - (4 + 6N)\right]0.997^N \\
&= (4 + 6N) + (4 + N - 4 - 6N)0.997^N \\
&= (4 + 6N) + (-5N)0.997^N \\
&= 4 + 6N - 5N \cdot 0.997^N
\end{aligned}
\]

### Step 5: Obtain the Average Cost Per Diode \(A\)

Divide \(E[C]\) by \(N\):

\[
A(N) = \frac{4 + 6N - 5N \cdot 0.997^N}{N} = \frac{4}{N} + 6 - 5 \cdot 0.997^N
\]

Now \(A\) is a deterministic function of the batch size \(N\). Your goal is to find the integer \(N\) that minimizes \(A(N)\).

### Step 6: Optimize

This is a single‑variable optimization problem. You can find the minimum by taking the derivative of \(A(N)\) with respect to \(N\) (treating \(N\) as continuous) and setting it to zero, or by evaluating \(A(N)\) for small integer values. The result is:

- Optimal batch size: \(N = 17\) diodes.
- Minimum average cost: \(A(17) = 1.48\) cents per diode.

### Interpretation

If you test diodes in batches of 17, the average testing cost per diode is about 1.48 cents. This is lower than testing each diode individually (which would cost 1 cent per diode for testing plus the occasional replacement cost) or testing very large batches (where the replacement cost for a faulty batch becomes high). The model shows that grouping diodes into batches of 17 balances the fixed machine cost, the per‑diode testing cost, and the risk of having to replace an entire batch.

### Summary of Key Concepts

| Concept | Definition |
|---------|------------|
| Discrete probability model | A model where outcomes are countable and each outcome has a probability. |
| Expected value \(E[X]\) | The average value of a random variable, computed as sum of (outcome × probability). |
| Independence | Two events are independent if the occurrence of one does not affect the probability of the other. |
| Optimization | Finding the input value that minimizes (or maximizes) a function. |

### Check Your Understanding

1. Why is the probability that a batch has no faulty diodes equal to \(0.997^N\) and not \(0.997 \times N\)?

<details><summary>Answer</summary>Because the diodes are independent. The probability that all \(N\) are good is the product of the individual probabilities: \(0.997 \times 0.997 \times \dots\) (N times) = \(0.997^N\). Multiplying by \(N\) would be incorrect; that would represent the sum of probabilities, not the joint probability.</details>

2. In the expression for \(E[C]\), why is the cost for a faulty batch \(4 + 6N\) instead of \(4 + N + 5\)?

<details><summary>Answer</summary>When a batch is faulty, every diode must be replaced. Replacement costs 5 cents per diode, so for \(N\) diodes the replacement cost is \(5N\) cents. Adding the base cost (4) and the per‑diode testing cost (1 per diode, total \(N\)) gives \(4 + N + 5N = 4 + 6N\).</details>

3. Suppose the probability of a faulty diode were 1% instead of 0.3%. Would you expect the optimal batch size to be larger or smaller than 17? Explain briefly.

<details><summary>Answer</summary>Smaller. A higher fault probability increases the chance that a batch contains at least one fault, making large batches more risky (higher expected replacement cost). To reduce that risk, you would test smaller batches, so the optimal \(N\) would be less than 17.</details>

4. What is the practical meaning of the term \(5 \cdot 0.997^N\) in the formula for \(A(N)\)?

<details><summary>Answer</summary>It represents the expected savings per diode from the fact that a batch with no faults avoids the replacement cost. The term \(5 \cdot 0.997^N\) is subtracted from the baseline cost \(4/N + 6\). As \(N\) increases, \(0.997^N\) decreases, so the savings shrink, eventually causing the average cost to rise.</details>
## Setting Up the Expected Value and Probability Calculations

In this section, you will learn how to perform sensitivity analysis on the expected value model for diode testing. You will compute how changes in the estimated probability of a faulty diode affect the average cost per diode. This analysis confirms whether your optimal batch size is robust to estimation errors.

### Sensitivity to Batch Size Constraints



The probability that diodes actually fail affects the cost. If a diode is faulty, testing costs more than 1 cent per diode. It costs 5 cents to test each diode in a batch of 17.

You can perform sensitivity analysis just as you did with optimization and dynamic systems earlier in the course. Sensitivity analysis is an integral part of mathematical modeling.

Consider that the factory might only allow testing in batches of 5 or 10. You cannot always test 17 at a time. If diodes come in sets of 5, you would need to move to 15 or 20 at a time.

If you sketch the cost function or plot it in Desmos or another graphing tool, you will see that the function is flat around the minimum. This flatness means you have a lot of wiggle room. Even going down to 15 diodes per batch does not increase the minimum cost by a large amount. This observation is itself a sensitivity computation. It tells you that if you do not get exactly 17 in every batch, you still have wiggle room and it will not cost much more.

### Interrogating the Probability of Faulty Diodes



Let Q represent the probability of a faulty diode. In the original model, Q was 0.3 percent, or 0.003. This value appears in the cost function.

The average cost A can be written as:

A = (4 / N) + 6 - 5 * (1 - Q)^N

When Q equals 0.003, the term (1 - Q)^N equals 0.997, which matches the original model.

You want to interrogate the sensitivity of the model with respect to this probability Q. The estimate that 0.3 percent of diodes are faulty is just an estimation. It is not necessarily true. You need to see how robust the model is.

This is still an optimization problem. There was probability involved originally, but you used an expected value to remove that probability and arrive at a standard optimization problem, the same type you started the course with.

### Computing Sensitivity of A with Respect to Q



At N equal to 17, you can compute sensitivities. The sensitivity of A with respect to Q uses the formula:

Sensitivity = (dA / dQ) * (Q / A)

This formula gives the relative change in A for a given relative change in Q.

For this model, the sensitivity is approximately 0.16. This is a very small number. For every 1 percent change in Q, there is only a 0.1 percent change in A.

This is a fantastic robustness computation. Because the sensitivity number is so tiny, changing Q does not have a large effect on changing A. You have a lot of wiggle room. Even if you did not estimate the probability of 0.3 percent exactly right, the model is very insensitive or inelastic.

### Why Sensitivity Matters for Real Data



This value Q will always be an estimation. The best you can do is take historical data. For example, you could look at all diodes sent out last year and find that 0.2997 percent turned out to be faulty. That is where you estimate this probability.

This is exactly the type of situation where sensitivity analysis is important. Maybe last year was a slightly skewed year. Perhaps you actually have far fewer faulty diodes, but there was some weird humidity in the factory that caused a few more failures than usual.

What you are seeing here is an extremely insensitive model to the value of Q. This means your optimal batch size of 17 is robust even if your estimate of the fault probability is off.

### Looking Ahead

The next lecture in this series covers continuous probability models. This section used a discrete probability model. It came from the fact that you had discrete values of N to choose from, and there were only two probabilities at play: either every diode works or at least one is faulty. In the next lecture, you will consider when values can take on a continuum, such as when something is less than a certain value but could be anything less.

### Check Your Understanding

1. What does a sensitivity value of 0.16 for A with respect to Q tell you about the model?

<details><summary>Answer</summary>
A sensitivity of 0.16 means that for every 1 percent change in Q (the probability of a faulty diode), the average cost A changes by only 0.16 percent. This indicates the model is very insensitive to changes in Q, meaning the optimal batch size is robust even if the estimate of Q is slightly wrong.
</details>

2. Why is it important to perform sensitivity analysis on the probability Q in this diode testing model?

<details><summary>Answer</summary>
The probability Q is always an estimate based on historical data. Historical data can be skewed by unusual conditions, such as humidity in the factory. Sensitivity analysis tells you whether a small error in estimating Q would significantly change the optimal batch size or the average cost. In this case, the model is insensitive, so estimation errors are not a problem.
</details>

3. How does the shape of the cost function near its minimum relate to sensitivity?

<details><summary>Answer</summary>
The cost function is flat around its minimum. This flatness means that even if you cannot use exactly 17 diodes per batch (for example, if batches must be in multiples of 5), moving to 15 or 20 does not increase the cost much. This is a form of sensitivity analysis that shows the model has wiggle room.
</details>

4. Write the formula for the average cost A in terms of N and Q, and explain what each term represents.

<details><summary>Answer</summary>
A = (4 / N) + 6 - 5 * (1 - Q)^N

- (4 / N): The fixed cost of testing (4 cents) divided by the batch size N.
- 6: The base cost per diode (6 cents) if no testing is done.
- 5 * (1 - Q)^N: The expected savings from testing, where 5 cents is saved per diode if no diode in the batch is faulty, and (1 - Q)^N is the probability that all N diodes are good.
</details>
## Deriving the Average Cost Function and Finding the Optimal Batch Size

### The transition from dynamic systems to probability models

This lecture begins the third major unit of the course: probability models. The earlier units covered optimization and dynamical systems, and those ideas carry forward into stochastic models. Probability is not a replacement for the earlier tools. Instead, probability provides a way to describe randomness, and then optimization and sensitivity analysis are used to make decisions under that randomness. This is the same pattern seen in the data fitting lecture, where optimization ideas from the beginning of the course were reused.

### Probability refresher

Before building the model, the video reviews the probability concepts needed for the example.

#### Random variables and discrete probability distributions

A random variable, denoted X, is a quantity whose value is the outcome of a random process. In this section, X follows a discrete probability distribution, meaning X can take on only a finite number of states. For example, rolling a standard die gives six possible states: 1, 2, 3, 4, 5, and 6.

For each possible state, there is a probability, denoted P_i, that X equals that state. Each probability satisfies:

- 0 ≤ P_i ≤ 1, where 0 means impossible and 1 means certain.
- The sum of all probabilities equals 1: P_1 + P_2 + ... + P_N = 1.

The second condition is a completeness assumption. It says that all possible outcomes have been accounted for. If a standard die is rolled, the probability of rolling a 7 is 0, so 7 is not included as a state. The list of probabilities, P_1, P_2, ..., P_N, is called the probability distribution of X.

#### Expected value

The mean or expected value of X, written E[X], is a weighted average of the possible states. The formula is:

E[X] = P_1 * X_1 + P_2 * X_2 + ... + P_N * X_N

For a fair six-sided die, each P_i is 1/6, so:

E[X] = (1/6)(1) + (1/6)(2) + (1/6)(3) + (1/6)(4) + (1/6)(5) + (1/6)(6) = 3.5

The expected value is 3.5 because every outcome is equally likely, so the average is the midpoint of 1 and 6.

#### Independence

Two random variables, Y and Z, drawn from discrete distributions are independent if the probability that Y takes on one value and Z takes on another value is the product of their individual probabilities:

P(Y = i and Z = j) = P(Y = i) * P(Z = j)

For example, if Y and Z are both fair six-sided dice, then:

P(Y = 2 and Z = 1) = (1/6)(1/6) = 1/36

The result on one die does not affect the result on the other. Independence is what allows probabilities to be multiplied in the diode model below.

### The diode testing problem

#### Problem setup

Imagine an electronics manufacturer that produces diodes. Quality control engineers want to detect faulty diodes before shipping them. It is estimated that about 0.3 percent of all diodes are faulty, which as a probability is 0.003. The faulty diodes appear at random, so there is no way to predict which diodes are bad.

Two testing strategies are available:

1. Test every diode individually. This costs 5 cents per diode.
2. Test diodes in batches. Testing a batch of n diodes costs a base price of 4 cents plus 1 cent per diode, so the cost is 4 + n cents. If the entire batch is good, the batch passes. If at least one diode in the batch is faulty, then each diode in the batch must be tested individually, adding 5 cents per diode on top of the batch test.

The goal is to choose the batch size n that minimizes the average testing cost per diode. The following diagram shows the decision flow:

```
For each batch of n diodes:
   Machine tests the whole batch (cost 4 + n cents)
        |
        v
   Are all n diodes good?
      /          \
     yes          no
    /              \
Pass the batch   Test each diode individually
(cost 4 + n)     (extra cost 5n cents)
                 total cost 4 + n + 5n = 4 + 6n
```

#### Model variables

| Variable | Meaning |
| --- | --- |
| n | Number of diodes in each test batch, the decision variable |
| C | Testing cost for one group of n diodes, a random outcome |
| A | Average testing cost in cents per diode, equal to E[C] / n |
| Q | Probability that a single diode is faulty, initially 0.003 |
| P | Probability that a batch of n diodes contains no faulty diodes |

C is random because the cost depends on whether the batch contains a faulty diode. A is not random; it is the expected value of C divided by n.

#### Cost when n = 1

If n = 1, each diode is tested individually, so the average cost per diode is A = 5 cents. There is no batch of size greater than 1, so the outcome is simply the individual testing cost.

#### Cost when n > 1

For a batch of size n, there are two possible outcomes:

- No faulty diodes in the batch. The cost is only the batch test cost: 4 + n cents.
- At least one faulty diode in the batch. The batch test is needed first, then every diode in the batch is tested individually. The total cost is:

4 + n + 5n = 4 + 6n cents

The expected value of C will combine these two costs with their probabilities.

#### Computing the probability that a batch is good

Since 0.3 percent of diodes are faulty, the probability that one diode is good is:

1 - 0.003 = 0.997

So a single diode is good with probability 0.997. Because each diode is independent, the probability that all n diodes in a batch are good is the product of n individual good probabilities:

P = 0.997^n

The probability that at least one diode in the batch is faulty is therefore:

1 - P = 1 - 0.997^n

There are only two possibilities for a batch: either all diodes are good, or at least one is faulty. The two probabilities add to 1, so all possible outcomes are accounted for.

#### Expected cost for a group

The expected value of C is the sum of each possible cost multiplied by its probability:

E[C] = (4 + n) * 0.997^n + (4 + 6n) * (1 - 0.997^n)

This expression can be simplified by expanding the second term:

E[C] = (4 + n) * 0.997^n + (4 + 6n) - (4 + 6n) * 0.997^n

Combine the two terms that contain 0.997^n:

E[C] = 4 + 6n + [(4 + n) - (4 + 6n)] * 0.997^n

Since (4 + n) - (4 + 6n) = -5n, this becomes:

E[C] = 4 + 6n - 5n * 0.997^n

#### Average cost per diode

The average testing cost per diode, A, is the expected cost per group divided by the number of diodes in the group:

A = E[C] / n

Substitute the simplified expected cost:

A(n) = (4 + 6n - 5n * 0.997^n) / n

Divide each term by n:

A(n) = 4/n + 6 - 5 * 0.997^n

This is the average cost function. It is now a deterministic function of the batch size n, so the randomness has been removed by taking the expected value.

### Finding the optimal batch size

To minimize A(n), take the derivative with respect to n and set it equal to 0. The derivative is (added context):

A'(n) = -4/n^2 - 5 * ln(0.997) * 0.997^n

Since ln(0.997) is negative, the second term is positive, so A'(n) increases as n grows. Setting A'(n) = 0 and solving numerically gives:

n ≈ 17

At n = 17, the average cost is:

A(17) = 4/17 + 6 - 5 * 0.997^17 ≈ 1.48 cents per diode

So the optimal policy is to organize the diodes into batches of 17. The batch machine test for 17 diodes costs 4 + 17 = 21 cents. Most batches will pass, and the average cost across all diodes, including the rare batches that need individual retesting, is about 1.48 cents per diode.

### Sensitivity analysis

Sensitivity analysis asks how much the optimal result changes when assumptions change. There are two important sensitivity questions for this model.

#### Sensitivity to practical batch size restrictions

The optimal batch size 17 may not be practical if the factory can only test batches in multiples of 5. In that case, n = 15 or n = 20 would be natural alternatives. The cost curve is fairly flat near the minimum, so choosing 15 or 20 instead of 17 does not increase the average cost by much. This gives the factory some flexibility in how batches are organized.

#### Sensitivity to the fault probability Q

The 0.3 percent fault rate is an estimate, so it is worth asking how sensitive A is to changes in Q. Rewrite the average cost function using Q as the faulty diode probability:

A(n) = 4/n + 6 - 5 * (1 - Q)^n

When Q = 0.003, 1 - Q = 0.997.

The sensitivity of A with respect to Q is measured by the relative change formula:

S(A, Q) = (dA/dQ) * (Q/A)

This value gives the percentage change in A for a 1 percent change in Q. At n = 17:

- dA/dQ = 5n * (1 - Q)^(n-1) ≈ 81.06
- Q/A ≈ 0.003 / 1.4813 ≈ 0.002025
- S(A, Q) ≈ 81.06 * 0.002025 ≈ 0.16

A sensitivity of about 0.16 means that a 1 percent increase in Q produces only a 0.16 percent increase in A. The model is very insensitive to Q. If the true fault probability is somewhat higher or lower than 0.3 percent, the average cost per diode stays nearly the same.

This insensitivity is valuable because Q is always an estimate. It might be obtained from historical data, such as the fraction of diodes that failed in previous production runs. A past year could have been unusual because of humidity or other factory conditions. The low sensitivity means the recommended batch size remains reasonable even if the estimate is not exact.

### Summary

The diode testing example is a discrete probability model. The process has a finite set of outcomes for each batch: either no faulty diodes, or at least one faulty diode. By taking an expected value, the random cost C was converted into a deterministic function A(n). Minimizing A(n) gave an optimal batch size of 17 and an average cost of about 1.48 cents per diode. The sensitivity analysis showed that the optimal solution is robust both to batch size restrictions and to errors in the estimated fault probability.

### Check your understanding

1. Why is the probability that a batch of n diodes contains no faulty diodes equal to 0.997^n?

<details>
<summary>Answer</summary>
Each diode has probability 0.997 of being good, and the condition of each diode is independent of the others. Independent probabilities are multiplied together, so the probability that all n diodes are good is 0.997 multiplied by itself n times, which is 0.997^n.
</details>

2. Write the expected testing cost E[C] for a group of n diodes before simplifying, and then give the simplified form.

<details>
<summary>Answer</summary>
Before simplifying:

E[C] = (4 + n) * 0.997^n + (4 + 6n) * (1 - 0.997^n)

Simplified:

E[C] = 4 + 6n - 5n * 0.997^n
</details>

3. The sensitivity of A to Q is about 0.16. If Q increases by 1 percent, what percent change in A do you expect?

<details>
<summary>Answer</summary>
A is expected to increase by about 0.16 percent. A 1 percent change in Q causes approximately a 0.16 percent change in A.
</details>

4. Why is it acceptable that the factory cannot test exactly 17 diodes per batch, for example if batches must be multiples of 5?

<details>
<summary>Answer</summary>
The average cost curve is flat near the minimum, so choosing a nearby batch size such as 15 or 20 increases the average cost only slightly. The optimal solution is not sensitive to small changes in n.
</details>
## Sensitivity Analysis with Respect to Batch Size and Fault Probability

This section covers how to analyze the sensitivity of an optimal batch testing strategy to changes in the estimated fault probability. You will learn how to compute the sensitivity of the average testing cost to changes in the fault probability and interpret the results.

### Review of Discrete Probability Basics

Before building the model, recall three fundamental concepts from discrete probability.

**Random variable and discrete probability distribution.** A random variable X can take on one of only finitely many states. For example, rolling a six-sided die gives six possible states (1 through 6). Each state has a probability P_i between 0 and 1. The sum of all probabilities equals 1, meaning all possible outcomes are accounted for.

**Expected value (mean).** The expected value E[X] is the weighted average of all possible outcomes:

E[X] = sum from i=1 to N of P_i * X_i

For a fair six-sided die, each P_i = 1/6, so E[X] = (1/6)(1+2+3+4+5+6) = 3.5.

**Independence.** Two random variables Y and Z are independent if the probability that Y takes value i and Z takes value j equals the product of their individual probabilities:

P(Y=i and Z=j) = P(Y=i) * P(Z=j)

For example, rolling two independent six-sided dice: the probability of rolling a 2 on the first die and a 1 on the second die is (1/6)*(1/6) = 1/36.

### The Diode Testing Problem

You work at an electronics manufacturing firm that produces diodes. Quality control engineers want to detect faulty diodes before shipping. The problem is to minimize the average testing cost per diode.

**Known parameters:**
- 0.3% of diodes are faulty (probability q = 0.003)
- 99.7% of diodes are good (probability 1 - q = 0.997)
- Testing one diode individually costs 5 cents
- Testing a batch of n diodes costs 4 + n cents (4 cents base plus 1 cent per diode)
- If a batch contains any faulty diode, you must then test each diode individually at 5 cents per diode

**Decision variable:** n = number of diodes per test group (batch size)

**Random variable:** C = testing cost for a group (depends on whether the group contains faulty diodes)

**Objective:** Minimize A = average testing cost per diode = E[C] / n

### Computing the Expected Cost

The expected cost E[C] depends on two possible outcomes:

1. The group contains no faulty diodes (probability P)
2. The group contains at least one faulty diode (probability 1 - P)

**Step 1: Find P, the probability that all n diodes in a batch are good.**

Since each diode is independent and has a 0.997 probability of being good:

P = (0.997)^n

**Step 2: Write the expected value formula.**

E[C] = (cost if no faults) * P + (cost if at least one fault) * (1 - P)

Cost if no faults = 4 + n (just the batch test)
Cost if at least one fault = (4 + n) + 5n = 4 + 6n (batch test plus individual testing of all n diodes)

Therefore:

E[C] = (4 + n) * (0.997)^n + (4 + 6n) * (1 - (0.997)^n)

**Step 3: Simplify the expression.**

E[C] = 4 + 6n - 5n * (0.997)^n

**Step 4: Compute the average cost per diode.**

A(n) = E[C] / n = (4/n) + 6 - 5 * (0.997)^n

### Finding the Optimal Batch Size

To minimize A(n), take the derivative with respect to n and set it equal to zero. The result is:

Optimal batch size n = 17
Minimum average cost A = 1.48 cents per diode

This means you should organize diodes into batches of 17. The machine tests each batch for 21 cents (4 base plus 17 cents). Most batches pass, but when a batch fails, you pay 5 cents per diode to test all 17 individually.

### Sensitivity to Batch Size Constraints

The factory may only allow batch sizes in multiples of 5 (e.g., 15 or 20). The function A(n) is flat near the minimum, so moving to n=15 or n=20 increases the average cost only slightly. This gives you flexibility in implementation.

### Sensitivity to Fault Probability

The fault probability q = 0.003 is an estimate based on historical data. You need to know how sensitive the optimal solution is to changes in this estimate.

**Step 1: Rewrite A in terms of q.**

Since (0.997)^n = (1 - q)^n:

A(n) = (4/n) + 6 - 5 * (1 - q)^n

**Step 2: Compute the sensitivity of A with respect to q at n=17.**

The sensitivity S(A, q) is the relative change in A divided by the relative change in q:

S(A, q) = (dA/dq) * (q/A)

First, compute dA/dq:

dA/dq = -5 * n * (1 - q)^(n-1) * (-1) = 5n * (1 - q)^(n-1)

At n=17 and q=0.003:

dA/dq = 5 * 17 * (0.997)^16

(0.997)^16 is approximately 0.953

dA/dq is approximately 5 * 17 * 0.953 = 81.0

Now compute S(A, q):

S(A, q) = 81.0 * (0.003 / 1.48) = 81.0 * 0.00203 = 0.164

**Step 3: Interpret the sensitivity value.**

S(A, q) = 0.16 means that for every 1% change in q, A changes by only 0.16%. This is a very small sensitivity, indicating the model is robust to errors in estimating the fault probability.

### Why Sensitivity Matters

The fault probability q is always an estimate. Historical data might show 0.2997% or 0.301% faulty diodes. Factory conditions (humidity, temperature) can cause temporary fluctuations. A low sensitivity value means you can trust your optimal batch size even if the true fault probability differs slightly from your estimate.

### Summary of Key Results

| Quantity | Value |
|----------|-------|
| Optimal batch size n | 17 |
| Minimum average cost A | 1.48 cents per diode |
| Sensitivity S(A, q) | 0.16 |
| Interpretation | 1% change in q causes 0.16% change in A |

### Check Your Understanding

1. Why is the expected value formula for E[C] written as a weighted sum of two terms?

<details><summary>Answer</summary>Because there are only two possible outcomes for a batch: either it contains no faulty diodes (probability P) or it contains at least one faulty diode (probability 1-P). The expected value is the sum of each outcome's cost multiplied by its probability.</details>

2. What does a sensitivity value of 0.16 tell you about the model's robustness?

<details><summary>Answer</summary>It tells you the model is very robust. A 1% change in the fault probability q causes only a 0.16% change in the average cost A. Even if the true fault probability differs from the estimate, the optimal batch size still gives nearly the same average cost.</details>

3. If the factory can only test batches in multiples of 5, why is n=15 or n=20 acceptable?

<details><summary>Answer</summary>The function A(n) is flat near the minimum at n=17. Moving to n=15 or n=20 increases the average cost only slightly, so the solution is insensitive to small changes in batch size.</details>

4. How does the independence assumption affect the calculation of P?

<details><summary>Answer</summary>Independence allows you to multiply individual probabilities. Since each diode has a 0.997 probability of being good, the probability that all n diodes are good is (0.997)^n. Without independence, you could not simply multiply these probabilities.</details>
## Key takeaways

- Discrete probability models use random variables that take finitely many states, each with a probability between 0 and 1, and all probabilities sum to 1 because of the completeness of information assumption.
- The expected value of a discrete random variable is calculated as a weighted sum of outcomes and their probabilities.
- Two discrete random variables are independent if the probability of both taking specific values equals the product of their individual probabilities.
- The diode testing problem illustrates how to formulate a real world quality control problem as a discrete probability model using the five step method: define variables, assign probabilities, compute expected cost, optimize, and perform sensitivity analysis.
- The expected testing cost per batch is derived as 4 plus 6n minus 5n times 0.997 to the n, leading to the average cost per diode function a equals 4 over n plus 6 minus 5 times 0.997 to the n.
- The optimal batch size that minimizes average testing cost per diode is n equals 17, yielding an average cost of 1.48 cents per diode.
- The cost function is flat near the minimum, so using batch sizes of 15 or 20 instead of 17 does not increase cost significantly.
- Sensitivity analysis shows that a 1 percent change in the estimated fault probability causes only a 0.16 percent change in the average cost, indicating the model is robust to estimation errors.
- This example demonstrates how probability can be used to remove randomness through expected values, reducing the problem to a deterministic optimization.
- The five step method provides a structured approach to building, solving, and interpreting discrete probability models in real world applications.
## Glossary

| Term | Definition |
|---|---|
| discrete probability distribution | A list of all possible values a discrete random variable can take together with the probability of each value, where all probabilities are between 0 and 1 and sum to 1. |
| random variable | A variable whose possible values are numerical outcomes of a random phenomenon, often denoted by capital letters like X or C. |
| state | One of the finitely many possible values that a discrete random variable can take. |
| probability | A number between 0 and 1 that measures the likelihood of a specific outcome occurring, with 1 meaning certainty and 0 meaning impossibility. |
| completeness of information assumption | The assumption that all possible states of a random variable are known and that the probabilities of those states sum to 1, accounting for every possible outcome. |
| expected value | The long run average of a random variable, computed as the sum of each outcome multiplied by its probability. |
| weighted sum | A sum where each term is multiplied by a weight, in this context the weight is the probability of the corresponding outcome. |
| independence | The property of two random variables such that the probability of both taking specific values is the product of their individual probabilities, meaning the outcome of one does not affect the other. |
| faulty diode | A diode that does not meet quality standards and must be detected before shipment, estimated to occur with a probability of 0.3 percent in the example. |
| batch testing | A quality control procedure where multiple items are tested together as a group rather than individually, with a cost structure that may include a fixed base fee plus a per item fee. |
| cost function | A mathematical expression that describes the total cost of testing a batch of diodes as a function of the batch size and the presence of faulty diodes. |
| average cost | The expected cost per diode, obtained by dividing the expected testing cost of a batch by the number of diodes in that batch. |
| decision variable | A variable that the modeler can control, in this case the batch size n, which is chosen to optimize the outcome. |
| optimization | The process of finding the value of the decision variable that minimizes or maximizes the objective function, here minimizing the average cost per diode. |
| derivative | A mathematical tool that measures the rate of change of a function; setting the derivative to zero helps find local minima or maxima. |
| sensitivity analysis | The study of how the output of a model (here the average cost) changes in response to changes in input parameters (here the fault probability). |
| relative change | A measure of change expressed as a percentage of the original value, often used in sensitivity analysis via elasticity. |
| elasticity | A dimensionless sensitivity measure calculated as the ratio of the percentage change in the output to the percentage change in the input, here computed as 0.16 for the average cost with respect to fault probability. |
| robustness | The property of a model being relatively insensitive to errors or variations in input parameters, meaning the output remains close to the optimum even when inputs are not perfectly accurate. |
| five step method | A structured approach to mathematical modeling: ask the question, select the modeling approach, formulate the model, solve the model, and interpret the results. |
## Footnotes and deeper context

1. **Independence of diodes.** The model assumes that each diode's fault status is independent of others. In practice, defects may cluster due to manufacturing batch issues, which could violate this assumption. The model's robustness should be checked against clustered defects.
2. **Expected value derivation.** The expected cost formula E[C] = 4 + 6n - 5n(0.997)^n comes from simplifying the sum of (4+n) * (0.997)^n plus (4+n+5n) * (1 - 0.997)^n. The term 4+n+5n simplifies to 4+6n because the individual testing cost of 5n is added to the batch test cost of 4+n.
3. **Optimization using calculus.** The derivative of the average cost function a(n) = 4/n + 6 - 5(0.997)^n is set to zero to find the critical point. Since n is integer, the optimal integer batch size is 17, but the continuous approximation gives a value near 17.2; rounding to 17 is appropriate.
4. **Sensitivity measure elasticity.** The elasticity of a with respect to q is computed as (da/dq) * (q/a) at n=17. The result 0.16 means that a 1% increase in the fault probability q leads to only a 0.16% increase in average cost a, confirming low sensitivity.
5. **Five step method in the video.** The video does not explicitly enumerate the five steps but follows them: step 1 is asking how to minimize testing cost, step 2 is choosing a discrete probability model, step 3 is formulating the expected cost function, step 4 is solving for n=17, and step 5 is interpreting the sensitivity results.
6. **Cost structure assumptions.** The example uses hypothetical costs: 5 cents per individual test, 4 cents base plus 1 cent per diode for batch testing. Real world costs may differ, and additional factors like machine downtime or labor rates could affect the optimal batch size. The model should be recalibrated with actual cost data.
7. **Continuity of n.** In the derivative step, n is treated as a continuous variable. For integer n, the optimal value is found by checking values around 17. The cost at n=17 and n=18 are nearly identical, so the model's recommendation is robust to integer rounding.
## Where to go next

- **Introduction to Probability by Grinstead and Snell.** This free online textbook provides a thorough foundation in discrete probability, including expectation, independence, and applications. It covers the concepts used in the diode testing problem in greater depth.
- **Mathematical Modeling by Mark M. Meerschaert.** This book explains the five step method in detail and applies it to many modeling scenarios, including probabilistic models. It is a canonical resource for learning how to structure and solve real world problems mathematically.
- **Khan Academy Probability and Statistics.** A free online resource with video lessons and exercises on discrete random variables, expected value, and independence. It is useful for beginners who need to review the probability basics assumed in the course.
- **Desmos Graphing Calculator.** An online tool that can plot the average cost function a(n) = 4/n + 6 - 5*(0.997)^n and allow you to explore the flat region around the minimum. This helps in understanding sensitivity to batch size visually.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
