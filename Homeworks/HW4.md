# Probability and Statistics — Computer Engineering

### Homework 4 — Continuous Random Variables and Simulation

**Total: 100 points + 25 optional bonus points**

This homework focuses on:

- Continuous random variables, PDFs, and CDFs
- Uniform and Normal distributions
- Expectation and variance for continuous random variables
- The Central Limit Theorem and Law of Large Numbers
- Simulation and Monte Carlo estimation
- Joint continuous distributions
- Marginal distributions, independence, and conditional probability

> The Exponential distribution and transformations of continuous random variables were covered in Homework 3.

---

## Question 1 — A/B Testing, the Central Limit Theorem, and Monte Carlo Simulation (25 Points)

An online retailer tests two versions of a product page, **A** and **B**.

The true conversion rates are:

$$
p_A = 0.04,
\qquad
p_B = 0.045.
$$

Let

$$
\hat{p}_A = \text{sample conversion rate for version A},
$$

$$
\hat{p}_B = \text{sample conversion rate for version B},
$$

and define

$$
D = \hat{p}_B - \hat{p}_A.
$$

For each experiment, suppose that:

- 1000 users are independently shown version A,
- another 1000 users are independently shown version B.

### (a) Simulation — 4 points

Simulate **10,000 independent A/B experiments**.

For each experiment:

1. Generate the number of purchases for A and B.
2. Calculate $\hat{p}_A$ and $\hat{p}_B$.
3. Calculate

$$
D = \hat{p}_B - \hat{p}_A.
$$

### (b) Simulated distribution — 4 points

Plot a histogram of the 10,000 simulated values of $D$.

Describe its:

- shape,
- center,
- spread.

Does the distribution appear approximately Normal?

### (c) CLT approximation — 5 points

Using the Central Limit Theorem, derive an approximate distribution for $D$.

In particular, find

$$
E[D]
$$

and

$$
\operatorname{Var}(D).
$$

Then write your approximation in the form

$$
D \approx N(\mu_D,\sigma_D^2).
$$

### (d) Probability that B performs better — 4 points

Using your Normal approximation, calculate

$$
P(D > 0).
$$

Interpret this probability in the context of the A/B test.

### (e) Theory versus simulation — 3 points

From your 10,000 simulations, calculate the proportion for which

$$
D > 0.
$$

Compare this empirical result with the theoretical result from part (d).

### (f) Monte Carlo stability — 5 points

The number of simulated experiments affects the accuracy and stability of a simulation-based estimate.

Estimate $P(D>0)$ repeatedly using:

$$
100,\qquad 1000,\qquad 10000
$$

simulated experiments.

For each simulation size, repeat the whole estimation several times.

Compare how much the estimated value of $P(D>0)$ changes from run to run.

Briefly explain:

- which simulation size produces the most stable estimate,
- why increasing the **number of simulated experiments** makes the Monte Carlo estimate more stable.

> **Important:** Do not confuse the number of users in each A/B experiment with the number of times the experiment is simulated. These are two different quantities.

---

## Question 2 — Law of Large Numbers and Sampling Bias (20 Points)

A ministry of health wants to estimate vaccination coverage across rural villages.

Assume the true population vaccination rate is

$$
p = 0.75.
$$

### (a) Law of Large Numbers — 6 points

In your own words, explain what the **Law of Large Numbers (LLN)** predicts should happen to the sample vaccination rate as the sample size increases.

For each of the following sample sizes,

$$
n = 10,\ 50,\ 100,\ 1000,
$$

simulate **1000 independent samples**.

For every sample, calculate the estimated vaccination rate.

Plot or summarize the distributions of the estimates for the four sample sizes.

Explain how your simulation illustrates the Law of Large Numbers.

### (b) Sampling error — 4 points

Now use

$$
n = 100.
$$

Simulate 1000 samples.

Count how many estimated vaccination rates are more than **5 percentage points** away from the true population value of $0.75$.

That is, count how many estimates fall outside

$$
[0.70,0.80].
$$

Report:

- the number of such samples,
- the proportion of such samples.

### (c) What if the sampling method is biased? — 7 points

Now suppose the population contains two groups:

- Group A makes up 60% of the population and has vaccination probability $0.85$.
- Group B makes up 40% of the population and has vaccination probability $0.60$.

First verify that the overall population vaccination rate is

$$
0.60(0.85)+0.40(0.60)=0.75.
$$

Now suppose the sampling procedure is biased:

- 80% of sampled individuals come from Group A,
- 20% come from Group B.

Simulate the estimated vaccination rate for increasingly large sample sizes.

For example, consider

$$
n = 10,\ 50,\ 100,\ 1000,\ 10000.
$$

What value does the estimate appear to approach?

Explain why increasing the sample size does **not** eliminate this error.

### (d) Interpretation — 3 points

Briefly discuss:

> Why does a very large sample size not necessarily guarantee an accurate estimate of the population?

Distinguish between:

- random sampling error,
- systematic sampling bias.

---

## Question 3 — PDFs, CDFs, Uniform Distribution, Expectation, and Variance (25 Points)

### Part A — Where Are the Raisins?

A cereal box is 30 cm tall.

Because the cereal settles during transportation, raisins are more concentrated near the bottom of the box.

Suppose the physical density of raisins at height $h$, measured in raisins per centimeter, is

$$
r(h)=40-h,
\qquad
0 \leq h \leq 30.
$$

Let $H$ denote the height of a randomly selected raisin.

### (a) From physical density to probability density — 4 points

First calculate the total number of raisins predicted by this model:

$$
\int_0^{30}(40-h)\,dh.
$$

Then use this value to construct the probability density function

$$
f_H(h).
$$

Clearly state the support of $H$.

Verify that your PDF satisfies

$$
\int_0^{30} f_H(h)\,dh = 1.
$$

### (b) Find and graph the CDF — 5 points

Derive the CDF

$$
F_H(h)=P(H\leq h).
$$

Write the complete piecewise CDF for

$$
h<0,
\qquad
0\leq h\leq30,
\qquad
h>30.
$$

Plot both:

- $f_H(h)$,
- $F_H(h)$.

Briefly explain why the PDF decreases with height while the CDF must always increase.

### (c) Probability — 3 points

Find the probability that a randomly selected raisin is located in the **bottom third** of the box:

$$
P(H\leq10).
$$

Interpret your answer in words.

### (d) Expected height and variance — 6 points

Compute

$$
E[H]
=
\int_0^{30} h f_H(h)\,dh
$$

and

$$
E[H^2]
=
\int_0^{30} h^2 f_H(h)\,dh.
$$

Then use

$$
\operatorname{Var}(H)
=
E[H^2]-E[H]^2
$$

to calculate the variance.

Interpret $E[H]$ in the context of the cereal box.

---

### Part B — What if the Raisins Were Uniformly Distributed?

Now suppose instead that raisins were distributed uniformly throughout the height of the box, so that every interval of equal length contains the same expected proportion of raisins.

Let

$$
U\sim\operatorname{Uniform}(0,30).
$$

### (e) Uniform PDF, CDF, mean, and variance — 4 points

Write the PDF and CDF of $U$, including their complete piecewise definitions.

Then compute

$$
E[U]
$$

and

$$
\operatorname{Var}(U).
$$

You may derive these quantities directly using integrals or use the standard formulas after explaining where they come from.

### (f) Compare the two models — 3 points

For the Uniform model, compute

$$
P(U\leq10).
$$

Compare this with your result for

$$
P(H\leq10).
$$

Also compare

$$
E[U]
$$

with

$$
E[H].
$$

Explain intuitively why the two models give different answers.

---

## Question 4 — Joint Continuous Random Variables (30 Points)

Imagine two continuous random variables:

- $X$ = hours of study per week, where $0 \leq X \leq 10$,
- $Y$ = GPA score, where $0 \leq Y \leq 4$.

Consider the joint probability density

$$
f_{X,Y}(x,y)=cxy
$$

over the triangular region

$$
0 \leq x \leq 10,
\qquad
0 \leq y \leq \frac{2}{5}x.
$$

Outside this region,

$$
f_{X,Y}(x,y)=0.
$$

### (a) Understand the support — 5 points

Sketch the valid region of $(X,Y)$ in the $xy$-plane.

Explain why the support is triangular.

### (b) Find the normalization constant — 7 points

Find the value of $c$ such that the total probability over the valid region is 1:

$$
\int_0^{10}
\int_0^{\frac{2}{5}x}
cxy\,dy\,dx
=
1.
$$

Show your integration.

### (c) Conditional probability from a slice — 8 points

We want to calculate

$$
P(Y>2\mid X=6).
$$

Before doing the calculation, open the following 3D Desmos visualization:

https://www.desmos.com/3d/4a4xplyayl

Rotate the graph and make sure you understand what the surface and the highlighted valid region represent.

In this visualization, the function has **not** been set to zero outside the valid region. Instead, the valid region is shown using a different color.

Also note that the vertical scale has intentionally been modified to make the graph easier to see, so you should focus on the shape rather than the exact height.

Now focus on the slice where

$$
X=6.
$$

For $X=6$, the possible values of $Y$ are

$$
0\leq Y\leq\frac{12}{5}.
$$

Add the following equation to Desmos:

$$
y\geq2.
$$

Use the graph to understand which part of the $X=6$ slice corresponds to:

- the **denominator**: all possible values of $Y$ when $X=6$,
- the **numerator**: the part where $Y>2$ when $X=6$.

Then compute

$$
P(Y>2\mid X=6)
=
\frac{
\displaystyle\int_2^{12/5} f_{X,Y}(6,y)\,dy
}{
\displaystyle\int_0^{12/5} f_{X,Y}(6,y)\,dy
}.
$$

For a continuous random variable,

$$
P(X=6)=0,
$$

so we do not calculate this using ordinary point probabilities.

You can think of the expression above as

$$
\frac{\text{density in the part where }Y>2}
{\text{total density along the slice }X=6}.
$$

### (d) Marginal distributions and independence — 10 points

Derive both marginal densities:

$$
f_X(x)
$$

and

$$
f_Y(y).
$$

Clearly state their supports.

Then determine whether $X$ and $Y$ are independent.

Support your answer mathematically by checking whether

$$
f_{X,Y}(x,y)
=
f_X(x)f_Y(y).
$$

Also briefly explain what the triangular shape of the valid region suggests about whether $X$ and $Y$ can be independent.

> You may use Wolfram Alpha or another symbolic mathematics tool to **check** your integrations after deriving the marginal densities yourself.

---

# Optional Bonus Question — Conditional Density and Conditional Expectation (25 Bonus Points)

A marketing analyst wants to understand customer behavior using the following continuous random variables:

- $X$: time spent on the website, in minutes, where $0\leq X\leq20$,
- $Y$: money spent, in dollars, where $0\leq Y\leq2X$.

They model the joint distribution using

$$
f_{X,Y}(x,y)
=
\begin{cases}
\displaystyle\frac{3}{16000}y,
& 0\leq x\leq20,\quad 0\leq y\leq2x,\\
0,
& \text{otherwise}.
\end{cases}
$$

### (a) Verify the joint PDF — 4 points

Verify that $f_{X,Y}(x,y)$ is a valid probability density function.

In particular, show that

$$
\int_0^{20}
\int_0^{2x}
f_{X,Y}(x,y)\,dy\,dx
=
1.
$$

### (b) Marginal density — 4 points

Compute the marginal density

$$
f_X(x).
$$

Clearly state its support.

### (c) Conditional density and conditional expectation — 7 points

Compute the conditional density

$$
f_{Y\mid X}(y\mid x).
$$

Clearly state the possible values of $y$ for a given value of $x$.

Then use the conditional density to calculate

$$
E[Y\mid X=x].
$$

Interpret $E[Y\mid X=x]$ in the context of customer behavior.

### (d) Simulation — 6 points

Simulate **10,000 customers** from the joint distribution.

Because $X$ is continuous, observations will generally not have exactly the same value of $X$.

Therefore, divide the observed values of $X$ into small intervals, or **bins**.

For each bin:

- calculate the average observed value of $X$,
- calculate the average observed value of $Y$.

Plot these empirical conditional averages and compare them with the theoretical relationship

$$
E[Y\mid X=x].
$$

Discuss whether the simulation agrees with the theoretical result.

### (e) Interpretation — 4 points

Based on the conditional expectation, briefly discuss what the model suggests about the relationship between time spent on the website and expected spending.

How could such information potentially be useful when designing advertising or upselling strategies?

Also mention at least one reason why this mathematical relationship alone should **not** automatically be interpreted as a causal relationship.