---
title: 'Multivariate Analysis: Assignment 2'
author: "Michael Gant"
date: "03 April 2018"
output: pdf_document
---





#Principle Component Analysis
##Underlying Method
Principle Component Analysis (PCA) is a non-parametric method of extracting relevant information from a data set. This is accomplished through decomposing the variance-covariance structure and redundancy reduction. 
\
\
Decomposing the variance-covariance structure is done via linear combinations of the observed data$\boldsymbol{X}$, which essentially form a new, more meaningful basis on which to re-express the data. The new basis can be represented by a simple linear equation:
\[
  \boldsymbol{P}\boldsymbol{X} = \boldsymbol{Y} 
\]
where $\boldsymbol{X}$ is the observed data, $\boldsymbol{P}$ is the linear transformation matrix and $\boldsymbol{Y}$ is the new representation of the data. This equation gives a simple overview of what PCA does. The question now what linear combination to choose.
\
\
The derivation of PCA is based on finding coefficients that maximise $\boldsymbol{a}' \Sigma \boldsymbol{a}$ subject to $\boldsymbol{a}'\boldsymbol{a}=1$ where $\Sigma$ is the covariance matrix of $\boldsymbol{X}$. The coefficients $\boldsymbol{a}_i$ define the linear combinations to obtain $\boldsymbol{Y}$ as follows:
\begin{align*}
Y_1  = \boldsymbol{a}'_1 \boldsymbol{X} \\
Y_2  = \boldsymbol{a}'_2 \boldsymbol{X} \\
\vdots \\
Y_p  = \boldsymbol{a}'_p \boldsymbol{X}
\end{align*}
where $\text{Var}(Y_i) = \boldsymbol{a}_i' \Sigma \boldsymbol{a}_i$ and $\text{Cov}(Y_i, Y_k) = \boldsymbol{a}_i' \Sigma \boldsymbol{a}_k$ for $i,k = 1,..,p$\
\
It can be shown that the coefficient vectors, $\boldsymbol{a}_i$, are the eigenvectors of the covariance matrix of $\boldsymbol{X}$. The associated eigenvalues,$\lambda_i$, show how much of the total variance is decomposed by the corresponding eigenvector with large eigenvalues explaining more variance than smaller ones. 
\
\
Thus we can find $\boldsymbol{Y}$ as the matrix of row vector principle components using the eigenvectors above. As eigenvectors are not correlated, the covariance matrix of $\boldsymbol{Y}$ is a diagonal matrix. Thus it can be shown that $\sum_{i=1}^{p}\text{Var}(\boldsymbol{X}_i) = \lambda_1 + \lambda_2 +...+ \lambda_p = \sum_{i=1}^{p}\text{Var}(\boldsymbol{Y}_i)$ and we can calculate the total proportion of variance due to the j'th principle component as:
\[
\frac{\lambda_j}{\lambda_1 + \lambda_2 +...+ \lambda_p}
\]

##Application to National Track Records

The objective of applying PCA to the given National Track Record data is to determine the linear combinations of variables that explain the majority of the variance. The times for 100m, 200m, 400m, 800m, 1500m, 3000m for females from 55 countries were analysed first. The data was scaled and then PCA was applied. The first 2 principle components are tabulated below with their respective proportion:



|    |   m100|   m200|   m400|   m800|  m1500|  m3000| Marathon| Eigenvalue| Proportion of Variance|
|:---|------:|------:|------:|------:|------:|------:|--------:|----------:|----------------------:|
|PC1 | -0.378| -0.383| -0.368| -0.395| -0.389| -0.376|   -0.355|   5.808100|                   0.83|
|PC2 |  0.407|  0.414|  0.459| -0.161| -0.309| -0.423|   -0.389|   0.628849|                   0.09|



The first principle component combines the variables in roughly equal proportions, basically a weighted average but with negative weights. This can be interpreted an overall score of the athletic ability. The second principle component has positive coefficients for the shorter distance events and negative coefficients for the longer distance events. This can be interpreted as the principle component measuring the difference between the short and long distance events. The proportion of variance explained by the first principle component is 83% and the second is 9%. Together, the first 2 principle components explain the majority of the observed variance. \
\
Multiplying the data matrix $\boldsymbol{X}$ by the eigenvector related to the first principle component gives us an overall athletic score for each athlete. The rankings of the athletes and their respective countries are summarised below:



|PC1   |Country       |
|:-----|:-------------|
|3.299 |U.S.A.        |
|3.048 |Germany       |
|3.043 |Russia        |
|2.989 |China         |
|2.518 |France        |
|2.443 |GreatBritain  |
|2.406 |CzechRepublic |
|2.274 |Poland        |
|2.123 |Romania       |
|1.932 |Australia     |



From the rankings it can be seen that the athlete from U.S.A. has the highest score and the Samoan athlete has the lowest score.
\
\
The data is now transformed from the athletes time of the events to the athletes speed in the event measured in meters per second. The prior PCA methods are applied again on the converted data and the following summaries are obtained:



|    |   m100|   m200|   m400|  m800| m1500| m3000| Marathon| Eigenvalue| Proportion of Variance|
|:---|------:|------:|------:|-----:|-----:|-----:|--------:|----------:|----------------------:|
|PC1 |  0.374|  0.381|  0.367| 0.393| 0.390| 0.381|    0.359|   5.832225|                  0.833|
|PC2 | -0.425| -0.417| -0.438| 0.152| 0.282| 0.397|    0.440|   0.648025|                  0.093|



The first 2 principle components can be interpreted the same as before but the proportion of variance explained is slightly higher at 83.3% and 9.3% for the first 2 principle components respectively. The analysis done when the records are converted to meters per second is preferred over the record times as the speed combines the information from the time taken for the event and the distance of the event. \
\
The rankings of the athletes on first principle component have changed slightly and the first 10 are shown below:



|PC1   |Country       |
|:-----|:-------------|
|3.598 |U.S.A.        |
|3.318 |Russia        |
|3.316 |China         |
|3.304 |Germany       |
|2.681 |GreatBritain  |
|2.639 |France        |
|2.533 |CzechRepublic |
|2.395 |Poland        |
|2.3   |Romania       |
|2.019 |Australia     |



Plotting a scree plot below shows that the first 2 principle components are the most important when using the visual elbow rule.\

![plot of chunk plo1](figure/plo1-1.png)
Moving on to the PCA of the male records, the data is slightly different as there are 2 events which males compete in that women don't and 1 event that females compete in that males don't. The following 2 tables show the first 2 principle components for the male events with time records and speed respectively:



|    |   m100|   m200|   m400|   m800|  m1500| Marathon|  m5000| m10000| Eigenvalue| Proportion of Variance|
|:---|------:|------:|------:|------:|------:|--------:|------:|------:|----------:|----------------------:|
|PC1 | -0.332| -0.346| -0.339| -0.353| -0.366|   -0.354| -0.370| -0.366|   6.702921|                  0.838|
|PC2 | -0.529| -0.470| -0.345|  0.089|  0.154|    0.387|  0.295|  0.334|   0.638401|                  0.080|





|    |  m100|  m200|  m400|   m800|  m1500| Marathon|  m5000| m10000| Eigenvalue| Proportion of Variance|
|:---|-----:|-----:|-----:|------:|------:|--------:|------:|------:|----------:|----------------------:|
|PC1 | 0.332| 0.345| 0.337|  0.354|  0.368|    0.354|  0.371|  0.366|   6.625476|                  0.828|
|PC2 | 0.522| 0.471| 0.361| -0.093| -0.161|   -0.380| -0.294| -0.333|   0.677329|                  0.085|



The interpretation of the first 2 principle components is exactly the same as for the female athletes. For the males, the first principle component is a weighted average of the times or speeds for the athletes various events. The first principle component explains the majority of the variance in both case and the second principle component represents a much smaller proportion of the variance. The second principle component compares the difference between the short and long distance events. 
\
\
As with the female athletes, the rankings of the male athletes scored by the first principle components for the records in time and speed respectively are summarised in the table below:



|PC1   |Country      |
|:-----|:------------|
|3.828 |U.S.A.       |
|2.915 |GreatBritain |
|2.608 |Kenya        |
|2.402 |France       |
|2.353 |Australia    |
|2.244 |Italy        |
|2.208 |Brazil       |
|2.138 |Germany      |
|2.074 |Portugal     |
|2.008 |Canada       |





|PC1   |Country      |
|:-----|:------------|
|4.125 |U.S.A.       |
|3.085 |GreatBritain |
|2.878 |Kenya        |
|2.536 |France       |
|2.464 |Australia    |
|2.345 |Italy        |
|2.281 |Brazil       |
|2.239 |Germany      |
|2.185 |Portugal     |
|2.098 |Belgium      |



The rankings change slightly as before but the top 5 remain the same.\
\
Comparisons between the principle component analysis results from the female data to the male data should be approached with caution due to the set of different events that each gender competed in. The values of the coefficients and eigenvalues cannot be compared due to the scaling and centering of the data. However, the proportion of variances can be compared and it can be seen that the proportion of variance explained is very similar across genders. 




#Factor Analysis
##Underlying Method

The primary motication for Factor Analysis is to describe the covariance relationships among the latent (unobservable) variables. These latent variables are measurements that cannot be directly obsevered due to their nature, such as happiness or standard of living. Proxies can be used to estimate their values but it is not possible to get a true measure. These latent variables are called factors. The asssumption is made that if there are variables that are highly correlated, they act as proxies and represent the underlying factor. The factor analysis model is mathematically represented as:

\begin{equation}
  \boldsymbol{X}-\boldsymbol{\mu} = \boldsymbol{L}\boldsymbol{F} + \boldsymbol{e}
\end{equation}
where $\boldsymbol{X}$ is our observed data, $\boldsymbol{\mu}$ is the mean vector of the data, $\boldsymbol{L}$ is the matrix of factor loadings, $\boldsymbol{F}$ is the vector of unobserved common factors and $\boldsymbol{e}$ is the vector of unobserved specific factors. The elements of the factor loading matrix, $l_{ij}$ represent the estimate of the association between the i'th observed variable and the j'th unobserved factor.\
\
The factor analysis model is similar to a multiple regression model, but the "explanatory variables" are the unobserved factors, $f_1, f_2, ...,f_m$ where $m$ is less than the number of variables $p$. Thus the factor analysis model represents the data in a lower dimension.\
\
Under the factor analysis model, covariance matrix of the data, $\boldsymbol{\Sigma}$, can be expressed as:
\[
\boldsymbol{\Sigma} = \boldsymbol{L}\boldsymbol{L}' + \boldsymbol{\Psi}
\]
where $\boldsymbol{\Psi}$ is the diagonal covariance matrix of $\boldsymbol{e}$. The right-hand side is a simplified representation of $\boldsymbol{\Sigma}$ depending on the chosen number of factors ,$m$. Ideally the number of estimated values $mp + p$ is substantially smaller than the number of unique $\boldsymbol{\Sigma}$ estimates, $p(p+1)/2$, without being too small so as not to be able to adequately represent $\boldsymbol{\Sigma}$.\
\
Before going into estimation of the parameters, the rotational ambiguity of factor analysis needs to be addressed. When the number of factors is greater than 1, it can be shown that there are an inifinte number of orthogonal matrices that satisfy the required assumptions and equivalently fit the data. This ambigutiy is exploited to justify the factor rotation in order to obtain a more parsimonous model.   
\
\
There are 2 different ways to estimate the parameters of a factor model, namely:
\begin{itemize}
\item Principle Component method
\item Maximum Likelihood Estimation method
\end{itemize}

The Principle Component method calculates the sample covariance matrix, $\boldsymbol{S}$, and then, using spectral decompostion, the factor loading matrix is estimated by the eigenvalue-eigenvector pairs of $\boldsymbol{S}$. The estimate of the specific variance matrix, $\boldsymbol{\Psi}$, is given by the diagonal elements of $\boldsymbol{S} - \boldsymbol{\tilde{L}}\boldsymbol{\tilde{L}}'$. \
\
If the variables are standardized, the sample correlation matrix used is $\boldsymbol{R}$. The choice of $m$ is the number of positive eigenvalues of $\boldsymbol{S}$ or the number of eigenvalues of $\boldsymbol{R}$ greater than 1. \
\
The Maximum Likelihood Estimation method makes a normal distribution assumption about the common factors, $\boldsymbol{F}$ , and the specific factors, $\boldsymbol{e}$. Thus maximum likelihood estimates for the factor loadings and the specific variances can be obtained thorugh numerical maximization.\
\
The ambgiuity of rotation was discussed earlier and is brought up again. As factor models are equivalent to a rotated factor model, an appropriate rotation may be found that results in more interpretable factors. The Varimax rotation is one such appropriate rotation that maximises the variances of the squares of the factor loadings. Another rotation is the promax method of oblique rotations, which is used when factors are not independent from one another.\
\
Once a satisfactory factor model has been created and rotated, the factor scores can be estimated. Factor scores are the estimated values of the common factors and are simialar to principal components. There are 2 methods of esitmation that are considered, namely, weighted least squares and regresssion.  

##Application 
As with PCA in the previous section, the National Track Record data is analysed using factor models. Firstly the female athletes are considered. Due to the consideration of only the first 2 principle components from the PCA section, the factor analysis will only assume 2 underlying factors. The maximum likelihood method is used to estimate the loading matrix and is tabulated below:



|         |      m100|      m200|      m400|       m800|      m1500|
|:--------|---------:|---------:|---------:|----------:|----------:|
|Factor 1 | 0.8759975| 0.8984409| 0.8262161|  0.9251484|  0.9742924|
|Factor 2 | 0.3719032| 0.4106494| 0.4064980| -0.0054296| -0.1856409|





|         |      m100|      m200|     m400|       m800|      m1500|      m3000|   Marathon| Proportion of Variance|
|:--------|---------:|---------:|--------:|----------:|----------:|----------:|----------:|----------------------:|
|Factor 1 | 0.8804116| 0.9109752| 0.844602|  0.9207781|  0.9657499|  0.9443679|  0.8336690|                  0.812|
|Factor 2 | 0.3471652| 0.3911207| 0.349982| -0.0440971| -0.1951144| -0.3038984| -0.2048342|                  0.081|



The loadings of factor 1 in both case are all very close to 1, indicating a strong influence on the variables. For the second factor, the majority of the loadings are significant except the loadings for the 800m in both cases and marathon events of the time record data. 

The loadings are now rotated to obtain better interpretations 

