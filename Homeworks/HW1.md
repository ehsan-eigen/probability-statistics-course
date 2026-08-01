# Statistics and Probability — Homework 1

## Problem 1 — Poker hands (20 points)

You can easily look up the probabilities of 5-card poker hands, for example at [https://en.wikipedia.org/wiki/Poker_probability](https://en.wikipedia.org/wiki/Poker_probability).

For this problem, consider the following two hand types:

- **Two pair:** two cards of one rank, two cards of another rank, and one card of a third, different rank. Example: {2♡, 2♠, 5♡, 5♣, K♢}
- **Three of a kind:** three cards of one rank, and two other cards of two different ranks. Example: {2♡, 2♠, 2♣, 5♣, K♡}

**(a)** Compute the probability that a random 5-card hand is either two pair or three of a kind. *(10 points)*

**(b)** Compute the probability that the hand contains at least two cards of the same rank. *(10 points)*

---

## Problem 2 — Two unusual dice (20 points)

We have two dice with the following numbers written on their faces:

- **Blue die:** 3, 3, 3, 3, 6, 6
- **White die:** 2, 2, 2, 5, 5, 5

Assume all faces of each die are equally likely.

**(a)** If we roll the white die once and the blue die once, find the probability that white wins — that is, the probability that the white die shows a larger number than the blue die. *(8 points)*

**(b)** Suppose we roll the white die twice and the blue die twice. What is the probability that the sum of the white rolls exceeds the sum of the blue rolls? *(12 points)*

---

## Problem 3 — A three-round gambling game (25 points)

Consider the following gambling game.

If the die comes up 6, you receive 1,000,000 Toman. Otherwise, you must pay 500,000 Toman.

You enter the game with an initial balance of 1,000,000 Toman and play three rounds. If your money runs out before the three rounds are over, the game ends at that round.

**(a)** Propose a suitable sample space Ω for this problem. *(5 points)*

**(b)** Define a random variable *X* representing the profit you obtain for each outcome in Ω. If you lose money, the profit is negative. *(4 points)*

**(c)** Derive and sketch the PMF and the CDF of *X*. *(8 points)*

**(d)** Using the random variable and PMF above, compute the expected value of this game. Is it a fair game? *(4 points)*

**(e)** Using the CDF, state the probability that this game turns out to be profitable, i.e. that *X* is strictly positive. *(4 points)*

*Hint:* Your profit at the end of the game is determined by the difference between the number of wins and the number of losses.

---

## Problem 4 — Spam detection (15 points)

In a spam email detection system, we define the following two events:

- Event A = "the email contains the word *free*"
- Event B = "the email is spam"

Based on a dataset of 10,000 emails, the following was observed:

- 3,000 emails contain the word *free*
- 4,000 emails are spam
- 1,500 emails both contain *free* and are spam

**(a)** Are events A and B independent? *(7 points)*

**(b)** Compute *P(B | A)* and interpret the result: does seeing the word *free* increase the probability that an email is spam? *(8 points)*

---

## Problem 5 — Which die is it? (20 points)

There are five dice in a drawer:

- one 4-sided die (D4)
- two 6-sided dice (D6)
- two 8-sided dice (D8)

As is standard, the faces of a die are numbered from 1 to *n*, where *n* is the number of faces. Your friend secretly picks one of the five dice at random. Let *S* be the number of faces of the chosen die.

Without showing you the chosen die, your friend rolls it and tells you the result. Let *R* be the roll outcome.

**(a)** Use Bayes' rule to find *P(S = s | R = 3)* for *s* = 4, 6, 8. *(12 points)*

**(b)** If *R* = 3, which die is the most likely one? Briefly explain why the answer differs from the prior. *(8 points)*
