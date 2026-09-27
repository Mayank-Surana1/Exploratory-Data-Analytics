# NumPy Complete Guide

A structured, hands-on reference covering the core capabilities of NumPy, the foundational Python library for numerical computing, data analysis, and machine learning. This repository walks through array creation, manipulation, mathematical operations, and statistical analysis using clear, practical examples.

## Overview

NumPy (Numerical Python) is the fundamental open-source library for scientific computing in Python. It introduces the ndarray, a fast and memory-efficient multidimensional array object, along with a comprehensive set of mathematical functions to operate on that data. This notebook serves as a complete, categorized walkthrough of the library's essential features.

## Table of Contents

1. Installation and Setup
2. Array Creation
3. Array Reshaping
4. Array Attributes
5. Data Type Conversion
6. Arithmetic Operations
7. Universal Functions
8. Slicing and Indexing
9. Array Iteration
10. Element Modification
11. Statistical Operations
12. Logical Operations and Boolean Indexing

## Installation and Setup

Covers installing NumPy through pip and importing the library into a Python environment as the conventional alias np, which is the standard convention used throughout the scientific Python ecosystem.

## Array Creation

Demonstrates the construction of one-dimensional and multidimensional arrays using np.array, along with generated structures such as ranges through np.arange, matrices of ones through np.ones, and identity matrices through np.eye. Includes inspection of core properties including shape, dimension count, and data type at the point of creation.

## Array Reshaping

Explains how to alter the structure of an array without changing its underlying data, using the reshape method. Includes practical guidance on matching element counts correctly to avoid dimension mismatch errors.

## Array Attributes

Details the essential metadata every array exposes, including shape (the size along each dimension), ndim (the number of dimensions), size (the total element count), dtype (the data type of the elements), and itemsize (the memory footprint of each element in bytes).

## Data Type Conversion

Covers converting arrays between data types using the astype method, such as transforming floating-point values into integers, along with precision handling techniques like rounding values before conversion to preserve numerical accuracy.

## Arithmetic Operations

Illustrates element-wise arithmetic across arrays, including addition, multiplication, and division, forming the basis of vectorized computation that allows operations to run without explicit loops.

## Universal Functions

Introduces NumPy's universal functions, known as ufuncs, which apply mathematical operations element-wise across an entire array at high speed. Includes square root, exponential, and trigonometric functions such as sine.

## Slicing and Indexing

Covers extracting specific elements, rows, columns, and subarrays using index and slice notation. Clarifies the inclusive-start and exclusive-stop convention that governs range-based selection in NumPy.

## Array Iteration

Demonstrates traversing array elements efficiently using np.nditer, a multidimensional iterator that simplifies looping over arrays of any dimensionality.

## Element Modification

Shows how to update array values directly through index assignment, including single-element updates and broadcasted assignment across entire rows or slices.

## Statistical Operations

Covers descriptive statistics available in NumPy, including mean, median, standard deviation, and variance, along with data normalization techniques used to standardize values for analysis and modeling.

## Logical Operations and Boolean Indexing

Explains how to filter array data using logical conditions and boolean masks, enabling the selection of elements that satisfy one or more comparison criteria in a single, readable expression.

## Prerequisites

Python 3.x and pip are required. Install NumPy using the command below.

```
pip install numpy
```

## Usage

Clone this repository and open the notebook in Jupyter Notebook, JupyterLab, or Google Colab to run the examples interactively.

```
git clone <repository-url>
cd numpy-complete-guide
jupyter notebook
```

## Repository Contents

| File | Description |
|------|-------------|
| Numpy Complete Guide.ipynb | Jupyter notebook containing all categorized examples and outputs |
| README.md | Project documentation and reference guide |

## Skills Demonstrated

Array manipulation, vectorized computation, data type handling, statistical analysis, and boolean filtering using NumPy, forming a strong foundation for data analysis, scientific computing, and machine learning workflows.

## License

This project is open for educational and reference use.
