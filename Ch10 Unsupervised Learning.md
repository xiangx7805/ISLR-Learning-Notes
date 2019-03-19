# 10 Unsupervised Learning :octocat:


Table of Contents
------------------   
* <a href="#Recap"> Recap - Supervised vs. Unsupervised Learning</a>   
* <a href="#Check List"> Check List </a>  
* <a href="#Challenge"> Challenge of Unsupervised Learning</a>  
* <a href="#PCA"> Principal Components Analysis</a>

## <a id="Recap"/>Recap - Supervised vs. Unsupervised Learning

|            |    **Supervised Learning**  | **Unsupervised Learning**  |
|  :--------: | :---------------------------------- | :----------------------------------  |
| **DATA** |     a set of p features ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p), and a response *Y*, measured on n observations.  |  only a set of features ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p) measured on n observations.  |   
| **GOAL** |   to predict *Y* using ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)   |    to discover interesting things about the measurements on ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)  e.g. Is there an informative way to visualize the data? Canwe discover subgroups among the variables or among the observations?      |             


## <a id="Check List"/>Check List
In the Chapter 10 of *ISLR*, we focus on two particular types of unsupervised learning:   

- [x] **principal components analysis**    
> a tool used for **data visualization** or **data pre-processing** before applying supervised techniques

- [x] **clustering**  
> a broad class of methods for **discovering unknown subgroups** in data.

## <a id="Challenge"/>Challenge of Unsupervised Learning

1. **There is no simple goal**, like response prediction. More often performed as part of an **exploratory data analysis**.   
2. **Hard to assess the results**. Since there is no universally accepted mechanism for performing cross-validation or validating results on an independent data set -- No way to check.

:hear_no_evil:However, it's often easier to obtain *unlabeled data* than *labeled data*(which usually require human intervention).

## <a id="PCA"/>Principal Components Analysis :octopus:

PCA
*  produce a low-dimensional representation of a dataset. it finds a sequence of ① **linear combinations** of the variable that have ② **maximum variance**, and are mutually ③ **uncorrelated**.  
*  apart from producing derived variables for use in supervised learning  problems, PCA also serves as a tool for data visualization.

### Why CPA?
When p is large, impossible to look at ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Cbegin%7Bpmatrix%7D%20p%5C%5C%202%20%5Cend%7Bpmatrix%7D) = *p(p-1)/2* two-dimensional scatterplots. So we need to ﬁnd a low-dimensional representation of the data that captures as much of the information as possible.

PCA seeks a small number of dimensions that are as interesting as possible, where the concept of **interesting** is measured by the **amount that the observations vary along each dimension**. Each of the dimensions found by PCA is **a linear combination of the p features**.

Then, how to find these dimensions?

### How? - Math details

* The ﬁrst principal component of a set of features ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p) is the normalized linear combination of the features: ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20Z1%20%3D%20%5Cphi%20_%7B11%7DX_1%20&plus;%20%5Cphi%20_%7B21%7DX_2%20&plus;%20...%20&plus;%20%5Cphi%20_%7Bp1%7DX_p)  
that has the largest variance. By normalized, we mean that  ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%20_%7Bj1%7D%5E2%20%3D1).

*  the elements ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Cphi%20_%7B11%7D%2C%20...%20%2C%20%5Cphi%20_%7Bp1%7D) : **the loadings of ﬁrst principal component**, the loadings make up the **principal component loading vector** : ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Cphi%20_1%20%3D%28%5Cphi%20_%7B11%7D%2C%20%5Cphi%20_%7B21%7D%2C%20...%20%2C%20%5Cphi%20_%7Bp1%7D%29%5ET).

*  We constrain the loadings so that their sum of squares is equal to one, since otherwise setting these elements to be arbitrarily large in absolute value could result in an arbitrarily large variance.
