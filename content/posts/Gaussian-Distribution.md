---
title: "on Gaussian Distribution"
date: 2024-03-17T12:58:05+08:00
# weight: 1
# aliases: ["/first"]
tags: []
author: dada
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Gaussian distribution"
canonicalURL: "https://dada325.github.io/dadaBlog/Gaussian-Distribution"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "https://unsplash.com/photos/a-black-and-white-photo-of-a-pattern-4cBVro7SHLs" 
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

<img src="https://unsplash.com/photos/a-black-and-white-photo-of-a-pattern-4cBVro7SHLs" />

## The Fundamental Role of Gaussian Distribution in Machine Learning

The Gaussian distribution, also known as the normal distribution, stands as a cornerstone in statistical modeling and machine learning. Its mathematical elegance and natural occurrence in real-world phenomena make it an indispensable tool for data scientists and researchers.

## Mathematical Foundation

The univariate Gaussian distribution is characterized by its probability density function:

$$ p(x|\mu,\sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) $$

For multivariate cases with D dimensions, the distribution takes the form:

$$ p(\mathbf{x}|\boldsymbol{\mu},\boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}}\exp\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right) $$

where μ represents the mean vector and Σ denotes the covariance matrix.

## Theoretical Significance

The central limit theorem underscores the Gaussian distribution's fundamental importance. It states that the sum of many independent random variables tends toward a Gaussian distribution, regardless of their original distributions[4]. This property makes the Gaussian distribution particularly valuable in modeling complex systems where multiple factors contribute to an outcome.

## Applications in Machine Learning

### Parameter Estimation and Inference

In statistical learning, the Gaussian distribution forms the basis for many parameter estimation techniques. Maximum likelihood estimation under Gaussian assumptions leads to elegant closed-form solutions for many problems. The mathematical tractability of Gaussian distributions simplifies many complex calculations in statistical inference.

### Preliminaries and Notation

Let's establish our mathematical framework:

- X = {x₁, ..., xₙ}: N independent observations
- xᵢ ∈ ℝᵈ: Each observation is a D-dimensional vector
- μ ∈ ℝᵈ: Mean vector (unknown parameter)
- Σ ∈ ℝᵈˣᵈ: Covariance matrix (unknown parameter)

## Detailed Derivation

### Step 1: Probability Density Function

The multivariate Gaussian PDF is given by:

$$ p(\mathbf{x}|\boldsymbol{\mu},\boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}}\exp\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right) $$

This expression contains three key components:

1. Normalization constant: $(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}$
2. Mahalanobis distance: $(\mathbf{x}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})$
3. Exponential function that ensures non-negativity

### Step 2: Likelihood Function Construction

Due to independence of observations, we multiply individual probabilities:

$$ L(\boldsymbol{\mu},\boldsymbol{\Sigma}|\mathbf{X}) = \prod\_{i=1}^N p(\mathbf{x}\_i|\boldsymbol{\mu},\boldsymbol{\Sigma}) $$

This gives:

$$ L(\boldsymbol{\mu},\boldsymbol{\Sigma}|\mathbf{X}) = \prod\_{i=1}^N \frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}}\exp\left(-\frac{1}{2}(\mathbf{x}\_i-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}\_i-\boldsymbol{\mu})\right) $$

### Step 3: Log-Likelihood Transformation

Taking the natural logarithm simplifies our optimization:

$$ \begin{align*}
\ln L &= \sum_{i=1}^N \ln\left[\frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}}\exp\left(-\frac{1}{2}(\mathbf{x}_i-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}_i-\boldsymbol{\mu})\right)\right] \\
&= -\frac{ND}{2}\ln(2\pi) - \frac{N}{2}\ln|\boldsymbol{\Sigma}| - \frac{1}{2}\sum_{i=1}^N(\mathbf{x}_i-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}_i-\boldsymbol{\mu})
\end{align*} $$

This transformation:

- Converts products to sums
- Simplifies the exponential terms
- Makes derivatives more tractable

### Step 4: Mean Vector Optimization

Taking the derivative with respect to μ:

$$ \begin{align*}
\frac{\partial \ln L}{\partial \boldsymbol{\mu}} &= \frac{1}{2}\sum_{i=1}^N 2\boldsymbol{\Sigma}^{-1}(\mathbf{x}_i-\boldsymbol{\mu}) \\
&= \boldsymbol{\Sigma}^{-1}\sum_{i=1}^N(\mathbf{x}_i-\boldsymbol{\mu})
\end{align*} $$

Key points:

- The derivative of the quadratic form yields a linear term
- Σ⁻¹ is symmetric, simplifying the derivation

### Step 5: Mean Vector Solution

Setting the derivative to zero:

$$ \boldsymbol{\Sigma}^{-1}\sum\_{i=1}^N(\mathbf{x}\_i-\boldsymbol{\mu}) = \mathbf{0} $$

Since Σ is positive definite (hence invertible):

$$ \hat{\boldsymbol{\mu}}_{MLE} = \frac{1}{N}\sum_{i=1}^N \mathbf{x}\_i $$

This shows that the MLE of the mean is the sample average.

### Step 6: Covariance Matrix Optimization

The derivative with respect to Σ requires matrix calculus:

$$
\begin{align*}
\frac{\partial \ln L}{\partial \boldsymbol{\Sigma}} &= -\frac{N}{2}\boldsymbol{\Sigma}^{-1} + \frac{1}{2}\sum_{i=1}^N\boldsymbol{\Sigma}^{-1}(\mathbf{x}_i-\boldsymbol{\mu})(\mathbf{x}_i-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}
\end{align*}
$$

Important matrix calculus rules used:

- $\frac{\partial}{\partial \mathbf{A}} \ln|\mathbf{A}| = (\mathbf{A}^{-1})^T$
- $\frac{\partial}{\partial \mathbf{A}} \mathbf{x}^T\mathbf{A}^{-1}\mathbf{x} = -(\mathbf{A}^{-1}\mathbf{xx}^T\mathbf{A}^{-1})^T$

### Step 7: Covariance Matrix Solution

Setting the derivative to zero and solving:

$$ \hat{\boldsymbol{\Sigma}}_{MLE} = \frac{1}{N}\sum_{i=1}^N(\mathbf{x}\_i-\hat{\boldsymbol{\mu}})(\mathbf{x}\_i-\hat{\boldsymbol{\mu}})^T $$

This is the sample covariance matrix.

## Implementation and Practical Considerations

```python
import numpy as np

def multivariate_gaussian_mle(X: np.ndarray) -> tuple:
    """
    Compute MLE for multivariate Gaussian distribution

    Args:
        X: Data matrix of shape (N, D)
            N: number of samples
            D: dimension of each sample

    Returns:
        tuple: (mu_hat, sigma_hat)
            mu_hat: MLE of mean vector (D,)
            sigma_hat: MLE of covariance matrix (D, D)
    """
    # Sample size and dimension
    N, D = X.shape

    # Mean estimation
    mu_hat = np.mean(X, axis=0)

    # Covariance estimation
    centered_X = X - mu_hat
    sigma_hat = (centered_X.T @ centered_X) / N

    return mu_hat, sigma_hat
```

### Numerical Stability Considerations:

1. For high-dimensional data, compute the centered data matrix first
2. Use numerically stable algorithms for matrix operations
3. Check for positive definiteness of the estimated covariance matrix

This detailed derivation provides the mathematical foundation for understanding multivariate Gaussian parameter estimation, which is crucial in many machine learning applications.
