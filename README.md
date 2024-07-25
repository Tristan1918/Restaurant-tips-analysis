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
|----|------------|------|--------|--------|-----|--------|------|
| 0  | 16.99      | 1.01 | Female | No     | Sun | Dinner | 2    |
| 1  | 10.34      | 1.66 | Male   | No     | Sun | Dinner | 3    |
| 2  | 21.01      | 3.50 | Male   | No     | Sun | Dinner | 3    |
| 3  | 23.68      | 3.31 | Male   | No     | Sun | Dinner | 2    |
| 4  | 24.59      | 3.61 | Female | No     | Sun | Dinner | 4    |


https://colab.research.google.com/drive/1kGmqFLiU5PdmEDMI2vEBs5sGEOTti1ng#scrollTo=uS05KPXsDZPQ&line=2&uniqifier=1
