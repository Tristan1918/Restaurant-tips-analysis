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

## 🚭 Non-smokers
Now repeat it for non-smokers. Use the following variables:

- min => non_smokers_tip_min
- max => non_smokers_tip_max
- mean => non_smokers_tip_mean
- median => non_smokers_tip_median
```python
non_smokers_tip_min = non_smokers_df.tip.min()
non_smokers_tip_max = non_smokers_df.tip.max()
non_smokers_tip_mean = non_smokers_df.tip.mean()
non_smokers_tip_median = non_smokers_df.tip.median()
```
Make the same dataframe containing the measures of central tendency for non-smokers as we did for whole dataset. Then output it.
```python 
non_smokers_df_values = [non_smokers_tip_min, non_smokers_tip_max, non_smokers_tip_mean, non_smokers_tip_median]
non_smokers_df_values = map(lambda x: round(x, 4), non_smokers_df_values)
non_smokers_df_mct = pd.DataFrame(non_smokers_df_values, index=['min', 'max', 'mean', 'median'])
non_smokers_df_mct
```
|        | 0      |
|--------:|--------:|
| min    | 1.0000 |
| max    | 9.0000 |
| mean   | 2.9919 |
| median | 2.7400 |

## 📝 Conclusion
Let's show the retrieved results together
```python
all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Smokers': {'min': smokers_tip_min, 'max': smokers_tip_max, 'mean': smokers_tip_mean, 'median': smokers_tip_median},
    'Non-smokers': {'min': non_smokers_tip_min, 'max': non_smokers_tip_max, 'mean': non_smokers_tip_mean, 'median': non_smokers_tip_median}
}
all_mct = pd.DataFrame(all_vals_dict)
all_mct
```
|        | Common    | Smokers  | Non-smokers |
|--------:|-----------:|----------:|-------------:|
| min    | 1.000000  | 1.00000  | 1.000000    |
| max    | 10.000000 | 10.00000 | 9.000000    |
| mean   | 2.998279  | 3.00871  | 2.991854    |
| median | 2.900000  | 3.00000  | 2.740000    |

## Look at histograms
There are a lot of cases, when comparing the measures of central tendency is not enough. This is because they only show the most typical values. However, the way data is distributed is equally important. There are situations where measures of central tendency are exactly the same, but due to different distributions, it is incorrect to say that the datasets are similar.
```python
fig, axis = plt.subplots(1, 3, figsize = (15, 5))

#Whole data
axis[0].hist(data.tip, color = '#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

#Smokers
axis[1].hist(smokers_df.tip, color = '#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Smokers tip values')
axis[1].grid(True)

#Non_smokers
axis[2].hist(non_smokers_df.tip, color = '#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Non-smokers tip values')
axis[2].grid(True)
```
![image](https://github.com/user-attachments/assets/357e43e5-a37f-43d9-8279-439f68b17e64)

# 👨👩 Do males give more tips?
Let's figure out the difference between male and female in terms of their behavior and purchasing habits in public catering establishments.
# Separate male and female
Create a new dataframe male_df containing only info about male.
```python
male_df = pd.DataFrame(data = data[data.sex == 'Male'])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
male_df.sample(5)
```
| id  | total_bill | tip  | sex  | smoker | day  | time   | size |
|-----:|------------:|------:|------:|--------:|------:|--------:|------:|
| 54  | 25.56      | 4.34 | Male | No     | Sun  | Dinner | 4    |
| 53  | 9.94       | 1.56 | Male | No     | Sun  | Dinner | 2    |
| 173 | 31.85      | 3.18 | Male | Yes    | Sun  | Dinner | 2    |
| 196 | 10.34      | 2.00 | Male | Yes    | Thur | Lunch  | 2    |
| 222 | 8.58       | 1.92 | Male | Yes    | Fri  | Lunch  | 1    |

Also create another one dataframe female_df containing only female.
```python
female_df = pd.DataFrame(data = data[data.sex == 'Female'])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
female_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day | time   | size |
|-----:|------------:|------:|--------:|--------:|-----:|--------:|------:|
| 67  | 3.07       | 1.00 | Female | Yes    | Sat | Dinner | 1    |
| 229 | 22.12      | 2.88 | Female | Yes    | Sat | Dinner | 2    |
| 225 | 16.27      | 2.50 | Female | Yes    | Fri | Lunch  | 2    |
| 162 | 16.21      | 2.00 | Female | No     | Sun | Dinner | 3    |
| 71  | 17.07      | 3.00 | Female | No     | Sat | Dinner | 3    |

# Compare their measures of central tendency
As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

## 👨 Male
Calculate measures of central tendency for male and save them into the following variables:
- min => male_df_tip_min
- max => male_df_tip_max
- mean => male_df_tip_mean
- median => male_df_tip_median
```python
male_df_tip_min = male_df.tip.min()
male_df_tip_max = male_df.tip.max()
male_df_tip_mean = male_df.tip.mean()
male_df_tip_median = male_df.tip.median()
```
Let's show the resulting values for male:
```python
male_df_values = [male_df_tip_min, male_df_tip_max, male_df_tip_mean, male_df_tip_median]
male_df_values = map(lambda x: round(x, 4), male_df_values)
male_df_mct = pd.DataFrame(male_df_values, index=['min', 'max', 'mean', 'median'])
male_df_mct
```
|        | 0       |
|--------:|---------:|
| min    | 1.0000  |
| max    | 10.0000 |
| mean   | 3.0896  |
| median | 3.0000  |

## 👩 Female
Calculate measures of central tendency for female and save them into the following variables:
- min => female_df_tip_min
- max => female_df_tip_max
- mean => female_df_tip_mean
- median => female_df_tip_median
```python
female_df_tip_min = female_df.tip.min()
female_df_tip_max = female_df.tip.max()
female_df_tip_mean = female_df.tip.mean()
female_df_tip_median = female_df.tip.median()
```
Let's show the resulting values for female:
```python
female_df_values = [female_df_tip_min, female_df_tip_max, female_df_tip_mean, female_df_tip_median]
female_df_values = map(lambda x: round(x, 4), female_df_values)
female_df_mct = pd.DataFrame(female_df_values, index=['min', 'max', 'mean', 'median'])
female_df_mct
```
|        | 0      |
|--------:|--------:|
| min    | 1.0000 |
| max    | 6.5000 |
| mean   | 2.8334 |
| median | 2.7500 |

## 📝 Conclusion
Let's show the retrieved results together
```python
all_vals_dict_1 = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Male': {'min': male_df_tip_min, 'max': male_df_tip_max, 'mean': male_df_tip_mean, 'median': male_df_tip_median},
    'Female': {'min': female_df_tip_min, 'max': female_df_tip_max, 'mean': female_df_tip_mean, 'median': female_df_tip_median}
}
all_mct_1 = pd.DataFrame(all_vals_dict_1)
all_mct_1
```
|        | Common    | Male      | Female   |
|--------:|-----------:|-----------:|----------:|
| min    | 1.000000  | 1.000000  | 1.000000 |
| max    | 10.000000 | 10.000000 | 6.500000 |
| mean   | 2.998279  | 3.089618  | 2.833448 |
| median | 2.900000  | 3.000000  | 2.750000 |

## Look at histograms
There are a lot of cases, when comparing the measures of central tendency is not enough. This is because they only show the most typical values. However, the way data is distributed is equally important. There are situations where measures of central tendency are exactly the same, but due to different distributions, it is incorrect to say that the datasets are similar.
```python
fig, axis = plt.subplots(1, 3, figsize = (15, 5))

#Whole data
axis[0].hist(data.tip, color = '#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

#Male
axis[1].hist(male_df.tip, color = '#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Male tip values')
axis[1].grid(True)

#Female
axis[2].hist(female_df.tip, color = '#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Female tip values')
axis[2].grid(True)
```
![image](https://github.com/user-attachments/assets/e07fafb9-373d-4e82-9377-0639b84680d6)

# 📆 Do weekends bring more tips?
Let's figure out the difference between weekday and weekend 
# Separate weekday and weekend
Create a new dataframe weekday_df containing only info about weekday.
```python
weekday_df = pd.DataFrame(data = data[(data.day != 'Sat') & (data.day != 'Sun')])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
weekday_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day  | time   | size |
|-----:|------------:|------:|--------:|--------:|------:|--------:|------:|
| 93  | 16.32      | 4.30 | Female | Yes    | Fri  | Dinner | 2    |
| 222 | 8.58       | 1.92 | Male   | Yes    | Fri  | Lunch  | 1    |
| 96  | 27.28      | 4.00 | Male   | Yes    | Fri  | Dinner | 2    |
| 149 | 7.51       | 2.00 | Male   | No     | Thur | Lunch  | 2    |
| 196 | 10.34      | 2.00 | Male   | Yes    | Thur | Lunch  | 2    |

Also create another one dataframe weekend_df containing only weekend.
```python
weekend_df = pd.DataFrame(data = data[(data.day == 'Sat') | (data.day == 'Sun')])
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
weekend_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day | time   | size |
|-----:|------------:|------:|--------:|--------:|-----:|--------:|------:|
| 60  | 20.29      | 3.21 | Male   | Yes    | Sat | Dinner | 2    |
| 218 | 7.74       | 1.44 | Male   | Yes    | Sat | Dinner | 2    |
| 37  | 16.93      | 3.07 | Female | No     | Sat | Dinner | 3    |
| 176 | 17.89      | 2.00 | Male   | Yes    | Sun | Dinner | 2    |
| 155 | 29.85      | 5.14 | Female | No     | Sun | Dinner | 5    |

# Compare their measures of central tendency
As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

## 📆 Weekday
Calculate measures of central tendency for male and save them into the following variables:
- min => weekday_df_tip_min
- max => weekday_df_tip_max
- mean => weekday_df_tip_mean
- median => weekday_df_tip_median
```python
weekday_df_tip_min = weekday_df.tip.min()
weekday_df_tip_max = weekday_df.tip.max()
weekday_df_tip_mean = weekday_df.tip.mean()
weekday_df_tip_median = weekday_df.tip.median()
```
Let's show the resulting values for weekday:
```python
weekday_df_values = [weekday_df_tip_min, weekday_df_tip_max, weekday_df_tip_mean, weekday_df_tip_median]
weekday_df_values = map(lambda x: round(x, 4), weekday_df_values)
weekday_df_mct = pd.DataFrame(weekday_df_values, index=['min', 'max', 'mean', 'median'])
weekday_df_mct
```
|        | 0      |
|--------:|--------:|
| min    | 1.0000 |
| max    | 6.7000 |
| mean   | 2.7628 |
| median | 2.5000 |


## 📆 Weekend
Calculate measures of central tendency for weekend and save them into the following variables:
- min => weekend_df_tip_min
- max => weekend_df_tip_max
- mean => weekend_df_tip_mean
- median => weekend_df_tip_median
```python
weekend_df_tip_min = weekend_df.tip.min()
weekend_df_tip_max = weekend_df.tip.max()
weekend_df_tip_mean = weekend_df.tip.mean()
weekend_df_tip_median = weekend_df.tip.median()
```
Let's show the resulting values for weekend:
```python
weekend_df_values = [weekend_df_tip_min, weekend_df_tip_max, weekend_df_tip_mean, weekend_df_tip_median]
weekend_df_values = map(lambda x: round(x, 4), weekend_df_values)
weekend_df_mct = pd.DataFrame(weekend_df_values, index=['min', 'max', 'mean', 'median'])
weekend_df_mct
```
|        | 0       |
|--------:|---------:|
| min    | 1.0000  |
| max    | 10.0000 |
| mean   | 3.1153  |
| median | 3.0000  |

## 📝 Conclusion
Let's show the retrieved results together
```python
all_vals_dict_2 = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Weekday': {'min': weekday_df_tip_min, 'max': weekday_df_tip_max, 'mean': weekday_df_tip_mean, 'median': weekday_df_tip_median},
    'Weekend': {'min': weekend_df_tip_min, 'max': weekend_df_tip_max, 'mean': weekend_df_tip_mean, 'median': weekend_df_tip_median}
}
all_mct_2 = pd.DataFrame(all_vals_dict_2)
all_mct_2
```
|        | Common    | Weekday | Weekend   |
|--------:|-----------:|---------:|-----------:|
| min    | 1.000000  | 1.00000 | 1.000000  |
| max    | 10.000000 | 6.70000 | 10.000000 |
| mean   | 2.998279  | 2.76284 | 3.115276  |
| median | 2.900000  | 2.50000 | 3.000000  |

## Look at histograms
There are a lot of cases, when comparing the measures of central tendency is not enough. This is because they only show the most typical values. However, the way data is distributed is equally important. There are situations where measures of central tendency are exactly the same, but due to different distributions, it is incorrect to say that the datasets are similar.
```python
fig, axis = plt.subplots(1, 3, figsize = (15, 5))

#Whole data
axis[0].hist(data.tip, color = '#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

#Weekday
axis[1].hist(weekday_df.tip, color = '#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Weekday tip values')
axis[1].grid(True)

#Weekend
axis[2].hist(weekend_df.tip, color = '#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Weekend tip values')
axis[2].grid(True)
```
![image](https://github.com/user-attachments/assets/e87bdfb0-745e-4ec1-bf70-2ce28bcdaca1)

# 🕑 Do dinners bring more tips?
Let's figure out the difference between lunch and dinner. 
# Separate lunch and dinner
Create a new dataframe lunch_df containing only info about lunch.
```python
lunch_df = data[data.time == 'Lunch']
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
lunch_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day  | time  | size |
|-----:|------------:|------:|--------:|--------:|------:|-------:|------:|
| 85  | 34.83      | 5.17 | Female | No     | Thur | Lunch | 4    |
| 78  | 22.76      | 3.00 | Male   | No     | Thur | Lunch | 2    |
| 125 | 29.80      | 4.20 | Female | No     | Thur | Lunch | 6    |
| 82  | 10.07      | 1.83 | Female | No     | Thur | Lunch | 1    |
| 137 | 14.15      | 2.00 | Female | No     | Thur | Lunch | 2    |

Also create another one dataframe dinner_df containing only dinner.
```python
dinner_df = data[data.time == 'Dinner']
```
Check whether everything is okay. Output a test sample (5 random rows):
```python
dinner_df.sample(5)
```
| id  | total_bill | tip  | sex    | smoker | day | time   | size |
|-----:|------------:|------:|--------:|--------:|-----:|--------:|------:|
| 98  | 21.01      | 3.00 | Male   | Yes    | Fri | Dinner | 2    |
| 93  | 16.32      | 4.30 | Female | Yes    | Fri | Dinner | 2    |
| 172 | 7.25       | 5.15 | Male   | Yes    | Sun | Dinner | 2    |
| 17  | 16.29      | 3.71 | Male   | No     | Sun | Dinner | 3    |
| 151 | 13.13      | 2.00 | Male   | No     | Sun | Dinner | 2    |

# Compare their measures of central tendency
As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

## 🕑 Lunch
Calculate measures of central tendency for lunch and save them into the following variables:
- min => lunch_df_tip_min
- max => lunch_df_tip_max
- mean => lunch_df_tip_mean
- median => lunch_df_tip_median
```python
lunch_df_tip_min = lunch_df.tip.min()
lunch_df_tip_max = lunch_df.tip.max()
lunch_df_tip_mean = lunch_df.tip.mean()
lunch_df_tip_median = lunch_df.tip.median()
```
Let's show the resulting values for lunch:
```python
lunch_df_values = [lunch_df_tip_min, lunch_df_tip_max, lunch_df_tip_mean, lunch_df_tip_median]
lunch_df_values = map(lambda x: round(x, 4), lunch_df_values)
lunch_df_mct = pd.DataFrame(lunch_df_values, index=['min', 'max', 'mean', 'median'])
lunch_df_mct
```
|        | 0      |
|--------:|--------:|
| min    | 1.2500 |
| max    | 6.7000 |
| mean   | 2.7281 |
| median | 2.2500 |

## 🕑 Dinner
Calculate measures of central tendency for weekend and save them into the following variables:
- min => dinner_df_tip_min
- max => dinner_df_tip_max
- mean => dinner_df_tip_mean
- median => dinner_df_tip_median
```python
dinner_df_tip_min = dinner_df.tip.min()
dinner_df_tip_max = dinner_df.tip.max()
dinner_df_tip_mean = dinner_df.tip.mean()
dinner_df_tip_median = dinner_df.tip.median()
```
Let's show the resulting values for dinner:
```python
dinner_df_values = [dinner_df_tip_min, dinner_df_tip_max, dinner_df_tip_mean, dinner_df_tip_median]
dinner_df_values = map(lambda x: round(x, 4), dinner_df_values)
dinner_df_mct = pd.DataFrame(dinner_df_values, index=['min', 'max', 'mean', 'median'])
dinner_df_mct
```
|        | 0       |
|--------:|---------:|
| min    | 1.0000  |
| max    | 10.0000 |
| mean   | 3.1027  |
| median | 3.0000  |

## 📝 Conclusion
Let's show the retrieved results together
```python
all_vals_dict_3 = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Lunch': {'min': lunch_df_tip_min, 'max': lunch_df_tip_max, 'mean': lunch_df_tip_mean, 'median': lunch_df_tip_median},
    'Dinner': {'min': dinner_df_tip_min, 'max': dinner_df_tip_max, 'mean': dinner_df_tip_mean, 'median': dinner_df_tip_median}
}
all_mct_3 = pd.DataFrame(all_vals_dict_3)
all_mct_3
```
|        | Common    | Lunch    | Dinner   |
|--------:|-----------:|----------:|----------:|
| min    | 1.000000  | 1.250000 | 1.00000  |
| max    | 10.000000 | 6.700000 | 10.00000 |
| mean   | 2.998279  | 2.728088 | 3.10267  |
| median | 2.900000  | 2.250000 | 3.00000  |

## Look at histograms
There are a lot of cases, when comparing the measures of central tendency is not enough. This is because they only show the most typical values. However, the way data is distributed is equally important. There are situations where measures of central tendency are exactly the same, but due to different distributions, it is incorrect to say that the datasets are similar.
```python
fig, axis = plt.subplots(1, 3, figsize = (15, 5))

#Whole data
axis[0].hist(data.tip, color = '#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

#Lunch
axis[1].hist(lunch_df.tip, color = '#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Lunch tip values')
axis[1].grid(True)

#Dinner
axis[2].hist(dinner_df.tip, color = '#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Dinner tip values')
axis[2].grid(True)
```
![image](https://github.com/user-attachments/assets/25d4e298-b930-4bf1-aebb-0e4c693b87fe)

