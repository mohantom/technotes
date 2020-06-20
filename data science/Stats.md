Statistics and Probability
---------------------------
Joint distribution
Interquartile range (IQR)
Shifting: add or remove values for every element
	Changes: mean, median, mode
	Stay the same: range, IQR
Correlation does not give causality (one cause another): Pearson correlation coefficient
Box-and whisker plots
 

Frequency histograms, polygons -> density curve -> prediction
Left-skewed or left-tailed, or negatively skewed
Central tendency: median vs mean
	Spread: IQR vs STD 
Identity outlier (fences): 1.5IQR
	Low outlier: Q1 – 1.5 IQR; high outlier: Q3 + 1.5 IQR

Z-score = (x  - u) / sigma, how after x is from u in terms of sigma
Z table always gives the area to the left


 

Binomial distribution
Cn,k * p^k * (1-p)^(n-k)
Mean = np
Variance: np(1-p)

Bernoulli random variable 
(special binomial, only 1 trial)
	Success 1, failure 0
	Mean = p, variance = p(1-p)
Geometric random variable
	How many times of trial until we get a success
	P(s = n) = p (1-p)^(n-1)  // only succeed at nth trial
	P(s < 4) = P(1) + P(2) + P(3)  // get first success in the first 3 trials
	1 – P(1) – P(2) // takes more than 2 trials to get a success
	1 – P(1) // takes at least 2 trials to get a success
	Mean = 1/p
	Variance = (1-p)/p^2 

Poisson distribution
	P(x) = lamdax * e-lamd/ x!
	$ from scipy.stats import poisson
	$ poisson.pmf(4, 8) // exactly  at 4
	$ poisson.cmf(2, 8) // fewer than 3
	$ poisson.pmf(0, 8/12) // no delivery between 4:00 and 4:05pm

Sampling
	Random sampling
	Stratified random sampling: population -> groups/segments (stratum, strata) -> random 
	Clustering: population -> groups ->random selection of groups. Usually to reduce costs. Convenience sampling

Central limit theorem (CLT)
Sample std = population std / n^0.5
If population is not normal distribution, sampling can be normal:
	Random samples, independence condition, > 30 samples
Example: mean = 8.7, std = 0.4, what’s probability of 25 samples with mean within 0.2
	Sample std = 0.4/5 = 0.08. Z = 0.2/0.08 = 2.5; check table, P = P(+2.5) – P(-2.5)
 
Hypothesis testing
Z-score
Eg, 400 sample, 63% is teenage. Is it fair to say most are teenager?
Sample size matters! If only 40 sample, it will fail to reject (most are not teenager)
Type I error: reject a null hypothesis that should not be rejected (which is true). False positive
Type II error: fail to reject null hypothesis that should have been rejected (which is false). False negative
Student’s t-test
compare two sample/population


F-test and ANOVA
What is the prob that two samples have the same variance?
What is the prob that 3 or more samples come from the same population?
 

Two-way ANOVA
Tet two independent variables at the same time
 
Goal of ANOVA is t separate different aspects of the total variance
A row is called a block
	SSG: sum of squares block
	SSB: sum of squares block
	SST: sum of squares total
	SSE: sum of squares error = SST – SSG –SSB
	Df-error = (n-blocks -1) * (n-groups – 1)
Two-way ANOVA with replication
$ from scipy import stats
$ stats.f.ppf(1-0.05, dfn=2, dfd=27)  # 3.354
Normal distributions and z-scores
68-95-99.7 rule
$ from scipy import stats
$ stats.norm.cdf(z) # z = 0.7  => 0.7580
$ stats.norm.ppdf(0.95) # z = 1.645
Excel: STDEV.S(B3:B12)
T value: T.INV(significance level eg 0.5, degree of freem eg 18) = -1.734064 (1-etail) 
$ from scipy.stats import ttest_ind
$ a = [1184, 1203…]
$ b = [1136, 1178, …]
$ ttest_ind(a, b).stattistic  # 2.279
$ ttest_ind(a, b).pvalue/ 2  # 0.01752

Regression
Linear regression
$ from scipy.stats import linregress
$ slope =linregress(x, y).slope
$ intercept = linregress(x,y).intercept
Multiple regression
$ from sklearn.linear_model import LinearRegression
$ reg = LinearRegression()
$ reg.fit(list(zip(x1, x2)), y)
$ b1, b2 = reg.coef_[0], reg.coef_[1]
$ b0 = reg.intercept_
Chi-square analysis
 
Example: 6 servers with failure rate which should be the same. Based on the data, can we assume that the servers fail at the same rate?
Server	Observed
A	46
B	36
C	52
D	26
E	42
F	38

$ from scipy.stats import chi2
$ chi2.isf(0.05, 5) # chi value look up
