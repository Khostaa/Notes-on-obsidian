Access Data -> Explore and Process Data -> Extract Insights -> Report Insights

- Dirty data can appear because of duplicate values, mis-spellings, data type parsing errors and legacy systems.
- without making sure that data is properly cleaned in the exploration and processing phase, we'll surely compromise the insights and reports subsequently generated.

# Data type constraints
## Python data type
- str
- int
- float
- bool
- datetime
- category

## Strings to Integers
- Pandas uses 'object' to store strings.
```python
# Get DataFrame information
sales.info()

# to remove $ sign from Revenue column
# use .str.strip() method, specifying the string we want to strip as an argument
sales['Revenue'] = sales['Revenue'].str.strip("$")

# change revenue column to an integer by using .astype() method, specifying the desired data type as argument
sales['Revenue'] = sales['Revenue'].astype("int")

# revenue values were decimal, Revenue column need to be converted to float

# Verify that Revenue is now an integer
assert sales['Revenue'].dtype == 'int'
# if this statement is not True, raises 'Assertion error.'

```
## Categorical data
A common type of data seems numeric but actually represents categories with a finite set of possible categories. This is called categorical data.

```python
# know summary statistics of column of DataFrame
df['marriage_status'].describe()

# the summary statistics are much more aligned with that of a categorical variable for this DataFrame, discussing the number of observations, number of unique values, most frequent category instead of mean and standard deviation.

# convert to categorical
df['marriage_status'] = df["marriage_status"].astype('category')
```
# Data range constraints
```python
# to print first five entries of dataframe
movies.head()
```
- There is likely an error in data collection or parsing, when a variable is well beyond its range and treating it is essential to have accurate analysis.

## How to deal with out of range data?
- Dropping data
	- The simplest option is to drop the data. However, depending on the size of your out of range data, you could be losing out on essential information. As a rule of thumb, only drop data when a small proportion of your dataset is affected by out of range values, however you really need to understand your dataset before deciding to drop values.
- Setting custom minimums and maximums to your column
- Treat the data as missing and impute it.
- Setting custom value depending on business assumptions

### Dropping data
```python
# Movie example
import pandas as pd

# isolate the movies with rating higher than 5
movies[movies['avg_rating'] > 5]

# datas can be dropped in two different ways
# 1. Drop values using filtering
# create a new filtered movies DataFrame where we only keep values of avg_rating lower than or equal to 5
movies = movies [movies['avg_rating'] <=5]

# 2. Drop using .drop() method
# .drop() method takes in as argument the r                       ow indices of movies for which the avg_rating is higher than 5
# setting *inplace* arguement to *True* so that values are dropped in place and we don't have to create a new column.

movies.drop(movies[movies['avg_rating'] > 5].index, inplace = True)

# Assert results
assert movies['avg_rating'].max() <= 5

# changing out of range value to hard limit
# doen using .loc() method
	# returns all cells that fit a custom row and a column index.
	# takes 1st argument as row index, in code below - all instances of avg_rating above 5
	# takes 2nd argument as column argument, which is here the avg_rating column.


# convert avg_rating > 5 to 5
movies.loc[movies['avg_rating'] > 5, 'avg_rating'] = 5
```

# What are duplicate values?
- Duplicate values can be diagnosed when we have the same exact information repeated across multiple rows, for a some or all column in our DataFrame.
## why do they occur?
- Data entry and human error
- join or merge errors
- bugs and design errors

## How to find duplicate values?
- using **.duplicated()** method
- returns a Series of boolean values that are True for duplicate values, and False, for non-duplicated values.
```python
# get duplicates across all columns
dupicates = height_weight.duplicated()
print(duplicates) 
```
- see exactly which rows are affected  by using as such:
```python
height_weight[duplicates]
```
- without playing around with the arguments of the method can lead to misleading results, as all the columns are required to have duplicate values by default, with all duplicate values being marked as True except for the first occurrence. This limits our ability to properly diagnose what type of duplication we have, and how to effectively treat it.
- To properly calibrate finding duplicates:
	- *subset* argument: List of column names to check for duplication.
	- *keep* argument: Whether to keep first('*first*'), last('*last*') or all ('*False*') duplicate values.
- The keep argument lets us keep the first occurrence of a duplicate value by setting it to the string first, the last occurrence of a duplicate value by setting it the string last, or keep all occurrences of duplicate values by setting it to False

- checking for duplicates across the first name, last name, and address variables, and we're choosing to keep all duplicates.
```python
# column names to check for duplication
column_names = ['first_name', 'last_name', 'address']
duplicates = height_weight.duplicated(subset = column_name, keep = False)

# output duplicate values
height_weight[duplicates]
```
## finding duplicate rows
```python
height_weight[duplicates].sort_values(by = 'row_name')
```
## treat duplicate values
- for complete duplicates, all that is required is to keep one of them only and discard the others.
 - using **.drop_duplicates()** method

```python
- subset : List of column names to check for duplication
- keep : Whether to keep first ('first'), last('last') or all('False') duplicate values.
- inplace : Drop duplicated rows directly inside DataFrame without creating new object (True).

# drop duplicates
# dropping complete duplicates only, so it's not necessary nor advisable to set a subset, and since the keep argument takes in first as default, we can keep it as such. Note that we can also set it as last, but not as False as it would keep all duplicates.
height_weight.drop_duplicates(inplace = True)
```

```python
# output duplicate values
column_names = ['first_name', 'last_name', 'address']
duplicates = height_weight.duplicated(subset = column_names, keep = False)
height_weight[duplicates].sort_values(by= 'first_name')
```
- we can use a statistical measure to combine each set of duplicated values. we can combine these rows into one by computing the average mean between them, or the maximum, or other statistical measures, this is highly dependent on a common sense understanding of our data, and what type of data we have.
- using *grouby()* method chained with *agg()* method.
-  lets you group by a set of common columns and return statistical values for specific columns when the aggregation is being performed.
```python
# group by column names and produce statistical summaries
column_names = ['first_name', 'last_name', 'address']
summaries = {'height': 'max', 'weight': 'mean'}
height_weight = height_weight.groupby(by = column_names).agg(summaries).reset_index()

```
 For example here, we created a dictionary called summaries, which instructs groupby to return the maximum of duplicated rows for the height column, and the mean duplicated rows for the weight column. We then group height_weight by the column names defined earlier, and chained it with the agg method, which takes in the summaries dictionary we created. We chain this entire line with the dot-reset_index() method, so that we can have numbered indices in the final output. We can verify that there are no more duplicate values by running the duplicated method again, and use brackets to output duplicate rows.    

![[Cleaning Data in Python 1.pdf]]
# Membership constraints

- categorical data represent variables that represent predefined set of categories.
e.g: marriage status: married, unmarried
	Loan status: default, payed, no_load

- To run machine learning models on categorical data, they are often coded as numbers. Since categorical data represent a predefined set of categories, they can't have values that go beyond these predefined categories.

- Inconsistencies in our categorical data for a variety of reasons
	- data entry issues with free text vs dropdown fields
	- data parsing errors
	- other types of erros

- How to treat these problems
	- drop the rows with incorrect categories
	- remapping incorrect categories to correct ones
	- Inferring categories

- It's always good practice to keep a log of all possible values of your categorical data, as it will help us systematically spot all rows with inconsistencies.

## A note on joins
- Anti joins, take in two DataFrames A and B, and return data from one DataFrame that is not contained in another.
	- example, we are performing a left anti join of A and B, and are returning the columns of DataFrames A and B for values only found in A of the common column between them being joined on.
	- What is in  A and not in B
-  Inner joins, return only the data that is contained in both DataFrames.
	- For example, an inner join of A and B, would return columns from both DataFrames for values only found in A and B, of the common column between them being joined on.
	- what is both in A and B
- To drop inconsistent rows and keep ones that are only consistent. We just use the **tilde** symbol while subsetting which returns everything except inconsistent rows.
```python
# getting incosistent categores from blood_type column by deducting all the categories.
inconsistent_categories = set(study_data['blood_type']).difference(categories['blood_type'])

# get and print rows with inconsistent categories
inconsistent_rows = study_data['blood_type'].isin(incosistent_categories)
study_data[inconsistent_rows]

# Drop inconsistent categories and get consistent data only
consistent_data = study_data[~inconsistent_rows]

```

## Categorical variable
### what type of errors could we have?
- value inconsistency
- collapsing too many categories to few
- making sure data is of type *category*

#### Value consistency
```python
# Capitalization - problem
# e.g: 'married', 'Married', "UNMARRIED", "unmarried"...

# Get marriage status column
marriage_status = demographics['marriage_status']
marriage_status.value_counts() # .value_counts() - works on Series only

# Get value counts on DataFrame
marriage_status.groupby('marriage_status').count()

# Capitalize
marriage_status['marriage_status'] = marriage_status['marriage_status'].str.upper()
marriage_status['marriage_status'].value_counts()

# Lowercase
marriage_status['marriage_status'] = marriage_status['marriage_status'].str.lower()
marriage_status['marriage_status'].value_counts()
```

```python
# Leading or Trailing spaces
# e.g: 'married ', 'married', 'unmarried', ' unmarried'...

# Get marriage status column
marriage_status = demographics['marriage_status']
marriage_status.value_counts()

# Strip all spaces
demographics = demographics['marriage_status'].str.strip()
demographics['marriage_status'].value_counts()
```

#### Collapsing data into categories
- create categories out of data: *income_group* column from *income* column.
- to create categories out of data it can be done in two ways
```python
# using qcut()
# divides data based on its distribution into number of categories set in q argument
# may misrepresents group as we don't instrut qcut where the ranges actually lie
import pandas as pd
group_names = ['0-200k', '200k-500k', '500k+']
demographics['income_group'] = pd.qcut(demographics['household_income'], q = 3, labels = group_names)

# pring income_group column
demographics[['income_group', 'household_income]]
```

```python
# Using cut() - create category ranges and names
import numpy as np
ranges = [0, 200000, 500000, np.inf] # np.inf - infinity 
group_names = ['0-200k', '200k-500k', '500k+']

# Create income group column
demographics['income_group'] = pd.cut(demographics['household_income'], bins= ranges, labels = group_names)

demographis[['income_group', 'household_income']]
```

```python
# map categories into fewer ones: reducing categories in categorical column

# Operating_system* column is: 'Microsoft', 'MacOS', "IOS", 'Android', "Linux"
# Operating system column should become: 'DesktopOS', "MobileOS"

# create mapping dictionary and replace
mapping = {'Microsoft':'DesktopOS', 'MacOS':'DesktopOS', 'Linux':'DesktopOS', 'IOS':'MobileOS', 'Android':'MobileOS'}

devices['operating_system'] = devices['operating_system'].replace(mapping)
devices['operating_system'].unique()

```
# Cleaning text data
- common text data problems
	- Data inconsistency
	- Fixed length violations
	- Typos
```python
# read a CSV file
phones = pd.read_csv('phones.csv')
print(phones)

# Fixing the phone number column
# Replace '+' with "00"
phones["Phone number"] = phones["Phone number"].str.replace("+", "00")
phones

# Replace "-" with nothing
phones['Phone number'] = phones["Phone number"].str.replace("-", "")
phones

# Replace phone numbers with lower than 10 digits to NaN
digits = phones['Phone number'].str.len()
phones.loc[digits < 10, "Phone number"] = np.nan
phones

# checking
# find the length of each row in phone number column
sanity_check = phone['Phone number'].str.len()

# Assert minimum phone number length is 10
assert sanity_check.min() >= 10

# Assert all numbers do not have "+" or "-"
assert phone['Phone number'].str.contains("+|-").any() == False

## Remember *assert* returns nothing if condition passes
```

## For Complicated examples
- Regular expression give us ability to search for any pattern in text data, like only digits
```python
# Replace anything that is not a *Digit* with nothing
phones['Phone number'] = phones['Phone number'].str.replace(r'\D+', '')
```
![[Cleaning Data in Python 2.pdf]]

# Uniformity
```python
# Reading a CSV file
temperatures = pd.read_csv('temperatures.csv')
temperatures.head()

## Identifying if outlier is present or not using graphs
# Import matplotlib
import matplotlib.pyplot as plt
# Create scatter plot
plt.scatter(x = 'Date', y='Temperature', data = temperatures)

# Create title, xlabel and ylabel
plt.title("Temperature in Celcius March 2019 - NYC")
plt.xlabel('Dates')
plt.ylabel('Temperatures in Celcius')

# Shot plot
plt.show()

# Treating temperatures data
# some Fahrenheit data are present so, converting them into Celcius
temp_fah = temperatures.loc[temperatures['Temperature'] > 40, 'Temperature']
temp_cels = (temp_fah - 32)* (5/9)
temperatures.loc[temperatures['Temperature'] > 40, 'Temperature'] = temp_cels

# Assert conversion is correct
assert temperatures['Temperature'].max() < 40
```

## Datetime Formatting
- *datetime* is useful for representing dates
- **pandas.to_datetime()**
	- can recognize most formats automatically
	- sometimes fails with erroneous or unrecognizable formats
	- The *pandas.to_datetime()* function automatically accepts most date formats, but could raise errors when certain formats are unrecognizable.
- these inconsistencies can easily be treated by converting date column to datetime.

## Treating date data
```python
# converts to datetime - but won't work
birthdays['Birthday'] = pd.to_datetime(birthdays['Birthday'])

# will work!
birthdays['Birthdays'] = pd.to_datetime(birthdays['Birthday'], infer_datetime_format = True, errors = 'coerce')
# infer_datetime_format - attempt to infer format of each date
# errors = 'coerce' i.e, return NA for rows where conversion failed.
# This will infer the format and return missing value for dates that couldn't be identified and converted instead of a value error.

# another way
birthdays['Birthday'] = birthdays['Birthday'].dt.strftime("%d-%m-%Y")
birthdays.head()
```
### Treating ambiguous date data
- is *2019-03-08* in August or March?
	-  convert to *NA* and treat accordingly.
	- infer format by understanding the data source.
	- infer format by understanding the previous and subsequent data in DataFrame
---
ambiguous dates require a thorough understanding of where your data comes from. Diagnosing problems is the first step in finding the best solution!

```python
# Find values of acct_cur that are equal to 'euro'
acct_eu = banking['acct_cur'] == 'euro'

  
# Convert acct_amount where it is in euro to dollars
banking.loc[acct_eu, 'acct_amount'] = banking.loc[acct_eu, 'acct_amount'] * 1.1

  
# Unify acct_cur column by changing 'euro' values to 'dollar'
banking.loc[acct_eu, 'acct_cur'] = 'dollar'
 

# Assert that only dollar currency remains
assert banking['acct_cur'].unique() == 'dollar'
```

# Cross field validation
- Common challenge when merging data from multiple sources is data integrity, or more broadly making sure that our data is correct.
- Cross field validation is the use of multiple fields in dataset to sanity check the integrity of data.
- example: summing economy, business and first class values and making sure that are equal to total passengers on the plane
```python
import pandas as pd

flights = pd.read_csv('flights.csv')
flights.head()

# axis = 1: row
sum_classes = flights[['economy_class', 'business_class', 'first_class']].sum(axis = 1)

passenger_equ = sum_classes == flights['total_passengers']
# find and filter out rows with inconsistent passenger totals
inconsistent_pass = flights[~passenger_equ]
consistent_pass = flights[passenger_equ]
```

```python
# verify age of 'users'

import pandas as pd
import datetime as dt

# convert to datetime and get today's date
users['Birthday'] = pd.to_datetime(users['Birthday'])
today = dt.date.today()

# for each row in the birthday column, calculate year difference
age_manual = today.year - users['Birthday'].dt.year

# find instances where ages match
age_equ = age_manual == users['Age']

# find and filter out rows with inconsistent age
inconsitent_age = users[~age_equ]
consistent_age = users[age_equ]
```

## what to do when we catch inconsistencies?
- Dropping data
- set to missing and impute
- apply rules from domain knowledge

# Completeness
## What is a missing data?
- Missing data is when no data value is stored for a variable in an observation.
- it is commonly represented as *NA* or *NaN*, but can take arbitrary values like 0 or dot (.).
- causes due to technical or human errors.

```python
import pandas as pd
airquality = pd.read_csv('airquality.csv')
print(airquality)

# find rows with missing values using .isna() method
# .isna() - returns True for missing values and False for complete values across all our rows and columns

# Return missing values
airquality.isna()

# Get summary of missigness i.e returns a breakdown of missing values per column in the dataframe 
# by chaining .isna() with .sum() method
airquality.isna().sum() # returns no. of missing values in each column of dataframe
```

### Missingno
- useful package for visualizing and understanding missing data
```python
import missingno as msno
import matplotlib.pyplot as plt

# visualing missingness
msno.matrix(airquality)
plt.show()

# msno.matrix() - shows how missing values are distributed across a column
# in figure it shows co2 values are randomly scattered throughtout the column

# so lets isolate the rows of airquality with missing co2 values to confirm it

# isolate missing and complete values aside
missing = airquality[airquality['CO2'].isna()] # for missing co2 values
complete = airquality[~airquality['CO2'].isna()] # for complete co2 values

# Describe complete DataFrame
complete.describe()

# Describe missing DataFrame
missing.describe()
# shows missing values with mean tempr at -39 and min and max of -49 and -30 resp.

# sort the dataframe by temperature column
sorted_airquality = airquality.sort_values(by = 'Temperature')
msno.matrix(sorted_airquality)
plt.show()

# shows all missing values at top as sorted from smallest to largest temperature while plotting using msno.matrix()
```

## Missingness types
1. Missing completely at Random (MCAR)
	- no systematic relationship between missing data and other values
	- e.g: data entry errors when inputting data
2. Missing at Random (MAR)
	 - Systematic relationship between missing data and other observed value
	 - e.g: missing ozone data for high temperatures
	 - such as our CO2 data being missing for low temperatures.
3. Missing Not at Random (MNAR)
	- Systematic relationship between missing data and unobserved data
	- e.g: Missing temperature values for high temperatures.
	- For example, when it's really hot outside, the thermometer might stop working, so we don't have temperature measurements for days with high temperatures.

## How to deal with missing data?
- Simple approaches
	-  Drop missing data
	- Impute with statistical measures (mean, median, mode..)
- More complex approaches:
	- Imputing using an algorithmic approach
	- Impute with machine learning models


Each missingness type requires a specific approach, and each type of approach has drawbacks and positives, so make sure to dig deeper in DataCamp's course library on dealing with missing data.

## Dealing with missing data
- Drop missing values using .dropna() method along with subset argument which lets us pick which column's missing values to drop.
```python
airquality.head()

# Drop missing values
airquality_dropped = airquality.dropna(subset= ['CO2']).
airquality_dropped.head()

# Replacing with statistical measures
co2_mean = airquality['CO2'].mean()

# Replaces the missing values of CO2 using mean value of CO2 by using .fillna() method
# Fillna takes in a dictionary with columns as keys, and the imputed value as values
# We can even feed custom values into fillna pertaining to our missing data if we have enough domain knowledge about our dataset

airquality_imputed = airquality.fillna({'CO2': co2_mean})
airquality_imputed.head()
```
![[Cleaning Data in Python 3.pdf]]
# Comparing Strings
- discovering the world of record linkage

## Minimum edit distance
- is a systematic way to identify how close  2 strings are
- i.e, least possible amount of steps, that could get us from one word to another with operations
	- Inserting new characters
	- deleting them
	- substituting them
	- transposing consecutive characters
example: to get from "INTENTION" to "EXECUTION"
![[Minimum edit distance.png]]
		- DELETE I from intention and add C between E and N
		- substitute first N with E, T with X and N with U
		- this leads to minimum edit distance being 5.

- The lower the edit distance, the closer two words are
![[Typos for word, Reading.png]]

## Minimum edit distance algorithms

| Algorithm           | Operations                                        |
| ------------------- | ------------------------------------------------- |
| Damerau-Levenshtein | insertion, substitution, deletion, transportation |
| Levenshtein         | insertion, substitution, deletion                 |
| Hamming             | substitution only                                 |
| Jaro distance       | transposition only                                |
Possible Packages: **nltk**, **thefuzz**, **textdistance**

## Simple string comparison
- thefuzz is a package to perform string comparison
- use fuzz's WRatio function to compute the similarity between reading and its typo, inputting each string as an argument.
- For any comparison function using thefuzz, our output is a score from 0 to 100 with 0 being not similar at all, 100 being an exact match.
```python
from thefuzz import fuzz

# compare reeding vs reading
fuzz.WRatio('Reeding', 'Reading')
# 86
```
## Partial strings and different orderings
```python
# Partial string comparison
fuzz.WRatio('Houston Rockets', 'Rockets')
# 90

# Partial string comparison with different order
fuzz.WRatio("Houston Rockets vs Los Angeles Lakers", 'Lakers vs Rockets')
# 86
```
## Comparison with arrays
- using the extract function from the process module from fuzzy wuzzy.
- Extract takes in a string, an array of strings, and the number of possible matches to return ranked from highest to lowest.
- returns a list of tuples with 3 elements, the first one being the matching string being returned, the second one being its similarity score, and the third one being its index in the array.
```python
# import process
from thefuzz import process

# Define string and array of possible matches
string = 'Houston Rockets vs Los Angeles Lakers'
choices = pd.Series(['Rockets vs Lakers', 'Lakers vs Rockets', 'Houson vs Los Angeles', 'Heat vs Bulls'])

process.extract(string, choices, limit = 2)

# [('Rockets vs Lakers', 86, 0), ('Lakers vs Rockets', 86, 1)]
```
## Collapsing categories with string similarity
- use **.replace()** to collapse e.g: **"eur"** into **"Europe"**
- But what if we had so many inconsistent categories that a manual replacement is simply not feasible? We can easily do that with string similarity!
```python
print(survey['state'].unique())
```

## Collapsing all of the state
```python
# for each correct category
for state in categories['state']:
	# Find potential matches in states with typoes
	matches = process.extract(state, survey['state'], limit = survey.shape[0])

	# find each potential match match
	for potential_match in matches:
		# If high similarity score
		if potential_match[1] >= 80:
			# Replace typo with correct accuracy
			survey.loc[survey['state']] == potential_match[0], 'state'] = state
```
create a for loop iterating over each correctly typed state in the categories DataFrame. For each state, we find its matches in the state column of the survey DataFrame, returning all possible matches by setting the limit argument of extract to the length of the survey DataFrame. Then we iterate over each potential match, isolating the ones only with a similarity score higher or equal than 80 with an if statement. Then for each of those returned strings, we replace it with the correct state using the loc method.

# Generating Pairs
- to merge all the DataFrames together and have one DataFrame containing all unique elements.
- When there are different duplicate values in both DataFrames with different naming, there will be no common unique identifier between the DataFrames and as the elements are differently named, a regular join or merge will not work.
## Record Linkage
- Record linkage is a act of linking data from different sources regarding the same entity.
- Generally, we clean two or more DataFrames, generate pairs of potentially matching records, score these pairs according to string similarity and other similarity metrics, and link them. All of these steps can be achieved with the recordlinkage package.
![[how record linkage works.png]]
```python
# import recordlinkage
import recordlinkage

# Create indexing object
indexer = recordLinkage.Index()

# Generate pairs blocked on state column using .block() method with 'state' column as input
indexer.block('state')
pairs = indexer.index(census_A, census_B)

print(pairs)
```
The resulting object, is a pandas multi index object containing pairs of row indices from both DataFrames, which is a fancy way to say it is an array containing possible pairs of indices that makes it much easier to subset DataFrames on.
```python
# Generate the pairs
pairs = indexer.index(census_A, census_B)

# Create a Compare object
# responsible for assigning different comparison procedures for pairs.
compare_cl = recordlinkage.Compare()

# Let's say there are columns for which we want exact matches between the pairs. To do that, we use the exact method.
# find exact matches for pairs of date_of_birth and state
# .exact() method
	# takes column name in question for each DataFrame
	# a label argument which lets us set the column name in the resulting DataFrame.
compare_cl.exact('date_of_birth', 'date_of_birth', label = 'date_of_birth')
compare_cl.exact('state', 'state', label='state')
# find similar matches for pairs of surname and address_1 using string similarity

# to compute string similarities between pairs of rows for columns that have fuzzy values, we use the dot string method, which also takes in the column names in question, the similarity cutoff point in the threshold argument, which takes in a value between 0 and 1, which we here set to 0.85.
compare_cl.string('surname', 'surname', threshold = 0.85, label='surname')
compare_cl.string('address_1', 'address_1', threshold = 0.85, label = 'address_1)

# Find matches
# To compute matches - use the compute function, which takes in the possible pairs, and the two DataFrames in question.
potential_matches = compare_cl.compute(pairs, census_A, census_B)

print(potential_matches)
```
Note that you need to always have the same order of DataFrames when inserting them as arguments when generating pairs, comparing between columns, and computing comparisons.
potential_matches - The output is a multi index DataFrame, where the first index is the row index from the first DataFrame, or census A, and the second index is a list of all row indices in census B. The *columns are the columns being compared*, with **values being 1 for a match**, and **0 for not a match.**

```python
# To find potential matches
# filter for rows where the sum of row values in higher than a certain threshold
potential_matches[potential_matches.sum(axis = 1) => 2]
```

# Linking DataFrames
```python
# import recordlinkage and generate full pairs
import recordlinkage
indexer = recordLinkage.Index()
indexer.block('state')
full_pairs = indexer.index(census_A, census_B)

# Comparision step
compare_cl = recordlinkage.Compare()
compare_cl.exact('date_of_birth', 'date_of_birth', label = 'date_of_birth')
compare_cl.exact('state', 'state', label = 'state')
compare_cl.string('surname', 'surname', threshold = 0.85, label='surname')
compare_cl.string('address1', 'address_1', threshold = 0.85, label = 'address_1')

potential_matches = compare_cl.compute(full_pairs, census_A, census_B)

print(potential_matches)
```
- potential_matches is a multi-index DataFrame which have two index columns, record id 1 and record id 2.
- 1st index col. - stores indices from census_A
- 2nd index col. - stores all possible indices from census_B, for each row index of census_A
- The columns of our potential matches are the columns we chose to link both DataFrame on, where the value is 1 for a match, and 0 otherwise.

## Linking DataFrames
- 1st step is: to isolate the potentially matching pairs to the ones we're pretty sure of
```python
# Probable matches
# by subsetting the rows where the row sum is above a certain number of columns, in this case 3.
matches = potential_matches[potential_matches.sum(axis=1) >= 3]
print(matches)
# The output is row indices between census A and census B that are most likely duplicates.
```
- 2nd step - to extract one of index columns, and subsetting its  associated DataFrame to filter for duplicates.
- Here we choose the second index column, which represents row indices of census B. We want to extract those indices, and subset census_B on them to remove duplicates with census_A before appending them together.
```python
# to access a DataFrame's index using index attribute
matches.index
# since this is a multi index DataFrame, it returns a multi index object containing pairs of row indices from census_A and census_B respectively.
```

```python
# to extract all census_B indices, so we chain it with the get_level_values method, which takes in which column index we want to extract its values. We can either input the index column's name, or its order, which is in this case 1.
# Get indices from census_B only
duplicate_rows = matches.index.get_level_values(1)
print(census_B_index)

# Finding duplicates in census_B
census_B_duplicates = census_B[census_B.index.isin(duplicate_rows)]

# Finding new rows in census_B
# find non duplicates by adding tilde (~) sign at beginning of subset
census_B_new = census_B[~census_B.index.isin(duplicate_rows)]

# Link the DataFrames!
full_census = census_A.append(census_B_new)

```
![[Cleaning Data in Python 4.pdf]]
