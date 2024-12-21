# Linear Algebra Course

## Table of Contents
1. [Introduction to Linear Algebra](#introduction-to-linear-algebra)
2. [Vectors](#vectors)
  - [Definition of Vectors](#definition-of-vectors)
  - [Vector Operations](#vector-operations)
    - [Addition](#addition)
    - [Scalar Multiplication](#scalar-multiplication)
    - [Dot Product](#dot-product)
3. [Matrices](#matrices)
  - [Definition of Matrices](#definition-of-matrices)
  - [Matrix Operations](#matrix-operations)
    - [Matrix Addition](#matrix-addition)
    - [Matrix Multiplication](#matrix-multiplication)
4. [Determinants](#determinants)
  - [Definition of Determinant](#definition-of-determinant)
  - [Calculating Determinants](#calculating-determinants)
    - [2x2 Matrix](#2x2-matrix)
    - [3x3 Matrix](#3x3-matrix)
5. [Vector Spaces](#vector-spaces)
  - [Definition of Vector Spaces](#definition-of-vector-spaces)
  - [Basis and Dimension](#basis-and-dimension)
6. [Linear Transformations](#linear-transformations)
  - [Definition of Linear Transformations](#definition-of-linear-transformations)
  - [Matrix Representation](#matrix-representation)
7. [Eigenvalues and Eigenvectors](#eigenvalues-and-eigenvectors)
  - [Definition of Eigenvalues and Eigenvectors](#definition-of-eigenvalues-and-eigenvectors)
  - [Finding Eigenvalues and Eigenvectors](#finding-eigenvalues-and-eigenvectors)
8. [Applications of Linear Algebra](#applications-of-linear-algebra)
9. [Conclusion](#conclusion)
10. [Further Reading](#further-reading)

---

## Introduction to Linear Algebra

Linear algebra is a branch of mathematics that deals with vectors, matrices, and linear transformations. It is fundamental in various fields such as computer science, physics, engineering, and economics.

---

## Vectors

### Definition of Vectors

A vector is an ordered list of numbers that can represent a point in space or a direction. Vectors can be represented in different dimensions.

**Example:**

A 2-dimensional vector can be represented as:

$$
\mathbf{v} = \begin{pmatrix} 3 \\ 4 \end{pmatrix}
$$

---

### Vector Operations

#### Addition

The sum of two vectors is obtained by adding their corresponding components.

**Example:**

If

$$
\mathbf{u} = \begin{pmatrix} 1 \\ 2 \end{pmatrix}, \quad \mathbf{v} = \begin{pmatrix} 3 \\ 4 \end{pmatrix}
$$

Then

$$
\mathbf{u} + \mathbf{v} = \begin{pmatrix} 1 + 3 \\ 2 + 4 \end{pmatrix} = \begin{pmatrix} 4 \\ 6 \end{pmatrix}
$$

#### Scalar Multiplication

Multiplying a vector by a scalar scales its components.

**Example:**

If

$$
k = 2, \quad \mathbf{v} = \begin{pmatrix} 3 \\ 4 \end{pmatrix}
$$

Then

$$
k \cdot \mathbf{v} = 2 \cdot \begin{pmatrix} 3 \\ 4 \end{pmatrix} = \begin{pmatrix} 6 \\ 8 \end{pmatrix}
$$

#### Dot Product

The dot product of two vectors is a scalar obtained by multiplying corresponding components and summing the results.

**Example:**

For

$$
\mathbf{u} = \begin{pmatrix} 1 \\ 2 \end{pmatrix}, \quad \mathbf{v} = \begin{pmatrix} 3 \\ 4 \end{pmatrix}
$$

The dot product is:

$$
\mathbf{u} \cdot \mathbf{v} = 1 \cdot 3 + 2 \cdot 4 = 3 + 8 = 11
$$

---

## Matrices

### Definition of Matrices

A matrix is a rectangular array of numbers arranged in rows and columns.

**Example:**

A \( 2 \times 3 \) matrix can be represented as:

$$
\mathbf{A} = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}
$$

---

### Matrix Operations

#### Matrix Addition

Matrices can be added if they have the same dimensions by adding their corresponding elements.

**Example:**

If

$$
\mathbf{A} = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 5 & 6 \\ 7 & 8 \end{pmatrix}
$$

Then

$$
\mathbf{A} + \mathbf{B} = \begin{pmatrix} 1 + 5 & 2 + 6 \\ 3 + 7 & 4 + 8 \end{pmatrix} = \begin{pmatrix} 6 & 8 \\ 10 & 12 \end{pmatrix}
$$

#### Matrix Multiplication

The product of two matrices is obtained by multiplying rows of the first matrix by columns of the second matrix.

**Example:**

If

$$
\mathbf{A} = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 5 & 6 \\ 7 & 8 \end{pmatrix}
$$

Then

$$
\mathbf{C} = \mathbf{A} \cdot \mathbf{B} = \begin{pmatrix} 1 \cdot 5 + 2 \cdot 7 & 1 \cdot 6 + 2 \cdot 8 \\ 3 \cdot 5 + 4 \cdot 7 & 3 \cdot 6 + 4 \cdot 8 \end{pmatrix} = \begin{pmatrix} 19 & 22 \\ 43 & 50 \end{pmatrix}
$$

---

## Determinants

### Definition of Determinant

The determinant is a scalar value that can be computed from a square matrix. It provides important information about the matrix, such as whether it is invertible.

### Calculating Determinants

#### 2x2 Matrix

For a \( 2 \times 2 \) matrix:

$$
\mathbf{A} = \begin{pmatrix} a & b \\ c & d \end{pmatrix}
$$

The determinant is calculated as:

$$
\text{det}(\mathbf{A}) = ad - bc
$$

**Example:**

For

$$
\mathbf{A} = \begin{pmatrix} 3 & 2 \\ 1 & 4 \end{pmatrix}
$$

The determinant is:

$$
\text{det}(\mathbf{A}) = (3)(4) - (2)(1) = 12 - 2 = 10
$$

#### 3x3 Matrix

For a \( 3 \times 3 \) matrix:

$$
\mathbf{A} = \begin{pmatrix} a & b & c \\ d & e & f \\ g & h & i \end{pmatrix}
$$

The determinant is calculated using:

$$
\text{det}(\mathbf{A}) = a(ei - fh) - b(di - fg) + c(dh - eg)
$$

**Example:**

For

$$
\mathbf{A} = \begin{pmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 5 & 6 & 0 \end{pmatrix}
$$

The determinant is:

$$
\text{det}(\mathbf{A}) = 1(1 \cdot 0 - 4 \cdot 6) - 2(0 \cdot 0 - 4 \cdot 5) + 3(0 \cdot 6 - 1 \cdot 5)
$$

Calculating step by step:

$$
= 1(0 - 24) - 2(0 - 20) + 3(0 - 5)
$$

$$
= -24 + 40 - 15 = 1
$$

---

## Vector Spaces

### Definition of Vector Spaces

A vector space is a set of vectors that can be added together and multiplied by scalars while satisfying certain axioms (like closure, associativity, etc.).

**Example:**

The set of all \( n \)-dimensional vectors is a vector space.

$$
V = \{ \mathbf{v} = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix} \, | \, x_i \in \mathbb{R} \}
$$

### Basis and Dimension

A basis of a vector space is a set of linearly independent vectors that span the space. The dimension is the number of vectors in the basis.

**Example:**

In \( \mathbb{R}^2 \), the vectors

$$
\mathbf{e_1} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad \mathbf{e_2} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$

form a basis, and the dimension is 2.

---

## Linear Transformations

### Definition of Linear Transformations

A linear transformation is a function between two vector spaces that preserves vector addition and scalar multiplication.

**Example:**

Let \( T: \mathbb{R}^2 \to \mathbb{R}^2 \) be defined by

$$
T(\mathbf{x}) = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \mathbf{x}
$$

Then \( T \) is a linear transformation.

### Matrix Representation

Every linear transformation can be represented by a matrix. The transformation of a vector can be expressed as matrix multiplication.

**Example:**

If

$$
T(\mathbf{x}) = A\mathbf{x} \text{ where } A = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}
$$

Then

$$
T\begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 2 \\ 6 \end{pmatrix}
$$

---

## Eigenvalues and Eigenvectors

### Definition of Eigenvalues and Eigenvectors

An eigenvector of a square matrix \( A \) is a non-zero vector \( \mathbf{v} \) such that

$$
A\mathbf{v} = \lambda \mathbf{v}
$$

where \( \lambda \) is the eigenvalue corresponding to the eigenvector \( \mathbf{v} \).

### Finding Eigenvalues and Eigenvectors

To find the eigenvalues, solve the characteristic equation:

$$
\text{det}(A - \lambda I) = 0
$$

**Example:**

For

$$
A = \begin{pmatrix} 4 & 1 \\ 2 & 3 \end{pmatrix}
$$

The characteristic polynomial is:

$$
\text{det}\left(\begin{pmatrix} 4 - \lambda & 1 \\ 2 & 3 - \lambda \end{pmatrix}\right) = (4 - \lambda)(3 - \lambda) - (2)(1)
$$

Expanding:

$$
= \lambda^2 - 7\lambda + 10 = 0
$$

Factoring:

$$
(\lambda - 5)(\lambda - 2) = 0 \implies \lambda_1 = 5, \lambda_2 = 2
$$

**Finding Eigenvectors:**

For \( \lambda = 5 \):

$$
(A - 5I)\mathbf{v} = 0 \implies \begin{pmatrix} -1 & 1 \\ 2 & -2 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0
$$

This gives \( x_1 = x_2 \). So, an eigenvector is:

$$
\mathbf{v_1} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}
$$

For \( \lambda = 2 \):

$$
(A - 2I)\mathbf{v} = 0 \implies \begin{pmatrix} 2 & 1 \\ 2 & 1 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0
$$

This gives \( 2x_1 + x_2 = 0 \) or \( x_2 = -2x_1 \). So, an eigenvector is:

$$
\mathbf{v_2} = \begin{pmatrix} 1 \\ -2 \end{pmatrix}
$$

---

## Applications of Linear Algebra

Linear algebra has numerous applications in various fields, including:

- **Computer Graphics**: Transformations and rendering of images.
- **Machine Learning**: Algorithms for data processing and modeling.
- **Economics**: Input-output models and optimization.
- **Physics**: Quantum mechanics and relativity.

---

## Conclusion

Linear algebra is a vital area of mathematics with broad applications. Mastering the concepts of vectors, matrices, and linear transformations is essential for students in various scientific and engineering fields.

---

## Further Reading

- "Linear Algebra and Its Applications" by David C. Lay
- "Introduction to Linear Algebra" by Gilbert Strang
- Online resources such as Khan Academy and MIT OpenCourseWare for interactive learning.
