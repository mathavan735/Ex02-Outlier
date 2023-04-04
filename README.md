Ex02-Outlier

You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

(1) Remove outliers using IQR 

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

    (i) Using IQR detect weight outliers and print them

    (ii) Using IQR, detect height outliers and print them



DEVELOPED BY: Mathavan s

REFERENCE NO: 212221220031

import pandas as pd
import seaborn as sns
import numpy as np
from scipy import stats
df=pd.read_csv('bhp.csv')
print(df['price_per_sqft'])
sns.boxplot(x="price_per_sqft",data=df)
df.shape


q1=df['price_per_sqft'].quantile(0.25)
q3=df['price_per_sqft'].quantile(0.75)
iqr=q3-q1
print("FIRST QUANTILE=",q1,"\nSECOND QUANTILE=",q3)
low=q1-1.5*iqr
high=q3+1.5*iqr
df_filtered=df[((df['price_per_sqft']>=low)&(df['price_per_sqft']<=high))]
sns.boxplot(x="price_per_sqft",data=df_filtered)


from scipy import stats
import numpy as np
z=np.abs(stats.zscore(df['price_per_sqft']))
df_filtered=df_filtered[(z<3)]
sns.boxplot(x='price_per_sqft',data=df_filtered)


q1=df.quantile(0.25)
q3=df.quantile(0.75)
iqr=q3-q1
low=q1-1.5*iqr
high=q3+1.5*iqr
df_fil=df[((df<=high)&(df>=low))]
outliers=np.setdiff1d(df['weight'],df_fil['weight'])
print("THE OUTLIERS IN THE DATA SET WEIGHT:",outliers)


q1=df.quantile(0.25)
q3=df.quantile(0.75)
iqr=q3-q1
low=q1-1.5*iqr
high=q3+1.5*iqr
df_fil=df[((df<=high)&(df>=low))]
outliers=np.setdiff1d(df['height'],df_fil['height'])
print("THE OUTLIERS IN THE DATA SET height:",outliers)


![Screenshot (16)](https://user-images.githubusercontent.com/119560261/227783342-d25b5b69-26e5-4e7e-a0f1-bba37886cf19.png)
![Screenshot (17)](https://user-images.githubusercontent.com/119560261/227783357-8429d78f-6d61-4a39-8009-27568154f221.png)
![Screenshot (18)](https://user-images.githubusercontent.com/119560261/227783366-e89e32c6-1579-4bc9-80c3-516bc1818f99.png)
![Screenshot (19)](https://user-images.githubusercontent.com/119560261/227783375-fe03a415-e5a0-4136-9631-cd6441ab427c.png)
![Screenshot (20)](https://user-images.githubusercontent.com/119560261/227783381-6dca7e49-c026-4617-b760-98300d88d2d9.png)
