---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.6
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

[Your Name Here]

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
# your code here 
```

---

## Question 2

In the code cell below, perform the following steps: 

1. Write a function called `translate_regions` that takes a `DataFrame` row as its input. Assuming that the input `DataFrame` has the exact structure of `df_gss_sample`, write the function so that it converts each numerical code in the `reg16` and `region` columns respectively into their appropriate semantic/string categories.
2. Call the function on `df_gss_sample` using the `apply()` method and capture the results as new columns in `df_gss_sample` called `reg16_trans` and `region_trans` respectively.
3. Display the first ten rows of the columns `reg16`, `region`, `reg16_trans`, and `region_trans` in the DataFrame `df_gss_sample`

__Hint:__ Use the`regions` dictionary in the code cell below in your function. You may also need to handle some cases where the column value is not found in the dictionary.

```python
# your code here 
```

---

## Question 3

In the code cell below, perform the following steps: 

1. Subset the `df_gss_sample` DataFrame so that you are working only with the `prestg10` and `sibs` columns.
2. Using `groupby` and `agg` methods, group your subset DataFrame on the respondent's number of siblings and display summary columns for: (a) the mean `prestg10` for each `sibs` count; and (2) the number of rows (n) used for each mean value.
3. Display all 28 rows of the grouped and aggregated DataFrame in the code cell below
4. In the markdown cell below, explain whether the mean `prestg10` scores suggest a relationship between professional prestige and number of siblings.


```python
# your code here 
```

```python
[Your markdown here]
```

---

## Question 4

In the code cell below, perform the following steps: 

1. Building on Question 3, alter your subset from the `df_gss_sample` DataFrame so that you are working with the `fund16` column (how fundamentalist was the respondent at age 16), in addition to the `prestg10` and `sibs` columns.
2. Using `groupby` and `agg` methods, group the subset DataFrame on the `sibs` column, and subgroup on the `fund16` column. Display summary columns for: (a) the mean `prestg10` for each `sibs` count; and (b) the number of rows (n) used for each mean value for each combination of `fund16` and `sibs` values. 
3. Display the entirety of the grouped and aggregated DataFrame in the code cell below
4. In the markdown cell below, explain how controlling for religiousity in this way affects your interpretation of the association between professional prestige and number of siblings.

```python
# your code here 
```

[Your markdown here]
