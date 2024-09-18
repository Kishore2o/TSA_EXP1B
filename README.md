# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Netflix stock price data
### ALGORITHM:
1. Import libraries like pandas, numpy, and matplotlib.

2. Load the dataset using pandas.

3. Check for missing values and handle them if necessary.

4. Apply differencing to remove trends in the data.

5. Remove seasonality by differencing at the seasonal lag.

6. Apply log transformation to stabilize variance.

7. Visualize the data before and after applying each transformation.

8. Print and plot the results.
### PROGRAM:
## DEVELOPED BY : Kishore S
## REG NO : 212222240050
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load the NFLX dataset
data = pd.read_csv('/content/NFLX.csv')

# Check for missing values
print("Missing values:\n", data.isnull().sum())

# Select only the Date and Close columns and rename them
data = data[['Date', 'Close']]
data.rename(columns={'Close': 'StockPrice'}, inplace=True)

# Convert the StockPrice column to numeric, handling commas if any
data['StockPrice'] = pd.to_numeric(data['StockPrice'], errors='coerce')

# Convert the Date column to datetime
data['Date'] = pd.to_datetime(data['Date'])

# Set the Date column as the index
data.set_index('Date', inplace=True)

# Apply differencing to the stock price
data['Differenced'] = data['StockPrice'].diff()

# Apply seasonal differencing (e.g., lag of 12)
data['Seasonal_Differenced'] = data['StockPrice'].diff(12)

# Apply log transformation
data['Log_Transformed'] = np.log(data['StockPrice'])

# Drop any NA values that were created during differencing
data.dropna(inplace=True)

# Plot the original data and the transformations
plt.figure(figsize=(14, 8))

plt.subplot(3, 2, 1)
plt.plot(data['StockPrice'], label='Original Data')
plt.title('Original Data')
plt.legend()

plt.subplot(3, 2, 2)
plt.plot(data['Differenced'], label='Differenced Data')
plt.title('Regular Differencing')
plt.legend()

plt.subplot(3, 2, 3)
plt.plot(data['Seasonal_Differenced'], label='Seasonal Adjustment')
plt.title('Seasonal Adjustment')
plt.legend()

plt.subplot(3, 2, 4)
plt.plot(data['Log_Transformed'], label='Log Transformed')
plt.title('Log Transformation')
plt.legend()

plt.tight_layout()
plt.show()

# Display the first few rows of the transformed data
print("REGULAR DIFFERENCING:\n", data['Differenced'].head())
print("SEASONAL ADJUSTMENT:\n", data['Seasonal_Differenced'].head())
print("LOG TRANSFORMATION:\n", data['Log_Transformed'].head())
```

### OUTPUT:
![image](https://github.com/user-attachments/assets/8540bdc6-1e07-4c54-97f4-7d12d86a8da7)


### REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/1eb3ab90-6d5d-48f9-acf3-9042c1e63d98)


### SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/5eceef6a-9ebe-4bb8-9b17-152ad8f769a6)



### LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/482e6a11-a6ba-4959-9195-d95cc4cf165a)


### RESULT:
The python code for the conversion of non stationary to stationary data on Netflix stock price data
data was executed successfully.
