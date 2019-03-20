# 10 Unsupervised Learning :octocat:


Table of Contents
------------------   
* <a href="#Recap"> Recap - Supervised vs. Unsupervised Learning</a>   
* <a href="#Check List"> Check List </a>  
* <a href="#Challenge"> Challenge of Unsupervised Learning</a>  
* <a href="#PCA"> Principal Components Analysis</a>
  * <a href="#Lab1"> Lab 1: Principal Components Analysis</a>
* <a href="#Clustering"> Clustering Methods</a>  
  * <a href="#K-Means"> K-Means Clustering</a>
    * <a href="#Lab2"/> Lab 2: K-Means Clustering
  * <a href="#Hierarchical"> Hierarchical Clustering</a>  
  * <a href="#Practical"> Practical Issues in Clustering</a>
* <a href="#Labcase"/> Lab Case: NCI60 Data Example</a>
  * <a href="#LabcasePCA"/> PCA on the NCI60 Data</a>
  * <a href="#LabcaseCluster"/> Clustering the Observations of the NCI60 Data</a>



## <a id="Recap"/>Recap - Supervised vs. Unsupervised Learning

|            |    **Supervised Learning**  | **Unsupervised Learning**  |
|  :--------: | :---------------------------------- | :----------------------------------  |
| **DATA** |     a set of p features ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p), and a response *Y*, measured on n observations.  |  only a set of features ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p) measured on n observations.  |   
| **GOAL** |   to predict *Y* using ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)   |    to discover interesting things about the measurements on ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)  e.g. Is there an informative way to visualize the data? Can we discover subgroups among the variables or among the observations?      |             
| **EVALUATION**  | More clearly deﬁned and more objectively |   |


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

*  We constrain the loadings so that their sum of squares is equal to one, aka ![equation](https://latex.codecogs.com/svg.latex?%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%20%5E2_%7Bj1%7D%3D1), since otherwise setting these elements to be arbitrarily large in absolute value could result in an arbitrarily large variance.

:dizzy: Now we have a *n* x *p* dataset, how do we compute the **First principal component**?

> **Note:** we only care about **variance**.

Thus we assume that each of the variables in X has been centered to have mean zero (that is, the column means of X are zero). We then look for the linear combination of the sample feature values of the form  
![equation](https://latex.codecogs.com/svg.latex?z_%7Bi1%7D%3D%5Cphi%20_%7B11%7Dx_%7Bi1%7D%20&plus;%5Cphi%20_%7B21%7Dx_%7Bi2%7D%20&plus;%20...%20&plus;%5Cphi%20_%7Bp1%7Dx_%7Bip%7D) has largest sample variance, under constraint that ![equation](https://latex.codecogs.com/svg.latex?%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%20%5E2_%7Bj1%7D%3D1).

In other words, the ﬁrst principal component loading vector solves the optimization problem  
![equation](https://latex.codecogs.com/svg.latex?%5Cunderset%7B%20%5Cphi_%7B11%7D%2C...%2C%5Cphi_%7Bp1%7D%20%7D%7Bmaximize%7D%20%5Cleft%20%5C%7B%20%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20%5Cleft%20%28%20%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi_%7Bj1%7Dx_%7Bij%7D%20%5Cright%20%29%20%5E2%5Cright%20%5C%7D%20%2C%20%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%5E2_%7Bj1%7D%20%3D1%20),  
aka ![equation](https://latex.codecogs.com/svg.latex?%5Cunderset%7B%20%5Cphi_%7B11%7D%2C...%2C%5Cphi_%7Bp1%7D%20%7D%7Bmaximize%7D%20%5Cleft%20%5C%7B%20%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20z%5E2_%7Bi1%7D%20%5Cright%20%5C%7D.)

And since ![equation](https://latex.codecogs.com/svg.latex?%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20x_%7Bij%7D%20%3D%200) , ![equation](https://latex.codecogs.com/svg.latex?%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20z_%7Bi1%7D%20%3D%200) as well.

The maximize problem can be solved via an eigen decomposition.

* How to find second principal component after the frst one?  (*ISLR p376-377*)

* **Geometric interpretation for the ﬁrst principal component** :   
  *  The loading vector ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Cphi%20_1%20%3D%28%5Cphi%20_%7B11%7D%2C%20%5Cphi%20_%7B21%7D%2C%20...%20%2C%20%5Cphi%20_%7Bp1%7D%29%5ET) with elements ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfn_cm%20%5Csmall%20%5Cphi%20_%7B11%7D%2C%20...%20%2C%20%5Cphi%20_%7Bp1%7D) deﬁnes a direction in feature space along which the data vary the most.
  *  If we project the n data points ![equation](https://latex.codecogs.com/svg.latex?x_1%2C%20...%20%2C%20x_n) onto this direction, the projected values are the principal component scores ![equation](https://latex.codecogs.com/svg.latex?z_%7B11%7D%2C%20.%20.%20.%20%2C%20z_%7Bn1%7D) themselves.

#### Another Interpretation of Principal Components

*  Interpretaion :  we describe the principal component loading vectors as the directions in feature space along which the data vary the most, and the principal component scores as projections along these directions.

*   Alternatively, **principal components provide low-dimensional linear surfaces that are closest to the observations.**

The ﬁrst principal component loading vector has a very special property: **it is the line in p-dimensional space that is closest to the n observations** (using average squared Euclidean distance as a measure of closeness).  That means: we seek a single dimension of the data that lies as close as possible to all of the data points, since such a line will likely provide a good summary of the data.

Using this interpretation, together the ﬁrst M principal component score vectors and the ﬁrst M principal component loading vectors provide the best M-dimensional approximation (in terms of Euclidean distance) to
the *i* th observation ![equation](https://latex.codecogs.com/svg.latex?x_%7Bij%7D) . This representation can be written ![equation](https://latex.codecogs.com/svg.latex?x_%7Bij%7D%20%5Capprox%20%5Csum_%7BM%7D%5E%7Bm%3D1%7D%20z_%7Bim%7D%20%5Cphi%20_%7Bjm%7D) (assuming the original data matrix X is column-centered). In other words, together the M principal component score vectors and M principal component loading vectors can give a good approximation to the data when M is suﬃciently large. When M = *min(n − 1, p)* , then the representation
is exact: ![equation](https://latex.codecogs.com/svg.latex?x_%7Bij%7D%20%3D%20%5Csum_%7BM%7D%5E%7Bm%3D1%7D%20z_%7Bim%7D%20%5Cphi%20_%7Bjm%7D)

#### More on CPA
1. **Scaling the variables**. The variables should be centered to have mean zero. Furthermore, the results obtained when we perform PCA will also depend on whether the variables have been individually scaled (each multiplied by a diﬀerent constant).

2. **Uniqueness of the Principal Components**. Each principal component loading vector is unique, up to a sign flip. Similarly, the score vectors are unique up to a sign flip, since the variance of Z is the same as the variance of −Z.

3. **The Proportion of Variance Explained (PVE)**.   
The total variance present in a data set (assuming that the variables have been centered to have mean zero) is deﬁned as ![equation](https://latex.codecogs.com/svg.latex?%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20Var%28X_j%29%20%3D%20%5Csum_%7Bj%3D1%7D%5Ep%20%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%20x_%7Bij%7D%5E2)

and the variance explained by the *mth* principal component is ![equation](https://latex.codecogs.com/svg.latex?%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20z_%7Bim%7D%5E2%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%5Cleft%20%28%20%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%20_%7Bjm%7Dx_%7Bij%7D%20%5Cright%20%29%5E2)

Therefore, the PVE of the *mth* principal component is given by ![equation](https://latex.codecogs.com/svg.latex?%5Cfrac%7B%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%5Cleft%20%28%20%5Csum_%7Bp%7D%5E%7Bj%3D1%7D%20%5Cphi%20_%7Bjm%7Dx_%7Bij%7D%20%5Cright%20%29%5E2%7D%7B%20%5Csum_%7Bj%3D1%7D%5Ep%20%5Csum_%7Bi%3D1%7D%5En%20x_%7Bij%7D%5E2%7D)

In total, there are min(n − 1, p) principal components, and their PVEs sum to one.

4.  **Deciding How Many Principal Components to Use**.  
We typically decide on the number of principal components required to visualize the data by examining a **scree plot** -- looking for an **elbow** in the scree plot.

5.  **Other Uses for Principal Components**.
We perform regression, classiﬁcation, and clustering using the principal component score vectors as features -- lead to *less noisy* results.


### <a id="Lab1"/> Lab 1: Principal Components Analysis



## <a id="Clustering"/> Clustering Methods

* Different Mechanisms between PCA & Clustering:
  *  PCA looks to ﬁnd a low-dimensional representation of the observations that explain a good fraction of the variance.  
  *  Clustering looks to ﬁnd homogeneous subgroups among the observations.

### <a id="K-Means"/> K-Means Clustering

*  Minimizing the within-cluster variation, using squared Euclidean distance.  
![equation](https://latex.codecogs.com/svg.latex?%5Cunderset%7Bminimize%7D%7BC_1%2C...C_k%7D%20%5Cleft%20%5C%7B%20%5Csum_%7BK%7D%5E%7Bk%3D1%7D%20%5Cfrac%7B1%7D%7B%5Cleft%20%7C%20C_k%20%5Cright%20%7C%7D%20%5Csum%20_%7Bi%2Ci%27%5Cin%20C_k%7D%20%5Csum_%7Bj%3D1%7D%5E%7Bp%7D%20%28x_%7Bij%7D-x_%7Bi%27j%7D%29%5E2%20%5Cright%20%5C%7D), |Ck| denotes the number of observations in the kth cluster.

----------  
*  **Algorithm of K-Means Clustering**
-----------  
1. Randomly assign a number, from 1 to K, to each of the observations. These serve as initial cluster assignments for the observations.
2. Iterate until the cluster assignments stop changing:
   (a)   For each of the K clusters, compute the cluster centroid. Thekth cluster centroid is the vector of the p feature means for the observations in the kth cluster.
   (b)   Assign each observation to the cluster whose centroid is closest (where closest is deﬁned using Euclidean distance).
--------------

#### <a id="Lab2"/> Lab 2: K-Means Clustering

### <a id="Hierarchical"/> Hierarchical Clustering


### <a id="Practical"/> Practical Issues in Clustering



## <a id="Labcase"/> Lab Case: NCI60 Data Example

#### <a id="LabcasePCA"/> PCA on the NCI60 Data

#### <a id="LabcaseCluster"/> Clustering the Observations of the NCI60 Data
