# Statistics and Probability - Homework 2

## Question 1 (10 points)

In a mobile game:

- 30% of the time players receive 50 coins
- 50% of the time they receive 100 coins
- 20% of the time they receive 200 coins

Let the random variable $C$ represent the number of coins a player receives.

Compute $\mathrm{VAR}(C)$ in two ways:

- **Method 1:** From the definition of variance, i.e. $E\big[(X - E[X])^2\big]$
- **Method 2:** From the relation $\mathrm{Var}(X) = E[X^2] - E[X]^2$

## Question 2 (10 points)

Suppose $X$ and $Y$ are two independent random variables. We know that:

$$\mathrm{Var}(2X - Y) = 6$$

$$\mathrm{Var}(X + 2Y) = 9$$

Find $\mathrm{VAR}(X)$ and $\mathrm{VAR}(Y)$.

## Question 3 — A three-round gambling game (30 points)

Consider the following gambling game.

If the die comes up 6, you receive 1,000,000 Toman. Otherwise, you must pay 500,000 Toman.

You enter the game with an initial balance of 1,000,000 Toman and play three rounds. If your money runs out before the three rounds are over, the game ends at that round.

**(a)** Propose a suitable sample space $\Omega$ for this problem. *(5 points)*

**(b)** Define a random variable $X$ representing the profit you obtain for each outcome in $\Omega$. If you lose money, the profit is negative. *(5 points)*

**(c)** Derive and sketch the PMF and the CDF of $X$. *(10 points)*

**(d)** Using the random variable and PMF above, compute the expected value of this game. Is it a fair game? *(5 points)*

**(e)** Using the CDF, state the probability that this game turns out to be profitable. *(5 points)*

*Hint:* Your profit at the end of the game is determined by the difference between the number of wins and the number of losses.

## Question 4 (35 points)

You are designing a reliable data transfer protocol.

While sending data packets, each packet may be dropped with probability 15% due to network instability. Suppose that sending a single message (call it a *session*) requires 20 independent packets to be sent.

Assume:

$$X \sim \text{Binomial}(n = 20,\ p = 0.15)$$

where $n = 20$ is the number of packets, $p = 15\%$ is the probability that each packet is dropped, and $X$ is the number of packets dropped in a session.

1. Compute the expected number of dropped packets ($E[X]$) and the variance ($\mathrm{VAR}(X)$). *(8 points)*
2. Find the probability that 3 or fewer packets are dropped in a session. *(8 points)*
3. The system is designed so that if more than 2 packets are dropped, it repeats the entire session — that is, it starts sending the packets from the beginning again (a *retry*), and keeps retrying until the session is delivered successfully. Compute the expected number of retries needed to send one session. *(12 points)*
   - *Hint:* Use the geometric distribution. A failure corresponds to more than 2 packets being dropped out of the 20, and a success corresponds to 2 or fewer packets being dropped.
4. If the system sends 100 messages (i.e. 100 sessions) per hour, what is the expected number of retries per hour? *(7 points)*

## Question 5 (15 points)

Suppose $n$ guests are present at a gathering. The probability that any two randomly chosen guests already know each other is $p$. Compute the expected number of three-person friendship circles (triangles) in this gathering.

*Hint:* Use the linearity of expectation.

---

## Bonus — HW2 Programming (40 optional points)

*This programming part is optional; its 40 points are bonus and are not counted toward the 100-point total above.*

### Random Inspection and Profit Analysis

An inspector tests components one by one until he either finds a defective part or has tested 15 parts. Each component is defective with probability $p = 0.1$, independently.

- **Inspection cost:** \$5 per component tested.
- **Success bonus:** If a defective part is found on or before the 15th test (i.e., at trial $d \le 15$), the inspector receives a \$50 bonus and stops testing.
- **Failure penalty:** If no defective is found in 15 tests, the inspector incurs a \$200 penalty (and stops after test 15).

Let the random profit $P$ be defined as:

$$
P =
\begin{cases}
50 - 5d, & \text{if the first defective appears at test } d \le 15, \\
-200 - 5 \cdot 15, & \text{if no defective in 15 tests.}
\end{cases}
$$

#### 1. Expected Profit *(15 points)*

Write a short Python script to evaluate the expected profit:

$$\mathbb{E}[P] = \sum_{d=1}^{15} (50 - 5d) \cdot P(D = d) + (-275) \cdot P(D > 15),$$

where the random variable $D$ represents the position of the first defective part, and

$$P(D = d) = (1 - p)^{d-1} p, \qquad P(D > 15) = (1 - p)^{15}.$$

#### 2. Variance of Profit *(10 points)*

Extend your code to compute the variance:

$$\mathrm{Var}[P] = \mathbb{E}[P^2] - (\mathbb{E}[P])^2,$$

where

$$\mathbb{E}[P^2] = \sum_{d=1}^{15} (50 - 5d)^2 \cdot P(D = d) + (-275)^2 \cdot P(D > 15).$$

#### 3. Risk-Adjusted Decision *(15 points)*

A risk-averse manager evaluates the policy using a risk-adjusted metric:

$$R = \mathbb{E}[P] - \lambda \sqrt{\mathrm{Var}[P]},$$

with risk aversion parameter $\lambda = 0.2$. Using your code, compute $R$. Based on the value of $R$, determine whether this inspection policy is favorable ($R > 0$).

*Hint:* Use a loop or a NumPy array over $d = 1, \ldots, 15$ to compute the sums. Handle the tail event $D > 15$ separately. Your solution should fit in about 8–10 lines of Python code.
