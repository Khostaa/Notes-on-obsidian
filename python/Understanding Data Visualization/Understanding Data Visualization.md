# A plot tells a thousand words
## Three ways of getting insights
### Calculating summary statistics
- mean, median, standard deviation
### Running models
- linear and logistic regression
### Drawing plots
- scatter, bar, histogram

Choosing type of plot depends upon whether your variables are Continuous or Categorical.
- Continuous: usually numbers
	- heights, temperatures, revenues
- Categorical: usually text
	- eye colors, countries, industry
- can be either
	- age is continuous, but age group is categorical
	- time is continuous, but month of year is categorical

# Histogram
- Histograms are a type of plot that takes one continuous variable as its input.
- it allows you to answer questions about the shape of that variable's distribution.
- For example, to know the highest, lowest and most common values.
- x-axis is the variable that we are interested in -  a variable is grouped into bins i.e, intervals and is plotted against another variable
- The appearance of histogram is strongly influenced by the *choice of binwidth.*
- Choosing a narrow or wide binwidth might cause problems
- In general, it is difficult to know the best binwidth before you draw the plot, so you'll need to experiment with several values.
- The appearance of a histogram is heavily influenced by the width of its _bins_: the intervals that determine where each bar lies on the x-axis. If the bins are too wide, you don't see enough detail in the shape of the distribution. If the bins are too narrow, the distribution can be obscured by noise. It's very difficult to know the "best" binwidth, until you physically look at the plot

## Modality: how many peaks?
- Unimodal - distribution with one peak
- Bimodal - distribution with two peaks
- Trimodal - distribution with three peaks, and so on.
![[modality.png]]
## Skewness: is it symmetric?
- whether or not distribution is symmetric or not
- **Left-skewed** : has outliers, i.e, extreme values on left.
- **Right-skewed** : has outliers i.e, extreme values on the right
- a left-skewed distribution, the skewer points leftwards, and in a right-skewed distribution, the skewer points rightwards.
![[skewness.png]]

## Kurtosis: how many extreme values?
- kurtosis of distribution affects the number of outliers.
- A leptokurtic distribution has a narrow peak and lots of extreme values.
- A mesokurtic distribution is something that looks like the bell curve from a normal distribution.
- A platykurtic distribution has a broad peak and few extreme values.
![[kurtosis.png]]

# Box Plots
- Box plot splits a continuous variable by a categorical variable and allows us to compare the resulting distribution in a space-efficient way.
- Middle Line - median of distribution
- Box extends from lower quartile to upper quartile
	- lower quartile - point where one quarter of values are below it - Q1
	- upper quartile - point where 3 quarter of values are below it - Q3
	- Interquartile range (IQR) = upper quartile - lower quartile
- horizontal lines, "Whiskers" : each extends to one and a half times the interquartile range, but then are limited to reaching actual data points.
	- smallest value greater than lower quartile minus 1.5 times IQR
	- largest value less than upper quartile plus 1.5 times IQR
- Points are extreme values, that is, values that are outside the range of the whiskers.
![[Understanding data visualization 1.pdf]]
# Scatter plots
## when to use?
- when you have two continuous variables
- when you want to answer questions about the relationships between two variables.

- For a scatter plot of price versus area: you'd say: it's a scatter plot of "Price versus Area"
	- can also be described in Logarithmic plot

## Correlation
- Correlation is a measure of how well you can draw a straight line through points
- if that straight line goes upwards as you move to right, it's called a Positive Correlation
- if the line goes down as you move right, it's called negative correlation.
![[correlation graphs.png]]
The red line in each panel shows what perfect negative correlation would look like. The green lines show perfect positive correlation. In the left-most panel.
- strong negative correlation - x value increase, y value decreases
- strong positive correlation - x value increase, y value increases
- middle panel show intermediate states
- 3rd panel - shows no correlation, the values of y are completely unrelated to values of x.

- For complicated shape, you'll need to be more creative in how you describe the relationship.

## Adding trend lines
- adding trend lines in scatter plot is a great way to see if you have linear relationship between x and y variables.
- sometimes straight line might be a terrible fit.
- When a straight trend line is a poor fit, one alternative is to use a curve.

# Line plots
## When to use?
- when you have two continuous variables
- when you want to answer questions about their relationship
- consecutive observations are connected somehow

Usually, but now always, the x-axis is dates or times.
- Multiple lines can be drawn on the same plot and compare them.
- When a straight trend line is a poor fit, one alternative is to use a curve.

## Trend lines
sometimes when linear trend line is poor fit, Transforming the plot to use a logarithmic scale before fitting the trend line could be much better fit.

- Time x-axis doesn't always imply the line plot
- You don't always need dates or times on the x-axis.

# Bar plots
- Most common case
	- you have a categorical variable
	- you want counts or percentage of each category
- Occasionally
	- you want another numeric score for each category, and need to include zero in the plot.
- you usually sort the bars by the count
- To make it easier to read, values in x and y axis could be swapped
- bars could be stacked on top of each other

## Differences between box plots and bar plots

box plot - designed to answer about the spread of variable
bar plot - designed to answer questions about a singe metric.

# Dot plots
- when you have categorical variable
- to display numeric scores for each category on a log scale,
- to display multiple numeric scores for each category.
![[Understanding data visualization 2.pdf]]

# Higher dimensions
- To visualize more than one or two dimensions.
- ways of drawing more than two dimensions on a flat screen:
	- color
	- size
	- transparency
	- shape
	- lots for panel
		- to draw panels for different subsets of the dataset.
	- line type(solid, dashes, dots)

## Colorspace for Data visualization
- Hue-chroma-luminance
	- designed to deal with issues of color perception.
- Hue is like color of rainbow, from red, through orange, green and blue, to purple and back to red
- Chroma is the intensity of color from grey to a bright color
	- you can go from grey to any other hue.
- luminance is the brightness of color, from black to white.
	- can go from black through cyan to white or black through red to white
![[colorspaces for data visualization.png]]

## Types of color scale
| Type        | Purpose                          | what to vary                        |
| ----------- | -------------------------------- | ----------------------------------- |
| qualitative | Distinguish unordered categories | hue (constant chroma and luminance) |
| sequential  | show ordering                    | chroma or luminance                 |
| diverging   | Show above or below a midpoint   | chroma or luminance with 2 hues     |
- Diverging type has sequential scale but neutral  color like white or gray in the middle, and have increasingly bold colors with different hues on either edge.

## Plotting many variables at once
- Pair plot work with up to about 10 variables at once and they show the distribution of each variable, and relationship between each pair of variables.
- Panel on the diagonal show the distribution of variables.
- Panels off the diagonal show the relationships between pairs of variables.
- When both variables are continuous, you see scatter plots of each pair of variables, and their correlation.
- When comparing a categorical variable to a continuous variable you get a box plot and a histogram of the continuous variable split by the categorical variable.
- Pair plots can be tremendously helpful for quickly exploring a new dataset.
- For the special case where you have many continuous variables, a close relative of the pair plot called a correlation heatmap is simpler, and scales to visualizing even more variables at once.
	- The idea is that you draw a pair plot, only including the panels for correlations, but instead of showing numbers, you show a color.
	- Correlation heatmaps are designed to show relationships between pairs of continuous variables. They are compact, so you can easily compare tens of variables at once.
- with four or more variables scatter plots can quickly become complicated to interpret.
### When should you use a correlation heatmap?
- when there are lots of continuous variables
- when you want a simple overview of how each pair of variables is related.
### when should you use a parallel coordinates plot
- when you have lots of continuous variables
- when you want to find patterns across these variables
- when you want to visualize clusters of observations.
![[Understanding data visualization 3.pdf]]

# Polar coordinates
- If you convert the coordinate system for the plot from Cartesian coordinates, that is, standard x and y axes, to polar coordinates, you get a pie plot.
- A pie plot is just a bar plot where the bar lengths are converted to angles.
- pie plot is harder to interpret than the bar plot

## when to use polar coordinates?
- almost never
- if you have a variable that is naturally circular(time of day, compass direction)

## Histogram + polar coords = rose plot
- convert the histograms to polar coordinates, forming a rose plot
- This is slightly different to the pie plot because it's the x-axis that is converted to angles, and the bar heights still remain as lengths.

# Axes of evil
- fundamental to bar plots is that the length of each bar is proportional to whatever value it represents.
- Problems with stacked bar plots
	- y -axis starting from points other than zero.
	- using two y-axes
		- This is typically done when you want to plot two things on the y-axis with very different scales
		- A much better solution is to admit that you are trying to plot two different things, and keep them in separate panels, so it's clear to your audience that they are different metrics.
# Sensory Overload
## Measures of good visualization
- how many interesting insights can your reader get from the plot?
- how quickly can they get the insights?
	- If your plot is being presented in a meeting, you might reasonably expect your audience to concentrate on your plot for twenty seconds. Often, you need to get your message across quickly.

# Chartjunk
- Chartjunk refers to anything in the plot that makes it harder for the reader to get insight into the data.
- Common problems
	- pictures
		- e.g: Using a picture of a man instead of a bar makes things harder to understand, not easier.
	- Skeuomorphism: reflections, shadows, etc.
		- Skeuomorphism: That means adding things that happen in the real world to virtual objects.
		- The 3D aspect makes it harder to accurately judge where they lie against the y-axis, so the bar heights have to be written in text to compensate. By stripping away all the junk, the data is easier to see.
	- Extra dimensions
		-  Bar plots are inherently two dimensional. You have categories on one axis, and a continuous variable on the other axis.
		- A 2D bar plot is easier to read.
	- Ostentatious colors or lines
		- In general, stripes or other forms of hatching should be avoided in plots because they're just plain difficult to stare at.
		- By removing the hatching, it's much nicer to look at the plot.
![[Understanding data visualization 4.pdf]]
