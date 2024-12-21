# Calculus Course

## Table of Contents
1. [Introduction to Calculus](#introduction-to-calculus)
2. [Limits](#limits)
    - [Definition of Limits](#definition-of-limits)
    - [Calculating Limits](#calculating-limits)
3. [Derivatives](#derivatives)
    - [Definition of Derivative](#definition-of-derivative)
    - [Rules of Differentiation](#rules-of-differentiation)
    - [Applications of Derivatives](#applications-of-derivatives)
4. [Integrals](#integrals)
    - [Definition of Integral](#definition-of-integral)
    - [Fundamental Theorem of Calculus](#fundamental-theorem-of-calculus)
    - [Applications of Integrals](#applications-of-integrals)
5. [Multivariable Calculus](#multivariable-calculus)
    - [Partial Derivatives](#partial-derivatives)
    - [Multiple Integrals](#multiple-integrals)
6. [Conclusion](#conclusion)

---

## Introduction to Calculus

Calculus is the mathematical study of continuous change, focusing on rates of change (derivatives) and accumulation of quantities (integrals).

---

## Limits

### Definition of Limits

A limit is a value that a function approaches as the input approaches some value.

**Example:**

$$
\lim_{x \to 2} (3x + 1) = 7
$$

### Calculating Limits

#### Example 1: Direct Substitution

$$
\lim_{x \to 3} (x^2 - 9) = 3^2 - 9 = 0
$$

#### Example 2: Factoring

$$
\lim_{x \to 1} \frac{x^2 - 1}{x - 1} = \lim_{x \to 1} \frac{(x - 1)(x + 1)}{x - 1} = \lim_{x \to 1} (x + 1) = 2
$$

---

## Derivatives

### Definition of Derivative

The derivative measures how a function changes as its input changes.

**Example:**

The derivative of \(f(x) = x^2\) is:

$$
f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h} = 2x
$$

### Rules of Differentiation

1. **Power Rule**: $$\frac{d}{dx}(x^n) = nx^{n-1}$$
2. **Product Rule**: $$\frac{d}{dx}(uv) = u'v + uv'$$
3. **Quotient Rule**: $$\frac{d}{dx}\left(\frac{u}{v}\right) = \frac{u'v - uv'}{v^2}$$

#### Example:

Differentiate \(f(x) = x^3 - 5x + 2\):

$$
f'(x) = 3x^2 - 5
$$

### Applications of Derivatives

- Finding tangents to curves
- Optimization problems (maxima and minima)

---

## Integrals

### Definition of Integral

An integral calculates the area under a curve.

**Example:**

The integral of \(f(x) = x^2\) is:

$$
\int x^2 \, dx = \frac{x^3}{3} + C
$$

### Fundamental Theorem of Calculus

This theorem links differentiation and integration.

**Example:**

If \(F(x)\) is the antiderivative of \(f(x)\), then:

$$
\int_a^b f(x) \, dx = F(b) - F(a)
$$

---

### Applications of Integrals

- Calculating areas and volumes
- Solving problems in physics and engineering

---

## Multivariable Calculus

### Partial Derivatives

Partial derivatives measure how a function changes with respect to one variable while keeping others constant.

**Example:**

If \(f(x, y) = x^2y + 3xy^2\):

$$
\frac{\partial f}{\partial x} = 2xy + 3y^2
$$

### Multiple Integrals

Multiple integrals extend the concept of integration to functions of several variables.

**Example:**

The double integral of \(f(x, y) = x + y\) over a region \(R\):

$$
\iint_R (x + y) \, dA
$$

---

## Conclusion

Calculus is a powerful tool in mathematics, providing essential techniques for understanding changes and areas. This course covers the foundational concepts necessary for further study in mathematics and its applications in various fields.

---

## Further Reading

- "Calculus" by James Stewart
- "Calculus: Early Transcendentals" by William L. Briggs and Lyle Cochran
