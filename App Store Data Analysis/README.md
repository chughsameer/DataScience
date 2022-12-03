# App-Store-Data-Analysis
With this data analysis project, we examined the app_store data. Dataset links are given below.

Dataset link: https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps

### import
```Python

import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
import seaborn as sns
from warnings import filterwarnings
filterwarnings("ignore")

import ppscore

#Import Library RobustScaler
from sklearn.preprocessing import RobustScaler
#Cluster Model
from sklearn.cluster import KMeans 
from sklearn.metrics import silhouette_score
```
```Python
data.head()
```
![DataHead()](https://user-images.githubusercontent.com/98213315/205430638-3a056361-b584-44dc-b5e9-17d0888fd203.png)


```Python
#about data
data.info()
```
![datainfo](https://user-images.githubusercontent.com/98213315/205438120-b3b13b3d-fddd-41ec-b551-b5426e4258d5.png)


```Python
plt.style.use('fivethirtyeight')
plt.Figure(figsize=(6.5,4.3))

plt.subplot(2,1,2)
plt.title("Visual price distribution")
sns.stripplot(data=paid_apps,y='price',jitter=True,orient='h',size=5)
plt.show()
```
![VisualPriceDistribution](https://user-images.githubusercontent.com/98213315/205438194-31f8bfc3-8bf3-4f90-bdfd-31d9347f66b6.png)


```Python
top_apps = top_apps.sort_values('price',ascending=False)

visualizer(top_apps.price,top_apps.track_name,"bar","Top 7 apps on basis of price","Price (in U$D)","App Name")
```

![Top7apps](https://user-images.githubusercontent.com/98213315/205438281-81bbcb2a-dfc4-4d25-8837-f35aab82ba74.png)


```Python
paid_apps.head()
```
![PaidApps](https://user-images.githubusercontent.com/98213315/205438316-27e5a5b8-581e-47c2-b899-7d8f7dc17b47.png)


```Python
data['prime_genre'].value_counts()
```

![Prime_genre](https://user-images.githubusercontent.com/98213315/205438349-7c4cd6b7-82fa-4654-9173-f0aa1ef434cc.png)


```Python
#Top_Categories accorrding to number of apps
new_data_cate.head(10)
```
![Prime_genre Numberofapps](https://user-images.githubusercontent.com/98213315/205438394-420d3d49-3702-4619-ac71-1509261aa1c9.png)


```Python
sns.barplot(y='prime_genre',x='number of apps',data=new_data_cate.head(10))
```

![prime_genre Barplot](https://user-images.githubusercontent.com/98213315/205438441-55271b82-2dab-42dc-9f59-9c7d41a5ea4d.png)

```Python
plt.figure(figsize=(10,5))
plt.scatter(x=paid_apps.price , y=paid_apps.prime_genre,c='DarkBlue')
plt.title('Price & Category')
plt.xlabel('Price')
plt.ylabel('Category')
plt.show()
```
![price category](https://user-images.githubusercontent.com/98213315/205438503-4020425c-3e15-4558-81f6-2523f4a6c50a.png)



### Paid Apps v/s Free Apps

```Python
names = ['|free apps|','|paid apps|']
values = [sum_free,sum_paid]
plt.figure(figsize=(4,4))
plt.suptitle("Count of free and paid apps")
plt.bar(names,values)
plt.show()
```
![paidapp vs freeappsindex](https://user-images.githubusercontent.com/98213315/205438596-89cf4935-acba-4d93-a0b5-8bfddd2310d8.png)


### Categories of paid apps and free apps
```Python
# for pie chart
pies = table[["%free","%paid"]].head()
pies.columns = ["free apps","paid apps"]
```
```Python
plt.figure(figsize=(15,10))
pies.T.plot.pie(subplots=True,figsize=(20,4),colors=['#800080','#ADD8E6'],autopct = '%1.0f%%')    
plt.show()
```

![indexcategorywisefreepaid](https://user-images.githubusercontent.com/98213315/205438725-a0c1bd50-0d78-4e5b-8bd3-9a698058f907.png)

```Python
visualizer(paid_apps.user_rating,paid_apps.prime_genre,"bar","User_rating in all category","User-Rating","Category")
```

![Userrating in all cate](https://user-images.githubusercontent.com/98213315/205438752-25a4a6ff-bff3-48ca-b98d-f6c602aa0bc5.png)

```Python
top_apps = top_apps.sort_values('price',ascending=False)

visualizer(top_apps.user_rating , top_apps.track_name,'bar','Top 7 apps on the basis of price with user rating','User-Rating','App Name' )
```

![top7appsuserrating](https://user-images.githubusercontent.com/98213315/205438788-eae0e1b7-3db2-4922-b069-84b2e0799635.png)


```Python
colouring = ['#fc910d','#f5ed05','#09ed52','#ed3b09','#e01bda']
plt.figure(figsize=(15,15))
label_names = data.broad_genre.value_counts().sort_index().index
size = data.broad_genre.value_counts().sort_index().tolist()

my_circle = plt.Circle( (0,0) , 0.7 , color='white')
plt.pie(size, labels=label_names, colors=colouring ,autopct="%1.0f%%")
p=plt.gcf()
p.gca().add_artist(my_circle)
plt.show()
```

![Ring](https://user-images.githubusercontent.com/98213315/205438819-d2f2ce33-5669-4599-9718-ebc3fbf724ba.png)


```Python
plt.figure(figsize=(15,15))
f = pd.DataFrame(index=np.arange(0,10,2),data=category['free'].values,columns=['num']) #index=(0,2,4,6,8)
p = pd.DataFrame(index=np.arange(1,11,2),data=category['paid'].values,columns=['num']) #index=(1,3,5,7,9)
final = pd.concat([f,p],names=['labels']).sort_index()

plt.figure(figsize=(25,25))
group_names=data.broad_genre.value_counts().sort_index().index
group_size =data.broad_genre.value_counts().sort_index().to_list()
h = ['Free','Paid']
subgroups_names = 5*h
sub=['#A2C3DB','#8871A0']
subcolours = 5*sub
subgroup_size = final.num.tolist()
# subgroup_size

# 1st ring (outside)
fig, ax = plt.subplots()
ax.axis('equal')
mypie , _ = ax.pie(group_size,radius=2.5,labels=group_names,colors=colouring,labeldistance=0.7)
plt.setp( mypie,width=1.2,edgecolor='white')

#2nd ring (inside)
mypie2,_ = ax.pie(subgroup_size,radius=1.6,labels=subgroups_names,colors=subcolours,labeldistance=0.8)
plt.setp(mypie2,width=0.8,edgecolor='white')
plt.margins(0,0)

plt.show()
```

![DoubleRing](https://user-images.githubusercontent.com/98213315/205438856-cb6f2351-69ac-495a-a20e-1bc59b34d1b0.png)



With this project, we have examined and analyzed the applications in the app store according to both their prices and categories.
