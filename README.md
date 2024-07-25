### 🍽️ Restaurant Tips Analysis
![image](https://github.com/user-attachments/assets/5cf15e7e-752c-4e65-a104-b787b720a281)
This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations. We will examine the relationship between different variables and the tips given.

The dataset consists of information from 244 restaurant bills, collected in the US in 1987.

It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.

## 📥 Data import
First, let's import the needed libraries: Pandas & Matplotlib.
```python
import pandas as pd
import matplotlib.pyplot as plt
```
Then load data from the following link: https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv
```python
data = pd.read_csv('https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv')
```

## 🔍 Data exploration
Let's take a look at the first 5 rows to be sure, that data is loaded properly:
```python
data.head(5)
```
| id | total_bill | tip  | sex    | smoker | day | time   | size |
|----:|------------:|------:|--------:|--------:|-----:|--------:|------:|
| 0  | 16.99      | 1.01 | Female | No     | Sun | Dinner | 2    |
| 1  | 10.34      | 1.66 | Male   | No     | Sun | Dinner | 3    |
| 2  | 21.01      | 3.50 | Male   | No     | Sun | Dinner | 3    |
| 3  | 23.68      | 3.31 | Male   | No     | Sun | Dinner | 2    |
| 4  | 24.59      | 3.61 | Female | No     | Sun | Dinner | 4    |

## Column types checking
Show the columns of the dataframe and their types:
```python
data.info()
```
![image](https://github.com/user-attachments/assets/79a922ef-83a7-44a0-ab76-d7d08f2011a6)

We have string columns considered as objects. Let's fix their types and make them string:
```python
data[["sex", "smoker", "day", "time"]] = data[["sex", "smoker", "day", "time"]].astype('string')
```
Check again (output columns and their types):
```python
data.info()
```
![image](https://github.com/user-attachments/assets/e337aa11-4132-47d0-ab72-404a4b09f9e6)

Nice! We finished this. Look like we are ready to explore some statistics on the given data.

## Basic descriptive statistics
Show a descriptive statistics of the numeric columns:
```python
data.describe()
```
|       | id         | total_bill | tip        | size       |
|-------:|------------:|------------:|------------:|------------:|
| count | 244.000000 | 244.000000 | 244.000000 | 244.000000 |
| mean  | 121.500000 | 19.785943  | 2.998279   | 2.569672   |
| std   | 70.580923  | 8.902412   | 1.383638   | 0.951100   |
| min   | 0.000000   | 3.070000   | 1.000000   | 1.000000   |
| 25%   | 60.750000  | 13.347500  | 2.000000   | 2.000000   |
| 50%   | 121.500000 | 17.795000  | 2.900000   | 2.000000   |
| 75%   | 182.250000 | 24.127500  | 3.562500   | 3.000000   |
| max   | 243.000000 | 50.810000  | 10.000000  | 6.000000   |

## Tip value influencers
# 🚬 Do people who smoke give more tips?
Let's figure out the difference between smokers and non-smokers in terms of their behavior and purchasing habits in public catering establishments.
# Separate smokers and non-smokers
Create a new dataframe smokers_df containing only info about smokers.
```python
smokers_df = pd.DataFrame(data = data[data.smoker == 'Yes'])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
smokers_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day  | time   | size |
|-----:|------------:|------:|--------:|--------:|------:|--------:|------:|
| 164 | 17.51      | 3.00 | Female | Yes    | Sun  | Dinner | 2    |
| 189 | 23.10      | 4.00 | Male   | Yes    | Sun  | Dinner | 3    |
| 184 | 40.55      | 3.00 | Male   | Yes    | Sun  | Dinner | 2    |
| 171 | 15.81      | 3.16 | Male   | Yes    | Sat  | Dinner | 2    |
| 201 | 12.74      | 2.01 | Female | Yes    | Thur | Lunch  | 2    |

Also create another one dataframe non_smokers_df containing only non-smokers.
```python
non_smokers_df = pd.DataFrame(data = data[data.smoker == 'No'])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
non_smokers_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day  | time   | size |
|-----:|------------:|------:|--------:|--------:|------:|--------:|------:|
| 89  | 21.16      | 3.00 | Male   | No     | Thur | Lunch  | 2    |
| 29  | 19.65      | 3.00 | Female | No     | Sat  | Dinner | 2    |
| 227 | 20.45      | 3.00 | Male   | No     | Sat  | Dinner | 4    |
| 46  | 22.23      | 5.00 | Male   | No     | Sun  | Dinner | 2    |
| 84  | 15.98      | 2.03 | Male   | No     | Thur | Lunch  | 2    |

# Compare their measures of central tendency
As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

# 🌏 Whole dataset
Let's try to calculate measures of central tendency for the whole dataset first.

Calculate them for the 'tip' column through the whole dataset and save them into the following variables:

- min => common_tip_min
- max => common_tip_max
- mean => common_tip_mean
- median => common_tip_median
```python
common_tip_min = data.tip.min()
common_tip_max = data.tip.max()
common_tip_mean = data.tip.mean()
common_tip_median = data.tip.median()
```
Let's show the resulting values for whole dataset
```python
common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
common_values = map(lambda x: round(x, 4), common_values)
common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
common_mct
```
|        | 0       |
|--------:|---------:|
| min    | 1.0000  |
| max    | 10.0000 |
| mean   | 2.9983  |
| median | 2.9000  |

## 🚬 Smokers
Do the same taking into account only smokers. Use the following variables:
- min => smokers_tip_min
- max => smokers_tip_max
- mean => smokers_tip_mean
- median => smokers_tip_median
```python
smokers_tip_min = smokers_df.tip.min()
smokers_tip_max = smokers_df.tip.max()
smokers_tip_mean = smokers_df.tip.mean()
smokers_tip_median = smokers_df.tip.median()
```
Let's output the results in the same format.

Make the same dataframe containing the measures of central tendency for smokers as we did for whole dataset. Then output it.
```python
smokers_df_values = [smokers_tip_min, smokers_tip_max, smokers_tip_mean, smokers_tip_median]
smokers_df_values = map(lambda x: round(x, 4), smokers_df_values)
smokers_df_mct = pd.DataFrame(smokers_df_values, index=['min', 'max', 'mean', 'median'])
smokers_df_mct
```
|        | 0       |
|--------:|---------:|
| min    | 1.0000  |
| max    | 10.0000 |
| mean   | 3.0087  |
| median | 3.0000  |
