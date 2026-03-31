# Doornik–Hansen Test

---

In this section we describe the **Doornik–Hansen test**, which is a statistical test used to assess **multivariate normality** based on **skewness and kurtosis**.

The test combines information about:

1. **Asymmetry (skewness)**
2. **Tail behavior (kurtosis)**

into a single statistic to evaluate whether the data follow a multivariate normal distribution.

---

## Doornik–Hansen Test in R

The test can be implemented manually using previously computed skewness and kurtosis measures.

```{r}
# Assuming Mardia components already computed

# Skewness component (approximate)
Z1 <- sqrt(EAS)

# Kurtosis component (already standardized)
Z2 <- z

# Doornik–Hansen statistic
DH <- Z1^2 + Z2^2

# p-value
pValueDH <- pchisq(DH, df = 2, lower.tail = FALSE)
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

---

## Basic idea of the Test

---

The Doornik–Hansen test is based on the idea that for normally distributed data:

* Skewness should be close to zero
* Kurtosis should be close to its theoretical value

The test transforms both quantities into approximately normal variables and combines them.

---

## Skewness Component

---

Let ($b_{1,p}$) be the multivariate skewness.

The skewness statistic is transformed into a standardized variable:

$$
Z_1 \approx \sqrt{EAS}
$$

where $$EAS = \frac{n}{6} b_{1,p}$$

---

## Kurtosis Component

---

Let ($b_{2,p}$) be the multivariate kurtosis.

The standardized kurtosis statistic is:

$$
Z_2 =
\frac{b_{2,p} - p(p+2)}
{\sqrt{\frac{8p(p+2)}{n}}}
$$

Under the null hypothesis:

$$
Z_2 \sim N(0,1)
$$

---

## Global Test Statistic

---

The Doornik–Hansen statistic is defined as:

$$
DH = Z_1^2 + Z_2^2
$$

---

## Distribution

---

Under the null hypothesis:

$$
DH \sim \chi^2_2
$$

---

## Decision Rule

---

The p-value is computed using the chi-square distribution.

* If p-value > ($\alpha$), do not reject ($H_0$)
* If p-value ≤ ($\alpha$), reject ($H_0$)

---

## Prove Characteristics
--- 
The Doornik–Hansen test is particularly suitable for continuous multivariate data where deviations from normality may arise from both skewness and kurtosis simultaneously. It is especially useful in moderate sample sizes, as it combines these two components into a single statistic, providing a unified assessment of normality. The test performs well when variables are approximately continuous and the data structure does not involve strong categorical effects or discrete levels. Additionally, it is effective in detecting subtle departures from normality that may not be evident when analyzing skewness or kurtosis separately. However, it may be less appropriate for very small samples or datasets with strong non-linear dependencies, as these conditions can affect the accuracy of the transformations used in the test.

## Interpretation

---

If the p-value is greater than the significance level, there is no evidence against multivariate normality.

Otherwise, the data are not consistent with a multivariate normal distribution.

---

## Example

---

Consider a dataset where we already computed:

* ($Z_1$ = 1.5)
* ($Z_2$ = 0.8)

### Global Statistic

$$
DH = Z_1^2 + Z_2^2
$$

$$
DH = (1.5)^2 + (0.8)^2
$$

$$
DH = 2.25 + 0.64 = 2.89
$$

---

## Distribution

---

Since the statistic follows:

$$
DH \sim \chi^2_2
$$

The p-value is:

$$
p = P(\chi^2_2 > 2.89)
$$

---

## Interpretation

---

If the p-value is greater than ($\alpha$), we do not reject the null hypothesis.

Otherwise, we conclude that the data deviate from multivariate normality.

---

## Remarks

---

The Doornik–Hansen test provides a **joint assessment of skewness and kurtosis**, making it a powerful alternative to tests based solely on one aspect of the distribution.

It is particularly useful because it combines both types of deviations into a single statistic.
