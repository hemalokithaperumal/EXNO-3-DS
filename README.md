## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
df=pd.read_csv("Encoding Data.csv")
df
```
![1](https://github.com/user-attachments/assets/cc4ecbc8-b3a6-48bc-8eb0-9837edf97ed6)

```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```
![2](https://github.com/user-attachments/assets/fc5870c2-2886-459a-8395-57680c613347)

```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```
![3](https://github.com/user-attachments/assets/a7ca1a5e-6a00-41f0-b654-97e6f421d121)

```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![4](https://github.com/user-attachments/assets/9f22c909-0b5a-4fc7-8691-79728ec85b7f)

```
from sklearn.preprocessing import OneHotEncoder
# Use sparse_output=False instead of sparse=False
ohe = OneHotEncoder(sparse_output=False)
df2 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
```
```
df2=pd.concat([df2,enc],axis=1)
df2
```
![6](https://github.com/user-attachments/assets/345869e0-c6a0-442c-a1e0-2920118e8f32)

```
pd.get_dummies(df2,columns=["nom_0"])
```
![7](https://github.com/user-attachments/assets/727d6aa4-6c2f-4c63-b3c5-da3db5e9ee2f)

```
pip install --upgrade category_encoders
```
```
from category_encoders import BinaryEncoder
df=pd.read_csv("dt.csv")
df
```
![9](https://github.com/user-attachments/assets/6c2501ec-858e-4fe5-8e9e-d8c8216e551f)
```
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![image](https://github.com/user-attachments/assets/1fb507a8-9d2f-4503-910a-7bc52453c383)

```
df.skew()
```

`![image](https://github.com/user-attachments/assets/9e13945b-22ec-41b8-b448-c7ab42661094)
```
df["Highly Positive Skew"]=np.log(df["Highly Positive Skew"])
df
```
![image](https://github.com/user-attachments/assets/68fdb7e6-bda0-403e-9ec1-ad58a3518436)


```
df["Moderate Positive Skew"]=np.reciprocal(df["Moderate Positive Skew"])
df
```

![image](https://github.com/user-attachments/assets/3a55b224-9c40-4993-8548-d1db527bd1e2)
```
df["Moderate Negative Skew_yeojohnson"],parameter=stats.yeojohnson(df["Moderate Negative Skew"])
df
```
![image](https://github.com/user-attachments/assets/7b59d15c-e2b9-4f5f-8a7f-054cb0380617)

```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/c3999973-02fa-40ca-a959-5fdd9f473b78)

``
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/da9a3506-5542-4cc3-8a0b-e1a8375dd0a4)

```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```

![image](https://github.com/user-attachments/assets/93b1e932-4e17-4d34-934e-093705d0aa72)

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()

```

![image](https://github.com/user-attachments/assets/e14553fb-d32c-42fd-9d93-bfe1a083da19)

# RESULT:

       Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully.

       
