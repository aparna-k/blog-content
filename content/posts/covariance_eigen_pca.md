---
title: "Covariance, Eigen Vectors and Principal Components - PCA Part 1/3"
date: 2017-03-10T19:59:42+05:30
---

## Covariance matrix:

[Here is a really good reference](http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/) to build an intuition for covariance matrix

Also known as the variance-covariance matrix, holds information about how two random variables (in this case two features) vary with respect to one another

Covariance is a measure of how much two random variables vary together. It’s similar to variance, but where variance tells you how a single variable varies, co variance tells you how two variables vary together.

<a href="http://www.statisticshowto.com/covariance/"><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/covariance.png"/></a>

A covariance matrix summarizes the co-variances of a set of variables in a matrix

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/covariance_matrix_formula.png" /></a>

Where,

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/covariance_formula.png" /></a>

The operator **E** is the mean (expected value) of it's argument

<a href="https://en.wikipedia.org/wiki/Covariance_matrix"><img class="special-img-class" style="max-width:400px; max-height:450px" src="/img/pca/mean.png" /></a>

##### Shape of covariance matrix:

The following figure illustrates the shape of data and their corresponding covariance matrix

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" src="/img/pca/shape_of_covariance.png" /></a>

Understanding the shape:

*Top-Left*:

&sigma;(x, x) = 5 -> Variance of x w.r.t itself, i.e., variance of x <br>
&sigma;(x, y) = 4 -> Variance of x w.r.t y <br>
&sigma;(y, x) = 4 -> Variance of y w.r.t x <br>
&sigma;(y, y) = 6 -> Variance of y w.r.t itself, i.e., variance of y <br>

This implies that x, y have a positive covariance, i.e., x increases as y increases

*Top-Right*:

&sigma;(x, x) = 5 -> Variance of x w.r.t itself, i.e., variance of x <br>
&sigma;(x, y) = -4 -> Variance of x w.r.t y <br>
&sigma;(y, x) = -4 -> Variance of y w.r.t x <br>
&sigma;(y, y) = 6 -> Variance of y w.r.t itself, i.e., variance of y <br>

This implies that x, y have a negative covariance, i.e., x decreases as y increases and vice-versa

*Bottom-Left*:

&sigma;(x, x) = 5 -> Variance of x w.r.t itself, i.e., variance of x <br>
&sigma;(x, y) = 0 -> Variance of x w.r.t y <br>
&sigma;(y, x) = 0 -> Variance of y w.r.t x <br>
&sigma;(y, y) = 1 -> Variance of y w.r.t itself, i.e., variance of y <br>

This implies that x, y have a zero covariance, i.e., x and y have no relationship. Also the variance of x is much higher than y giving the shape that we see where the data is spread out maximally in the x direction

*Bottom-Right*:

&sigma;(x, x) = 1 -> Variance of x w.r.t itself, i.e., variance of x <br>
&sigma;(x, y) = 0 -> Variance of x w.r.t y <br>
&sigma;(y, x) = 0 -> Variance of y w.r.t x <br>
&sigma;(y, y) = 5 -> Variance of y w.r.t itself, i.e., variance of y <br>

This implies that x, y have a zero covariance, i.e., x and y have no relationship. Also the variance of y is much higher than x giving the shape that we see where the data is spread out maximally in the y direction

### Eigenvectors of Covariance matrix:

I highly recommend watching this [video](https://www.youtube.com/watch?v=PFDu9oVAE-g) to get an intuition about eigen vectors

Eigen vectors are special vectors for a given matrix, which when multiplied by the matrix do not change their [span](https://www.youtube.com/watch?v=k7RM-ot2NWY) but change their scale or magnitude

Eigenvalues is the scale by which an eigenvector changes when multiplied by a given matrix.

In other words, for an eigen vector of a matrix, multiplying the vector with the matrix is the same as multiplying the vector with a scalar. The scalar being the eigen value

This equation can be represented as:

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" src="/img/pca/eigen_vector_formula.png" /></a>

> **Property**: For a covariance matrix, the Eigenvector with the largest Eigenvalue points in the direction of maximal variance


Eigenvectors and eigenvalues for the covariance matrices described above

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" src="/img/pca/eigen_vectors_cov_matrix2.png" /></a>

<a href="http://www.visiondummy.com/2014/04/geometric-interpretation-covariance-matrix/"><img class="special-img-class" src="/img/pca/eigen_vectors_cov_matrix1.png" /></a>

> Given a set of eigen vectors for the covariance matrix, the principal components are the eigen vectors with the largets eigen values

