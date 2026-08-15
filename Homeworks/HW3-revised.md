# Probability and Statistics — Computer Engineering
## Homework 3

> **Theme:** functions of random variables (transformations, and the sum / minimum / maximum of several variables) and the continuous distributions we have studied (exponential, normal), with the binomial/Poisson link at the end.
>
> A few parts ask you to **prove** a result; a few others ask you to **simulate** a result you cannot yet derive by hand. That contrast is intentional. (When we say a result is found *empirically*, we mean exactly this — estimating it by simulation.)

---

## Question 1 — The normal distribution (25 points)

The measurement error of a sensor (in millivolts) is modeled as

$$E \sim N\big(\mu = 0,\ \sigma^2 = 4\big).$$

The sensor reports the true voltage plus a random error $E$.

**(a)** What is the probability that a measurement error lies between $-3$ mV and $+3$ mV? (4 points)

**(b)** Find the number $e > 0$ such that $P(|E| \le e) = 0.99$. (5 points)

**(c)** A specification requires that the error not exceed $5$ mV. Under the current model, what proportion of measurements **violate** it (i.e. have $|E| > 5$ mV)? (5 points)

**(d)** To meet a stricter specification — at most $1\%$ of measurements outside $\pm 5$ mV — the manufacturer recalibrates to reduce $\sigma$. Find the **largest** standard deviation $\sigma$ that still guarantees this $1\%$ violation rate (keeping $\mu = 0$). (7 points)

**(e)** In one or two sentences, explain intuitively why reducing $\sigma$ lowers the violation rate. (4 points)

> **Tools.** You may use a standard-normal table by hand, or Python:
> ```python
> from scipy.stats import norm
> ```
> with `norm.cdf` (probability from a value) and `norm.ppf` (value from a probability). See [this explanation](https://stackoverflow.com/questions/809362/how-to-calculate-cumulative-normal-distribution).

---

## Question 2 — Transformation of a random variable (25 points)

Two internet providers, $A$ and $B$, bill customers monthly. A customer downloads $X$ gigabytes per month, where $X$ follows an exponential distribution with a **mean of 50 GB** (rate $\lambda = 1/50$). The two providers turn usage into a monthly bill (in dollars) differently:

- Provider $A$: $\quad R_A = 25 + 0.5\,X \qquad$ (a \$25 base fee plus \$0.50 per GB)
- Provider $B$: $\quad R_B = 18 + 5\sqrt{X} \qquad$ (an \$18 base fee, with a usage charge that grows more slowly)

**(a)** For each of $R_A$ and $R_B$: determine its support (range of possible values), and find its PDF and CDF. (12 points)

**(b)** Compute $P(R_A > 50)$ and explain in words what this probability means. (4 points)

**(c)** Compute the expected value and variance of $R_A$ and of $R_B$. (You may leave $E[\sqrt{X}]$ in integral form or evaluate it.) (7 points)

**(d)** You should find that the two providers collect a **similar average bill** per customer, so comparing them on revenue alone is not very informative — the real difference is in *risk*. Which pricing model would a company with **lower risk tolerance** prefer, i.e. which one produces **less variable** revenue? Justify your answer using the variances you computed in part (c). (2 points)

> **Reminder.**
> - $R_A = aX + b$ is a **linear** transformation.
> - $R_B = a\sqrt{X} + b$ is a **nonlinear** transformation. There are two ways to find its PDF:
>   1. **CDF-first (recommended — usually easier):** find the CDF by writing $F_R(r) = P(R \le r) = P\big(a\sqrt{X} + b \le r\big)$, solve the inequality for $X$ to rewrite this in terms of $F_X$, then **differentiate** to obtain the PDF, $f_R(r) = F_R'(r)$.
>   2. **Change-of-variables formula:** $f_R(r) = f_X\big(g^{-1}(r)\big)\,\left|\frac{d}{dr}\,g^{-1}(r)\right|.$
>
>   Both give the same answer, but starting from the CDF is generally less error-prone (no Jacobian formula to memorize, and no absolute value to forget).
> - When you compute $E[\sqrt{X}]$ in part (c) you will get an integral with no elementary antiderivative. **Write the integral out explicitly**; you may then evaluate it by hand, or use a tool (Wolfram Alpha, or an AI assistant) to get its numerical value.

---

## Question 3 — Combination of random variables: Sum (20 points)

Provider $A$ from Question 2 has **100 independent customers**, each billed the amount $R_A$ defined there. The company's **total monthly income** is the sum of the individual bills:

$$Y = R_{A,1} + R_{A,2} + \cdots + R_{A,100}.$$

Before doing the parts, read the following — it explains which questions about a sum are easy and which are hard.

### Means and variances are easy — and do not depend on the distributions involved

For *any* random variables $Z_1, \dots, Z_n$, the expected value of their sum is always the sum of their expected values:

$$E[Z_1 + \cdots + Z_n] = E[Z_1] + \cdots + E[Z_n].$$

This is **linearity of expectation**. It needs no assumptions at all — the variables need not be independent and may follow any distributions. If, in addition, the variables are **independent**, then the variances also add:

$$\mathrm{Var}[Z_1 + \cdots + Z_n] = \mathrm{Var}[Z_1] + \cdots + \mathrm{Var}[Z_n].$$

### The full distribution is the hard part

The mean and variance do **not**, on their own, determine the *shape* of the distribution — many different distributions share the same mean and variance. Finding the actual distribution of a sum is much harder, and the sum need not even stay in the same distribution *family* as its parts:

- You have already seen one such case: the sum of independent **Bernoulli** variables (each $0$ or $1$) is a **Binomial** — the family changes, since a binomial is not a Bernoulli.
- The sum of independent **exponential** variables is likewise **not** exponential (it is an *Erlang / Gamma* distribution, which we will not study in this course).
- The sum of independent **normal** variables, on the other hand, **is** again normal. (We will not prove this in this course, but you will confirm it below by simulation.)

You will now explore the two continuous cases by simulation — the mean and variance you can get from the easy rules above, but the shape you must observe empirically.

### Part A — Usage $X$ is exponential (as in Question 2)

Each customer's usage is $X_i \sim \text{Exp}(\text{mean } 50)$, exactly as in Question 2, so each bill is $R_{A,i} = 25 + 0.5\,X_i$.

**(a)** Simulate the total income $Y$ many times (each realization is a sum of 100 independent bills). Report the simulated mean and variance and check they agree with $100\,E[R_A]$ and $100\,\mathrm{Var}(R_A)$ (using the values from Question 2). Then plot a histogram of $Y$ and confirm that its **shape is no longer exponential**; describe how it differs. (10 points)

### Part B — Usage $X$ is normal instead

Now suppose usage is normally distributed, $X_i \sim N(\mu = 50,\ \sigma = 5)$, so each bill is still $R_{A,i} = 25 + 0.5\,X_i$.

**(b)** State $E[Y]$ and $\mathrm{Var}(Y)$ (the same rules apply). Then simulate $Y$, plot its histogram, and overlay the corresponding normal density to confirm that the total income is **still normal**. (10 points)

---

## Question 4 — The memoryless property (10 points)

A drilling project is awarded by a **tender**: company $A$ announces a price that is exponentially distributed with a mean of \$12 million,

$$X_A \sim \text{Exp}(\text{mean } 12).$$

Suppose an insider **leaks** that company $A$'s announced price will be **greater than \$10 million**.

**(a)** Given this information, what is the probability that $A$'s price will exceed \$15 million? (4 points)

**(b)** Compare your answer with the *unconditional* probability $P(X_A > 5)$. What property of the exponential distribution does this illustrate — and in plain words, what does it mean here (does knowing the price is "already above \$10 million" change how much *more* we should expect)? (3 points)

**(c)** Prove this property in general: show that for an exponential random variable,
$$P(X > s + t \mid X > s) = P(X > t) \qquad \text{for all } s, t \ge 0.$$
(3 points)

---

## Question 5 — Binomial and Poisson (20 points)

You publish an app on the Play Store. Each week it is shown to about $1000$ users, and on average $5$ install it. Assume install decisions are independent.

**(a)** Over the coming month (take $1$ month $= 4$ weeks, i.e. $4000$ views), compute the probability of **more than $25$** new installs. (10 points)

**(b)** Using Python, compute and plot the probability mass function of the number of monthly installs **twice** — once with the binomial distribution and once with the Poisson distribution — on the same axes. Show the two are nearly identical, and explain in one sentence why the Poisson approximation is accurate here. (10 points)

> **Tools.**
> ```python
> from scipy.stats import binom, poisson
> ```
> Useful functions: `binom.pmf`, `binom.cdf`, `poisson.pmf`, `poisson.cdf`. For the Poisson model use rate $\lambda = np$.

---

### Optional

## Question 6 — Combination of random variables: Max and Min (20 bonus points)

Recall the tender from Question 4. A second firm $B$ also submits a bid, independently of $A$, and the **lower** price wins the project. Their prices are exponentially distributed, and the winning price is their minimum:

$$X_A \sim \text{Exp}(\text{mean } 12), \qquad X_B \sim \text{Exp}(\text{mean } 13), \qquad T = \min(X_A,\ X_B).$$

In Question 3 we saw that a *sum* of random variables has an easy mean and variance but a distribution that may or may not stay in a familiar family. The same is true of the **minimum** and **maximum**. Sometimes the minimum has a clean, familiar distribution; sometimes it has none, and simulation is the only way forward. The two parts below show one case of each.

### Part I — When the minimum is tractable (the tender)

**(a)** Show that $T = \min(X_A, X_B)$ is again **exponentially distributed**, and find its rate and mean. Then compute $P(T < 10)$. (10 points)

> **Hint.** Work with the survival function $P(T > t) = P(X_A > t \text{ and } X_B > t)$ and use independence.

### Part II — When the minimum is *not* tractable (normals)

Two independent servers process a request; their times (in ms) are $X_1 \sim N(100, 15^2)$ and $X_2 \sim N(120, 20^2)$, and you receive the response from whichever finishes first, so you wait $M = \min(X_1, X_2)$.

**(b)** Unlike the exponential case, $M$ has **no simple analytical distribution**, and even its expected value $E[M]$ has no elementary closed form. Simulate $100{,}000$ values of $M$, plot a histogram, and report the sample mean as your estimate of $E[M]$. Is $E[M]$ smaller than $\min(100, 120) = 100$? Briefly explain why this must be so. (10 points)

> **Connecting the dots.** For exponentials the minimum stays in the same family (you proved it in (a)), so everything is available in closed form. For normals neither the distribution nor even the mean of the minimum is analytically simple — simulation is our only practical tool. This is the norm, not the exception: most combinations of random variables must be studied empirically.
