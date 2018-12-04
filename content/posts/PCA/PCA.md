---
title: "Principal Components Analysis - PCA Part 2/3"
date: 2017-03-11T19:59:42+05:30
---

## What is PCA?

In simple words, PCA is a technique used to *condense* a large number of features into a smaller set of features that can *almost* represent the original set.

## Why PCA?

> PCA is used for dimensionality reduction.

As the number of features increase in a dataset, the amount of data needed to draw meaningful insights increases exponentially.

This is called *"Curse of dimensionality"*. [Here is a video](https://www.youtube.com/watch?v=QZ0DtNFdDko) that explains this in simple terms.

PCA is a technique used to reduce diemnsions (or number of features).

## How is it done?

For the sake of simplicity, consider a set of two features X = { X<sub>1</sub>, X<sub>2</sub> }

We are trying to find a line Z onto which we can project the points in the plane formed by { X<sub>1</sub>, X<sub>2</sub> }

Below is a reasonable visual representation of the idea

<img class="special-img-class" style="max-width:400px; max-height:450px" src="https://liorpachter.files.wordpress.com/2014/05/pca_figure1.jpg?w=490&h=490" />

The line Z is the the 1D representation of the 2D dataset.

## What are principal components?

Similar to the line Z, there are other such lines, orthogonal to each other onto which points in the space can be projected.

Each of these lines capture the spatial information with varying degrees of accuracy. 

In the image below we want to pick e to maximize variability. i.e., the <span style="color:#5f5fff"> **purple** </span> line captures the variability among points better than the <span style="color:green"> **green** </span> line 

<a href='http://www.inf.ed.ac.uk/teaching/courses/iaml/slides/dim-2x2.pdf'><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/PCA1.png" /></a>

We want to do this, so that we reduce cases where points that are far apart in the original space are very close together on the projection.

The set of orthogonal lines that capture most amount of variability in the dataset are known as **principal components**.

## Calculating principal components

> Principal components are the eigen vectors of the covariance matrix of the dataset with the largest eigen values.

> The eigenvector with the largest eigenvalue is the direction along which the data set has the maximum variance

Refer to my previous post on [covariance, eigen vectors and pca]({{< ref "covariance_eigen_pca.md" >}}) for some background.

The technique of finding principal components is called ["Singular Value Decomposition (SVD)"](https://stats.stackexchange.com/questions/134282/relationship-between-svd-and-pca-how-to-use-svd-to-perform-pca)

However, we need not get into the details of SVD here, since for a symmetric matrix (which a covariance matrix is), **singular values are just the absolute values of the eigenvalues of eigenvectors of a covariance matrix.**

## Steps involved in PCA

1. Given a dataset, compute it's covariance matrix
2. Find the eigenvalues and eigenvectors for the covariance matrix
3. Sort the eigenvectors in descending order of their eigenvalues
4. Pick **K** eigenvectors from the sorted list (this set represents the maximum variance in data)

### Choosing **K** (the right number of eigen vectors)

Given a set of eigenvalues &lambda;<sub>1</sub>, &lambda;<sub>2</sub>, &lambda;<sub>3</sub> ... &lambda;<sub>n</sub> in descending order of magnitude, pick &lambda;<sub>1</sub>, &lambda;<sub>2</sub>, &lambda;<sub>3</sub> ... &lambda;<sub><b>K</b></sub> that ["explain the most variance"](https://ro-che.info/articles/2017-12-11-pca-explained-variance)

Pick **K** eigenvectors that explain 90% or more of the total variance, using the following equation

<a href='http://www.inf.ed.ac.uk/teaching/courses/iaml/slides/dim-2x2.pdf'><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/explained_variance_pca.png" /></a>

Typical threshold values are 0.9 or 0.95. 
We could set a explained variance threshold as high as 0.99 if we want to capture the original data with higher accuracy in the compressed representation.

## Reconstructing data from PCA:

Let **X<sub>raw</sub>** be the *n×p* data matrix with *n* rows (data points) and *p* columns (variables, or features). After subtracting the mean vector *μ* from each row, we get the centered data matrix **X**. 

Let **V** be the *p×k* matrix of some **K** eigenvectors that we want to use; these would most often be the **K** eigenvectors with the largest eigenvalues. Then the *n×k* matrix of PCA projections ("scores"
will be simply given by **Z=XV**.

The reconstruction of the original data from Z is given by

X̂raw = ZVT + μ

## Advice for applying PCA

1. **Perform feature scaling** if the range of values for different features vary greatly. 
Larger numbers are likely to have higher variance which can overwhelm the algorithm since we use PCs from the data's covariance matrix.

2. **Don't include PCA as a default step** in an ML system design. Only apply PCA if the training doesn't work well with the original large feature set.

3. **PCA is a good way to reduce memory requirements** and to speed up a learning algorithm

4. **PCA is not a good solution for overfitting**. Instead of reducing the number of features using PCA, use regularization.