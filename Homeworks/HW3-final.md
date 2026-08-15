# Probability and Statistics — Computer Engineering
## Homework 3

> **Theme:** functions of random variables (transformations, and the sum / minimum / maximum of several variables) and the continuous distributions we have studied (exponential, normal), with the binomial/Poisson link at the end.
>
> A few parts ask you to **prove** a result; a few others ask you to **simulate** a result you cannot yet derive by hand. That contrast is intentional.

---

## Question 1 — The normal distribution (20 points)

The measurement error of a sensor (in millivolts) is modeled as

$$E \sim N\big(\mu = 0,\ \sigma^2 = 4\big).$$

The sensor reports the true voltage plus a random error $E$.

**(a)** What is the probability that a measurement error lies between $-3$ mV and $+3$ mV? (3 points)

**(b)** Find the number $e > 0$ such that $P(|E| \le e) = 0.99$. (4 points)

**(c)** A specification requires that the error not exceed $5$ mV. Under the current model, what proportion of measurements **violate** it (i.e. have $|E| > 5$ mV)? (4 points)

**(d)** To meet a stricter specification — at most $1\%$ of measurements outside $\pm 5$ mV — the manufacturer recalibrates to reduce $\sigma$. Find the **largest** standard deviation $\sigma$ that still guarantees this $1\%$ violation rate (keeping $\mu = 0$). (5 points)

**(e)** In one or two sentences, explain intuitively why reducing $\sigma$ lowers the violation rate. (4 points)

> **Tools.** You may use a standard-normal table by hand, or Python:
> ```python
> from scipy.stats import norm
> ```
> with `norm.cdf` (probability from a value) and `norm.ppf` (value from a probability). See [this explanation](https://stackoverflow.com/questions/809362/how-to-calculate-cumulative-normal-distribution).

---

## Question 2 — The exponential distribution: data plans and pricing (25 points)

Two internet providers, $A$ and $B$, bill customers monthly. A customer downloads $X$ gigabytes per month, where $X$ follows an exponential distribution with a **mean of 50 GB** (rate $\lambda = 1/50$). The two providers turn usage into a monthly bill (in dollars) differently:

- Provider $A$: $\quad R_A = 25 + 0.5\,X \qquad$ (a \$25 base fee plus \$0.50 per GB)
- Provider $B$: $\quad R_B = 20 + 5\sqrt{X} \qquad$ (a \$20 base fee, with a usage charge that grows more slowly)

**(a)** For each of $R_A$ and $R_B$: determine its support (range of possible values), and find its PDF and CDF. (10 points)

**(b)** Compute the expected value and variance of $R_A$ and of $R_B$. (You may leave $E[\sqrt{X}]$ in integral form or evaluate it.) (5 points)

**(c)** Compute $P(R_A > 50)$ and explain in words what this probability means. (3 points)

**(d)** Simulate $100{,}000$ customers for each provider. For each: plot a histogram of the simulated bills, report the simulated mean, variance, and standard deviation, and overlay the theoretical PDF from part (a). Do the simulations match the theory? (5 points)

**(e)** You should find that the two providers collect a **similar average bill** per customer, so comparing them on revenue alone is not very informative — the real difference is in *risk*. Which pricing model would a company with **lower risk tolerance** prefer, i.e. which one produces **less variable** revenue? Justify your answer using the variances you computed in part (b). (2 points)

> **Reminder.**
> - $R_A = aX + b$ is a **linear** transformation.
> - $R_B = a\sqrt{X} + b$ is a **nonlinear** transformation, so finding its PDF requires the change-of-variables method:
> $$f_R(r) = f_X\big(g^{-1}(r)\big)\,\left|\frac{d}{dr}\,g^{-1}(r)\right|.$$

---

## Question 3 — Summing random variables: a provider's total income (15 points)

Provider $A$ from the previous question has **100 independent customers**. To keep things simple, suppose the provider earns \$1 per gigabyte, so customer $i$ contributes an amount $X_i$ (their monthly usage in GB), and the company's **total monthly income** is

$$Y = X_1 + X_2 + \cdots + X_{100}.$$

Before doing the parts, read the following — it explains which questions about a sum are easy and which are hard.

### Means and variances are easy — and do not depend on the distributions involved

For *any* random variables $X_1, \dots, X_n$, the expected value of their sum is always the sum of their expected values:

$$E[X_1 + \cdots + X_n] = E[X_1] + \cdots + E[X_n].$$

This is **linearity of expectation**. It needs no assumptions at all — the variables need not be independent and may follow any distributions. If, in addition, the variables are **independent**, then the variances also add:

$$\mathrm{Var}[X_1 + \cdots + X_n] = \mathrm{Var}[X_1] + \cdots + \mathrm{Var}[X_n].$$

(Variances add only under independence, because expanding the variance of a sum produces cross terms — the covariances — which are zero exactly when the variables are independent.)

### The full distribution is the hard part

Knowing the mean and variance of a sum tells us nothing about its **shape**, and the shape is much harder to pin down. In particular, the sum need not stay in the same distribution *family* as its parts:

- The sum of independent **exponential** variables is **not** exponential (it is an *Erlang / Gamma* distribution, which we will not study in this course).
- The sum of independent **normal** variables, on the other hand, **is** again normal.

You will now verify all of this — the easy part by hand, the hard part by simulation.

### Part A — Exponential usage

Assume each $X_i \sim \text{Exp}(\text{mean } 50)$, independently.

**(a)** Using the two facts above, show that $E[Y] = 100\,E[X]$ and $\mathrm{Var}(Y) = 100\,\mathrm{Var}(X)$, and give their numerical values. (5 points)

**(b)** Simulate the total income $Y$ many times (each realization is the sum of 100 independent exponential draws). Plot a histogram of $Y$ and confirm that, although its mean and variance are as in part (a), its **shape is no longer exponential**. Describe how the shape differs. (5 points)

### Part B — Normal usage

Now suppose instead that each $X_i \sim N(\mu = 50,\ \sigma = 5)$, independently.

**(c)** State $E[Y]$ and $\mathrm{Var}(Y)$ (the same rules apply). Then simulate $Y$, plot its histogram, and overlay the density of $N\big(100\cdot 50,\ 100\cdot 5^2\big)$ to confirm that the total income is **still normal**. (5 points)

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

## Question 5 — Combining random variables: minimum and maximum (15 points)

Recall the tender from Question 4. A second company $B$ also submits a bid, independently of $A$, and the **lower** price wins the project:

$$X_A \sim \text{Exp}(\text{mean } 12), \qquad X_B \sim \text{Exp}(\text{mean } 13), \qquad T = \min(X_A,\ X_B).$$

In Question 3 we saw that a *sum* of random variables has an easy mean and variance but a distribution that may or may not stay in a familiar family. The same is true of the **minimum** and **maximum** — quantities that arise whenever we care about the *first* or the *last* thing to happen. Sometimes the minimum has a clean, familiar distribution; sometimes it has none, and simulation is the only way forward. The two parts below show one case of each.

### Part I — When the minimum is tractable (the tender)

**(a)** Show that $T = \min(X_A, X_B)$ is again **exponentially distributed**, and find its rate and mean. Then compute $P(T < 10)$. (8 points)

> **Hint.** Work with the survival function $P(T > t) = P(X_A > t \text{ and } X_B > t)$ and use independence.

### Part II — When the minimum is *not* tractable (normals)

Two independent servers process a request; their times (in ms) are $X_1 \sim N(100, 15^2)$ and $X_2 \sim N(120, 20^2)$, and you receive the response from whichever finishes first, so you wait $M = \min(X_1, X_2)$.

**(b)** Unlike the exponential case, $M$ has **no simple analytical distribution**, and even its expected value $E[M]$ has no elementary closed form. Simulate $100{,}000$ values of $M$, plot a histogram, and report the sample mean as your estimate of $E[M]$. Is $E[M]$ smaller than $\min(100, 120) = 100$? Briefly explain why this must be so. (7 points)

> **Connecting the dots.** For exponentials the minimum stays in the same family (you proved it in (a)), so everything is available in closed form. For normals neither the distribution nor even the mean of the minimum is analytically simple — simulation is our only practical tool. This is the norm, not the exception: most combinations of random variables must be studied empirically.

---

## Question 6 — Binomial and Poisson (15 points)

You publish an app on the Play Store. Each week it is shown to about $1000$ users, and on average $5$ install it. Assume install decisions are independent.

**(a)** Over the coming month (take $1$ month $= 4$ weeks, i.e. $4000$ views), compute the probability of **more than $25$** new installs. (7 points)

**(b)** Using Python, compute and plot the probability mass function of the number of monthly installs **twice** — once with the binomial distribution and once with the Poisson distribution — on the same axes. Show the two are nearly identical, and explain in one sentence why the Poisson approximation is accurate here. (8 points)

> **Tools.**
> ```python
> from scipy.stats import binom, poisson
> ```
> Useful functions: `binom.pmf`, `binom.cdf`, `poisson.pmf`, `poisson.cdf`. For the Poisson model use rate $\lambda = np$.
