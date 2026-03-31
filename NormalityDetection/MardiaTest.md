# Normality Detection Proves
--- 

In this file we will see a brief explanation of two types of normality detection proves for multivariate analysis on statistics. Of course, we will have some videos, even short exercises about each prove. 

--- 
## Mardia Prove

This prove is caracterized because can be apply easily on R with the library MVN. Here the code for doing it: 

```{r}
# Download Library
if (!require(MVN)) install.packages("MVN")

# Load Library
library(MVN)

mvn(data, mvnTest = "mardia")
```

But now, theorycally, we can say that this prove have inside of it two proves: 

* Assymetric normal multivariate population coefficient prove 

* Curtosis normal multivariate population coefficient prove

For understanding this we got to define two statisticians fistable:

---

## Hypotheses
---

The test evaluates the following hypotheses:

$$
H_0 : \text{The data follow a multivariate normal distribution}
$$

$$
H_1 : \text{The data do not follow a multivariate normal distribution}
$$

Mardia's procedure is composed of two statistical tests:

- Multivariate skewness test  
- Multivariate kurtosis test

Both statistics are calculated using the Mahalanobis distance structure of the data, which considers the covariance relationships between variables.

--- 

## Data Matrix 


---

Suppose we have a data matrix:

$$
X =
\begin{bmatrix}
x_{11} & x_{12} & \dots & x_{1p} \\
x_{21} & x_{22} & \dots & x_{2p} \\
\vdots & \vdots & \dots & \vdots \\
x_{n1} & x_{n2} & \dots & x_{np}
\end{bmatrix}
$$

where:

- $n$ = number of observations  
- $p$ = number of variables  

Each row represents one multivariate observation.

---
## Centered Data Matrix 

---

The first step of the procedure is to center the data:

$$
X_c = \left(I_n - \frac{1}{n} J_n \right) X
$$

where:

- $I_n$ is the identity matrix  
- $J_n$ is a matrix of ones  

This operation subtracts the **sample mean vector** from each observation.

---

## Covariance Matrix 

--- 

The sample covariance matrix is defined as:

$$
S = \frac{1}{n} X_c^{T} X_c
$$


This matrix describes:

variances of each variable

covariances between variables

---

## Mahalanobis Structure Matrix 

--- 

Using the centered data and the covariance matrix we compute:

$$
M = X_c S^{-1} X_c^T
$$

The elements $m_{ij}$ of this matrix are used to compute the skewness and kurtosis coefficients.

The diagonal elements represent squared Mahalanobis distances.

--- 

## Multivariate Skewness 

--- 

The multivariate skewness coefficient is defined as:

$$
b_{1,p} =
\frac{1}{n^2}
\sum_{i=1}^{n}
\sum_{j=1}^{n}
m_{ij}^{3}
$$


This statistic measures the asymmetry of the multivariate distribution.

Under the null hypothesis of multivariate normality:

$$
\frac{n}{6} \, b_{1,p}
$$


follows approximately a chi–square distribution with

$$
\frac{p(p+1)(p+2)}{6}
$$


degrees of freedom.

---

## Multivariate Kurtosis

---

The multivariate kurtosis coefficient is defined as:

$$
b_{2,p} =
\frac{1}{n}
\sum_{i=1}^{n}
m_{ii}^{2}
$$


This statistic evaluates the tail behavior of the distribution.

For a multivariate normal distribution:

$$
E(b_{2,p}) = p(p+2)
$$

The standardized test statistic is:

$$
z =
\frac{b_{2,p} - p(p+2)}
{\sqrt{\frac{8p(p+2)}{n}}}
$$

which approximately follows a standard normal distribution.

---

## Decision Rule 

--- 

The null hypothesis of multivariate normality is evaluated using the p-values obtained from both tests.

If p-value > $\alpha$, the null hypothesis is not rejected.

If p-value ≤ $\alpha$, the null hypothesis is rejected.

To conclude that the dataset follows a multivariate normal distribution, both tests must be non-significant.

---
## Prove characteristics 
--- 

The Mardia test is a widely used method for assessing multivariate normality based on two key components: skewness and kurtosis. It evaluates whether the joint distribution of the data exhibits symmetry and tail behavior consistent with a multivariate normal distribution. One of its main strengths is that it provides separate measures for skewness and kurtosis, allowing the researcher to identify the specific type of deviation from normality. The test is asymptotic, meaning its accuracy improves with larger sample sizes, and it assumes that the covariance matrix is non-singular. However, it can be sensitive to outliers and may over-reject normality in the presence of small departures, especially in moderate to large samples. Despite these limitations, Mardia’s test remains a fundamental tool in multivariate analysis due to its interpretability and theoretical foundation.


## Interpretation
--- 

If the p-values of both the skewness and kurtosis tests are greater than the chosen significance level, there is no statistical evidence to reject multivariate normality.

Otherwise, the data cannot be considered multivariate normal.

---


## Example

Consider the following dataset with $n=4$ observations and $p=3$ variables.

### Data Matrix

$$
X=
\begin{bmatrix}
1 & 0 & -3 \\
5 & 3 & 1 \\
-2 & 4 & 1 \\
7 & 2 & 5
\end{bmatrix}
$$

---

### Centered Data Matrix

After subtracting the sample mean vector, we obtain

$$
X_c=
\begin{bmatrix}
-7/4 & -9/4 & -4 \\
9/4 & 3/4 & 0 \\
-19/4 & 7/4 & 0 \\
17/4 & -1/4 & 4
\end{bmatrix}
$$

---

### Mahalanobis Structure Matrix

Using the covariance matrix and the centered data,

$$
M=X_cS^{-1}X_c^T
$$

which yields

$$
M=
\begin{bmatrix}
3 & -1 & -1 & -1 \\
-1 & 3 & -1 & -1 \\
-1 & -1 & 3 & -1 \\
-1 & -1 & -1 & 3
\end{bmatrix}
$$

---

## Multivariate Skewness

The skewness coefficient is

$$
b_{1,p}=\frac{1}{n^2}\sum_{i=1}^{n}\sum_{j=1}^{n}m_{ij}^3
$$

For this example:

- diagonal elements: $3^3=27$
- off-diagonal elements: $(-1)^3=-1$

Thus

$$
b_{1,p}=6
$$

---

### Skewness Test Statistic

The skewness test statistic is

$$
EAS=\frac{n}{6}b_{1,p}
$$

Substituting $n=4$:

$$
EAS=\frac{4}{6}(6)=4
$$

The degrees of freedom are

$$
df=\frac{p(p+1)(p+2)}{6}
$$

For $p=3$:

$$
df=\frac{3(4)(5)}{6}=10
$$

Therefore the p-value is

$$
p=P(\chi^2_{10}>4)
$$

which gives

$$
p=0.9473
$$

---

## Multivariate Kurtosis

The kurtosis coefficient is

$$
b_{2,p}=\frac{1}{n}\sum_{i=1}^{n}m_{ii}^2
$$

Since the diagonal elements are $3$:

$$
b_{2,p}=\frac{1}{4}(9+9+9+9)
$$

$$
b_{2,p}=9
$$

---

### Kurtosis Test Statistic

The standardized statistic is

$$
z=
\frac{b_{2,p}-p(p+2)}
{\sqrt{\frac{8p(p+2)}{n}}}
$$

Substituting $p=3$ and $n=4$:

$$
z=\frac{9-15}{\sqrt{\frac{120}{4}}}
$$

$$
z=-1.0954
$$

The p-value is

$$
p=P(\chi^2_1>z^2)
$$

$$
p=0.2733
$$

---

## Interpretation

- Skewness p-value = **0.9473**
- Kurtosis p-value = **0.2733**

Since both p-values are greater than $0.05$($\alpha$), we **do not reject the null hypothesis**.

Therefore, the data are **consistent with a multivariate normal distribution**.

---

## Explanatory Video 

[Video explaining Mardia test](https://youtu.be/DAz9bNVlh_k?si=WXMD4zmb78kKQ56W)