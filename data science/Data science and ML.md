Data Science and Machine Learning with Python Hands On
----------------------------------------------------------
data-science-and-machine-learning-with-python-hands-on
2018.01.27
Set up
Enthought Canopy, jupyter, pydotplus
$ !pip install pydotplus
Panda, numpy, matplotlib, scipy

Types of Data
	Numerical: discrete, continuous
	Categorical: gender, race, states, product category
	Ordinal: mixture of numerical and categorical; eg, movie ratings

Basic stats
Mean, median, mode

Import matplotlib.pyplot as plt
Plt.hist(incomes, 50)
$ Incomes = np.random.normal(27000, 15000, 1000)
$ np.mean(incomes) // median, mode
$ Incomes = np.extend(incomes, [1000000])

$ ages = np.random.randint(18, high=90, size=500)
$ from scipy import stats
$ stats.mode(ages)
	ModeResult(mode=array([43]), count=array([14])) // mode is 43, count is 14

Variance, standard deviation
Variance: average of squared difference from the mean
Std. deviation: sqrt of variance
	One std deviation from the mean can be considered unusual
Sample variance: sum of squared difference, divided by n – 1
$ incomes.std()
$ incomes.var()

Probability density function, probability mass function
Probability density function (pdf): Probability in a range, (from v to v + sigma)
Probability mass function: for discrete date

Common data disbributions
Uniform distribution
$ np.random.uniform(-10.0, 10.0, 10000)

Normal / Gaussian distribution
$ from scipy.stats import norm
$ import matplotlib.pyplot as plt
$ x = np.arange(-3, 3, 0.001)
$ plt.plot(x, norm.pdf(x))

Exponential PDF (power law)
$ from scipy.stats import expon
$ plt.plot(x, expon.pdf(x))

Binomial probability
$ fro scipy.stats import binom
$ plt.plot(x, binom.pmf(x n, 10, 0.5)

Poisson probability mass function
Eg, website gets 500 visits/day, what’s the odds of getting 550?
$ from scipy.stats import poisson
$ plt.plot(x, poisson.pmf(x, 500))

Percentiles and moments
Percentile: a point where x% of values are less than that value, eg: income distribution
Quartiles (in normal dist.): middle is 50% of data
$ np.percentile(incomes, 50) // == median, 50% of incomes are less than 99.95

Moments: quantitative measures of the shape of a probability density function
1st moment is the mean
2nd moment is the variance
3rd moment is skew (r): how lopsided
	Distribution with longer tail on the left -> skew left, and a negative skew
	Long tail on the right -> skew right
4th moment is kurtosis: how thick is the tail, how sharp is the peak 
for norm, k = 0
	Higher peaks => higher kurtosis
$ np.mean(vals)
$ np.var(vals)
$ import scipy.stats as sp
$ sp.skew(vals)
$ sp.kurtosis(vals)

Matplotlib
MatPlotLib.ipynb
$ plt.savefig(‘c:\\Users\\WT\\myplot.png’, format=’png’)

axes = plt.axes()
axes.set_xlim([-5, 5])
axes.set_ylim([0, 1.0])
axes.set_xticks([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5])
axes.set_yticks([0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0])
axes.grid()
plt.xlabel('Greebles')
plt.ylabel('Probability')
plt.plot(x, norm.pdf(x), ‘b-‘) // blue, solid line
plt.plot(x, norm.pdf(x, 1.0, 0.5), ‘r:’) // red, hash line
plt.legend(['Sneetches', 'Gacks'], loc=4)
plt.show()


XKCD Style :)

Line, bar, pie, scatter, histogram
Box & whisker plot

uniformSkewed = np.random.rand(100) * 100 - 40
high_outliers = np.random.rand(10) * 50 + 100
low_outliers = np.random.rand(10) * -50 - 100
data = np.concatenate((uniformSkewed, high_outliers, low_outliers))
plt.boxplot(data)
plt.show()
 

Covariance and correlation

import numpy as np
from pylab import *

def de_mean(x):
    xmean = mean(x)
    return [xi - xmean for xi in x]

def covariance(x, y):
    n = len(x)
    return dot(de_mean(x), de_mean(y)) / (n-1)  // dot is for vector multiply

pageSpeeds = np.random.normal(3.0, 1.0, 1000)
purchaseAmount = np.random.normal(50.0, 10.0, 1000)

scatter(pageSpeeds, purchaseAmount)

covariance (pageSpeeds, purchaseAmount)
pageSpeeds.std()
np.cov()


np.corrcoef(pageSpeeds, purchaseAmount)

Conditional probability
ConditionalProbabilityExercise.ipynb
P(B|A) = P(A,B)/P(A)
Homework

Baye’s theorem
Video 019
P(A|B) = P(A)P(B|A)/P(B) = P(A,B)/P(B)

Predictive Models
Linear regression
Least square
Gradient descent: for higher degree, 3D
R-squared = 1 – sum of squared errors / sum of squared variation from mean

$ from scipy import stats
$ slope, intercept, r_value, p_value, std_err = stats.linregress(pageSpeeds, purchaseAmount)


polynomial regression
	don’t overfitting (train/test)
	high r2 => curve fits data, but may not be a good predictor
$ x = np.array(pageSpeeds)
$ y = np.array(purchaseAmount)
$ p4 = np.poly1d(np.polyfit(x, y, 4))
$ from sklearn.metrics import r2_score
$ r2 = r2_score(y, p4(x))


Multivariate regression
$ import statsmodels.api as sm
$ from sklearn.preprocessing import StandardScaler
$ scale = StandardScaler()

$ X = df[['Mileage', 'Cylinder', 'Doors']]
$ y = df['Price']
$ X[['Mileage', 'Cylinder', 'Doors']] = scale.fit_transform(X[['Mileage', 'Cylinder', 'Doors']].as_matrix())
$ est = sm.OLS(y, X).fit()
$ est.summary()

Multi-Level models
Some effects happen at various levels, model and account for the interdependencies
Health -> cell, organ, whole, family, city, world


Machine Learning with Python
Supervised vs unsupervised
Unsupervised learning: not given any answers to learn from
Supervised learning: train (80% data set)/test (20%)
	Need to ensure both sets are large enough. Must be selected randomly. A great way to guard against overfitting.
	Train/test is not infallible (overfitting can still happen): k-fold cross validation

Train/test
Random 80% train, 20% test

Bayesian methods
Spam methods
Naïve Bayes: assuming different words independent of each other
NaiveBayes.ipynb

K-means clusters
Movie genre, geographic data
Split data into K groups that are closest to K centroids
Unsupervised learning
KMeans.ipynb

Measuring Entropy
Measure of a data set’s disorder, 0 if all the classes are the same
H(S) = -p1lnp1 – … -pnlnpn	// pn is the proportion of data for each class
Decision trees
Filter out resumes
In each step, find the attribute we can use to partition the data set to minimize the entropy of the data at the next step -> greedy algorithm (ID3). It might not result in an optimal tree, but it works.
Very susceptible to overfitting -> construct several alternate decision trees and let them “vote” on the final classification

Ensemble learning
DecisionTree.ipynb
Random forests was an example of ensemble learning
Use multiple models to try and solve the same problem, and let them vote on the results.
Advanced ensemble learning
Bayes Optimal Classifier: theoretical the best, but almost always impractical

Support Vector Machines (SVM)
Works well for classifying higher-dimensional data (lots of features)
“kernel trick”, supervised technique 
SVC.ipynb, 036 [Activity] Using SVM to cluster people using scikit-learn.mp4

Recommend system
User-based collaborative filtering
	Matrix of things each user bought/viewed/rated
	Compute similarity scores between users
	Find users similar to you
	Recommend stuff they bought/viewed/rated that you haven’t yet

Problems:
	People are fickle; tastes change
	There are usually many more people than things: require more computing
	People do bad things: people may game the system, schilling attack


Item-based collaborative filtering 
(better than user-based, Amazon uses it)
	A movie will always be the same, it doesn’t change
	Few things than people -> less computation
	Harder to game the system
Based on what people actually bought, not viewed

Find every pair of movies that were watched by the same people => measure the similarity of their ratings across all users => sort by movie, then by similarity strength
SimilarMovie.ipynb (good example of pandas)
popularMovies = movieStats[‘rating’][‘size’] >= 100 // only include movies that are rated by more than 100 people

ItemBasedCF.ipynb

More techniques
K-Nearest Neighbor (KNN)
The number k is important, should be big enough to cover important dataset.
Supervised training
Using KNN to predict a rating for a movie
KNN.ipynb

Dimensionality reduction, principal component analysis
PCA, singular value decomposition (SVD)
K-means clustering
	Finds “eigenvectors” in the higher dimensional data that define hyperplanes that split the data while preserving the most variance in it => project onto the hyperplanes
	Also useful for things like image compression and facial recognition
Example: Iris data (PCA.ipynb)
	4 dimension: Petal (height, width), sepals (height, width)
Scikit-learn

Data warehouse, ETL, ELT
Hadoop, hive, spark, MapReduce
Extra raw data (eg, logs) => load it in as-is => transform 

Reinforcement Learning (Q-learning)
Pack-man
Exploration problem: always choose the action for a given state with the highest Q.
Better way: introduce an epsilon term where if a random number is < epsilon, don’t follow the highest Q but choose at random. Choosing epsilon can be tricky.
Markov decision processes (MDPs, or discrete time stochastic control process)
Dynamic programming: break down into a collection of simpler subproblems, store the solution; next time, compute again using the stored solution (instead of computing again)

Dealing with Real-World Data
Error = bias^2 + variance

K-Fold Cross Validation
Train/test: 2 buckets
	K buckets, train each bucket and measure performance against the test set
	Take the average of the k-1 r-squared scores

Scikit-learn makes this even easier than train/test
KFoldCrossValidation.ipynb

Data cleaning
Extremely important, weblog

Clean invalid data

Normalize data: 
scikit-learning “whiten”
Always read the documentation for each library you use

Detect outliers
	Data points at 2-3x of standard deviation
	Outlier.ipynb
	Filtered = [e for e in data if (u-2*s < e < u+2*s)]


Apache Spark_ Machine Learning on Big Data
 
Resilient Distributed Dataset (RDD)
DAG engine (directed acylic graph) optimizes workflows
Spark core
	Spark streaming
	Spark sql
	MLLib
	GraphX

SparkContext:
	Created by your driver program, making RDD

Creating RDD
	Nums = parallelize([1, 2, 3, 4])
	Sc.textFile(file:///...)
	HiveCtx = HiveContext(sc)  orws = hiveCtx.sql(“SELECT * FROM users”)

Transforming RDD
	Map, flatmap, filter, distinct, sample, union, intersection, subtract, Cartesian

	Action methods: Collect, count, countByValue, take, top, reduce…

MLLib
New data types:
	Vector (dense, sparse)
	LabeledPoint
	Rating

Decision tree in Spark
SparkDecisionTree.py
$ spark-submit SparkDecisionTree.py

K-Means clustering in Spark
SparkKMeans.py

TF-IDF
TF: term frequency
IDF: inverse document frequency, how often a word occurs in a document
Document frequency: how often a word occurs in an entire set of documents
TF-IDF.py
Spark2.0
	dataFrame, dataset

Experiment design
A/B testing: 
new performance / controlled one
variance is the enemy
T-tests and p-value
T-tests: ratio of standard deviation of two sets, the higher the bigger difference
p-value: lower value -> small chance caused by random change? Should be 1%, 5%
TTest.ipynb
$ from scipy import stats
$ stats.ttest_ind(A, B)

A/B Test Gotchas
Correlation does not imply causation
	It could still be random chance, other factors could be at play
Novelty Effects
	New feature will catch users’ attention, but it doesn’t last long; re-run experiments much later
Seasonal Effects: holiday, weather
Selection Bias: random selection of customers for A or B isn’t really random
Data pollution: are robots affecting? Are outliers?

Deep learning
Gradient Descent: moving parameters to minimize error
Faster way to find the local minimum: Autodiff, reverse-mode autodiff
Softmax
	Used for classification
	Given a score for each classe -> produce probability of each class -> highest probability is the answer

Neuron -> Cortical columns -> Perceptron -> multi-layer perceptrons
Deep learning in the Tensorflow playground
Playground.tensorflow.org
Backpropagation
Activation functions
Optimization functions

Keras
Built on top of tensorflow for deep learning
Integrate with scikit_learn

Convolutional Neural Network (CNN)
When don’t know where the pattern might be -> find pattern

Recurrent Neural Network (RNN)
Time-series data -> predict future behavior
