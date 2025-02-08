# Project 1
## The Problem
There is a large divide between urban and rural areas in America. This project looks to find the difference between the median household income in urban and rural counties, and which states have the largest gap.

## The Data
A data set using data from the U.S. Census Bureau's 2023 American Community Survery was used for this project. The data used a method to define urban counties as counties with a population above the median, otherwise, the county was classified as rural.
[data set](https://www.kaggle.com/datasets/ahmedmohamed2003/income-urban-vs-rural-for-each-county/data)



```python
#import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
#Data set being used
df = pd.read_csv("Income_Urban_VS_Rural.csv")
```

## Preprocessing
This dataset was very clean to begin with, and contained no null values. However, and issue was found with two counties having extremely low median household incomes that threw off the averages for their states. Those two counties have small populations, and the values given to them appeared to be generic filler data, so the two counties were removed from the dataset.


```python
df.isnull().sum()
```




    County                     0
    State                      0
    FIPS                       0
    State FIPS Code            0
    County FIPS Code           0
    Total Population           0
    Median Household Income    0
    Urban-Rural                0
    dtype: int64




```python
df.dtypes
```




    County                     object
    State                      object
    FIPS                        int64
    State FIPS Code             int64
    County FIPS Code            int64
    Total Population            int64
    Median Household Income     int64
    Urban-Rural                object
    dtype: object




```python
df.groupby(['State'])['Median Household Income'].mean()
```




    State
    Alabama                 5.419584e+04
    Alaska                  7.940733e+04
    Arizona                 6.266260e+04
    Arkansas                5.115593e+04
    California              8.700114e+04
    Colorado                7.479234e+04
    Connecticut             9.330678e+04
    Delaware                8.031167e+04
    District of Columbia    1.062870e+05
    Florida                 6.546791e+04
    Georgia                 6.048755e+04
    Hawaii                  9.128340e+04
    Idaho                   6.577025e+04
    Illinois                6.857970e+04
    Indiana                 6.868068e+04
    Iowa                    6.983003e+04
    Kansas                  6.442795e+04
    Kentucky                5.590920e+04
    Louisiana               5.525036e+04
    Maine                   6.687212e+04
    Maryland                9.415212e+04
    Massachusetts           9.654629e+04
    Michigan                6.430395e+04
    Minnesota               7.575739e+04
    Mississippi             4.851435e+04
    Missouri                5.950310e+04
    Montana                 6.229455e+04
    Nebraska                6.688039e+04
    Nevada                 -3.914490e+07
    New Hampshire           8.652050e+04
    New Jersey              1.008907e+05
    New Mexico              5.546864e+04
    New York                7.643269e+04
    North Carolina          6.107221e+04
    North Dakota            7.253702e+04
    Ohio                    6.810123e+04
    Oklahoma                5.827297e+04
    Oregon                  6.996544e+04
    Pennsylvania            6.961363e+04
    Puerto Rico             2.369932e+04
    Rhode Island            9.674900e+04
    South Carolina          5.700570e+04
    South Dakota            6.692577e+04
    Tennessee               5.899419e+04
    Texas                  -2.560190e+06
    Utah                    8.017572e+04
    Vermont                 7.504250e+04
    Virginia                7.495723e+04
    Washington              7.636338e+04
    West Virginia           5.474625e+04
    Wisconsin               7.171549e+04
    Wyoming                 7.336004e+04
    Name: Median Household Income, dtype: float64




```python
#Texas and Nevada Seem to have two counties that throw averages off
df.sort_values(by = ['Median Household Income'], ascending=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>County</th>
      <th>State</th>
      <th>FIPS</th>
      <th>State FIPS Code</th>
      <th>County FIPS Code</th>
      <th>Total Population</th>
      <th>Median Household Income</th>
      <th>Urban-Rural</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1753</th>
      <td>Esmeralda County</td>
      <td>Nevada</td>
      <td>32009</td>
      <td>32</td>
      <td>9</td>
      <td>962</td>
      <td>-666666666</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2655</th>
      <td>Kenedy County</td>
      <td>Texas</td>
      <td>48261</td>
      <td>48</td>
      <td>261</td>
      <td>52</td>
      <td>-666666666</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3186</th>
      <td>Las Marías Municipio</td>
      <td>Puerto Rico</td>
      <td>72083</td>
      <td>72</td>
      <td>83</td>
      <td>8790</td>
      <td>16170</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3172</th>
      <td>Guánica Municipio</td>
      <td>Puerto Rico</td>
      <td>72055</td>
      <td>72</td>
      <td>55</td>
      <td>13266</td>
      <td>16210</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3166</th>
      <td>Comerío Municipio</td>
      <td>Puerto Rico</td>
      <td>72045</td>
      <td>72</td>
      <td>45</td>
      <td>18775</td>
      <td>17254</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2850</th>
      <td>Fairfax County</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>51</td>
      <td>59</td>
      <td>1144474</td>
      <td>150113</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2927</th>
      <td>Falls Church city</td>
      <td>Virginia</td>
      <td>51610</td>
      <td>51</td>
      <td>610</td>
      <td>14593</td>
      <td>154734</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>227</th>
      <td>San Mateo County</td>
      <td>California</td>
      <td>6081</td>
      <td>6</td>
      <td>81</td>
      <td>745100</td>
      <td>156000</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>229</th>
      <td>Santa Clara County</td>
      <td>California</td>
      <td>6085</td>
      <td>6</td>
      <td>85</td>
      <td>1903297</td>
      <td>159674</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2874</th>
      <td>Loudoun County</td>
      <td>Virginia</td>
      <td>51107</td>
      <td>51</td>
      <td>107</td>
      <td>427082</td>
      <td>178707</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
<p>3222 rows × 8 columns</p>
</div>




```python
filtered_df = df[df['Median Household Income'] >= 0]
filtered_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>County</th>
      <th>State</th>
      <th>FIPS</th>
      <th>State FIPS Code</th>
      <th>County FIPS Code</th>
      <th>Total Population</th>
      <th>Median Household Income</th>
      <th>Urban-Rural</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Autauga County</td>
      <td>Alabama</td>
      <td>1001</td>
      <td>1</td>
      <td>1</td>
      <td>59285</td>
      <td>69841</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Baldwin County</td>
      <td>Alabama</td>
      <td>1003</td>
      <td>1</td>
      <td>3</td>
      <td>239945</td>
      <td>75019</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Barbour County</td>
      <td>Alabama</td>
      <td>1005</td>
      <td>1</td>
      <td>5</td>
      <td>24757</td>
      <td>44290</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bibb County</td>
      <td>Alabama</td>
      <td>1007</td>
      <td>1</td>
      <td>7</td>
      <td>22152</td>
      <td>51215</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blount County</td>
      <td>Alabama</td>
      <td>1009</td>
      <td>1</td>
      <td>9</td>
      <td>59292</td>
      <td>61096</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3217</th>
      <td>Vega Baja Municipio</td>
      <td>Puerto Rico</td>
      <td>72145</td>
      <td>72</td>
      <td>145</td>
      <td>54058</td>
      <td>23877</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3218</th>
      <td>Vieques Municipio</td>
      <td>Puerto Rico</td>
      <td>72147</td>
      <td>72</td>
      <td>147</td>
      <td>8147</td>
      <td>17531</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3219</th>
      <td>Villalba Municipio</td>
      <td>Puerto Rico</td>
      <td>72149</td>
      <td>72</td>
      <td>149</td>
      <td>21778</td>
      <td>24882</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>3220</th>
      <td>Yabucoa Municipio</td>
      <td>Puerto Rico</td>
      <td>72151</td>
      <td>72</td>
      <td>151</td>
      <td>29868</td>
      <td>21279</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3221</th>
      <td>Yauco Municipio</td>
      <td>Puerto Rico</td>
      <td>72153</td>
      <td>72</td>
      <td>153</td>
      <td>33509</td>
      <td>21918</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
<p>3220 rows × 8 columns</p>
</div>




```python
#Median household income of counties by state
filtered_df.groupby(['State'])['Median Household Income'].mean()
```




    State
    Alabama                  54195.835821
    Alaska                   79407.333333
    Arizona                  62662.600000
    Arkansas                 51155.933333
    California               87001.137931
    Colorado                 74792.343750
    Connecticut              93306.777778
    Delaware                 80311.666667
    District of Columbia    106287.000000
    Florida                  65467.910448
    Georgia                  60487.553459
    Hawaii                   91283.400000
    Idaho                    65770.250000
    Illinois                 68579.696078
    Indiana                  68680.684783
    Iowa                     69830.030303
    Kansas                   64427.952381
    Kentucky                 55909.200000
    Louisiana                55250.359375
    Maine                    66872.125000
    Maryland                 94152.125000
    Massachusetts            96546.285714
    Michigan                 64303.951807
    Minnesota                75757.390805
    Mississippi              48514.353659
    Missouri                 59503.095652
    Montana                  62294.553571
    Nebraska                 66880.387097
    Nevada                   75206.125000
    New Hampshire            86520.500000
    New Jersey              100890.666667
    New Mexico               55468.636364
    New York                 76432.693548
    North Carolina           61072.210000
    North Dakota             72537.018868
    Ohio                     68101.227273
    Oklahoma                 58272.974026
    Oregon                   69965.444444
    Pennsylvania             69613.626866
    Puerto Rico              23699.320513
    Rhode Island             96749.000000
    South Carolina           57005.695652
    South Dakota             66925.772727
    Tennessee                58994.189474
    Texas                    64736.901186
    Utah                     80175.724138
    Vermont                  75042.500000
    Virginia                 74957.233083
    Washington               76363.384615
    West Virginia            54746.254545
    Wisconsin                71715.486111
    Wyoming                  73360.043478
    Name: Median Household Income, dtype: float64




```python
national_income_dif = filtered_df.groupby(['Urban-Rural'])['Median Household Income'].mean()
national_income_dif.plot(kind = 'bar')
plt.ylabel('Income')
plt.title("National Median Household Income in Urban vs. Rural Counties")
```




    Text(0.5, 1.0, 'National Median Household Income in Urban vs. Rural Counties')




    
![png](output_10_1.png)
    



```python
#Groups median household income by state and whether it's urban or rural
filtered_urban_rural = filtered_df.groupby(['State', 'Urban-Rural'])['Median Household Income'].mean()
```


```python
nc_urban_rural = filtered_df[filtered_df['State'] == 'North Carolina'].groupby(['State', 'Urban-Rural'])['Median Household Income'].mean()
```


```python
nc_urban_rural.plot(kind = 'bar')
plt.ylabel("Income")
plt.title("NC Median Household Income Urban vs. Rural")
```




    Text(0.5, 1.0, 'NC Median Household Income Urban vs. Rural')




    
![png](output_13_1.png)
    



```python
sns.set(rc={"figure.figsize":(20,12)}) # change the figure size to width=20, height=12
sns.scatterplot(data=filtered_df, x='Median Household Income', y='State', hue='Urban-Rural')
```




    <Axes: xlabel='Median Household Income', ylabel='State'>




    
![png](output_14_1.png)
    



```python
nc_df = filtered_df[filtered_df['State'] == 'North Carolina']
va_df = filtered_df[filtered_df['State'] == 'Virginia']
pr_df = filtered_df[filtered_df['State'] == 'Puerto Rico']
```


```python
sns.set(rc={"figure.figsize":(20,12)}) # change the figure size to width=20, height=12
sns.scatterplot(data=filtered_df, x='Total Population', y='Median Household Income', hue='Urban-Rural')
```




    <Axes: xlabel='Total Population', ylabel='Median Household Income'>




    
![png](output_16_1.png)
    



```python
sns.set(rc={"figure.figsize":(20,12)}) # change the figure size to width=20, height=12
sns.scatterplot(data=nc_df, x='Total Population', y='Median Household Income')
```




    <Axes: xlabel='Total Population', ylabel='Median Household Income'>




    
![png](output_17_1.png)
    



```python
sns.set(rc={"figure.figsize":(20,12)}) # change the figure size to width=20, height=12
sns.scatterplot(data=va_df, x='Total Population', y='Median Household Income')
```




    <Axes: xlabel='Total Population', ylabel='Median Household Income'>




    
![png](output_18_1.png)
    



```python
sns.set(rc={"figure.figsize":(20,12)}) # change the figure size to width=20, height=12
sns.scatterplot(data=pr_df, x='Total Population', y='Median Household Income')
```




    <Axes: xlabel='Total Population', ylabel='Median Household Income'>




    
![png](output_19_1.png)
    


## Findings
When comparing the median income between urban and rural counties, there is a clear trend of urban counties being wealthier than rural counties in every state that has a rural county (Connecticut does not have any rural counties). Though urban counties tend to have higher incomes than rural counties, the most populous counties are not always the counties witht the highest median household incomes. In the cases of both North Carolina and Virginia, the counties with highest income were not the most populous. Virginia also appeared to have a large median household income range, with their being a massive difference between their county witht he lowest income and their county with the highest income.

There was one unintended finding from this data, which is the large disparity between median household incomes of counties in Puerto Rico and those of counties within a state. The counties with the lowest median household incomes were found in Puerto Rico, and the Puerto Rican county with the heighest median household income was still far below many urban counties within states.

## Impact
These findings provide important insight into the economic disparities between urban and rural counties, and which states have the largest disparity. The unequal economic condition of Puerto Rico when compared to states was also shown through this data set. One possible harm of this data is it being used to make disparaging claims about states (or a territory in the case of Puerto Rico) that have low median household incomes, and being used to portray rural areas as poor and downtrodden.


```python

```
