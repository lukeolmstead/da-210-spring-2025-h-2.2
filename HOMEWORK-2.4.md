---
jupyter:
  jupytext:
    formats: md,ipynb
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.6
  kernelspec:
    display_name: Python [conda env:base] *
    language: python
    name: conda-base-py
---

[Luke Olmstead]

# DA 210 -- Spring 2025 -- Homework 2.4 -- Professor Lavin

## Directions 

1. These questions will _mostly_ focus on tabular data and Pandas, which will likely include new material, as well as some review and deepening of CS-11x.
2. Don't forget to add your name above. You can edit the markdown by double-clicking on the cell. 
3. Save your work often and commit your changes using git/Github Desktop.
4. When you are finished, save your work, convert the Jupytext Notebook to .html format, and submit the HTML file on Canvas.
5. When you have completed homework 2.1 - 2.4, push your updated repo to Github.com.

__Reminders:__ 

- You are not permitted to get the answers from a classmate or to use Github Copilot, chatGPT, etc. on this homework. These exercises are for practice so, if you use outside help in a way that's not permitted, you are only cheating yourself out of a chance to learn and prepare for future quizzes and tests. 
- Working with an ARC tutor and visiting our TA's office hours are both permitted, but they should be provide advice and support, and you should not expect them to do your work for you. 


---

## Load Data

Copy/paste the following code block to the code cell below and make sure it runs without error:

```
import pandas as pd 

# load sample csv
df_gss_sample = pd.read_csv('data/gss_sample.csv', index_col=0, low_memory=False, encoding='utf8') 

# load rows counts of full data
gss_full_row_counts = pd.read_csv('data/gss_full_row_counts.csv', index_col=0, low_memory=False, encoding='utf8')

# load years per variable data
gss_years_per_var = pd.read_csv('meta/gss_data_years_per_var.csv', index_col=0, low_memory=False, encoding='utf8')

# load data dictionary
gss_data_dictionary =  pd.read_csv('meta/gss_data_dictionary.csv', index_col=0, low_memory=False, encoding='latin1')
```


---

## Question 1

In the code cell below, perform the following steps: 

1. Using only basic column assignment methods, use the respondent's `age` and `agewed` values in `df_gss_sample` to derive a new column called `years_since_married` that represents the number of years since the respondent was married. 
2. Using only basic column assignment methods, use the `year` and `years_since_married` variables in `df_gss_sample` to derive a new column called `approx_year_wed` that represents the approximate year the respondent was married. 
3. Display the first ten rows of the columns `year`, `age`, `agewed`, `marital`, `years_since_married`, and `approx_year_wed` in the DataFrame `df_gss_sample`

```python
import pandas as pd 

# load sample csv
df_gss_sample = pd.read_csv('data/gss_sample.csv', index_col=0, low_memory=False, encoding='utf8') 

# load rows counts of full data
gss_full_row_counts = pd.read_csv('data/gss_full_row_counts.csv', index_col=0, low_memory=False, encoding='utf8')

# load years per variable data
gss_years_per_var = pd.read_csv('meta/gss_data_years_per_var.csv', index_col=0, low_memory=False, encoding='utf8')

# load data dictionary
gss_data_dictionary =  pd.read_csv('meta/gss_data_dictionary.csv', index_col=0, low_memory=False, encoding='latin1')


df_gss_sample['years_since_married'] = df_gss_sample['age'] - df_gss_sample['agewed']

df_gss_sample['approx_year_wed'] = df_gss_sample['year'] - df_gss_sample['years_since_married']

print(df_gss_sample[['year', 'age', 'agewed', 'marital', 'years_since_married', 'approx_year_wed']].head(10))

```

---

## Question 2

In the code cell below, perform the following steps: 

1. Write a function called `translate_regions` that takes a `DataFrame` row as its input. Assuming that the input `DataFrame` has the exact structure of `df_gss_sample`, write the function so that it converts each numerical code in the `reg16` and `region` columns respectively into their appropriate semantic/string categories.
2. Call the function on `df_gss_sample` using the `apply()` method and capture the results as new columns in `df_gss_sample` called `reg16_trans` and `region_trans` respectively.
3. Display the first ten rows of the columns `reg16`, `region`, `reg16_trans`, and `region_trans` in the DataFrame `df_gss_sample`

__Hint:__ Use the`regions` dictionary in the code cell below in your function. You may also need to handle some cases where the column value is not found in the dictionary.

```python
regions = {0: 'foreign', 1: 'new england', 2: 'middle atlantic', 3: 'east north central',  4: 'west north central', 5: 'south atlantic', 6: 'east south atlantic', 7: 'west south central', 8: 'mountain', 9: 'pacific'}

def translate_regions(row):
    reg16_trans = regions.get(row['reg16'], "Unknown") if pd.notna(row['reg16']) else "Unknown"
    region_trans = regions.get(row['region'], "Unknown") if pd.notna(row['region']) else "Unknown"
    return pd.Series([reg16_trans, region_trans])

df_gss_sample[['reg16_trans', 'region_trans']] = df_gss_sample.apply(translate_regions, axis=1)

print(df_gss_sample[['reg16', 'region', 'reg16_trans', 'region_trans']].head(10))
```

---

## Question 3

In the code cell below, perform the following steps: 

1. Subset the `df_gss_sample` DataFrame so that you are working only with the `prestg10` and `sibs` columns.
2. Using `groupby` and `agg` methods, group your subset DataFrame on the respondent's number of siblings and display summary columns for: (a) the mean `prestg10` for each `sibs` count; and (2) the number of rows (n) used for each mean value.
3. Display all 28 rows of the grouped and aggregated DataFrame in the code cell below
4. In the markdown cell below, explain whether the mean `prestg10` scores suggest a relationship between professional prestige and number of siblings.


```python
subset = df_gss_sample[['prestg10', 'sibs']]

sibs = subset.groupby('sibs').agg(mean_prestg10=('prestg10', 'mean'), n=('prestg10', 'count')).reset_index()

print(sibs.to_string(index=False))
```

The data above suggests that there may be a slight negative relationship between the number of siblings and professional prestige prestg10. As the number of siblings increases, the mean prestg10 score decreases. For example, individuals with no siblings have a higher mean prestige score of 47.3, while those with more than 10 siblings have lower scores, with the mean dropping to 28 for 27 siblings. A possible factor that influences this relationship between the number of siblings and prestg10 could be resource allocation within families. Larger families may face greater and higher financial constraints, leading to less access to education or career development. With more siblings, the family's resources such as, time and money may be spread thinner, potentially limiting opportunities for higher education, which would lead to lower prestige occupations. 


---

## Question 4

In the code cell below, perform the following steps: 

1. Building on Question 3, alter your subset from the `df_gss_sample` DataFrame so that you are working with the `fund16` column (how fundamentalist was the respondent at age 16), in addition to the `prestg10` and `sibs` columns.
2. Using `groupby` and `agg` methods, group the subset DataFrame on the `sibs` column, and subgroup on the `fund16` column. Display summary columns for: (a) the mean `prestg10` for each `sibs` count; and (b) the number of rows (n) used for each mean value for each combination of `fund16` and `sibs` values. 
3. Display the entirety of the grouped and aggregated DataFrame in the code cell below
4. In the markdown cell below, explain how controlling for religiousity in this way affects your interpretation of the association between professional prestige and number of siblings.

```python
subset = df_gss_sample[['prestg10', 'sibs', 'fund16']]

groups = subset.groupby(['sibs', 'fund16']).agg(mean_prestg10=('prestg10', 'mean'), n=('prestg10', 'count') ).reset_index()

print(groups.to_string(index=False))
```

Controlling for religiosity allows us to better understand how it influences the relationship between professional prestige and the number of siblings. By accounting for religiosity, we can see if the association between these two variables is directly influenced by religious beliefs or practices. This helps clarify whether the relationship between professional prestige and the number of siblings is stronger or weaker depending on someone's religious background, offering a more accurate interpretation of the data. Religion might play a part because religious beliefs and practices can shape family dynamics, values, and decisions about having children. Some religious traditions encourage larger families, which could influence the number of siblings a person has. Additionally, religion may impact career choices or views on professional success, potentially affecting how individuals prioritize professional prestige. By controlling for religiosity, we can account for these factors, allowing for a clearer understanding of the relationship between professional prestige and the number of siblings without the influence of religious beliefs.


```python

```
