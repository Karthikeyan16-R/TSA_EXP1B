# Ex.No: 1B  CONVERSION OF NON STATIONARY TO STATIONARY DATA
### Name : Karthikeyan R
### REG NUM : 212222240045
### Date: 

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

train = pd.read_csv("/content/rainfall.csv")
# Change 'Date' to 'date' to match the column name in the DataFrame
train['date'] = pd.to_datetime(train['date'], format='%Y-%m-%d')  
train.set_index('date', inplace=True)  
train.head()

# Change 'Price' to 'rainfall' to match the column name in the DataFrame
train['rainfall'].plot(title='Rainfall') 

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

# Change 'Price' to 'rainfall' to match the column name in the DataFrame
adf_test(train['rainfall'])
```

### REGULAR DIFFERENCING:
```
train['rainfall_diff'] = train['rainfall'] - train['rainfall'].shift(1) # Changed 'Price' to 'rainfall' to match column name
train['rainfall_diff'].dropna().plot(title='Differenced Rainfall') # Changed title to reflect the change
```

### SEASONAL ADJUSTMENT:
```
n = 7
# Changed 'Price' to 'rainfall' to match column name
train['rainfall_seasonal_diff'] = train['rainfall'] - train['rainfall'].shift(n) 
# Changed title to reflect the change
train['rainfall_seasonal_diff'].dropna().plot(title='Seasonally Differenced Rainfall')
```
### LOG TRANSFORMATION:

```
train['rainfall_log'] = np.log(train['rainfall']) # Changed 'Price' to 'rainfall'
train['rainfall_log_diff'] = train['rainfall_log'] - train['rainfall_log'].shift(1)
train['rainfall_log_diff'].dropna().plot(title='Log Differenced Rainfall') # Changed title to reflect change
```


### OUTPUT:

![image](https://github.com/user-attachments/assets/0230d946-1999-4a64-9f74-4070c6a3b6a0)



REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/d72b6ff5-edbc-4e86-a20f-11c460a64df9)


SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/8d61e08f-60f4-4589-9678-1180e8f98d17)


LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/1b21a633-1a4d-4ea0-87a9-27e69ba7009b)



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
