# 10 Unsupervised Learning :octocat:


Table of Contents
=================

* [Recap - Supervised vs. Unsupervised Learning](## Recap - Supervised vs. Unsupervised Learning)
* [Check List](## Check List)
* [Challenge of Unsupervised Learning](## Challenge of Unsupervised Learning)


## Recap - Supervised vs. Unsupervised Learning

|            |    Supervised Learning  | Unsupervised Learning  |
|  :--------: | :---------------------  | :----------------------------------  | 
| **DATA** |     a set of p features ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cfn_cs%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p), and a response *Y*, measured on n observations.  |  only a set of features ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cfn_cs%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p) measured on n observations.  |   
| **GOAL** |   to predict *Y* using ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cfn_cs%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)   |    to discover interesting things about the measurements
on ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cfn_cs%20X_1%2C%20X_2%2C%20.%20.%20.%20%2C%20X_p)  e.g. Is there an informative way to visualize the data? Canwe discover subgroups among the variables or among the observations?      |             


## Check List
In the Chapter 10 of *ISLR*, we focus on two particular types of unsupervised learning:   

- [x] principal components analysis  
> a tool used for **data visualization** or **data pre-processing** before applying supervised techniques

- [x] clustering
> a broad class of methods for **discovering unknown subgroups** in data.

## Challenge of Unsupervised Learning
