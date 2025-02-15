---
jupyter:
  jupytext:
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

Luke Olmstead
# DA 210 -- Spring 2025 -- Homework 2.1 -- Professor Lavin

## Directions 

1. These questions will _mostly_ focus on tabular data and Pandas, which will likely include new material, as well as some review and deepening of CS-11x.
2. Don't forget to add your name above. You can edit the markdown by double-clicking on the cell. 
3. Save your work often and commit your changes using git/Github Desktop.
4. When you are finished, save your work, convert the Jupytext Notebook to .html format, and submit the HTML file on Canvas.
5. When you have completed homework 2.1 - 2.4, push your updated repo to Github.com.

__Reminders:__ 

- You are not permitted to get the answers from a classmate or to use Github Copilot, chatGPT, etc. on this homework. These exercises are for practice so, if you use outside help in a way that's not permitted, you are only cheating yourself out of a chance to learn and prepare for future quizzes and tests. 
- Working with an ARC tutor and visiting our TA's office hours are both permitted, but they should be provide advice and support, and you should not expect them to do your work for you. 


## Question 1

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

Print the `dtype` of the following variables:

- `df_gss_sample['sex']` 
- `df_gss_sample['hrs1']`
- `df_gss_sample['happy']`
- `df_gss_sample['sibs']`
- `gss_data_dictionary['variable']`
- `gss_data_dictionary['var_doc_label']`
- `gss_data_dictionary['missing']`

__Note:__ The need for 'utf8' and 'latin1' parameters may vary by operating system. If you have errors, try loading each csv in separate blocks, and omit `encoding` argument as needed. 

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

print(df_gss_sample['sex'])
print(df_gss_sample['hrs1'])
print(df_gss_sample['happy'])
print(df_gss_sample['sibs'])
print(gss_data_dictionary['variable'])
print(gss_data_dictionary['var_doc_label'])
print(gss_data_dictionary['missing'])
```

In the markdown cell below, fill in the markdown table address whether each datatypes is appropriate for the variable it contains and why.


---

## Question 2

In the code cell below manipulate the `gss_years_per_var` DataFrame by dropping the `year` column and renaming the `year_main` column to `year`. Save the result as a new variable called `gss_years_per_var_renamed` and, finally, print the dtype of the new `year` column.

```python
gss_years_per_var_renamed = gss_years_per_var.drop(columns=['year']).rename(columns={'year_main' : 'year'})

print(gss_years_per_var_renamed['year'].dtype)
```

<!-- #region jp-MarkdownHeadingCollapsed=true -->
---

## Question 3

We can get the sum of every `True` value for every column in `gss_years_per_var` using some code that looks like this: 

```
year_sums = pd.DataFrame(gss_years_per_var.sum())

```

Write some code below that uses the `loc` method to get the name of every variable that has a `True` value for all 34 year represented in the dataset (1972-2022). Make sure you print your result. 
<!-- #endregion -->

```python
year_sums = gss_years_per_var.sum()

variables_all_years = year_sums.loc[year_sums == 34]

print(variables_all_years.index.tolist())
```

---

## Question 4

In the markdown cell below, use information from our metadata files and the GSS website to answer the following questions:

1. What is the purpose of the GSS? How did it originate? How is it conducted, and who participates? What kinds of questions are on the survey, and how have the questions have changed over time?
2. What are the `occ`, `occ10`, `occ80` variables, and why do we have three different variables representing something so similar? Why does `occ10` have more coverage than `occ` and `occ80`? 
3. What is the `wtssps` variable, and what does it represent?

__Hint__: to explore GSS variables, you can look at the variable names, the 'var_doc_label' column in `gss_data_dictionary` and the GSS Data Explorer at https://gssdataexplorer.norc.org/.


| Question| Your Response |
|---|---|
| Purpose | |
| Origin | |
| Procedure | |
| Participation | |
| `occ` variables | |
| `wtssps` variable | |


## Purpose
The purpose of the GSS was to learn information through a national representative survey that collected data on the attidudes, behaviors, and demographics of residents in the United States. 

## Origin
The GSS was first conducted in 1972 by the National Opinion Research Center at the University of Chicago and was used to measure how American society has changed over time helping with social and politcal research. 

## Procedure & Participation
The GSS was conducted through both in-person and online interviews picked at random. When they are interviewed they are asked several questions related to polical opinion, social behaviors, demphagraphic details, and attitudes. The GSS survey is conducted every two years. Many core questions have stayed the same but over the years, questions have changed based on technology use, climate change, and other social issues that have come about. 

## occ Variables
The occ, occ80, and occ10 variables all represent the survey respondents' job occupations corresponding to different classifications of different time periods. The occ refers to answers from 1972 to 1980, occ80 refers to answers from the 1980s through 2010, and occ10 refers to answers from 2010 and beyond. The reason why there are significantly more answers for occ10 is because it is the most modern and up to date database. Because surveys are no able to reach more people today then they would during the 80s and 90s for example, the GSS can collect more data. 

## wtssps Variable
The wtssps variable refers to the post-stratifcation weight that is used by the GSS to adjust the survey's data to better reflect the United States population distribution. The wtssps takes into account peoples' age, gender, race, and other demographic factors that would affect one's answer. The wtssps ensures that survey results are representative of the population of the United States as a whole.
