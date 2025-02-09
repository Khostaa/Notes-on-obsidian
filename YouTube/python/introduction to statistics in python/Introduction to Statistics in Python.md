# What is Statistics?
- is the practice and study of collecting and analyzing data.
- Summary Statistics
	- is a fact about a summary of some data like an average or a count
## What can statistics do?
- A more important question, however, is what can statistics do? With the power of statistics, we can answer tons of different questions like: How likely is someone to purchase a product? Are people more likely to purchase it if they can use a different payment system? How many occupants will your hotel have? How can you optimize occupancy? How many sizes of jeans need to be manufactured so they can fit 95% of the population? Should the same number of each size be produced? A question like, Which ad is more effective in getting people to purchase a product? can be answered with A/B testing.

## What can't statistics do?
- While statistics can answer a lot of questions, it's important to note that statistics can't answer every question. If we want to know why the TV series Game of Thrones is so popular, we could ask everyone why they like it, but they may lie or leave out reasons. We can see if series with more violent scenes attract more viewers, but even if they do, we can't know if the violence in Game of Thrones is the reason for its popularity, or if other factors are driving its popularity and it just happens to be violent.

## Types of Statistics
1. Descriptive Statistics
	-  Describe and summarize data
	- After asking four friends how they get to work, we can see that 50% of them drive to work, 25% ride the bus, and 25% bike. These are examples of descriptive statistics.
2. Inferential Statistics
	- use a sample of data to make inferences about a larger population
	- We could use inferential statistics to figure out what percent of people drive to work based on our sample data.

## Types of data
1. Numeric, or quantitative data
	- is made up of numeric values.
	- Continuous (Measured)
		- is often quantities that can be measured, like speed or time.
			- Airplane speed
			- time spent waiting in line
	- Discrete (Counted)
		- is usually count data, like
			- Number of pets
			- Number of packages shipped
1. Categorical, or qualitative data
	- is made up of values that belong to distinct groups.
	- Nominal (Unordered)
		-  is made up of categories with no inherent ordering, like
			- Married/Unmarried
			- Country of residence
	- Ordinal (ordered)
		- has an inherent order, like a survey question where you need to indicate the degree to which you agree with a statement.
		- strongly disagree
		- somewhat disagree
		- neither agree nor disagree
		- somewhat agree
		- strongly agree
- ***these aren't the only two types of data that exist - there are others too***

### Sometimes Categorial data can be represented as numbers
- Nominal (Unordered)
	- Married/Unmarried (1/0)
	- Country of residence (1, 2, ...)
- Ordinal (Ordered)
		- strongly disagree (1)
		- somewhat disagree (2)
		- neither agree nor disagree (3)
		- somewhat agree (4)
		- strongly agree (5)

- Being able to identify data types is important since the type of data you're working with will dictate what kinds of summary statistics and visualizations make sense for your data, so this is an important skill to master.
- For numerical data, we can use summary statistics like
	- mean
	- plots like scatter plots, but these don't make a ton of sense for categorical data.
- Similarly things like counts and barplots don't make much sense for numeric data.

# Measures of Center
## Histograms
- A histogram takes a bunch of data points and separates them into bins, or ranges of values.
- The heights of the bars represent the number of data points that fall into that bin
- Histograms are a great way to visually summarize the data, but we can use numerical summary statistics to summarize even further.

## Mean
- average
```python
import numpy as np
np.mean(msleep['sleep_total'])
```
- Since the mean is more sensitive to extreme values, it works better for symmetrical data.
## Median
- is the value where 50% of the data is lower than it, and 50% of the data is higher.
- We can calculate this by sorting all the data points and taking the middle one
```python
msleep['sleep_total'].sort_values()
np.median(msleep['sleep_total'])
```
- if the data is skewed, meaning it's not symmetrical, like this, median is usually better to use.

## Mode
-  is the most frequent value in the data.
```python
msleep['vore'].value_counts()
import statistics
statistics.mode(msleep['vore'])
```
- Mode is often used for categorical variables, since categorical variables can be unordered and often don't have an inherent numerical representation.

## Adding an outlier
- if the data is piled up on the right, with a tail on the left. Data that looks like this is called left-skewed data. 
- When data is piled up on the left with a tail on the right, it's right-skewed.

# Measures of Spread
- how spread or close apart the data points are.
## Variance
- average distance from each data point to data's mean.
- higher the variance, more spread out the data is.
- units: squared
### Calculating variance
- distance = subtract mean from each data point
- square each distance
- sum squared distances
- divide by number of datapoints - 1
#### Use np.var()
```python
np.var(msleep['sleep_total'], ddof=1)
# without ddof = 1, population variance is caculated instead of sample variance.
```

## Standard Deviation
- calculated by taking square root of variance.
```python
# method 1
np.sqrt(np.var(msleep['sleep_total'], ddof = 1))

# method 2
np.std(msleep['sleep_total'], ddof=1)
```
## Mean absolute Deviation
- takes absolute value of distances to the mean and then takes the mean of those differences.
```python
dists = msleep['sleep_total'] - mean(msleep$sleep_total)
np.mean(np.abs(dists))
```

## Differences between standard deviation and mean absolute deviation
- Standard deviation squares distances, so longer distances are penalized more than shorter ones, 
- mean absolute deviation penalizes each distance equally.
- One isn't better than the other, but SD is more common than MAD.

## Quantiles
```python
np.quantile(msleep['sleep_total'], 0.5)
# 0.5 quantile = median

# We can also pass in a list of numbers to get multiple quantiles at once.
# 0.25 = 1st quartile
# 0.5 = median
# 0.75 = third quartile
np.quantile(msleep['sleep_total'], [0, 0.25, 0.5 0.75, 1])
# output: array([1.9, 7.85, 10.1, 13.75, 19.9])
# This means that 25% of the data is between 1-point-9 and 7-point-85, another 25% is between 7-point-85 and 10-point-10, and so on.
```
### Box plots use quartiles
- bottom of box - first quartile
- top - third quartile
- middle line - second quartile or median
```python
import matplotlib.pyplot as plt
plt.boxplot(msleep['sleep_total'])
plt.show()
```

### Quartiles using np.linspace()
#### np.linspace()
- takes start, stop and number intervals
```python
# without linspace
np.quantile(msleep['sleep_total'], [0, 0.25, 0.5 0.75, 1])

# linspace syntax
np.linspace(start, stop, num)

# with linspace
np.quantile(msleep['sleep_total'], np.linspace(0, 1, 5))

# np.linspace(0, 1, 5) - start with 0, end with 1, and 5 different intervals.
```

## Interquartile range (IQR)
- It's the distance between the 25th and 75th percentile, which is also the height of the box in a boxplot.
```python
# method 1
np.quantile(msleep['sleep_total'], 0.75) - np.quantile(msleep['sleep_total'], 0.25)

# method 2
from scipy.stats import iqr
iqr(msleep['sleep_total'])
```
## Outliers
- data point that is substantially different from the others
- A data point is outlier if:
	- data < Q1 - 1.5 * IQR or
	- data > Q3 + 1.5 * IQR
### Finding outliers
![[finding outliers.png]]

## All in one go:
```python
msleep['bodywt'].describe()
```
![[exercise.png]]
![[Introduction to statistics in python 1.pdf]]

# What are the chances?
- People talk about chance pretty frequently, like what are the chances of closing a sale, of rain tomorrow, or of winning a game? But how exactly do we measure chance?
- we can measure the chances of an event using probability
$$
P(event) = \frac{no.- of- ways- event -can -happen}{total -no. -of -possible -outcomes}
$$

Probability - 0% - impossible
Probability - 100% - will certainly happen

## Sampling from DataFrame
- using sample() method
	- By default, it randomly sample one row from the DataFrame
```python
sales_counts.sample()
```
### Setting a random seed
- seed is a number that python's random number generator uses as a starting point.
- It will generate same random value each time.
```python
np.random.seed(10)
sales_count.sample()
```
### Sampling without/with replacement
- once picked, cannot not replaced : without replacement
- picked and replaced : with replacement
- settting *replace = True* - with replacement
```python
sales_counts.sample(5, replace = True)
```
## Independent events
- Two events are **independent** if the probability of the second event isn't affected by the outcome of the first event.
- Sampling with replacement = each pick is independent.

## Dependent events
- Two events are **dependent** if the probability of the second event is affected by the outcome of the first event.

# Discrete distributions
 - A probability distribution describes the probability of each possible outcome in a scenario.
 - Expected Value: mean of probability distribution.
 - When all outcomes have the same probability, like a fair die, this is a special distribution called a discrete uniform distribution.
## Visualizing a sample
e.g:
```python
# Rolling a dice 10 times
# Sample with replacement
rolls_10 = die.sample(10, replace = True)
rolls_10

# visualizing using histogram
rolls_10['number'].hist(bins=np.linspace(1, 7, 7))
plt.show()
```

- if we roll 1000 times, it looks even more like the theoretical probability distribution and the mean closely matches 3-point-5.
- This is called the law of large numbers, which is the idea that as the size of your sample increases, the sample mean will approach the theoretical mean.

# Continuous distributions
```python
# 0 - lower limit , 12 - Upper limit
# Probability of waiting less than 7 minutes
# P (wait time <= 7) 
from scipy.stats import uniform
uniform.cdf(7, 0, 12) 

# Probability of waiting more than 7 minutes
# P(wait time >= 7) = 1 - P(wait time <= 7)
from scipy.stats import uniform
1 - uniform (7, 0, 12)

# Probability of waiting more than = 4 minutes less than = 7 minutes
# P (4 <= wait time <= 7) = P (wait <= 7) - P(wait <=4)
from scipy.stats import uniform
uniform.cdf(7, 0, 12) - uniform.cdf(4, 0, 12)

# to calculate the probability of waiting between 0 and 12 minutes, we multiply 12 by 1/12, which is 1 or 100 %.

```

## Generating random number according to uniform distribution.
- use **uniform.rvs**
```python
from scipy.stats import uniform
# to generate 10 random values between 0 and 5
uniform.rvs(0, 5, size = 10) 
```
- Continuous distributions can take forms other than uniform where some values have a higher probability than others.
- No matter the shape of the distribution, the area beneath it must always equal 1.

## The binomial distribution
'#' - number
### Binary Outcome 
- outcome with two possible values i.e, 1 or 0, Success or Failure , Win or Loss, True or False.
- binom.rvs(# of coins, probability of heads/success, size = number(#) of trials)
#### A single flip
1 = head, 0 = tails
```python
from scipy.stats import binom
# Flip 1 coin with 50% probability of heads 1 times
binom.rvs(1, 0.5, size=1)
```
#### One flip many times
```python
# Flip 1 coin with 50% chance of success 8 times
binom.rvs(1, 0.5, size=8)
```
#### Many flips one time
```python
# Flip 8 coins with 50% chance fo success 1 time
binom.rvs(8, 0.5, size=1)
```
#### Many flips many times
```python
# Flip 3 coins with 50% chance of success 10 times
binom.rvs(3, 0.5, 10)
```
### Other proabilities
```python
# Flip 3 coins with 25% chance of success, 10 times
binom.rvs(3, 0.25, size = 10)
```

### Binomial distribution
- probability distribution of the number of successes in a sequence of independent trials.
- e.g: number of heads in a sequence of coin flips
- Described by *n* and *p*
	- *n*: total number of trials
	- *p*: probability of success
	- p - second argument, n - 3rd argument of binom.rvs
#### What's the probability of 7 heads?
P (heads = 7)
```python
# binom.pmf(num heads, num trials, prob. of heads)
binom.pmf(7, 10, 0.5)
```
#### What's the probability of 7 or fewer heads?
P(heads <= 7)
```python
binom.cdf(7, 10, 0.5)
```
#### What's the probability of more than 7 heads?
P (heads > 7)
```python
1 - binom.cdf(7, 10, 0.5)
```
### Expected value of Binomial distribution
Expected value = n * p
Expected no. of heads out of 10 fips = 10 * 0.5 = 5

## Independence
- it's important to remember that in order for the binomial distribution to apply, each trial must be independent,
- The binomial distribution is a probability distribution of the number of successes in a sequence of independent trials.
- so the outcome of one trial shouldn't have an effect on the next. For example, if we're picking randomly from these cards with zeros and ones, we have a 50-50 chance of getting a 0 or a 1.
- But since we're sampling without replacement, the probabilities for the second trial are different due to the outcome of the first trial. Since these trials aren't independent, we can't calculate accurate probabilities for this situation using the binomial distribution.
- Probabilities of second trial are altered due to outcome of the first.
![[Introduction to statistics in python 2.pdf]]

# The normal distribution
- Its shape is commonly referred to as a "bell curve". its characteristics are: 
	- it's symmetrical, left side is mirror image of right.
	- the area beneath the curve is 1.
	- the probability never hits 0, it looks like it does at the tail ends. only 0-points-006% of its area is contained beyond the edges of this graph.
- Normal distribution is described by its mean and standard deviation.
- When a normal distribution has mean 0 and a standard deviation of 1, it's a special distribution called the standard normal distribution
## Area under the normal distribution
- For the normal distribution, 68% of the area is within 1 standard deviation of the mean.
- 95% of the area falls within 2 standard deviations of the mean.
- 99.7% of the area falls within three standard deviations.
- This is sometimes called 68-95-99.7 rule.

- lots of histograms look normal.
- approximating data with the normal distribution.
	- mean = 161
	- standard deviation - 7
- what percent of women are shorter than 154 cm?
```python
from scipy.stats import norm
norm.cdf(154, 161, 7)
```
- what percent of women are taller than 154 cm?
```python
from scipy.stats import norm
1 - norm.cdf(154, 161, 7)
```
- what percent of women are 154-157 cm?
```python
norm.cdf(157, 161, 7) - norm.cdf(154, 161, 7)
```
- what height are 90% of women shorter than?
```python
norm.ppf(0.9, 161, 7)
```
- what height are 90% of women taller than?
```python
norm.ppf((1-0.9), 161, 7)
```
### Generating random numbers
```python
# Generate 10 random heights
norm.rvs(161, 7, size=10)
```
- Create a variable called `new_sales`, which contains 36 simulated amounts from a normal distribution with a mean of `new_mean` and a standard deviation of `new_sd`.
```python
new_sales = norm.rvs(new_mean, new_sd, size=36)
```

# The Central limit theorem
-  We have a Series of the numbers 1 to 6 called die. To simulate rolling the die 5 times, we'll call die-dot-sample. We pass in the Series we want to sample from, the size of the sample, and set replace to True. This gives us the results of 5 rolls.
```python
die = pd.Series([1, 2, 3, 4, 5, 6])
# Roll 5 times
samp_5 = die.sample(5, replace = True)
print(samp_5)
# take mean
np.mean(samp_5)
```
- **a sampling distribution will approach a normal distribution as the number of trials increases. This phenomenon is known as Central Limit Theorem.**
- *central limit theorem only applies when samples are taken randomly and are independent.*
- applies to Standard deviation, Proportions
- Estimate characteristics of unknown underlying distribution.
- More easily estimate characteristics of large populations.

# The Poisson distribution 
## Poisson processes
- events appear to happen at a certain rate, but completely random.
- e.g:
	- number of animals adopted from an animal shelter per week
	- number of people arriving at a restaurant per hour
	- number of earthquakes in California per year
## Poisson distribution
- Probability of some #(number) of events occurring over a fixed period of time.
- e.g:
	- Probability of 12 people arriving at a restaurant per hour
### Lambda
- average number of events per time interval

#### Probability of a single value
- if the average number of adoptations per week is 8, 
- what is P(# adoptions in a week = 5)?
```python
from scipy.stats import poisson
poisson.pmf(5, 8)
```
#### Probability of less than or equal to
- what is P(# adoptions in a week <=5)?
```python
from scipy.stats import poisson
poisson.cdf(5, 8)
```
#### Probability of greater than
- what is P(# adoptions in a week >5)?
```python
from scipy.stats import poisson
1- poisson.cdf(5, 8)
```
#### Sampling from a Poisson distribution
```python
from scipy.stats import poisson
poisson.rvs(8, size=10)
```
- the sampling distribution of sample means of a Poisson distribution looks normal with a large number of samples.
# Exponential distribution
- Probability of time between Poisson events
- e.g:
	- Probability of > 1 day between adoptions
	- Probability of < 10 minutes between restaurant arrivals
	- Probability of 6-8 months between earthquakes
- also uses Lambda (rate)
- Continuous
- e.g:
	- On average, one customer service ticket is created every 2 minutes
		- lambda = 0.5 customer service tickets created each minute
## Expected value of exponential distribution
In terms of rate(Poisson):
- lambda = 0.5 requests per minute
In terms of time between events (exponential):
- 1/lambda = 1 request per 2 minutes
- 1/0.5 = 2
```python
from scipy.stats import expon
# scale = 1/lambda = 1/0.5 = 2
# P(wait < 1 min) =
expon.cdf(1, scale = 2)

#P(wait > 4 min) = 
1 - expon.cdf(4, scale=2)

#P(1min < wait < 4min) =
expon.cdf(4, scale=2) - expon.cdf(1, scale=2)
```
# (Student's) t-distribution
- similar shape as the normal distribution, but not quite the same.
- This means that in a t-distribution, observations are more likely to fall further from the mean.
## Degrees of freedom
- The t-distribution has a parameter called degrees of freedom(df), which affects the thickness of the distribution's tails. 
	- Lower degrees of freedom results in thicker tails and a higher standard deviation. 
	- As the number of degrees of freedom increases, the distribution looks more and more like the normal distribution.
# Log-normal distribution
- Variable that follow a log-normal distribution have a logarithm that is normally distributed
- e.g:
	- length of chess games
	- adult blood pressure
	- number of hospitalizations in 2003 SARS outbreak
![[Introduction to statistics in python 3.pdf]]

# Correlation
## Relationships between two variables
- The variable on the x-axis is called the explanatory or independent variable, 
- and the variable on the y-axis is called the response or dependent variable.
## Correlation coefficient
- examine relationships between two numeric variables using a number called the correlation coefficient.
- is a number between -1 and 1, where 
	- the magnitude corresponds to the strength of the relationship between the variables, 
		- - correlation coefficient of 0.99 - this as a near-perfect or very strong relationship
		- If we know what x is, we'll have a pretty good idea of what the value of y could be.
		- x and y have a correlation coefficient of 0-point-75, and the data points are a bit more spread out.
		- x and y have a correlation of 0-point-56 and are therefore moderately correlated.
		- A correlation coefficient around 0-point-2 would be considered a weak relationship
		- When the correlation coefficient is close to 0, x and y have no relationship and the scatterplot looks completely random. This means that knowing the value of x doesn't tell us anything about the value of y. 
	- and the sign, positive or negative, corresponds to the direction of the relationship.
		- A positive correlation coefficient indicates that as x increases, y also increases. 
		- A negative correlation coefficient indicates that as x increases, y decreases.
### Visualizing relationships
- use seaborn, which is a plotting package built on top of matplotlib.
```python
import seaborn as sns
# msleep - DataFrame
sns.scatterplot(x='sleep_total', y='sleep_rem', data=msleep)
plt.show()
```
- adding a trend line - using seaborn's lmplot() function.
	- we'll set **ci to** **None** so that there aren't any confidence interval margins around the line.
```python
import seaborn as sns
# msleep - DataFrame
sns.lmplot(x='sleep_total', y='sleep_rem', data=msleep, ci=None)
plt.show()
```
### Computing correlation
- To calculate the correlation coefficient between two Series, use .corr() method.
- correlation between the sleep_total and sleep_rem columns of msleep, we can take the sleep_total column and call dot-corr on it, passing in the other Series we're interested in.
```python
msleep['sleep_total].corr(msleep['sleep_rem'])
```
- **correlation between x and y is the same thing as the correlation between y and x.**
- The method used here is Pearson product-moment correlation(r)
![[correlation types.png]]
## Correlation caveats
- The correlation coefficient measures the strength of linear relationships, and linear relationships only.
- Just like any summary statistic, correlation shouldn't be used blindly, and you should always visualize your data when possible.
## Log transformation
- When data is highly skewed, we can apply a log transformation using np.log()
```python
msleep['log_bodywt'] = np.log(msleep['bodywt'])

sns.lmplot(x='log_bodywt', y='awake', data=msleep, ci=None)
plt.show()
```
## Other transformations
- Log transformation(log(x))
- Square root transformation(sqrt(x))
- Reciprocal transformation (1/x)
- combinations of these, eg:
	- log(x) and log(y)
	- sqrt(x) and 1/y
## Why use transformation?
- Certain statistical methods rely on variables having a linear relationship, like calculating a correlation coefficient.
## Correlation doesn't imply causation
- This means that if x and y are correlated, x doesn't necessarily cause y
- if there is no any relation but high correlation, it is often called as *spurious correlation*.
- A phenomenon called confounding can lead to spurious correlations.
- In reality, it turns out that coffee does not cause lung cancer and is only associated with it, but it appeared causal due to the third variable, smoking. This third variable is called a confounder, or lurking variable.
# Design of experiments
- data is created as a result of a study that aims to answer a specific question.
- data needs to be analyzed and interpreted differently depending on how the data was generated and how the study was designed.
## Vocabulary
- Experiments generally aim to answer a question in the form, "What is the effect of the treatment on the response?
	- Treatment - explanatory or independent variable
	- response - response or dependent variable.
- what is the effect of an advertisement on the number of products purchased?
	- treatment - advertisement
	- response - no. of products purchased.
## Controlled experiments
- In a controlled experiment, participants are randomly assigned to either the treatment group or the control group, where the treatment group receives the treatment and the control group does not.
- Groups should be comparable, so that causation can be inferred.
### Gold standard of experiments will use certain tools
- Randomized controlled trial
	- participants are randomly assigned to the treatment or control group
	- choosing randomly helps ensure that groups are comparable.
- Placebo
	- resembles the treatment, but has no effect.
	- participants doesn't know which group they are in.
	- This is common in clinical trials that test the effectiveness of a drug. The control group will still be given a pill, but it's a sugar pill that has minimal effects on the response.
- Double-blind trial
	- the person administering the treatment or running the experiment also doesn't know whether they're administering the actual treatment or the placebo.
	- This protects against bias in the response as well as the analysis of the results.
- These different tools all boil down to the same principle:
> if there are fewer opportunities for bias to creep into your experiment, the more reliably you can conclude whether the treatment affects the response.
## Observational studies
- participants are not randomly assigned to groups. Instead, participants assign themselves, usually based on pre-existing characteristics.
- assignment isn't random, there's no way to guarantee that the groups will be comparable in every aspect, so observational studies can't establish causation, only association.
![[observational study.png]]
## Longitudinal vs. cross-sectional studies
![[differences between longitudinal vs cross-sectional studies.png]]
![[Introduction to statistics in python 4.pdf]]
