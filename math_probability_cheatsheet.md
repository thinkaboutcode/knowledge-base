# Probability Course

## Table of Contents
1. [Introduction to Probability](#introduction-to-probability)
2. [Basic Concepts](#basic-concepts)
    - [Sample Space](#sample-space)
    - [Events](#events)
3. [Types of Probability](#types-of-probability)
    - [Theoretical Probability](#theoretical-probability)
    - [Empirical Probability](#empirical-probability)
    - [Subjective Probability](#subjective-probability)
4. [Rules of Probability](#rules-of-probability)
    - [Addition Rule](#addition-rule)
    - [Multiplication Rule](#multiplication-rule)
5. [Conditional Probability](#conditional-probability)
6. [Bayes' Theorem](#bayes-theorem)
7. [Random Variables](#random-variables)
    - [Discrete Random Variables](#discrete-random-variables)
    - [Continuous Random Variables](#continuous-random-variables)
8. [Probability Distributions](#probability-distributions)
    - [Binomial Distribution](#binomial-distribution)
    - [Normal Distribution](#normal-distribution)
9. [Conclusion](#conclusion)

---

## Introduction to Probability

Probability is a branch of mathematics that deals with the likelihood of events occurring. It quantifies uncertainty and helps in making informed decisions based on potential outcomes.

---

## Basic Concepts

### Sample Space

The sample space is the set of all possible outcomes of a probabilistic experiment.

**Example:**

For a single six-sided die roll, the sample space \( S \) is:

$$
S = \{1, 2, 3, 4, 5, 6\}
$$

### Events

An event is a subset of the sample space. An event can consist of one or more outcomes.

**Example:**

Let \( E \) be the event of rolling an even number:

$$
E = \{2, 4, 6\}
$$

---

## Types of Probability

### Theoretical Probability

Theoretical probability is calculated based on the possible outcomes in a perfect world.

**Formula:**

$$
P(A) = \frac{\text{Number of favorable outcomes}}{\text{Total number of possible outcomes}}
$$

**Example:**

The probability of rolling a 3 on a die:

$$
P(3) = \frac{1}{6}
$$

### Empirical Probability

Empirical probability is based on observed data.

**Formula:**

$$
P(A) = \frac{\text{Number of times event A occurs}}{\text{Total number of trials}}
$$

**Example:**

If you roll a die 60 times and get a 3 on 10 occasions:

$$
P(3) = \frac{10}{60} = \frac{1}{6}
$$

### Subjective Probability

Subjective probability is based on personal judgment or experience rather than exact calculations.

**Example:**

A sports analyst might say that a particular team has a 70% chance of winning based on their performance, injuries, and other factors.

---

## Rules of Probability

### Addition Rule

The addition rule is used to find the probability of the union of two events.

**Formula:**

For any two events \( A \) and \( B \):

$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

**Example:**

Let \( A \) be the event of rolling an odd number, and \( B \) be the event of rolling a number greater than 4.

- \( P(A) = \frac{3}{6} = \frac{1}{2} \) (numbers 1, 3, 5)
- \( P(B) = \frac{2}{6} = \frac{1}{3} \) (numbers 5, 6)
- \( P(A \cap B) = P(5) = \frac{1}{6} \)

Thus,

$$
P(A \cup B) = \frac{1}{2} + \frac{1}{3} - \frac{1}{6} = \frac{3}{6} + \frac{2}{6} - \frac{1}{6} = \frac{4}{6} = \frac{2}{3}
$$

### Multiplication Rule

The multiplication rule is used to find the probability of the intersection of two events.

**Formula:**

For two independent events \( A \) and \( B \):

$$
P(A \cap B) = P(A) \cdot P(B)
$$

**Example:**

If the probability of getting a head when flipping a coin is \( P(H) = \frac{1}{2} \) and the probability of rolling a 4 on a die is \( P(4) = \frac{1}{6} \):

$$
P(H \cap 4) = P(H) \cdot P(4) = \frac{1}{2} \cdot \frac{1}{6} = \frac{1}{12}
$$

---

## Conditional Probability

Conditional probability is the probability of event \( A \) given that event \( B \) has occurred.

**Formula:**

$$
P(A | B) = \frac{P(A \cap B)}{P(B)}
$$

**Example:**

If a box contains 3 red and 2 blue balls, what is the probability of drawing a red ball given that a blue ball was drawn first?

1. Total balls: \( 5 \)
2. Probability of drawing a blue ball: \( P(B) = \frac{2}{5} \)
3. After drawing a blue ball, the probability of drawing a red ball:

$$
P(A | B) = \frac{P(A \cap B)}{P(B)} = \frac{\frac{3}{5}}{\frac{2}{5}} = \frac{3}{2}
$$

---

## Bayes' Theorem

Bayes' Theorem relates conditional probabilities and allows us to update the probability of an event based on new information.

**Formula:**

$$
P(A | B) = \frac{P(B | A) \cdot P(A)}{P(B)}
$$

**Example:**

In a medical test, suppose:

- The probability of having a disease \( P(D) = 0.01 \)
- The probability of testing positive given that you have the disease \( P(T | D) = 0.9 \)
- The probability of testing positive given that you do not have the disease \( P(T | \neg D) = 0.05 \)

To find the probability of having the disease given a positive test result \( P(D | T) \):

1. Calculate \( P(T) \):

$$
P(T) = P(T | D) \cdot P(D) + P(T | \neg D) \cdot P(\neg D) = 0.9 \cdot 0.01 + 0.05 \cdot 0.99
$$

$$
= 0.009 + 0.0495 = 0.0585
$$

2. Apply Bayes' Theorem:

$$
P(D | T) = \frac{P(T | D) \cdot P(D)}{P(T)} = \frac{0.9 \cdot 0.01}{0.0585} \approx 0.1538
$$

---

## Random Variables

### Discrete Random Variables

A discrete random variable can take on a countable number of values.

**Example:**

Let \( X \) be the random variable representing the number of heads in three coin tosses. The possible values are \( 0, 1, 2, 3 \).

### Continuous Random Variables

A continuous random variable can take on any value in a given range.

**Example:**

Let \( Y \) be the random variable representing the height of students in a class.

---

## Probability Distributions

### Binomial Distribution

The binomial distribution models the number of successes in a fixed number of independent Bernoulli trials.

**Formula:**

$$
P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}
$$

**Example:**

If a coin is flipped 10 times (n = 10) and the probability of heads (success) is \( p = 0.5 \), what is the probability of getting exactly 3 heads?

$$
P(X = 3) = \binom{10}{3} (0.5)^3 (0.5)^{10-3} = \binom{10}{3} (0.5)^{10} = \frac{120}{1024} \approx 0.1172
$$

### Normal Distribution

The normal distribution is a continuous probability distribution characterized by its bell-shaped curve.

**Properties:**
- Mean \( \mu \)
- Standard deviation \( \sigma \)

**Example:**

If the heights of students are normally distributed with a mean of \( \mu = 170 \) cm and standard deviation \( \sigma = 10 \) cm, the probability of a student being taller than 180 cm is calculated using the Z-score:

$$
Z = \frac{X - \mu}{\sigma} = \frac{180 - 170}{10} = 1
$$

Using standard normal distribution tables, find \( P(Z > 1) \) which gives the area to the right of \( Z = 1 \).

---

## Conclusion

Probability is a foundational concept in statistics and is widely used in various fields including finance, science, engineering, and everyday decision-making. Understanding probability helps in analyzing situations and making predictions based on data.

---

## Further Reading

- "A First Course in Probability" by Sheldon Ross
- "Introduction to Probability" by Dimitri P. Bertsekas and John N. Tsitsiklis
- Online resources such as Khan Academy and Coursera for interactive learning.
