# Probability and Statistics — Computer Engineering
## Homework 3

> **Theme:** functions of random variables (transformations, and the minimum/maximum of several variables) and the continuous distributions we have studied (uniform, exponential, normal), with the binomial/Poisson link at the end.
>
> Several parts ask you to **prove** a result (mean, variance, the memoryless property) — you now have all the tools for these. A few other parts ask you to **simulate** a result you cannot yet derive by hand; that contrast is intentional.

---

## Question 1 — Uniform distribution: the bus-stop problem (15 points)

You arrive at a bus stop at a **random time, uniformly distributed between 8:00 and 8:30 AM**. Buses arrive every 15 minutes — at **8:00, 8:15, and 8:30**. Let $T$ be your arrival time measured in minutes after 8:00, so $T \sim \text{Uniform}[0, 30]$, and let $W$ be the time you must wait until the next bus.

**(a)** What is the probability that you wait **less than 5 minutes**? (8 points)

**(b)** Write $W$ as a function of $T$, then compute the expected waiting time $E[W]$ **by integrating over the density of $T$** (show the integral, don't just quote a symmetry argument). (7 points)

> **Recall.** For $T \sim \text{Uniform}[a,b]$ the density is $f_T(t) = \dfrac{1}{b-a}$ for $t \in [a,b]$ and $0$ otherwise, and $E[g(T)] = \displaystyle\int_a^b g(t)\, f_T(t)\, dt$.

---

## Question 2 — Transformation of a random variable (10 points)

Let $X \sim \text{Uniform}\left[-\pi/2,\ +\pi/2\right]$ and define

$$Y = \sin(X).$$

**(a)** Determine the support (range of possible values) of $Y$. (3 points)

**(b)** Find the probability density function $f_Y(y)$, and state on which interval it is valid. (7 points)

> **Hint.** On $\left[-\pi/2,\ +\pi/2\right]$ the function $\sin$ is strictly increasing, hence invertible. Use the change-of-variables formula
> $$f_Y(y) = f_X\big(g^{-1}(y)\big)\,\left|\frac{d}{dy}\,g^{-1}(y)\right|.$$

---

## Question 3 — The normal distribution (20 points)

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

## Question 4 — The exponential distribution: data plans (25 points)

Two internet providers, $A$ and $B$, bill customers monthly. A customer downloads $X$ gigabytes per month, where $X$ follows an exponential distribution with a **mean of 5 GB** (rate $\lambda = 1/5$).

### Part I — Understanding $X$

**(a) (Prove the mean.)** Starting from the exponential density $f_X(x) = \lambda e^{-\lambda x}$ for $x \ge 0$, show by evaluating the integral that $E[X] = 1/\lambda$. State the value of $\mathrm{Var}(X)$. (4 points)

**(b) (Memoryless property.)** Prove **in general** that for the exponential distribution
$$P(X > s + t \mid X > s) = P(X > t) \quad \text{for all } s, t \ge 0.$$
Then compute $P(X > 10 \mid X > 5)$ and compare it with $P(X > 5)$. What does this say about a customer who has "already downloaded a lot"? (4 points)

### Part II — Pricing models

The two providers convert usage into a monthly bill (in dollars) differently:

- Provider $A$: $\quad R_A = 50 + 20X \qquad$ (a \$50 base fee plus \$20 per GB)
- Provider $B$: $\quad R_B = 40 + 30\sqrt{X} \qquad$ (a \$40 base fee, with a usage charge that grows more slowly)

**(c)** Find the PDF and CDF of $R_A$ and of $R_B$. (7 points)

**(d)** Compute the expected value and variance of $R_A$ and of $R_B$. (You may leave $E[\sqrt{X}]$ in integral form or evaluate it.) (4 points)

**(e)** Compute $P(R_A > 90)$ and explain in words what this probability means. (2 points)

**(f)** Simulate $100{,}000$ customers for each provider. For each: plot a histogram of the simulated bills, report the simulated mean, variance, and standard deviation, and overlay the theoretical PDF from part (c). Then state which provider has the **higher average bill** and which has **more variable** bills — and note which transformation (the linear one or the $\sqrt{\cdot}$ one) dampens variability. (4 points)

> **Reminder.**
> - $R_A = aX + b$ is a **linear** transformation.
> - $R_B = a\sqrt{X} + b$ is a **nonlinear** transformation, so its PDF requires the change-of-variables method (as in Question 2).

---

## Question 5 — Combining random variables: minimum and maximum (15 points)

When we build a new random variable out of several others, three things can be asked about it: its **mean**, its **variance**, and its full **distribution**. It is worth being clear about which of these is easy and which is hard.

> **Reminder — means and variances are easy.** For *any* random variables (whatever their distributions),
> $$E[X_1 + \cdots + X_n] = E[X_1] + \cdots + E[X_n]$$
> by **linearity of expectation** (no independence needed — it follows from $\int\!\!\int (x+y)\,f = \int x f + \int y f$). And *if they are independent*,
> $$\mathrm{Var}[X_1 + \cdots + X_n] = \mathrm{Var}[X_1] + \cdots + \mathrm{Var}[X_n],$$
> because the cross terms are covariances, which vanish under independence. This is exactly how the packet-drop count $X = Y_1 + \cdots + Y_n$ (a sum of Bernoullis) gets $E[X] = np$ and $\mathrm{Var}(X) = np(1-p)$.
>
> **The full distribution is the hard part.** The distribution of a combination is not always derivable in closed form, and the *family* is not always preserved:
> - Sum of $n$ Bernoulli$(p)$ $\to$ **Binomial**$(n,p)$ — the family *changes* (a binomial is not a Bernoulli).
> - Sum of independent **normals** $\to$ again **normal** — family preserved.
> - Sum of independent **exponentials** $\to$ a distribution called the **Erlang (Gamma)** distribution, which we will *not* cover in this course.
> - In general, no simple closed form need exist at all.

The same contrast appears for the **minimum** or **maximum** of random variables — quantities that show up whenever we care about "the first to happen" or "the last to happen." Sometimes the minimum has a clean distribution; sometimes it does not.

### Part I — When the minimum is tractable (the tender)

An oil company awards a drilling project through a **tender**: two firms $A$ and $B$ each announce a price, and the lower price wins. The prices are independent, with

$$X_A \sim \text{Exp}(\text{mean } 12), \qquad X_B \sim \text{Exp}(\text{mean } 13),$$

and the price paid is $T = \min(X_A,\ X_B)$.

**(a) (Prove it.)** Show that $T$ is again **exponentially distributed**, and find its rate and mean. Then compute $P(T < 10)$. (8 points)

> **Hint.** Work with the survival function $P(T > t) = P(X_A > t \text{ and } X_B > t)$ and use independence.

### Part II — When the minimum is *not* tractable (normals)

Two independent servers process a request; their times (in ms) are $X_1 \sim N(100, 15^2)$ and $X_2 \sim N(120, 20^2)$, and you get the response from whichever finishes first, so you wait $M = \min(X_1, X_2)$.

**(b)** Unlike the exponential case, $M$ has **no simple analytical distribution** — and even its expected value $E[M]$ has no elementary closed form. Simulate $100{,}000$ values of $M$, plot a histogram, and report the sample mean as your estimate of $E[M]$. Is $E[M]$ smaller than $\min(100, 120) = 100$? Briefly explain why this must be so. (7 points)

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
