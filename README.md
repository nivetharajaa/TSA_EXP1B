# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA

### Name:Nivetha A
### Register No: 212222230101

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("AirPassengers.csv")
train.timestamp = pd.to_datetime(train.Month, format = '%Y-%m')
train.drop('Month', axis=1, inplace = True)
train.head()
train['#Passengers'].plot()

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
adf_test(train['#Passengers'])

train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(1)
train['#Passengers_diff'].dropna().plot()
# Seasonal Differencing
n=7
train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(n)
train['#Passengers_diff'].dropna().plot()
# Transformation
train['#Passengers_log'] = np.log(train['#Passengers'])
train['#Passengers_log_diff'] = train['#Passengers_log'] - train['#Passengers_log'].shift(1)
train['#Passengers_log_diff'].dropna().plot()
```

### OUTPUT:



![image](https://github.com/user-attachments/assets/d5c0abcd-22ac-4db8-af29-638a5ca90918)

![image](https://github.com/user-attachments/assets/3e72fa48-db52-4fe1-a8e1-7adb1db17181)

### REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/5adb711c-fed8-47f9-8734-08d7aed40d3b)


### SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/4c7d73c2-e1d3-4fd5-8d5c-aceb91490ef7)


### LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/c05b0246-e203-4888-a127-a61bd1d8ca93)



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
