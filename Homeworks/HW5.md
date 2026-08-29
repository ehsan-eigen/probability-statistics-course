# Probability and Statistics — Computer Engineering

## Homework 5 — Covariance and Correlation

**Total: 100 points + 10 optional bonus points**

---

## What You May Use

You may use the definitions of covariance and correlation, together with linearity of expectation:

$$
\operatorname{Cov}(X,Y)
=
E\big[(X-E[X])(Y-E[Y])\big]
=
E[XY]-E[X]E[Y],
$$

$$
\operatorname{Cor}(X,Y)
=
\rho_{X,Y}
=
\frac{\operatorname{Cov}(X,Y)}
{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}},
$$

---

# Question 1 — Zero Correlation Does Not Mean Independence (25 points)

A sensor reports a discretized voltage $X$ that takes the values

$$
-2,-1,0,1,2
$$

each with probability $1/5$. The instantaneous power delivered by the circuit is

$$
Y=X^2.
$$

### (a) Joint Distribution — 3 points

Complete the following joint probability table for $X$ and $Y$. Include the marginal probabilities.

$$
\begin{array}{c|ccccc|c}
X & -2 & -1 & 0 & 1 & 2 & \text{Total}\\ \hline
Y=0 & & & & & &\\
Y=1 & & & & & &\\
Y=4 & & & & & &\\ \hline
\text{Total} & & & & & &1
\end{array}
$$

### (b) Expectations — 4 points

Find

$$
E[X]
\qquad\text{and}\qquad
E[Y].
$$

### (c) Independence — 4 points

Show that $X$ and $Y$ are **not independent**.

### (d) Covariance and Correlation — 5 points

Show that

$$
\operatorname{Cov}(X,Y)=0,
$$

and hence that

$$
\operatorname{Cor}(X,Y)=0.
$$

### (e) Scatter Plot and Interpretation — 3 points

Simulate $100$ independent samples from the joint distribution of $(X,Y)$, and produce a scatter plot of the sampled pairs. Then, in at most three sentences, respond to a classmate who says:

> *“Zero correlation means the two variables have nothing to do with each other.”*

Explain what correlation measures and what this example shows that correlation can miss.

### (f) Adding a Constant — 3 points

Using either of the two definitions of covariance, show that

$$
\operatorname{Cov}(X,Y+2)
=
\operatorname{Cov}(X,Y).
$$

### (g) Scaling — 3 points

Using either definition of covariance, show that

$$
\operatorname{Cov}(3X,Y)
=
3\operatorname{Cov}(X,Y),
$$

and conclude that

$$
\operatorname{Cov}(3X,Y+2)
=
3\operatorname{Cov}(X,Y).
$$

---

# Question 2 — Packet Routing and Perfect Negative Correlation (19 points)

A router forwards $n=300$ packets. Each packet independently goes to **link A** with probability $0.6$ or to **link B** with probability $0.4$.

Let

$$
A=\text{number of packets sent through link A},
$$

$$
B=\text{number of packets sent through link B}.
$$

Every packet takes exactly one of the two links, so

$$
A+B=300
$$

always.

### (a) Expectations — 4 points

Compute

$$
E[A]
\qquad\text{and}\qquad
E[B].
$$

### (b) Variances — 4 points

Compute

$$
\operatorname{Var}(A)
\qquad\text{and}\qquad
\operatorname{Var}(B).
$$

### (c) Covariance — 5 points

Compute

$$
\operatorname{Cov}(A,B).
$$

### (d) Correlation — 6 points

Compute

$$
\operatorname{Cor}(A,B)
$$

and interpret the value you obtain.

> Generally, if $A+B=c$ for some constant $c$ and $\operatorname{Var}(A)>0$ or $\operatorname{Var}(B)>0$, then
>
> $$
> \operatorname{Cor}(A,B)=?
> $$
>
> You might want to find $?$ yourself as an optional exercise.

---

# Question 3 — Covariance of Overlapping Sums (15 points)

Let

$$
X_1,X_2,\ldots
$$

be independent exponential random variables with rate $\lambda=2$, so that

$$
E[X_i]=\frac12,
\qquad
\operatorname{Var}(X_i)=\frac14.
$$

Define

$$
Y=\sum_{i=1}^{n}X_i,
$$

and

$$
Z=\sum_{i=n-7}^{2n-8}X_i,
$$

where $n\geq8$.

Compute

$$
\operatorname{Cov}(Y,Z)
$$

and

$$
\operatorname{Cor}(Y,Z).
$$

> **Hint:** Determine which random variables appear in both sums. What is the size of the overlap?

---

# Question 4 — Joint Continuous Distribution (16 points)

Consider the joint probability density function from **Question 4 of Homework 4**.

Compute

$$
\operatorname{Cov}(X,Y)
$$

and

$$
\operatorname{Cor}(X,Y).
$$

---

# Question 5 — Portfolio Diversification, Correlation, and Risk Aversion (25 points)

You have two risky assets, **Stock A** and **Stock B**:

| Stock | Expected Return | Standard Deviation |
| ----- | --------------: | -----------------: |
| A     |              6% |                12% |
| B     |              8% |                20% |

You invest a fraction $w$ of your money in Stock A and the remaining fraction $1-w$ in Stock B, where

$$
0\leq w\leq1.
$$

Thus:

* $w=1$: all money is invested in Stock A;
* $w=0$: all money is invested in Stock B;
* $0<w<1$: the investment is divided between the two stocks.

The portfolio return is

$$
R_p=wR_A+(1-w)R_B.
$$

The correlation between the two stock returns is $\rho$, where

$$
-1\leq\rho\leq1.
$$

A risk-averse investor evaluates a portfolio using

$$
U=E[R_p]-\alpha\sigma_p,
$$

where $\alpha\geq0$ is the **risk-aversion coefficient**. A portfolio with a larger $U$ is preferred because it provides a better trade-off between expected return and risk.

---

## Part 1 — Derive the Utility Function (8 points)

Using your knowledge of expectation, variance, covariance, and correlation:

1. Find $E[R_p]$.
2. Find $\operatorname{Var}(R_p)$.
3. Find $\sigma_p$.
4. Obtain the final expression for $U(w,\alpha,\rho)$.

You may use

$$
\operatorname{Cov}(R_A,R_B)
=
\rho\sigma_A\sigma_B.
$$

Show your steps.

---

## Part 2 — Explore the Utility in Desmos (17 points)

Use the following Desmos graph to study the utility function:

https://www.desmos.com/calculator/di8dratqy5

For fixed values of $\alpha$ and $\rho$, determine approximately:

* $w^*$: the value of $w$ that gives the highest utility;
* $u^*$: the maximum utility value shown in Desmos.

You do **not** need to find the maximum using derivatives or simulation.

> In the Desmos graph, $U$ has been multiplied by $10$ only to make the graph easier to visualize. This does not change $w^*$ or any of the conclusions.

For each case below, report approximately $w^*$ and $u^*$ and briefly explain the result using expected return, risk, variance, covariance, and correlation.

### (a) $\alpha=0.3,\ \rho=-0.3$ — 3 points

Is it better to invest fully in one stock or to diversify between the two?

Why can combining two risky stocks reduce the total portfolio risk?

### (b) $\alpha=0.4,\ \rho=1$ — 3 points

Which stock receives all or most of the investment?

Stock A has a lower expected return but is also less risky. Explain why it may be preferred in this case.

### (c) $\alpha=0,\ \rho=\text{anything}$ — 3 points

Change $\rho$ several times.

Does $w^*$ change?

Explain why correlation and risk do or do not matter when the investor is risk-neutral.

### (d) $\alpha=0.1,\ \rho=1$ — 3 points

Compare this result with part (b).

Both cases have exactly the same stocks and the same correlation. Why does changing only $\alpha$ change the preferred investment?

### (e) Perfect Negative Correlation: $\rho=-1$ — 5 points

Compare the following three cases:

* $\alpha=0.1$
* $\alpha=0.5$
* $\alpha=1$

For each case, record $w^*$ and $u^*$.

What do you notice?

Explain why, despite the large change in risk aversion, $w^*$ and the maximum utility do not change.

What is special about the portfolio risk at this value of $w$?

Use the meaning of

$$
\rho=-1
$$

to explain how two individually risky stocks can be combined to produce a portfolio with **zero risk**.

---

## Part 3 — Explore Further (Optional, 10 Bonus Points)

Freely change $\alpha$ and $\rho$ in Desmos.

Find:

1. one pair $(\alpha,\rho)$ for which the best choice is to invest **all the money in Stock A**;
2. one pair $(\alpha,\rho)$ for which the best choice is to invest **all the money in Stock B**;
3. values of $(\alpha,\rho)$ that give the **largest maximum utility** you can find;
4. values of $(\alpha,\rho)$ for which even the **maximum possible utility is negative**.

For each case, briefly explain why the result makes sense.

For the last case, does negative utility necessarily mean that the expected return is negative? Explain.

---

## Point Summary

| Question | Points |
| --- | ---: |
| Question 1 | 25 |
| Question 2 | 19 |
| Question 3 | 15 |
| Question 4 | 16 |
| Question 5, Parts 1–2 | 25 |
| **Required Total** | **100** |
| Question 5, Part 3 | **+10 Bonus** |