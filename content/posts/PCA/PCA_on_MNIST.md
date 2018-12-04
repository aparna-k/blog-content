---
title: "PCA on MNIST using SKLearn - PCA Part 3/3"
date: 2017-03-12T17:32:42+05:30
---

To understand basics of PCA, refer to my previous post [here]({{< ref "PCA.md" >}})

### Quick note regarding MNIST dataset:

Ref: https://en.wikipedia.org/wiki/MNIST_database#Dataset

The MNIST dataset is a large database of handwritten digits that are commonly used for training and testing ML models.

The **MNIST dataset in sklearn** conatains 1797 digits. Each digit is represented by an array of 64 values that represent a 8x8 pixel image. Each pixel value ranges from 0-16.

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns; sns.set()
from sklearn.decomposition import PCA
from sklearn.datasets import load_digits
digits = load_digits() # The MNIST digits
digits.data[0, :] # Each row is an 8x8 image
```




    array([ 0.,  0.,  5., 13.,  9.,  1.,  0.,  0.,  0.,  0., 13., 15., 10.,
           15.,  5.,  0.,  0.,  3., 15.,  2.,  0., 11.,  8.,  0.,  0.,  4.,
           12.,  0.,  0.,  8.,  8.,  0.,  0.,  5.,  8.,  0.,  0.,  9.,  8.,
            0.,  0.,  4., 11.,  0.,  1., 12.,  7.,  0.,  0.,  2., 14.,  5.,
           10., 12.,  0.,  0.,  0.,  0.,  6., 13., 10.,  0.,  0.,  0.])




```python
plt.gray() 
plt.matshow(digits.images[0]) # the digits come conveniently packaged as a matrix So we can quickly visualize this
plt.show()
```


    <matplotlib.figure.Figure at 0x10cd16c90>



![png](/img/pca/output_5_1.png)



```python
pca = PCA() # Initialize PCA
```


```python
pca.fit(digits.data) # Fit the model with digits.data
```




    PCA(copy=True, iterated_power='auto', n_components=None, random_state=None,
      svd_solver='auto', tol=0.0, whiten=False)




```python
print(digits.data.shape)
```

    (1797, 64)



```python
pca.explained_variance_ratio_.shape # These are the eigen values of the 
                                    # eigen vectors of the covariance matrix of the digits data
```




    (64,)




```python
pca.explained_variance_ratio_ # This is a convenient calculation, which is basically 
                                # each eigen value divided by the total sum of eigen values
                                # The eigen values come sorted in decreasing order of magnitude
                                # Remember, larger the eigen value, more variance it captures
```




    array([1.48905936e-01, 1.36187712e-01, 1.17945938e-01, 8.40997942e-02,
           5.78241466e-02, 4.91691032e-02, 4.31598701e-02, 3.66137258e-02,
           3.35324810e-02, 3.07880621e-02, 2.37234084e-02, 2.27269657e-02,
           1.82186331e-02, 1.77385494e-02, 1.46710109e-02, 1.40971560e-02,
           1.31858920e-02, 1.24813782e-02, 1.01771796e-02, 9.05617439e-03,
           8.89538461e-03, 7.97123157e-03, 7.67493255e-03, 7.22903569e-03,
           6.95888851e-03, 5.96081458e-03, 5.75614688e-03, 5.15157582e-03,
           4.89539777e-03, 4.28887968e-03, 3.73606048e-03, 3.53274223e-03,
           3.36683986e-03, 3.28029851e-03, 3.08320884e-03, 2.93778629e-03,
           2.56588609e-03, 2.27742397e-03, 2.22277922e-03, 2.11430393e-03,
           1.89909062e-03, 1.58652907e-03, 1.51159934e-03, 1.40578764e-03,
           1.16622290e-03, 1.07492521e-03, 9.64053065e-04, 7.74630271e-04,
           5.57211553e-04, 4.04330693e-04, 2.09916327e-04, 8.24797098e-05,
           5.25149980e-05, 5.05243719e-05, 3.29961363e-05, 1.24365445e-05,
           7.04827911e-06, 3.01432139e-06, 1.06230800e-06, 5.50074587e-07,
           3.42905702e-07, 1.17368844e-33, 1.17368844e-33, 1.15577716e-33])




```python
cumulative_sum = pca.explained_variance_ratio_.cumsum() # We can easily do a cumulative sum on the explained_variance_ratio
```


```python
plt.plot(cumulative_sum) 
plt.show()
```


![png](/img/pca/output_12_0.png)



```python
cumulative_sum
```




    array([0.14890594, 0.28509365, 0.40303959, 0.48713938, 0.54496353,
           0.59413263, 0.6372925 , 0.67390623, 0.70743871, 0.73822677,
           0.76195018, 0.78467714, 0.80289578, 0.82063433, 0.83530534,
           0.84940249, 0.86258838, 0.87506976, 0.88524694, 0.89430312,
           0.9031985 , 0.91116973, 0.91884467, 0.9260737 , 0.93303259,
           0.9389934 , 0.94474955, 0.94990113, 0.95479652, 0.9590854 ,
           0.96282146, 0.96635421, 0.96972105, 0.97300135, 0.97608455,
           0.97902234, 0.98158823, 0.98386565, 0.98608843, 0.98820273,
           0.99010182, 0.99168835, 0.99319995, 0.99460574, 0.99577196,
           0.99684689, 0.99781094, 0.99858557, 0.99914278, 0.99954711,
           0.99975703, 0.99983951, 0.99989203, 0.99994255, 0.99997555,
           0.99998798, 0.99999503, 0.99999804, 0.99999911, 0.99999966,
           1.        , 1.        , 1.        , 1.        ])




```python
print("indices of cumulative sum of ratios greater than .99", np.nonzero(cumulative_sum >= 0.99))
```

    ('indices of cumulative sum of ratios greater than .99', (array([40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56,
           57, 58, 59, 60, 61, 62, 63]),))


clearly 40 is the minimum number of principal components we must pick to preserve at least 99% variance 


```python
pca_components = PCA(49)
projected = pca_components.fit_transform(digits.data)
```


```python
projected.shape
```




    (1797, 49)




```python
# Let's try Eigenfacing MNIST for fun!
first_projected_number = projected[0, :]
plt.gray() 
plt.matshow(np.reshape(first_projected_number, (7, 7))) 
plt.show()
```


    <matplotlib.figure.Figure at 0x10d022410>



![png](/img/pca/output_18_1.png)



```python
# Let's try to retreive back the original pixel information
inverse_transform = pca_components.inverse_transform(projected)
inverse_transform.shape
```




    (1797, 64)




```python
first_projected_number = inverse_transform[0, :]
plt.gray() 
plt.matshow(np.reshape(first_projected_number, (8, 8))) 
plt.show()
```


    <matplotlib.figure.Figure at 0x10f37d0d0>



![png](/img/pca/output_20_1.png)


Let's try to see how the reconstruction turns out if we reduce the amount of variance we retain, so say we pick K = 20, which is approximately 90% of the original variance


```python
cumulative_sum[19]
```




    0.8943031165985262




```python
pca_components = PCA(19)
projected = pca_components.fit_transform(digits.data)
inverse_transform = pca_components.inverse_transform(projected)
inverse_transform.shape
first_projected_number = inverse_transform[0, :]
plt.gray() 
plt.matshow(np.reshape(first_projected_number, (8, 8))) 
plt.show()
```


    <matplotlib.figure.Figure at 0x10cce6750>



![png](/img/pca/output_23_1.png)


That's actually not too bad for this particular use case. The amount of variance we retain is a subjective to our data. The thumb rule is 95% or 99% variance is a good call
