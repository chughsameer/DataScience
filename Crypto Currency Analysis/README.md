
# Crypto-Currency Analysis

In this project, after extracting the data sets as csv, I tried to reflect them graphically and schematically about cryptocurrencies in finance by using data analysis and data visualization methods. In this project, there are other cryptocurrencies in the data set provided in this project, but if you want, you can do the same after reading them as csv files. I used 3 cryptocurrencies of my choice. These are  bitcoin, ethereum and dogecoin.


## Libraries and Utilities
```Python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```
### Let's take a look at our top five data
```Python
bitcoin_data.head()
```
![bitcoin_datahead](https://user-images.githubusercontent.com/98213315/204125804-1b342229-f8b2-49df-a242-82af2399c58c.png)

```Python
combine_df = pd.DataFrame({'Bitcoin':bitcoin_data['Close'],
                           'Ethereum':ethereum_data['Close'],
                           'Dogecoin':dogecoin_data['Close']})
```
![Combine_df](https://user-images.githubusercontent.com/98213315/204125822-c47003e5-7628-4f86-ae62-5473e4866624.png)

## Cryptocurrency Graph
```Python 
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
plt.figure(figsize=(13,5))
for col in combine_df.columns.values:
    plt.plot(combine_df[col],label = col)
plt.title("Cryptocurrency Graph")
plt.xlabel('Days')
plt.ylabel('Crypto Price($)')
plt.legend(combine_df.columns.values, loc= 'upper left')
plt.show()
```

![index](https://user-images.githubusercontent.com/98213315/204125829-46b8cba2-3e76-4058-801a-0a0e5a200b1b.png)

## Cryptocurrency Scaled Graph
```Python
#Visualising the Scaled Data
my_crypto = scaled_data
plt.figure(figsize=(13,5))
for col in scaled_data.columns.values:
    plt.plot(my_crypto[col],label = col)
plt.title("Cryptocurrency Scaled Data")
plt.xlabel("Days")
plt.ylabel("Crypto Scaled Price($)")
plt.legend(my_crypto.columns.values,loc = 'upper left')
plt.show()
```
![scaledindex](https://user-images.githubusercontent.com/98213315/204125838-c430d673-51f4-45b5-b997-838901680ffe.png)

## Daily Simple Return
```Python 
plt.figure(figsize=(13,5))
for col in DSR.columns.values:
    plt.plot(DSR.index,DSR[col],label=col,alpha= 0.7)
plt.title("Daily Simple Return")
plt.xlabel("Days")
plt.ylabel("Percentage (x 10)")
plt.legend(DSR.columns.values,loc = 'upper right')
plt.show()
```
![DailySimpleReturn](https://user-images.githubusercontent.com/98213315/204125841-9b56b3a8-3273-425f-89c0-4f5078958ab9.png)

## Heat Map
```Python
import seaborn as sns
plt.subplots(figsize = (12,12))
sns.heatmap(DSR.corr(),annot = True,fmt='0.2%')
```
![heatmap](https://user-images.githubusercontent.com/98213315/204125845-199c3ac9-4511-4f17-b793-0ec3cf6e0b1a.png)

## Daily Cumulative Return
```Python
plt.figure(figsize=(13,5))
for col in DCSR.columns.values:
    plt.plot(DCSR.index,DCSR[col],lw=2,label=col)
plt.title('Daily Cumulative Simple Return')
plt.xlabel('Days')
plt.ylabel('Growth for $1 investment')
plt.legend(DCSR.columns.values,loc = 'upper left',fontsize = 10)
plt.show()
```
![indexdailycummlativesimplereturn](https://user-images.githubusercontent.com/98213315/204125849-8a876ea3-021d-4d21-92a1-0a566ec14f4d.png)
