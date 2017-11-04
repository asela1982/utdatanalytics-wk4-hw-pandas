
## Option 1: Heroes of Pymoli

![Fantasy](../Images/Fantasy.jpg)

Congratulations! After a lot of hard work in the data munging mines, you've landed a job as Lead Analyst for an independent gaming company. You've been assigned the task of analyzing the data for their most recent fantasy game Heroes of Pymoli. 

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.

Your final report should include each of the following:

**Player Count**

* Total Number of Players

**Purchasing Analysis (Total)**

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue

**Gender Demographics**

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

**Purchasing Analysis (Gender)** 

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

**Most Popular Items**

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

**Most Profitable Items**

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

As final considerations:

* Your script must work for both data-sets given.
* You must use the Pandas Library and the Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames. 
* You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.  
* You must include a written description of three observable trends based on the data. 
* See [Example Solution](HeroesOfPymoli_Example.pdf) for a reference on expected format. 


```python
#import the necessary libraries
import os
import pandas as pd
import numpy as np
import json
```


```python
#derive the input file paths
filepath = os.path.join("","purchase_data.json")
```


```python
#construct the requried dataframes for the two json files
df = pd.read_json(filepath)
```


```python
#display the head of both the dataframe
display(df.head(5))
```


<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>



```python
#shape of the dataframes
display(df.shape)
```


    (780, 6)



```python
#datatypes of the dataframe
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 780 entries, 0 to 779
    Data columns (total 6 columns):
    Age          780 non-null int64
    Gender       780 non-null object
    Item ID      780 non-null int64
    Item Name    780 non-null object
    Price        780 non-null float64
    SN           780 non-null object
    dtypes: float64(1), int64(2), object(3)
    memory usage: 42.7+ KB


======================================================================================================================

**Player Count**

* Total Number of Players


```python
# Total Number of Players
df['SN'].nunique()
```




    573




```python
pd.DataFrame({"Total Number of Players":df['SN'].nunique()},index=[0]).style.set_properties(**{'background-color': 'ash',
                           'color': 'blue',
                           'border-color': 'white'})
```




<style  type="text/css" >
    #T_e921a3c6_c0ba_11e7_b4d3_186590d6f757row0_col0 {
            background-color:  ash;
            color:  blue;
            border-color:  white;
        }</style>  
<table id="T_e921a3c6_c0ba_11e7_b4d3_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Number of Players</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e921a3c6_c0ba_11e7_b4d3_186590d6f757" class="row_heading level0 row0" >0</th> 
        <td id="T_e921a3c6_c0ba_11e7_b4d3_186590d6f757row0_col0" class="data row0 col0" >573</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Purchasing Analysis (Total)**

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue


```python
# Number of Unique Items
df['Item ID'].nunique()
```




    183




```python
# Average Purchase Price
df['Price'].mean()
```




    2.931192307692303




```python
# Total Number of Purchases
len(df)
```




    780




```python
# Total Revenue
df['Price'].sum()
```




    2286.3299999999963




```python
pd.DataFrame({"Number of Unique Items":df['Item ID'].nunique(),
  "Average Purchase Price":df['Price'].mean(),
 "Total Number of Purchases":len(df),
"Total Revenue":df['Price'].sum()},index=[0]).style.set_properties(**{'background-color': 'ash',
                           'color': 'blue',
                           'border-color': 'white'})
```




<style  type="text/css" >
    #T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col0 {
            background-color:  ash;
            color:  blue;
            border-color:  white;
        }    #T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col1 {
            background-color:  ash;
            color:  blue;
            border-color:  white;
        }    #T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col2 {
            background-color:  ash;
            color:  blue;
            border-color:  white;
        }    #T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col3 {
            background-color:  ash;
            color:  blue;
            border-color:  white;
        }</style>  
<table id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Number of Unique Items</th> 
        <th class="col_heading level0 col2" >Total Number of Purchases</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757" class="row_heading level0 row0" >0</th> 
        <td id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col0" class="data row0 col0" >2.93119</td> 
        <td id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col1" class="data row0 col1" >183</td> 
        <td id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col2" class="data row0 col2" >780</td> 
        <td id="T_e9271d7a_c0ba_11e7_bd1c_186590d6f757row0_col3" class="data row0 col3" >2286.33</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Gender Demographics**

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed


```python
# get all the duplicate rows
display(df.loc[df.duplicated("SN",keep=False),:].sort_values("SN").head(10))
display(len(df.loc[df.duplicated("SN",keep=False),:]))
```


<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>431</th>
      <td>37</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Aduephos78</td>
    </tr>
    <tr>
      <th>308</th>
      <td>37</td>
      <td>Male</td>
      <td>79</td>
      <td>Alpha, Oath of Zeal</td>
      <td>2.88</td>
      <td>Aduephos78</td>
    </tr>
    <tr>
      <th>377</th>
      <td>37</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Aduephos78</td>
    </tr>
    <tr>
      <th>647</th>
      <td>26</td>
      <td>Male</td>
      <td>156</td>
      <td>Soul-Forged Steel Shortsword</td>
      <td>1.16</td>
      <td>Aeduera68</td>
    </tr>
    <tr>
      <th>721</th>
      <td>26</td>
      <td>Male</td>
      <td>39</td>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>2.35</td>
      <td>Aeduera68</td>
    </tr>
    <tr>
      <th>224</th>
      <td>26</td>
      <td>Male</td>
      <td>106</td>
      <td>Crying Steel Sickle</td>
      <td>2.29</td>
      <td>Aeduera68</td>
    </tr>
    <tr>
      <th>529</th>
      <td>38</td>
      <td>Male</td>
      <td>172</td>
      <td>Blade of the Grave</td>
      <td>1.69</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>359</th>
      <td>20</td>
      <td>Male</td>
      <td>32</td>
      <td>Orenmir</td>
      <td>4.95</td>
      <td>Aeliriam77</td>
    </tr>
    <tr>
      <th>637</th>
      <td>20</td>
      <td>Male</td>
      <td>18</td>
      <td>Torchlight, Bond of Storms</td>
      <td>1.77</td>
      <td>Aeliriam77</td>
    </tr>
  </tbody>
</table>
</div>



    375



```python
# drop the duplicate SN rows to get gender propotions
df_unique = df.drop_duplicates("SN", keep='first')
len(df_unique)
```




    573




```python
pd.DataFrame({'Percentage of players' : df_unique['Gender'].value_counts(normalize=True),
   'Total Count' : df_unique['Gender'].value_counts()}).style.bar(color='#05668D')
```




<style  type="text/css" >
    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row0_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row0_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row1_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 20.1%, transparent 0%);
        }    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row1_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 20.1%, transparent 0%);
        }    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row2_col0 {
            width:  10em;
             height:  80%;
        }    #T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row2_col1 {
            width:  10em;
             height:  80%;
        }</style>  
<table id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Percentage of players</th> 
        <th class="col_heading level0 col1" >Total Count</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757" class="row_heading level0 row0" >Male</th> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row0_col0" class="data row0 col0" >0.811518</td> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row0_col1" class="data row0 col1" >465</td> 
    </tr>    <tr> 
        <th id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757" class="row_heading level0 row1" >Female</th> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row1_col0" class="data row1 col0" >0.17452</td> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row1_col1" class="data row1 col1" >100</td> 
    </tr>    <tr> 
        <th id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row2_col0" class="data row2 col0" >0.0139616</td> 
        <td id="T_e92e23f6_c0ba_11e7_a9cb_186590d6f757row2_col1" class="data row2 col1" >8</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Purchasing Analysis (Gender)** 

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals (purchase total and divide it by the total count)


```python
summary_gender_purchasing = pd.DataFrame(df.groupby('Gender').agg({'Price':[np.mean,np.sum],'Item ID':'count'}))
summary_gender_purchasing.style.bar(color='#05668D')
```




<style  type="text/css" >
    #T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col0 {
            width:  10em;
             height:  80%;
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 19.0%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 20.1%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 31.1%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col1 {
            width:  10em;
             height:  80%;
        }    #T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col2 {
            width:  10em;
             height:  80%;
        }</style>  
<table id="T_e932816c_c0ba_11e7_bf73_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" colspan=2>Price</th> 
        <th class="col_heading level0 col2" >Item ID</th> 
    </tr>    <tr> 
        <th class="blank level1" ></th> 
        <th class="col_heading level1 col0" >mean</th> 
        <th class="col_heading level1 col1" >sum</th> 
        <th class="col_heading level1 col2" >count</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e932816c_c0ba_11e7_bf73_186590d6f757" class="row_heading level0 row0" >Female</th> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col0" class="data row0 col0" >2.81551</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col1" class="data row0 col1" >382.91</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row0_col2" class="data row0 col2" >136</td> 
    </tr>    <tr> 
        <th id="T_e932816c_c0ba_11e7_bf73_186590d6f757" class="row_heading level0 row1" >Male</th> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col0" class="data row1 col0" >2.95052</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col1" class="data row1 col1" >1867.68</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row1_col2" class="data row1 col2" >633</td> 
    </tr>    <tr> 
        <th id="T_e932816c_c0ba_11e7_bf73_186590d6f757" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col0" class="data row2 col0" >3.24909</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col1" class="data row2 col1" >35.74</td> 
        <td id="T_e932816c_c0ba_11e7_bf73_186590d6f757row2_col2" class="data row2 col2" >11</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals


```python
test = pd.DataFrame({'days': [0,31,45,60]})
test['range'] = pd.cut(test.days, [0,30,60,90], right=False)
test

# right : Indicates whether the bins include the rightmost edge or not. If
# right == True (the default), then the bins [1,2,3,4] indicate
# (1,2], (2,3], (3,4]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>days</th>
      <th>range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>[0, 30)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>31</td>
      <td>[30, 60)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45</td>
      <td>[30, 60)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>60</td>
      <td>[60, 90)</td>
    </tr>
  </tbody>
</table>
</div>




```python
age_bins = [0, 10, 15, 20, 25, 30, 35, 40, 100]
age_labels = ['<10', '10-14', '15-19', '20-24','25-29','30-34','35-39','40+']
df['Age_Group'] = pd.cut(df['Age'], bins ,labels = age_labels,right=False)
```


```python
summary_age = pd.DataFrame(df.groupby('Age_Group').agg({'Price':[np.mean,np.sum],'Item ID':'count'}))
```


```python
summary_age.style.bar(color='#05668D')
```




<style  type="text/css" >
    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 53.8%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 3.2%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 3.4%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col0 {
            width:  10em;
             height:  80%;
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 4.7%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 5.6%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 34.6%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 36.0%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 36.4%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 36.5%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 49.2%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 34.2%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 33.9%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 79.6%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 15.5%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 14.7%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 18.6%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col1 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 7.1%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col2 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 7.8%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col0 {
            width:  10em;
             height:  80%;
            background:  linear-gradient(90deg,#05668D 100.0%, transparent 0%);
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col1 {
            width:  10em;
             height:  80%;
        }    #T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col2 {
            width:  10em;
             height:  80%;
        }</style>  
<table id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" colspan=2>Price</th> 
        <th class="col_heading level0 col2" >Item ID</th> 
    </tr>    <tr> 
        <th class="blank level1" ></th> 
        <th class="col_heading level1 col0" >mean</th> 
        <th class="col_heading level1 col1" >sum</th> 
        <th class="col_heading level1 col2" >count</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Age_Group</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row0" ><10</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col0" class="data row0 col0" >2.98071</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col1" class="data row0 col1" >83.46</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row0_col2" class="data row0 col2" >28</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row1" >10-14</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col0" class="data row1 col0" >2.77</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col1" class="data row1 col1" >96.95</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row1_col2" class="data row1 col2" >35</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row2" >15-19</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col0" class="data row2 col0" >2.90541</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col1" class="data row2 col1" >386.42</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row2_col2" class="data row2 col2" >133</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row3" >20-24</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col0" class="data row3 col0" >2.91301</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col1" class="data row3 col1" >978.77</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row3_col2" class="data row3 col2" >336</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row4" >25-29</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col0" class="data row4 col0" >2.96264</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col1" class="data row4 col1" >370.33</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row4_col2" class="data row4 col2" >125</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row5" >30-34</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col0" class="data row5 col0" >3.08203</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col1" class="data row5 col1" >197.25</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row5_col2" class="data row5 col2" >64</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row6" >35-39</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col0" class="data row6 col0" >2.84286</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col1" class="data row6 col1" >119.4</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row6_col2" class="data row6 col2" >42</td> 
    </tr>    <tr> 
        <th id="T_e93f7f70_c0ba_11e7_934f_186590d6f757" class="row_heading level0 row7" >40+</th> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col0" class="data row7 col0" >3.16176</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col1" class="data row7 col1" >53.75</td> 
        <td id="T_e93f7f70_c0ba_11e7_934f_186590d6f757row7_col2" class="data row7 col2" >17</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value


```python
summary_spenders = pd.DataFrame(df.groupby(['SN']).agg({'Price':[np.mean,np.sum],'Item ID':'count'}))
```


```python
summary_spenders.sort_values(('Price','sum'),ascending=False)[:5].style.set_properties(**{'background-color': 'black',
                           'color': 'lawngreen',
                           'border-color': 'white'})
```




<style  type="text/css" >
    #T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }</style>  
<table id="T_e9455d82_c0ba_11e7_be64_186590d6f757" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" colspan=2>Price</th> 
        <th class="col_heading level0 col2" >Item ID</th> 
    </tr>    <tr> 
        <th class="blank level1" ></th> 
        <th class="col_heading level1 col0" >mean</th> 
        <th class="col_heading level1 col1" >sum</th> 
        <th class="col_heading level1 col2" >count</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e9455d82_c0ba_11e7_be64_186590d6f757" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col0" class="data row0 col0" >3.412</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col1" class="data row0 col1" >17.06</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row0_col2" class="data row0 col2" >5</td> 
    </tr>    <tr> 
        <th id="T_e9455d82_c0ba_11e7_be64_186590d6f757" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col0" class="data row1 col0" >3.39</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col1" class="data row1 col1" >13.56</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row1_col2" class="data row1 col2" >4</td> 
    </tr>    <tr> 
        <th id="T_e9455d82_c0ba_11e7_be64_186590d6f757" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col0" class="data row2 col0" >3.185</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col1" class="data row2 col1" >12.74</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row2_col2" class="data row2 col2" >4</td> 
    </tr>    <tr> 
        <th id="T_e9455d82_c0ba_11e7_be64_186590d6f757" class="row_heading level0 row3" >Haellysu29</th> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col0" class="data row3 col0" >4.24333</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col1" class="data row3 col1" >12.73</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row3_col2" class="data row3 col2" >3</td> 
    </tr>    <tr> 
        <th id="T_e9455d82_c0ba_11e7_be64_186590d6f757" class="row_heading level0 row4" >Eoda93</th> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col0" class="data row4 col0" >3.86</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col1" class="data row4 col1" >11.58</td> 
        <td id="T_e9455d82_c0ba_11e7_be64_186590d6f757row4_col2" class="data row4 col2" >3</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Most Popular Items**

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value


```python
summary_items = pd.DataFrame(df.groupby(['Item ID','Item Name']).agg({'Price':[np.mean,np.sum],'Item ID':'count'}))
```


```python
summary_items.sort_values(('Item ID','count'),ascending=False)[0:5].style.set_properties(**{'background-color': 'black',
                           'color': 'lawngreen',
                           'border-color': 'white'})
```




<style  type="text/css" >
    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }</style>  
<table id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" colspan=2>Price</th> 
        <th class="col_heading level0 col2" >Item ID</th> 
    </tr>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level1" ></th> 
        <th class="col_heading level1 col0" >mean</th> 
        <th class="col_heading level1 col1" >sum</th> 
        <th class="col_heading level1 col2" >count</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level0 row0" >39</th> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level1 row0" >Betrayal, Whisper of Grieving Widows</th> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col0" class="data row0 col0" >2.35</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col1" class="data row0 col1" >25.85</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row0_col2" class="data row0 col2" >11</td> 
    </tr>    <tr> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level0 row1" >84</th> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level1 row1" >Arcane Gem</th> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col0" class="data row1 col0" >2.23</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col1" class="data row1 col1" >24.53</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row1_col2" class="data row1 col2" >11</td> 
    </tr>    <tr> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level0 row2" >31</th> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level1 row2" >Trickster</th> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col0" class="data row2 col0" >2.07</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col1" class="data row2 col1" >18.63</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row2_col2" class="data row2 col2" >9</td> 
    </tr>    <tr> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level0 row3" >175</th> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level1 row3" >Woeful Adamantite Claymore</th> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col0" class="data row3 col0" >1.24</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col1" class="data row3 col1" >11.16</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row3_col2" class="data row3 col2" >9</td> 
    </tr>    <tr> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level0 row4" >13</th> 
        <th id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757" class="row_heading level1 row4" >Serenity</th> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col0" class="data row4 col0" >1.49</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col1" class="data row4 col1" >13.41</td> 
        <td id="T_fc6dad58_c0ba_11e7_a4f2_186590d6f757row4_col2" class="data row4 col2" >9</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

**Most Profitable Items**

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value


```python
summary_items = pd.DataFrame(df.groupby(['Item ID','Item Name']).agg({'Price':[np.mean,np.sum],'Item ID':'count'}))
```


```python
summary_items.sort_values(('Price','sum'),ascending=False)[0:5].style.set_properties(**{'background-color': 'black',
                           'color': 'lawngreen',
                           'border-color': 'white'})
```




<style  type="text/css" >
    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col0 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col1 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }    #T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col2 {
            background-color:  black;
            color:  lawngreen;
            border-color:  white;
        }</style>  
<table id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" colspan=2>Price</th> 
        <th class="col_heading level0 col2" >Item ID</th> 
    </tr>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level1" ></th> 
        <th class="col_heading level1 col0" >mean</th> 
        <th class="col_heading level1 col1" >sum</th> 
        <th class="col_heading level1 col2" >count</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level0 row0" >34</th> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level1 row0" >Retribution Axe</th> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col0" class="data row0 col0" >4.14</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col1" class="data row0 col1" >37.26</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row0_col2" class="data row0 col2" >9</td> 
    </tr>    <tr> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level0 row1" >115</th> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level1 row1" >Spectral Diamond Doomblade</th> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col0" class="data row1 col0" >4.25</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col1" class="data row1 col1" >29.75</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row1_col2" class="data row1 col2" >7</td> 
    </tr>    <tr> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level0 row2" >32</th> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level1 row2" >Orenmir</th> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col0" class="data row2 col0" >4.95</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col1" class="data row2 col1" >29.7</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row2_col2" class="data row2 col2" >6</td> 
    </tr>    <tr> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level0 row3" >103</th> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level1 row3" >Singed Scalpel</th> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col0" class="data row3 col0" >4.87</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col1" class="data row3 col1" >29.22</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row3_col2" class="data row3 col2" >6</td> 
    </tr>    <tr> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level0 row4" >107</th> 
        <th id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757" class="row_heading level1 row4" >Splitter, Foe Of Subtlety</th> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col0" class="data row4 col0" >3.61</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col1" class="data row4 col1" >28.88</td> 
        <td id="T_1f60e6e8_c0bb_11e7_a76f_186590d6f757row4_col2" class="data row4 col2" >8</td> 
    </tr></tbody> 
</table> 



======================================================================================================================

### Observations

    As per the Game's purchasing data, Eighty-one percent of men made a purchase, compared to 17% of women indicating that the game is more popular among the male demographics. 

    Those consumers aged 20 to 24, remain the key age demographic for pymoli, spending more money than any other age group.
    
    Those consumers aged 40 and above remain the age group purchasing high value items.


```python

```
