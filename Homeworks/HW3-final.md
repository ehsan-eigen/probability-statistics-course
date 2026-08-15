# Probability and Statistics — Computer Engineering
## Homework 3

> **Theme:** functions of random variables (transformations, and the minimum/maximum of several variables) and the continuous distributions we have studied (uniform, exponential, normal), with the binomial/Poisson link at the end.
>
> A few parts ask you to **prove** a result; a few others ask you to **simulate** a result you cannot yet derive by hand. That contrast is intentional.

---

## Question 1 — Uniform distribution: the bus-stop problem (15 points)

You arrive at a bus stop at a **random time, uniformly distributed between 8:00 and 8:30 AM**. Buses arrive every 15 minutes — at **8:00, 8:15, and 8:30**. Let $T$ be your arrival time measured in minutes after 8:00, so $T \sim \text{Uniform}[0, 30]$, and let $W$ be the time you must wait until the next bus.

**(a)** What is the probability that you wait **less than 5 minutes**? (8 points)

**(b)** Compute the expected waiting time $E[W]$. (7 points)

---

## Question 2 — The normal distribution (20 points)

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

## Question 3 — The exponential distribution: data plans and pricing (25 points)

Two internet providers, $A$ and $B$, bill customers monthly. A customer downloads $X$ gigabytes per month, where $X$ follows an exponential distribution with a **mean of 50 GB** (rate $\lambda = 1/50$). The two providers turn usage into a monthly bill (in dollars) differently:

- Provider $A$: $\quad R_A = 25 + 0.5\,X \qquad$ (a \$25 base fee plus \$0.50 per GB)
- Provider $B$: $\quad R_B = 20 + 5\sqrt{X} \qquad$ (a \$20 base fee, with a usage charge that grows more slowly)

**(a)** For each of $R_A$ and $R_B$: determine its support (range of possible values), and find its PDF and CDF. (10 points)

**(b)** Compute the expected value and variance of $R_A$ and of $R_B$. (You may leave $E[\sqrt{X}]$ in integral form or evaluate it.) (5 points)

**(c)** Compute $P(R_A > 50)$ and explain in words what this probability means. (3 points)

**(d)** Simulate $100{,}000$ customers for each provider. For each: plot a histogram of the simulated bills, report the simulated mean, variance, and standard deviation, and overlay the theoretical PDF from part (a). Do the simulations match the theory? (5 points)

**(e)** Which provider has the **higher average bill**, and which has **more variable** bills? Note which transformation — the linear one or the $\sqrt{\cdot}$ one — dampens variability, and briefly explain why. (2 points)

> **Reminder.**
> - $R_A = aX + b$ is a **linear** transformation.
> - $R_B = a\sqrt{X} + b$ is a **nonlinear** transformation, so finding its PDF requires the change-of-variables method:
> $$f_R(r) = f_X\big(g^{-1}(r)\big)\,\left|\frac{d}{dr}\,g^{-1}(r)\right|.$$

---

## Question 4 — The memoryless property (10 points)

Recall the tender in which company $A$ announces a price for a drilling project, where that price is exponentially distributed with a mean of \$12 million:

$$X_A \sim \text{Exp}(\text{mean } 12).$$

Suppose an insider **leaks** that company $A$'s announced price will be **greater than \$10 million**.

**(a)** Given this information, what is the probability that $A$'s price will exceed \$15 million? (4 points)

**(b)** Compare your answer with the *unconditional* probability $P(X_A > 5)$. What property of the exponential distribution does this illustrate — and in plain words, what does it mean here (does the leak of "already above \$10 million" change how much *more* we should expect)? (3 points)

**(c)** Prove this property in general: show that for an exponential random variable,
$$P(X > s + t \mid X > s) = P(X > t) \qquad \text{for all } s, t \ge 0.$$
(3 points)

---

## Question 5 — Combining random variables: minimum and maximum (15 points)

When we build a new random variable out of several others, we can ask three separate questions about it: what is its **mean**, what is its **variance**, and what is its full **distribution**? These three questions differ enormously in difficulty.

### Means and variances are easy — and do not depend on the distributions involved

For *any* random variables $X_1, X_2, \dots, X_n$, the expected value of their sum is always the sum of their expected values:

$$E[X_1 + X_2 + \cdots + X_n] = E[X_1] + E[X_2] + \cdots + E[X_n].$$

This is **linearity of expectation**. It needs no assumptions at all: the variables do not have to be independent, and they may follow any distributions whatsoever. It follows directly from the fact that the integral of a sum is the sum of the integrals.

For the **variance**, one extra condition is needed. If the variables are **independent**, then

$$\mathrm{Var}[X_1 + X_2 + \cdots + X_n] = \mathrm{Var}[X_1] + \mathrm{Var}[X_2] + \cdots + \mathrm{Var}[X_n].$$

Variances add only under independence because expanding the variance of a sum produces cross terms (the covariances between the variables), and those covariances are exactly zero when the variables are independent.

You have already used both of these facts: the number of dropped packets in a session, $X = Y_1 + \cdots + Y_n$, is a sum of independent Bernoulli trials, and that is precisely why $E[X] = np$ and $\mathrm{Var}(X) = np(1-p)$.

### The full distribution is the hard part

Knowing the mean and variance of a combination tells us **nothing** about its shape. Finding the actual distribution is far harder, and two different things can go wrong:

- **The family can change.** The sum of independent Bernoulli variables is a **Binomial** — *not* another Bernoulli. So a combination does not, in general, look like the pieces it is built from.
- **The result may be a distribution we have not studied, or none at all.** The sum of independent **normal** variables happens to be normal again (the family is preserved). But the sum of independent **exponential** variables is an *Erlang (Gamma)* distribution, which we will **not** cover in this course — and for many combinations no simple closed form exists at all.

The same story holds for the **minimum** and **maximum** of several random variables — quantities that arise whenever we care about the *first* thing to happen or the *last* thing to happen. Sometimes the minimum has a clean, familiar distribution; sometimes it has none, and simulation is the only way forward. The two parts below show one case of each.

### Part I — When the minimum is tractable (the tender)

In the tender, two firms $A$ and $B$ independently announce prices, and the lower price wins:

$$X_A \sim \text{Exp}(\text{mean } 12), \qquad X_B \sim \text{Exp}(\text{mean } 13), \qquad T = \min(X_A,\ X_B).$$

**(a)** Show that $T$ is again **exponentially distributed**, and find its rate and mean. Then compute $P(T < 10)$. (8 points)

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

---

### Optional

## Question 7 — Reading and comparing CDFs (10 bonus points)

The diagram shows the cumulative distribution function (CDF) of the monthly income of the citizens of four different countries. Using only these curves, compare the four countries — for example, which has the most people in poverty, which is the most equal, and which has the highest incomes.

![Cumulative income distributions for four countries](HW3-v2-q7-chart.png)

*Chart description: four CDF curves. The horizontal axis is monthly income in dollars (marked at \$5000, \$10000, \$15000, \$20000); the vertical axis is cumulative probability from $0$ to $1$. The **orange** curve rises fastest and saturates near $1$ earliest (income concentrated at low values). The **blue/purple** curve rises somewhat more slowly. The **red** curve stays low at first, then rises to reach $1$ near the high-income end. The **green** curve is a straight diagonal from the origin to the top-right (a uniform-like spread of income).*
