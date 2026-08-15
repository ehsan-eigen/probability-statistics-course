# Probability and Statistics — Computer Engineering
## Homework 3

> **Theme:** functions of random variables (transformations, minima, sums) and the continuous distributions we have studied (uniform, exponential, normal), plus the binomial/Poisson link. Several parts ask you to *simulate* a result you cannot yet derive by hand — this is intentional.

---

## Question 1 — Transformation of a random variable (10 points)

Let $X$ be a random variable with a uniform distribution on the interval $\left[-\pi/2,\ +\pi/2\right]$, and define

$$Y = \sin(X).$$

**(a)** Determine the support (range of possible values) of $Y$. (3 points)

**(b)** Find the probability density function $f_Y(y)$. State clearly on which interval it is valid. (7 points)

> **Hint.** On $\left[-\pi/2,\ +\pi/2\right]$ the function $\sin$ is strictly increasing, so it is invertible there. Use the change-of-variables (transformation) formula
> $$f_Y(y) = f_X\big(g^{-1}(y)\big)\,\left|\frac{d}{dy}\,g^{-1}(y)\right|.$$

---

## Question 2 — The normal distribution (20 points)

The measurement error of a sensor (in millivolts) is modeled as

$$E \sim N\big(\mu = 0,\ \sigma^2 = 4\big).$$

That is, the sensor reports the true voltage plus a random error $E$.

**(a)** What is the probability that a measurement error lies between $-3$ mV and $+3$ mV? (3 points)

**(b)** Find the number $e > 0$ such that $P(|E| \le e) = 0.99$. (4 points)

**(c)** According to a technical specification, the sensor error must not exceed $5$ mV. Under the current model, what proportion of measurements *violate* this specification (i.e. have $|E| > 5$ mV)? (4 points)

**(d)** To meet a stricter specification — at most $1\%$ of measurements outside the $\pm 5$ mV range — the manufacturer can reduce the standard deviation through recalibration. Compute the **largest** standard deviation $\sigma$ that guarantees this $1\%$ violation rate (keeping $\mu = 0$). (5 points)

**(e)** In one or two sentences, explain intuitively why reducing $\sigma$ lowers the violation rate. (4 points)

> **Tools.** For parts (b) and (d) you may work by hand with a standard-normal table (the critical values $z_{0.995}\approx 2.576$ and $z_{0.995}$ are relevant), or use Python:
> ```python
> from scipy.stats import norm
> ```
> and the functions `norm.cdf` (probability from a value) and `norm.ppf` (value from a probability). A short explanation of `cdf` vs. `ppf` is [here](https://stackoverflow.com/questions/809362/how-to-calculate-cumulative-normal-distribution).

---

## Question 3 — Minimum of exponentials, and the memoryless property (20 points)

An oil company outsources drilling projects through a **tender**: two private companies $A$ and $B$ simultaneously announce a price on a given day, and the project is awarded to whichever announces the **lower** price.

The price company $A$ will announce is exponentially distributed with a mean of \$12 million; company $B$'s price is exponentially distributed with a mean of \$13 million. The two prices are independent. Let

$$X_A \sim \text{Exp}(\text{mean } 12), \qquad X_B \sim \text{Exp}(\text{mean } 13), \qquad T = \min(X_A,\ X_B).$$

**(a)** Find the probability density function of $T$ and its expected value $E[T]$. (8 points)

**(b)** Compute the probability that the winning (lowest) bid is below \$10 million, i.e. $P(T < 10)$. (4 points)

**(c) (Memoryless property.)** Suppose we learn that company $A$'s bid exceeds \$10 million. Compute
$$P\big(X_A > 15 \ \big|\ X_A > 10\big),$$
and compare it with the unconditional probability $P(X_A > 5)$. What property of the exponential distribution does this illustrate? (4 points)

**(d) (Why the maximum is harder.)** Now imagine the reverse situation — an **auction** in which the company that offers the **highest** price wins, so the relevant variable is $M = \max(X_A, X_B)$. Using a **Python simulation**, generate many draws of $X_A$ and $X_B$ and plot the empirical distribution of $M$. Briefly explain why obtaining the exact distribution of a *maximum* by hand is generally more work than for a *minimum*. (4 points)

---

## Question 4 — Sums of random variables: an empirical exploration (15 points)

We have studied the *minimum* and *maximum* of random variables. The **sum** is another natural combination, but deriving its distribution by hand requires tools (convolution) we have not covered yet. Here you will explore two sums purely by **simulation** and compare against a distribution we simply hand you.

**(a) Sum of two exponentials.**
Two tasks are processed back-to-back. Each task's duration (in minutes) is independent and exponentially distributed with mean $5$. Let $S = X_1 + X_2$ be the total time.

- Simulate $100{,}000$ values of $S$ and plot a histogram (normalized to a density).
- It turns out that $S$ follows a **Gamma (Erlang) distribution**. For the sum of two independent exponentials with rate $\lambda = 1/5$, its density is
$$f_S(s) = \lambda^2\, s\, e^{-\lambda s}, \qquad s > 0.$$
Overlay this theoretical curve on your histogram. Does it match?
- From the theory above, $E[S] = 2/\lambda = 10$. Check that your simulated mean is close to this. (8 points)

**(b) Sum of two normals.**
Let $X_1 \sim N(100,\ 15^2)$ and $X_2 \sim N(120,\ 20^2)$ be independent, and let $S = X_1 + X_2$.

- Simulate $100{,}000$ values of $S$ and plot a histogram.
- Compute the simulated mean and variance. Are they close to $\mu_1 + \mu_2 = 220$ and $\sigma_1^2 + \sigma_2^2 = 625$?
- Overlay the density of $N(220,\ 625)$ (standard deviation $25$) on your histogram, and comment on the shape. (7 points)

> **Note.** You are not expected to *prove* that the sum of two exponentials is Gamma, or that the sum of two independent normals is again normal — those derivations come later. The goal here is to *observe* these facts empirically.

---

## Question 5 — Binomial and Poisson (15 points)

You have published an application on the Play Store. Each week it is shown to about $1000$ users, and on average $5$ of them install it. Assume the users' install decisions are independent.

**(a)** Over the coming month (take $1$ month $= 4$ weeks, i.e. $4000$ views), compute the probability that your app gets **more than $25$** new installs. (7 points)

**(b)** Using Python, compute and plot the probability mass function of the number of monthly installs **twice** — once with the binomial distribution and once with the Poisson distribution — on the same axes. Show that the two are very close, and explain in one sentence why the Poisson approximation works well here. (8 points)

> **Tools.**
> ```python
> from scipy.stats import binom, poisson
> ```
> Useful functions: `binom.pmf`, `binom.cdf`, `poisson.pmf`, `poisson.cdf`. (For the Poisson model, the rate is $\lambda = np$.)

---

## Question 6 — Capstone: revenue models and risk (20 points)

Two streaming platforms model their monthly revenue per customer as a function of $X$, the number of hours a random user watches per day:

- Company $A$: $\quad R_A = 50 + 20X$ dollars
- Company $B$: $\quad R_B = 40 + 30\sqrt{X}$ dollars

The viewing time $X$ follows an exponential distribution with parameter $3$ (rate $\lambda = 3$), so each user watches on average $1/3$ hour ($20$ minutes) per day. Users behave the same on both platforms; only the way activity converts to revenue differs.

**(a)** Find the PDF and CDF of $R_A$ and of $R_B$. (6 points)

**(b)** Compute the expected value and variance of $R_A$ and of $R_B$. (You may leave $E[\sqrt{X}]$ in integral form or evaluate it.) (4 points)

**(c)** Compute $P(R_A > 90)$ and explain in words what this probability means. (2 points)

**(d)** Simulate $100{,}000$ customers for **each** company. For each: plot a histogram of the simulated revenues, report the simulated mean, variance, and standard deviation, and overlay the theoretical PDF from part (a) on the histogram. Do the simulations match the theory? (6 points)

**(e) Discussion.** Which company has the higher **average** revenue per customer, and which one carries more **risk** (revenue volatility)? Briefly justify using your results above. (2 points)

> **Reminder.**
> - $R_A = aX + b$ is a **linear** transformation.
> - $R_B = a\sqrt{X} + b$ is a **nonlinear** transformation, so finding its PDF requires the change-of-variables (transformation) method.

---

### Optional

## Question 7 — Reading and comparing CDFs (10 bonus points)

The diagram below shows the cumulative distribution function (CDF) of the monthly income of the citizens of four different countries. Using only these curves, compare the economic conditions of the four countries — for example, which has the most people in poverty, which is the most equal, and which has the highest incomes.

![Cumulative income distributions for four countries](HW3-v2-q7-chart.png)

*Chart description: four CDF curves. The horizontal axis is monthly income in dollars (marked at \$5000, \$10000, \$15000, \$20000); the vertical axis is cumulative probability from $0$ to $1$. The **orange** curve rises fastest and saturates near $1$ earliest (income concentrated at low values). The **blue/purple** curve rises somewhat more slowly. The **red** curve stays low at first and then rises to reach $1$ near the high-income end. The **green** curve is a straight diagonal line from the origin to the top-right (a uniform-like spread of income).*
