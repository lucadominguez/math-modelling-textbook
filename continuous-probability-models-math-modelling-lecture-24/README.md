# Continuous Probability Models for Mathematical Modeling
> **Source:** [Continuous Probability Models - Math Modelling - Lecture 24](https://www.youtube.com/watch?v=0qi6s-injSo) by Math Modelling · 27:13 · Training document generated from the video.
**How to use this document:** read it top to bottom in place of watching the video. Screenshots appear exactly where the video depends on something visual, with links that jump to that moment. Questions at the end of each section confirm you learned the material. The glossary and footnotes add definitions and detail the video assumes you already have.
**Who this is for:** This course is for students or practitioners who have some background in calculus and discrete probability and want to learn how to model real-world waiting times and arrival processes using continuous probability distributions.
## Learning objectives

After working through this document you can:

1. Define a probability distribution function and a probability density function for a continuous random variable
2. Compute probabilities of intervals by integrating the density function
3. Calculate the expected value of a continuous random variable using integration
4. Describe the exponential distribution and its rate parameter lambda
5. Explain the lack of memory property of the exponential distribution and its practical meaning
6. Apply the exponential distribution to model waiting times in a radioactive decay example
7. Use the strong law of large numbers to estimate an unknown decay rate from observed data
8. Perform a sensitivity analysis to understand how the locking time affects the accuracy of the estimate
## Prerequisites

- Basic calculus: integration and differentiation
- Familiarity with discrete probability models (e.g., random variables, expected value)
- Understanding of the concept of a limit and Riemann sums
## Introduction to Continuous Probability Models

This section introduces continuous probability models, which describe random variables that can take any value within a range or interval. Unlike discrete models where outcomes are countable (like the six faces of a die), continuous models handle outcomes like time, distance, or temperature that can be any real number.

### Discrete vs. Continuous Random Variables

In the previous lecture, you learned about discrete probability models. A discrete random variable can only take on a countable number of distinct values. For example, rolling a standard six-sided die produces only the numbers 1, 2, 3, 4, 5, or 6. There are exactly six possible outcomes.

A continuous random variable, by contrast, can take on a continuum of values. It could be pi (3.14159...), e (2.71828...), 10, or any other real number along the real line. There are infinitely many possible values, even within a small interval.

### Probability Distribution Function (CDF)

For a continuous random variable, we define the probability that the variable is less than or equal to some number x. We write this as:

**F(x) = P(X ≤ x)**

Here:
- **X** (capital X) is the continuous random variable.
- **x** (lowercase x) is a specific number (like 3, 5, or 7).
- **F(x)** is called the **probability distribution function** (also known as the cumulative distribution function or CDF).

The probability distribution function F(x) gives the probability that the random variable X is less than or equal to the value x.

### Probability Density Function (PDF)

The **density function**, denoted as **f(x)** (lowercase f), is the derivative of the probability distribution function:

**f(x) = d/dx F(x)**

This relationship is fundamental. The density function f(x) describes how probability is distributed across the range of possible values. The distribution function F(x) accumulates that probability from negative infinity up to x.

| Term | Symbol | Definition | Role |
|------|--------|------------|------|
| Probability Distribution Function | F(x) | P(X ≤ x) | Gives cumulative probability up to x |
| Probability Density Function | f(x) | d/dx F(x) | Describes probability density at each point |

### Calculating Probabilities for Intervals

In practice, you are usually given the density function f(x). To find the probability that a continuous random variable X lies between two values a and b, use the fundamental theorem of calculus:

**P(a ≤ X ≤ b) = F(b) - F(a) = ∫ from a to b of f(x) dx**

This works because:
1. F(b) = P(X ≤ b) is the probability that X is less than or equal to b.
2. F(a) = P(X ≤ a) is the probability that X is less than or equal to a.
3. Subtracting removes everything less than a, leaving only the probability that X is between a and b.

The integral of the density function from a to b gives this same probability. Calculating probabilities for continuous random variables is therefore an integration problem.

(Added context: This connection between probability and integration is why continuous probability theory is deeply linked to calculus and, at more advanced levels, to measure theory. Measure theory provides a rigorous foundation for integration and probability.)

### Expected Value of a Continuous Random Variable

The **expected value** (or mean) of a continuous random variable X with density function f(x) is:

**E[X] = ∫ from -∞ to ∞ of x * f(x) dx**

This formula assumes the random variable can take values anywhere on the real line. If the variable is restricted to positive values only (for example, from 0 to infinity), the bounds of integration change accordingly:

**E[X] = ∫ from 0 to ∞ of x * f(x) dx**

The bounds are not fixed to negative infinity to positive infinity. You adjust them to match the domain of your random variable.

This integral representation comes from thinking about the limit of discrete probability events. Imagine dividing the domain into many small pieces. For each piece, you multiply the value of x by its probability (approximated by f(x) times the width of the piece). As the pieces become smaller and more numerous, the sum converges to an integral, just as Riemann sums converge to integrals in basic calculus.

### Key Relationships Summary

| Concept | Formula | Notes |
|---------|---------|-------|
| Distribution function | F(x) = P(X ≤ x) | Cumulative probability |
| Density function | f(x) = d/dx F(x) | Derivative of distribution |
| Probability in interval | P(a ≤ X ≤ b) = ∫ from a to b of f(x) dx | Integration of density |
| Expected value | E[X] = ∫ from -∞ to ∞ of x * f(x) dx | Bounds depend on domain |

### Check Your Understanding

1. What is the difference between a discrete random variable and a continuous random variable?

<details><summary>Answer</summary>
A discrete random variable can only take on a countable number of distinct values (like the numbers 1 through 6 on a die). A continuous random variable can take on any value within a range or interval (like any real number along the real line).
</details>

2. If you are given the density function f(x) for a continuous random variable, how do you calculate the probability that X lies between 2 and 5?

<details><summary>Answer</summary>
You integrate the density function from 2 to 5: P(2 ≤ X ≤ 5) = ∫ from 2 to 5 of f(x) dx. This is equivalent to F(5) - F(2), where F is the cumulative distribution function.
</details>

3. What is the relationship between the probability distribution function F(x) and the probability density function f(x)?

<details><summary>Answer</summary>
The density function f(x) is the derivative of the distribution function F(x). That is, f(x) = d/dx F(x). Conversely, F(x) is the integral of f(x) from negative infinity to x.
</details>

4. How does the expected value formula for a continuous random variable relate to sums for discrete random variables?

<details><summary>Answer</summary>
The expected value for a continuous random variable is an integral (∫ x * f(x) dx), which is the limit of a Riemann sum. For a discrete random variable, the expected value is a sum (∑ x * P(X = x)). The integral is the continuous analog of the discrete sum, where the density function f(x) replaces the probability mass function P(X = x).
</details>
## The Exponential Distribution and Lack of Memory

This section introduces the exponential distribution, a continuous probability model used to describe waiting times for events. You will learn its probability density function, how the rate parameter controls behavior, and the unique property of "lack of memory" that distinguishes this distribution.

### The Exponential Distribution as a Waiting-Time Model

The exponential distribution models the time you wait for an event to occur. Common examples include waiting for a customer to arrive at a store or waiting for a machine to fail. The independent variable is typically denoted by \( T \) because it represents time.

The probability that an event has *not* occurred by time \( t \) is given by the survival function:

\[
P(T > t) = e^{-\lambda t}
\]

Here, \( \lambda \) (lambda) is the **rate parameter**, and it must be greater than zero (\( \lambda > 0 \)).

**How the rate parameter works:**
- A **larger** lambda means the probability \( e^{-\lambda t} \) goes to zero **faster**. This corresponds to events happening more frequently (shorter waiting times).
- A **smaller** lambda means the probability goes to zero **slower**. This corresponds to events happening less frequently (longer waiting times).

**Intuition:** If customers arrive at a store at an average rate of one per hour, and it has been 55 minutes since the last customer, the probability that a customer will arrive soon is much higher than if a customer had just walked in. The exponential distribution captures this idea: the longer you wait, the more likely the event becomes.

### The Probability Density Function (PDF)

The **probability density function** (PDF) for the exponential distribution is:

\[
f(t) = \lambda e^{-\lambda t}
\]

This function describes the relative likelihood of the waiting time being exactly \( t \). To compute the probability that the waiting time falls within a specific interval, you integrate the PDF over that interval.

For example, to find the probability that a customer arrives between 1 hour and 2 hours:

\[
P(1 < T < 2) = \int_{1}^{2} \lambda e^{-\lambda t} \, dt
\]

This integral is the continuous analog of summing probabilities in a discrete distribution. You can compute it using the cumulative distribution function (CDF), which is \( P(T \leq t) = 1 - e^{-\lambda t} \).

### Conditional Probability and Lack of Memory

To understand the exponential distribution's unique property, you first need the definition of **conditional probability**. The probability that event A happens given that event B has already happened is:

\[
P(A \mid B) = \frac{P(A \cap B)}{P(B)}
\]

Here, \( A \cap B \) means both A and B occur.

#### The Lack of Memory Property

The exponential distribution has a property called **lack of memory** (also called memorylessness). This property is unique to the exponential distribution among continuous distributions (and the geometric distribution among discrete ones).

The lack of memory property states:

\[
P(X > s + t \mid X > s) = P(X > t)
\]

In words: If you have already waited \( s \) time units without the event occurring, the probability that you will wait an additional \( t \) time units is exactly the same as the probability of waiting \( t \) time units from the start.

**Proof using the exponential distribution:**

Start with the conditional probability formula:

\[
P(X > s + t \mid X > s) = \frac{P(X > s + t \cap X > s)}{P(X > s)}
\]

Since \( s + t > s \), the event \( X > s + t \) is a subset of \( X > s \). Therefore, the intersection is just \( X > s + t \):

\[
P(X > s + t \mid X > s) = \frac{P(X > s + t)}{P(X > s)}
\]

Now substitute the exponential survival function \( P(X > t) = e^{-\lambda t} \):

\[
P(X > s + t \mid X > s) = \frac{e^{-\lambda (s + t)}}{e^{-\lambda s}} = e^{-\lambda t}
\]

And \( e^{-\lambda t} \) is exactly \( P(X > t) \). Therefore:

\[
P(X > s + t \mid X > s) = P(X > t)
\]

**What this means in practice:** If you have already waited \( s \) minutes for a bus, the probability that you will wait another \( t \) minutes is the same as if you had just arrived at the bus stop. The past waiting time gives you no information about the remaining waiting time. This is why it is called "lack of memory": the distribution does not remember how long you have already waited.

### Check Your Understanding

1. **Question:** A call center receives calls at an average rate of 10 per hour. What is the probability that no call arrives in the next 6 minutes (0.1 hours)?

<details><summary>Answer</summary>
The rate parameter \( \lambda = 10 \) per hour. The probability of no call in 0.1 hours is \( P(T > 0.1) = e^{-10 \times 0.1} = e^{-1} \approx 0.3679 \).
</details>

2. **Question:** Using the lack of memory property, if you have already waited 30 minutes for a bus and the average waiting time is 15 minutes, what is the probability you will wait another 10 minutes?

<details><summary>Answer</summary>
The lack of memory property says \( P(X > 30 + 10 \mid X > 30) = P(X > 10) \). With \( \lambda = 1/15 \) per minute, \( P(X > 10) = e^{-(1/15) \times 10} = e^{-2/3} \approx 0.5134 \). The past 30 minutes of waiting do not affect this probability.
</details>

3. **Question:** True or false: The exponential distribution is the only continuous distribution that has the lack of memory property.

<details><summary>Answer</summary>
True. Among continuous distributions, only the exponential distribution has the lack of memory property. (The geometric distribution is its discrete counterpart.)
</details>

4. **Question:** If \( \lambda = 0.5 \), what is the probability that the waiting time is greater than 3 time units?

<details><summary>Answer</summary>
\( P(T > 3) = e^{-0.5 \times 3} = e^{-1.5} \approx 0.2231 \).
</details>
## Modeling Radioactive Decay with a Locking Counter

In this section we build a continuous probability model for a radioactive decay counter that “locks” for a fixed time after each detected decay. The goal is to understand how the observed waiting times between recorded decays relate to the true decay rate of the material.

### The memoryless property of the exponential distribution

Before we dive into the model, recall a key property of the exponential distribution: it is memoryless. This means that the probability of an event occurring in the next instant does not depend on how long you have already waited. The past does not matter. As the video puts it, “it doesn’t matter how long I waited. All that matters is how far you go in the future now.” This property will be important when we later model the additional waiting time after the counter unlocks.

### Problem setup

We have a sample of radioactive material that decays at an unknown rate. A counter detects each decay, but after registering a decay the counter locks for a fixed period of time. During this lock time no other decay can be recorded. The lock time is very small:

- Locking time `a = 3 × 10⁻⁹` seconds.

Because of this locking, some decays may be missed. We need to adjust the observed data to recover the true decay rate.

Define the following variables:

| Variable | Meaning |
|----------|---------|
| `λ` (lambda) | True decay rate of the material (per second) |
| `T_n` | Time of the n‑th recorded decay (as observed by the counter) |
| `x_n` | Time between the (n‑1)‑th and n‑th recorded decays: `x_n = T_n - T_{n-1}` |
| `a` | Locking time (3 × 10⁻⁹ seconds) |
| `y_n` | Additional waiting time beyond the lock time: `y_n = x_n - a` |

Because the counter locks for exactly `a` seconds after each recorded decay, the next decay cannot be recorded until at least `a` seconds have passed. Therefore:

`x_n ≥ a` with probability 1.

This lower bound means that `x_n` cannot follow an exponential distribution. An exponential random variable can take any non‑negative value, including values smaller than `a`. So we must decompose the waiting time into two parts:

1. The fixed lock time `a` (always present).
2. The random additional time `y_n` that we must wait after the counter unlocks until the next decay occurs.

### Modeling the additional waiting time

After the counter unlocks, the process “forgets” that it waited. The decays occur at random times with rate `λ`. The time until the next decay after the counter unlocks is therefore exponentially distributed with rate `λ`. That is:

`y_n ~ Exponential(λ)`

The probability density function (PDF) of `y_n` is:

`f(y) = λ e^{-λ y}` for `y ≥ 0`.

This is valid because the exponential distribution is memoryless: the fact that we already waited `a` seconds during the lock does not affect the future waiting time.

### Expected waiting time between recorded decays

We want the average value of `x_n`, the total time between recorded decays. Because expectation is linear:

`E[x_n] = E[a + y_n] = a + E[y_n]`

The expected value of an exponential random variable with rate `λ` is `1/λ`. This can be computed from the definition:

`E[y_n] = ∫₀^∞ t · λ e^{-λ t} dt`

Evaluating this integral (using integration by parts or known result) gives `1/λ`. Therefore:

`E[x_n] = a + 1/λ`

This formula tells us that the average observed waiting time is the lock time plus the average time between true decays. If the decay rate `λ` is very high (many decays per second), then `1/λ` is very small, and the observed waiting time is dominated by the lock time `a`. Conversely, if `λ` is low, the waiting time is mostly the exponential part.

### Summary of the model

- The observed waiting times `x_n` are not exponential because they have a minimum value `a`.
- By subtracting the fixed lock time, we obtain `y_n = x_n - a`, which is exponentially distributed with rate `λ`.
- The expected observed waiting time is `a + 1/λ`.

This decomposition allows us to estimate the true decay rate `λ` from the observed data: compute the average of the `x_n` values, subtract `a`, and take the reciprocal.

### Check your understanding

1. Why can’t we model the observed waiting time `x_n` directly as an exponential distribution?

<details><summary>Answer</summary>
Because an exponential distribution can take any non‑negative value, but `x_n` is always at least `a = 3 × 10⁻⁹` seconds. The exponential distribution would assign positive probability to values smaller than `a`, which is impossible due to the locking mechanism.
</details>

2. What property of the exponential distribution justifies modeling `y_n` as exponential after the lock time ends?

<details><summary>Answer</summary>
The memoryless property. After the counter unlocks, the time until the next decay does not depend on how long we already waited (the lock time). The process “starts fresh,” so the remaining waiting time follows the same exponential distribution as the original decay process.
</details>

3. If the true decay rate `λ` is 10⁶ decays per second, what is the expected observed waiting time `E[x_n]`? (Recall `a = 3 × 10⁻⁹` seconds.)

<details><summary>Answer</summary>
`E[x_n] = a + 1/λ = 3 × 10⁻⁹ + 1/10⁶ = 3 × 10⁻⁹ + 10⁻⁶ = 1.003 × 10⁻⁶` seconds. The lock time adds only a tiny fraction to the expected waiting time when the decay rate is high.
</details>

4. How would you estimate `λ` from a set of observed waiting times `x₁, x₂, …, x_N`?

<details><summary>Answer</summary>
Compute the sample mean `x̄ = (1/N) Σ x_i`. Then subtract the known lock time `a` to get an estimate of `E[y_n]`. Since `E[y_n] = 1/λ`, the estimate of `λ` is `1 / (x̄ - a)`. (Note: this estimator is valid only if `x̄ > a`.)
</details>
## Estimating the Decay Rate Using the Law of Large Numbers

In this section you will derive a practical estimator for the unknown decay rate \(\lambda\) of a radioactive source. The derivation uses only the observed times of decay events, the known locking time \(a\), and the Strong Law of Large Numbers. By the end of this section you will be able to compute an approximate value of \(\lambda\) from a finite set of observations.

### Review: Expected Waiting Time

Recall from the previous section that the expected waiting time between two consecutive recorded decays is:

\[
E[X_i] = a + \frac{1}{\lambda}
\]

Here:

- \(a\) is the locking time (the fixed dead time after each decay during which the detector cannot record a new event).
- \(\frac{1}{\lambda}\) is the mean of the exponential distribution that models the actual decay time (the time between the end of the lock and the next decay).
- \(X_i\) is the \(i\)-th waiting time: the time from the end of the \((i-1)\)-th lock to the end of the \(i\)-th lock.

Because every \(X_i\) has the same distribution, they all have the same mean \(E[X_i] = a + 1/\lambda\).

### The Strong Law of Large Numbers (SLLN)

The Strong Law of Large Numbers states: if you have a sequence of independent, identically distributed random variables with finite mean \(\mu\), then the sample average converges almost surely to \(\mu\) as the number of observations goes to infinity.

In our context, let \(X_1, X_2, \dots, X_n\) be the waiting times. The SLLN says:

\[
\frac{1}{n} \sum_{i=1}^{n} X_i \xrightarrow{\text{a.s.}} E[X_i] = a + \frac{1}{\lambda} \quad \text{as } n \to \infty.
\]

This is a theoretical limit. For a finite but large \(n\) we can write an approximation:

\[
\frac{1}{n} \sum_{i=1}^{n} X_i \approx a + \frac{1}{\lambda}.
\]

### Telescoping Sum of Waiting Times

We can simplify the sum \(\sum_{i=1}^{n} X_i\) by using the definition of each waiting time. Let \(t_0 = 0\) be the moment you start the clock. After the first lock, the detector records the first decay at time \(t_1\). The first waiting time is \(X_1 = t_1 - t_0\). The second waiting time is \(X_2 = t_2 - t_1\), and so on. In general:

\[
X_i = t_i - t_{i-1}.
\]

Now substitute these into the sum:

\[
\sum_{i=1}^{n} X_i = (t_1 - t_0) + (t_2 - t_1) + (t_3 - t_2) + \cdots + (t_n - t_{n-1}).
\]

This is a telescoping sum: all intermediate terms cancel. Because \(t_0 = 0\), we obtain:

\[
\sum_{i=1}^{n} X_i = t_n.
\]

The sum of the first \(n\) waiting times equals the time of the \(n\)-th recorded decay (the time since the clock started).

### Deriving the Estimator for \(\lambda\)

Combine the SLLN approximation with the telescoping result:

\[
\frac{1}{n} \sum_{i=1}^{n} X_i = \frac{t_n}{n} \approx a + \frac{1}{\lambda}.
\]

Now solve for \(\lambda\):

1. Multiply both sides by \(n\): \(t_n \approx n a + \frac{n}{\lambda}\).
2. Subtract \(n a\): \(t_n - n a \approx \frac{n}{\lambda}\).
3. Invert: \(\lambda \approx \frac{n}{t_n - n a}\).

Thus the estimator for the decay rate is:

\[
\boxed{\lambda \approx \frac{n}{t_n - n a}}
\]

where:

- \(n\) is the number of recorded decays.
- \(t_n\) is the time of the \(n\)-th decay (measured from the start of the experiment).
- \(a\) is the known locking time.

### Important Notes

- The approximation is valid only for large \(n\). The SLLN guarantees convergence as \(n \to \infty\); for finite \(n\) the estimate is approximate.
- The formula accounts for the locking time even if many decays occur during the lock period. The model does not require you to observe those hidden decays; the estimator automatically adjusts for them.
- If the locking time were zero (\(a = 0\)), the estimator would simplify to \(\lambda \approx n / t_n\), which is the classical maximum likelihood estimator for an exponential distribution without dead time. The presence of \(a\) shifts the denominator.

### Check Your Understanding

1. **Why can we replace \(\sum_{i=1}^n X_i\) with \(t_n\)?**  
   <details><summary>Answer</summary>  
   Because each \(X_i = t_i - t_{i-1}\) and \(t_0 = 0\), the sum telescopes to \(t_n\).  
   </details>

2. **What does the Strong Law of Large Numbers tell us about the average of the waiting times?**  
   <details><summary>Answer</summary>  
   It says that the average \(\frac{1}{n}\sum X_i\) converges almost surely to the common expected value \(a + 1/\lambda\) as \(n\) grows large.  
   </details>

3. **Suppose you record 100 decays, the 100th decay occurs at \(t_{100} = 250\) seconds, and the locking time is \(a = 0.5\) seconds. Estimate \(\lambda\).**  
   <details><summary>Answer</summary>  
   \(\lambda \approx \frac{100}{250 - 100 \times 0.5} = \frac{100}{250 - 50} = \frac{100}{200} = 0.5\) decays per second.  
   </details>

4. **If the locking time is unknown, can you still estimate \(\lambda\) using only the observed times?**  
   <details><summary>Answer</summary>  
   No. The estimator requires \(a\) explicitly. Without \(a\) you cannot separate the effect of the lock from the true decay rate. You would need at least two different experimental conditions to estimate \(a\) and \(\lambda\) simultaneously.  
   </details>
## Sensitivity Analysis and Conclusion

The exponential distribution models waiting times or arrival processes. In the radioactive decay example, the longer you wait, the higher the probability that a decay occurs. This same logic applies to a shopkeeper waiting for customers. The exponential distribution is simple but powerful.

### Approximation error from the strong law of large numbers

The strong law of large numbers states that the sample average converges to the true expected value only in the limit as the number of observations \(n\) goes to infinity. In practice, you cannot make an infinite number of observations. You must replace the limit with a finite number of observations, which introduces an approximation error. Be careful: the convergence is guaranteed only in the limit. The more observations you collect, the closer your estimate will be, but you never eliminate the error entirely.

### Sensitivity to the stopping time \(A\)

The stopping time \(A\) (also called the locking time) is the number of seconds the system is locked and unable to record decays. The estimated decay rate \(\lambda\) depends on \(A\). To quantify this dependence, compute the derivative of \(\lambda\) with respect to \(A\). The sensitivity is given by

\[
\frac{d\lambda}{dA} = \lambda \cdot A.
\]

This result comes from setting up the relationship between the estimate and the stopping time and then differentiating. (You can verify the derivative yourself using the chain rule.)

#### Interpretation of the sensitivity

The product \(\lambda \cdot A\) represents the expected number of decays that occur while the system is locked. This is the amount of information lost during each lock period.

- If \(A\) is very small, the sensitivity is small. You lose very little information.
- If \(\lambda\) is very large, many decays happen during the lock. You miss a lot of information, so the sensitivity is high.
- If \(\lambda\) is very small, almost no decays occur during the lock. You lose almost no information, and the sensitivity is low.

Thus, the sensitivity tells you how much information you lose every time you lock the system. To reduce sensitivity, you can shorten the locking time \(A\). If the system locks for longer, you risk missing more decays and the estimate becomes more sensitive to the exact value of \(A\).

### Conclusion

Even with a stopping time, you can still estimate the decay rate \(\lambda\) using the exponential distribution and the strong law of large numbers approximation. However, the estimate has a sensitivity that depends on both \(\lambda\) and \(A\). The symbolic result \(\frac{d\lambda}{dA} = \lambda A\) captures this dependence elegantly. The longer you stop, the more information you potentially lose.

In the next video, we will discuss statistics and the normal distribution (the bell curve), building on the intuition and methods developed here.

### Check your understanding

1.  Why does the strong law of large numbers introduce an approximation error when estimating the decay rate?

    <details><summary>Answer</summary>
    The strong law of large numbers guarantees convergence only in the limit as the number of observations goes to infinity. In practice, you use a finite number of observations, so the estimate is an approximation.
    </details>

2.  What does the sensitivity \(\lambda \cdot A\) represent physically?

    <details><summary>Answer</summary>
    It represents the expected number of decays that occur while the system is locked. This is the amount of information lost during each lock period.
    </details>

3.  If the decay rate \(\lambda\) is very small, is the sensitivity high or low? Explain why.

    <details><summary>Answer</summary>
    The sensitivity is low because \(\lambda \cdot A\) is small. When \(\lambda\) is small, very few decays happen during the lock, so you lose almost no information.
    </details>

4.  How can you reduce the sensitivity of the estimate to the stopping time?

    <details><summary>Answer</summary>
    By making the stopping time \(A\) smaller. A shorter lock period reduces the expected number of missed decays, lowering the sensitivity.
    </details>
## Key takeaways

- A continuous random variable can take any value in an interval, and its probability is described by a probability density function (PDF) rather than a probability mass function.
- The probability that a continuous random variable lies in an interval equals the integral of its PDF over that interval.
- The expected value of a continuous random variable is the integral of x times its PDF over the entire domain.
- The exponential distribution with rate parameter lambda models waiting times for events that occur at a constant average rate.
- The exponential distribution is memoryless: the probability of waiting an additional t units given that you have already waited s units equals the probability of waiting t units from the start.
- In a radioactive decay experiment with a locking counter, each decay locks the counter for a fixed time a, so the observed waiting time Xn is at least a.
- The additional waiting time beyond the lock time is exponentially distributed with rate lambda, leading to expected waiting time E[Xn] = a + 1/lambda.
- The strong law of large numbers implies that the average of observed waiting times converges to the expected value, allowing estimation of lambda from the total observation time Tn.
- The estimated decay rate lambda is approximately n divided by ( Tn minus n times a ), where n is the number of observed decays.
- Sensitivity analysis shows that the derivative d(lambda)/da equals lambda times a, which represents the expected number of decays missed during each lock period.
## Glossary

| Term | Definition |
|---|---|
| continuous random variable | A random variable that can take any value within a continuous range (e.g., real numbers) rather than a countable set of discrete values. |
| probability distribution function (CDF) | A function F(x) that gives the probability that a random variable X is less than or equal to a value x. |
| probability density function (PDF) | The derivative of the cumulative distribution function; the PDF f(x) describes the relative likelihood of a continuous random variable taking a particular value. |
| expected value | The long-run average value of a random variable, computed as the integral of x times the PDF over the domain. |
| exponential distribution | A continuous probability distribution with PDF f(t) = lambda * e^{-lambda t} for t >= 0, used to model the time between events in a Poisson process. |
| rate parameter (lambda) | A positive parameter that controls the speed of decay in the exponential distribution; larger lambda means shorter expected waiting times. |
| lack of memory property | A property of the exponential distribution where the probability of waiting an additional t units does not depend on how long you have already waited. |
| conditional probability | The probability of an event A occurring given that event B has already occurred, written as P(A|B) = P(A and B) / P(B). |
| radioactive decay | A random process where unstable atomic nuclei emit radiation; the time between decays often follows an exponential distribution. |
| locking time (a) | A fixed period during which a counter cannot record new decays after detecting one; in the example, a = 3e-9 seconds. |
| observation time (Tn) | The time of the nth recorded decay as measured by the counter. |
| waiting time (Xn) | The time interval between two successive recorded decays; Xn = Tn - T_{n-1}. |
| auxiliary variable (Yn) | The random additional waiting time beyond the lock time, modeled as exponential with rate lambda. |
| strong law of large numbers | A theorem stating that the sample average of independent, identically distributed random variables converges to their expected value almost surely as the sample size grows. |
| telescoping sum | A sum where interior terms cancel, leaving only the first and last terms; here the sum of Xn equals Tn because T0 = 0. |
| sensitivity analysis | The study of how the output of a model (e.g., estimated lambda) changes with respect to changes in its input parameters (e.g., locking time a). |
| derivative | A measure of how a function changes as its input changes; here d(lambda)/da = lambda * a. |
| Riemann sum | A method for approximating an integral by summing the areas of rectangles; used to motivate the transition from discrete sums to integrals. |
| measure theory | A branch of mathematics that generalizes integration and probability; the video mentions it as a deeper foundation for continuous probability. |
| Poisson process | A stochastic process where events occur continuously and independently at a constant average rate; the inter-event times are exponential. |
## Footnotes and deeper context

1. **Exponential distribution uniqueness.** The lack of memory property is unique to the exponential distribution among continuous distributions; for discrete distributions, the geometric distribution is the only memoryless distribution.
2. **Strong law of large numbers condition.** The strong law of large numbers requires that the random variables are independent and identically distributed with finite mean; the exponential waiting times satisfy this condition in the model.
3. **Locking time and Poisson process.** The counter with a lock time effectively creates a 'dead time' effect. In practice, such dead-time corrections are well-studied in nuclear physics, and the formula lambda approximately n/(Tn - n*a) is a standard first-order correction.
4. **Sensitivity interpretation.** The sensitivity d(lambda)/da = lambda * a equals the expected number of decays during a lock period only when the lock time is small relative to the mean waiting time; the derivation uses the implicit function theorem on the approximate relation.
5. **Continuous vs discrete probability.** The video contrasts continuous models with discrete ones (e.g., dice). For continuous random variables, probabilities of exact values are zero; only intervals have non-zero probability.
6. **Integration bounds.** The expected value integral for the exponential distribution is from 0 to infinity because waiting times are non-negative. The video's generic integration from minus infinity to infinity is adjusted by the PDF's support.
## Where to go next

- **Probability and Statistics for Engineers and Scientists by Walpole et al..** A standard textbook covering continuous probability models, exponential distribution, and law of large numbers in detail. The relevant chapters are on continuous distributions and estimation.
- **Introduction to Probability by Bertsekas and Tsitsiklis.** A widely used resource that explains the exponential distribution, memoryless property, and the strong law of large numbers with clear examples. Section 6.2 covers the exponential distribution.
- **Khan Academy: Exponential Distribution.** A free online video series that walks through the exponential distribution, its PDF, expected value, and lack of memory property with interactive exercises.
- **NIST/SEMATECH e-Handbook of Statistical Methods.** An authoritative online reference that includes sections on the exponential distribution, parameter estimation, and dead-time corrections in counting experiments. See 'Exponential Distribution' and 'Censoring and Truncation'.
---
*Printed by yt2textbook, an open tool from Zorost AI Lab. Screenshots are frames captured from the source video; each caption links to the exact moment it appears.*
