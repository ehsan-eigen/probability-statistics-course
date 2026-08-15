# Statistics and Probability — Homework 3

## Question 1 (10 points)

Suppose $X$ is a random variable with a uniform distribution on the interval $\left[-\pi/2,\ +\pi/2\right]$, and let $Y = \sin(x)$. Find the probability density function $f_{Y}(y)$.

## Question 2 (20 points)

An oil company intends to outsource its drilling and oil-extraction projects to private companies. Two private companies are active in this field. To decide which private company to award the work to, the oil company holds a tender. In this tender, both private companies announce their price proposals for carrying out the drilling project simultaneously on a specific day. The oil company will award the project to whichever company announces the lower price.

The oil company knows that the price company $A$ will announce is a random number from an exponential distribution with a mean of \$12 million, and company $B$'s price is a random number from an exponential distribution with a mean of \$13 million.

Therefore, the final price the oil company must pay for each drilling project is described by the random variable $T$:

$$T = \min(X_1, X_2)$$

**(a)** Find the probability density function (PDF) and the expected value of the variable $T$. (10 points)

**(b)** Compute the probability that the oil company receives a bid below \$10 million. (5 points)

**(c)** Show that if, instead of a tender (lowest price wins), we were dealing with an auction (highest price wins), obtaining the final distribution theoretically would be much more difficult — that is, if instead of the minimum price we were dealing with the maximum price. For example, suppose in this same problem the private companies proposed prices such that, by paying that price to the oil company, they would buy the right to exploit a well from the oil company, and the oil company sold this right to the highest bidder. Using simulation, plot the distribution of the maximum price. (5 points)

## Question 3 (20 points)

The measurement error of a sensor (in millivolts) is modeled as follows:

$$E \sim N(\mu = 0,\ \sigma^2 = 4)$$

That is, the sensor reads the true voltage value plus an error $E$.

**(a)** What is the probability that a measurement error lies in the interval $-3$ mV to $+3$ mV?

**(b)** Find the number $e > 0$ such that

$$P(|E| \le e) = 0.99$$

According to a technical specification, the sensor error must not exceed 5 mV.

**(c)** Under the current model, what proportion of measurements violate this specification (i.e., have $|E| > 5$ mV)?

**(d)** To meet a stricter specification — for example, at most 1% of measurements outside the $\pm 5$ mV range — the manufacturer can reduce the standard deviation through recalibration. Compute the maximum standard deviation that guarantees this 1% violation rate (while keeping $\mu = 0$).

**(e)** In simple terms, explain why reducing $\sigma$ decreases the violation rate.

## Question 4 (50 points)

Suppose two online movie- and series-streaming companies/platforms model their monthly revenue from each customer as follows:

- Company $A$'s revenue per user: $R_A = 50 + 20X$ dollars
- Company $B$'s revenue per user: $R_B = 40 + 30\sqrt{X}$ dollars

$X$ is the amount of time a random user watches movies daily on the platform. $X$ comes from an exponential distribution with parameter $3$. That is, each user watches, on average, $1/3$ hour — i.e., 20 minutes — of movies per day. As mentioned, the users of both platforms behave similarly, but the conversion of activity into revenue differs for each company.

**(a)** Find the PDF and CDF for the variables $R_A$ and $R_B$. (10 points)

**(b)** Compute the expected value and variance of the variables $R_A$ and $R_B$. (10 points)

**(c)** Obtain $P(R_A > 90)$ and explain the meaning of this expression in words. (5 points)

**(d)** Simulate 100,000 customers for each company. (15 points) For each company:

- Plot a histogram of the simulated revenues.
- Compute and report the following from your simulation output:
  - mean
  - variance
  - standard deviation
- Plot the theoretical distributions (PDF) on top of the histograms. Do the empirical distributions provide a good estimate of the theoretical distributions?

**(e)** Discussion and analysis: (10 points)

- Which company has the higher average revenue per customer?
- Which company has more risk (revenue volatility)?
- Which revenue model is more suitable for a small startup, and why?
- How does the transformation of $X$ affect the shape and risk of the revenue?

### Additional hints

Remember:

- If $Y = aX + b$, we have a linear transformation.
- If $Y = a\sqrt{X} + b$, the transformation is nonlinear, and you must use the transformation method to find the new PDF.
