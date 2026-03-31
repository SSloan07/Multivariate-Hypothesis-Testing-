# Royston Shapiro–Wilk Test
---

In this section we describe the **Royston Shapiro–Wilk test**, which is an extension of the classical **Shapiro–Wilk normality test** to the **multivariate case**.

The idea of the method is simple:

1. Apply the **Shapiro–Wilk test to each variable**.
2. Transform the obtained statistics.
3. Combine them into a **global statistic** to evaluate **multivariate normality**.

---

## Royston Test in R

The Royston test can also be applied in **R** using the `MVN` library.

```{r}
# Install library if necessary
if (!require(MVN)) install.packages("MVN")

# Load library
library(MVN)

# Apply Royston test
mvn(data, mvnTest = "royston")

```


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

If the p-value is greater than the significance level, there is no evidence against multivariate normality.

--- 

## Basic idea of the Test

---

The Royston test is based on the Shapiro–Wilk statistic, which measures how closely a dataset follows a normal distribution.

For a univariate variable, the Shapiro–Wilk statistic is defined as:

$$
W =
\frac{\left(\sum_{i=1}^{n} a_i x_{(i)}\right)^2}
{\sum_{i=1}^{n}(x_i-\bar{x})^2}
$$


where:

$x_{(i)}$ are the ordered sample values

$a_i$ are constants derived from expected normal order statistics

$\bar{x}$ is the sample mean

The statistic satisfies:

$0<W≤1$
$0<W≤1$

Values close to 1 indicate normality, while small values indicate deviation from normality.

--- 

## Data Matrix 

--- 

Suppose we have a dataset:

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

$n$ = number of observations

$p$ = number of variables

Each column represents one variable.

---

### Step 1: Apply Shapiro–Wilk to Each Variable

For each variable $X_j$ we compute the Shapiro–Wilk statistic:

$$
W_1, W_2, \ldots, W_p
$$

Each statistic evaluates univariate normality.

### Step 2: Log Transformation

The Royston method transforms each statistic using:

$$
y_i = \ln(1 - W_i)
$$

This transformation helps approximate the distribution of the statistic to a normal distribution.

### Step 3: Standardization

Each transformed statistic is standardized as:

$$
Z_i = \frac{y_i - \mu_i}{\sigma_i}
$$

where:

- $\mu_i$ and $\sigma_i$ depend on the sample size $n$
- these values are obtained from approximations derived by Royston

The standardized statistics approximately follow:

$$
Z_i \sim N(0,1)
$$

### Global Test Statistic 

The overall statistic of the Royston test is obtained by combining all standardized values:

$$
H = \sum_{i=1}^{p} Z_i^2
$$

Under the null hypothesis of multivariate normality:

$$
H \sim \chi^2_{p}
$$

where $p$ is the number of variables.

--- 

## Decision Rule 

---

The p-value is computed from the chi-square distribution.

If p-value > $\alpha$, the null hypothesis is not rejected.

If p-value ≤ $\alpha$, the null hypothesis is rejected.

For multivariate normality to be accepted, the combined statistic must be non-significant.

--- 

## Interpretation

--- 

If the p-value obtained from the Royston test is greater than the chosen significance level, there is no statistical evidence against multivariate normality.

Otherwise, the dataset cannot be considered multivariate normal.

--- 

## Example

--- 

Consider the following dataset with $n=4$ observations and $p=2$ variables.

Data Matrix
$$
X =
\begin{bmatrix}
2 & 5 \\
4 & 7 \\
6 & 9 \\
8 & 10
\end{bmatrix}
$$
	
### Shapiro-Wilk Statistics 

Applying the Shapiro–Wilk test to each variable gives:

| Variable | W | p-value |
|----------|----|---------|
| $X_1$ | 0.96 | 0.42 |
| $X_2$ | 0.93 | 0.31 |

### Log Transformation 

$$
y_i = \ln(1 - W_i)
$$

For example:

$$
y_1 = \ln(1 - 0.96)
$$

$$
y_2 = \ln(1 - 0.93)
$$

### Standarization 

Each value is standardized:

$$
Z_i = \frac{y_i - \mu_i}{\sigma_i}
$$

Assume we obtain:

$$
Z_1 = -0.30
$$

$$
Z_2 = -0.52
$$
---

## Global Statistics 

---

$$
H = Z_1^2 + Z_2^2
$$

$$
H = (-0.30)^2 + (-0.52)^2
$$

$$
H = 0.09 + 0.27 = 0.36
$$

---

## Distribution 

---


Since $p = 2$:

$$
H \sim \chi^2_{2}
$$

The p-value is

$$
p = P(\chi^2_{2} > 0.36)
$$

which is greater than $\alpha$(0.05 in this case).

---
## Interpretation
---
Since the p-value is greater than $\alpha$, we do not reject the null hypothesis.

Therefore, the data are consistent with a multivariate normal distribution.

---

## Explanatory video 

--- 

[Video explaning Royston Shapiro-Wilk test](https://youtu.be/opsuV2PmUcs?si=Am0nUv_0xIDyDOwp)