# Ex1 - Filtering and Sorting Data

This time we are going to pull data directly from the internet.
Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

### Step 1. Import the necessary libraries


```python
import pandas as pd 
import numpy as np 
```

### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv). 

### Step 3. Assign it to a variable called chipo.


```python
ch = pd.read_table("https://raw.githubusercontent.com/justmarkham/DAT8/master/data/chipotle.tsv")
ch
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>NaN</td>
      <td>$2.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Izze</td>
      <td>[Clementine]</td>
      <td>$3.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1</td>
      <td>Nantucket Nectar</td>
      <td>[Apple]</td>
      <td>$3.39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Chips and Tomatillo-Green Chili Salsa</td>
      <td>NaN</td>
      <td>$2.39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Tomatillo-Red Chili Salsa (Hot), [Black Beans...</td>
      <td>$16.98</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4617</th>
      <td>1833</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Sour ...</td>
      <td>$11.75</td>
    </tr>
    <tr>
      <th>4618</th>
      <td>1833</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Sour Cream, Cheese...</td>
      <td>$11.75</td>
    </tr>
    <tr>
      <th>4619</th>
      <td>1834</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Pinto...</td>
      <td>$11.25</td>
    </tr>
    <tr>
      <th>4620</th>
      <td>1834</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Lettu...</td>
      <td>$8.75</td>
    </tr>
    <tr>
      <th>4621</th>
      <td>1834</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Pinto...</td>
      <td>$8.75</td>
    </tr>
  </tbody>
</table>
<p>4622 rows × 5 columns</p>
</div>




```python
ch.shape[0] , ch.shape[1]
```




    (4622, 5)




```python
ch.describe(include="all")
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4622.000000</td>
      <td>4622.000000</td>
      <td>4622</td>
      <td>3376</td>
      <td>4622</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>50</td>
      <td>1043</td>
      <td>78</td>
    </tr>
    <tr>
      <th>top</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Chicken Bowl</td>
      <td>[Diet Coke]</td>
      <td>$8.75</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>726</td>
      <td>134</td>
      <td>730</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>927.254868</td>
      <td>1.075725</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>528.890796</td>
      <td>0.410186</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>477.250000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>926.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1393.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1834.000000</td>
      <td>15.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Step 4. How many products cost more than $10.00?


```python
ch.query('item_price > 10').item_name.nunique()
```




    31



### Step 5. What is the price of each item? 
###### print a data frame with only two columns item_name and item_price


```python
ch[["item_name" , "item_price"]]
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
      <th>item_name</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Izze</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Nantucket Nectar</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chips and Tomatillo-Green Chili Salsa</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chicken Bowl</td>
      <td>16.98</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4617</th>
      <td>Steak Burrito</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>4618</th>
      <td>Steak Burrito</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>4619</th>
      <td>Chicken Salad Bowl</td>
      <td>11.25</td>
    </tr>
    <tr>
      <th>4620</th>
      <td>Chicken Salad Bowl</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>4621</th>
      <td>Chicken Salad Bowl</td>
      <td>8.75</td>
    </tr>
  </tbody>
</table>
<p>4622 rows × 2 columns</p>
</div>



### Step 6. Sort by the name of the item


```python
ch.sort_values(by="item_name")
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3389</th>
      <td>1360</td>
      <td>2</td>
      <td>6 Pack Soft Drink</td>
      <td>[Diet Coke]</td>
      <td>12.98</td>
    </tr>
    <tr>
      <th>341</th>
      <td>148</td>
      <td>1</td>
      <td>6 Pack Soft Drink</td>
      <td>[Diet Coke]</td>
      <td>6.49</td>
    </tr>
    <tr>
      <th>1849</th>
      <td>749</td>
      <td>1</td>
      <td>6 Pack Soft Drink</td>
      <td>[Coke]</td>
      <td>6.49</td>
    </tr>
    <tr>
      <th>1860</th>
      <td>754</td>
      <td>1</td>
      <td>6 Pack Soft Drink</td>
      <td>[Diet Coke]</td>
      <td>6.49</td>
    </tr>
    <tr>
      <th>2713</th>
      <td>1076</td>
      <td>1</td>
      <td>6 Pack Soft Drink</td>
      <td>[Coke]</td>
      <td>6.49</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2384</th>
      <td>948</td>
      <td>1</td>
      <td>Veggie Soft Tacos</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>781</th>
      <td>322</td>
      <td>1</td>
      <td>Veggie Soft Tacos</td>
      <td>[Fresh Tomato Salsa, [Black Beans, Cheese, Sou...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2851</th>
      <td>1132</td>
      <td>1</td>
      <td>Veggie Soft Tacos</td>
      <td>[Roasted Chili Corn Salsa (Medium), [Black Bea...</td>
      <td>8.49</td>
    </tr>
    <tr>
      <th>1699</th>
      <td>688</td>
      <td>1</td>
      <td>Veggie Soft Tacos</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...</td>
      <td>11.25</td>
    </tr>
    <tr>
      <th>1395</th>
      <td>567</td>
      <td>1</td>
      <td>Veggie Soft Tacos</td>
      <td>[Fresh Tomato Salsa (Mild), [Pinto Beans, Rice...</td>
      <td>8.49</td>
    </tr>
  </tbody>
</table>
<p>4622 rows × 5 columns</p>
</div>



### Step 7. What was the quantity of the most expensive item ordered?


```python
ch.sort_values(by = "item_price", ascending = False).head(1)
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3598</th>
      <td>1443</td>
      <td>15</td>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>NaN</td>
      <td>44.25</td>
    </tr>
  </tbody>
</table>
</div>



### Step 8. How many times was a Veggie Salad Bowl ordered?


```python
ch[ch.item_name == 'Veggie Salad Bowl'].shape[0]
```




    18



### Step 9. How many times did someone order more than one Canned Soda?


```python
ch[(ch.item_name == 'Canned Soda') & (ch.quantity>1)].shape[0]
```




    20


