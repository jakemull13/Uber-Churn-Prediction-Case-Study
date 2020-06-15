## Case Study

Today we are going to use all the skills we have learned to tackle a real
problem in industry. The problem is churn prediction with a ride-sharing
company in San Francisco.  


## Import Data


```python
df = pd.read_csv('data/churn.csv')
df

df_train = pd.read_csv('data/churn_train.csv')
df_train

df_test = pd.read_csv('data/churn_test.csv')
df_test
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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>5.0</td>
      <td>4.7</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>2014-06-17</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-05-05</td>
      <td>Android</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>5.0</td>
      <td>4.3</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-07</td>
      <td>iPhone</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.9</td>
      <td>4.6</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>2014-06-29</td>
      <td>iPhone</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.9</td>
      <td>4.4</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>2014-03-15</td>
      <td>Android</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.2</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>2014-06-05</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-25</td>
      <td>iPhone</td>
      <td>2014-01-24</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-05-22</td>
      <td>Android</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-15</td>
      <td>iPhone</td>
      <td>2014-01-14</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-04-20</td>
      <td>Android</td>
      <td>2014-01-18</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 12 columns</p>
</div>






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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6.94</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-05-03</td>
      <td>Android</td>
      <td>2014-01-12</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.06</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-26</td>
      <td>Android</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>2</td>
      <td>True</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.50</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-05-21</td>
      <td>iPhone</td>
      <td>2014-01-02</td>
      <td>0.0</td>
      <td>1</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9.46</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>2.75</td>
      <td>Winterfell</td>
      <td>2014-01-10</td>
      <td>Android</td>
      <td>2014-01-09</td>
      <td>100.0</td>
      <td>1</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13.77</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-05-13</td>
      <td>iPhone</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39995</th>
      <td>2.06</td>
      <td>4.8</td>
      <td>4.3</td>
      <td>1.08</td>
      <td>Winterfell</td>
      <td>2014-04-02</td>
      <td>Android</td>
      <td>2014-01-26</td>
      <td>9.5</td>
      <td>8</td>
      <td>False</td>
      <td>90.5</td>
    </tr>
    <tr>
      <th>39996</th>
      <td>2.05</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>2014-05-09</td>
      <td>iPhone</td>
      <td>2014-01-08</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>85.7</td>
    </tr>
    <tr>
      <th>39997</th>
      <td>3.04</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-06-24</td>
      <td>Android</td>
      <td>2014-01-04</td>
      <td>0.0</td>
      <td>3</td>
      <td>True</td>
      <td>33.3</td>
    </tr>
    <tr>
      <th>39998</th>
      <td>3.49</td>
      <td>4.3</td>
      <td>3.3</td>
      <td>1.50</td>
      <td>Astapor</td>
      <td>2014-02-09</td>
      <td>iPhone</td>
      <td>2014-01-08</td>
      <td>40.0</td>
      <td>5</td>
      <td>False</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>39999</th>
      <td>4.25</td>
      <td>4.7</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-06-27</td>
      <td>iPhone</td>
      <td>2014-01-18</td>
      <td>0.0</td>
      <td>2</td>
      <td>True</td>
      <td>42.9</td>
    </tr>
  </tbody>
</table>
<p>40000 rows × 12 columns</p>
</div>






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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.48</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-01-07</td>
      <td>Android</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>2</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.81</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-04-29</td>
      <td>iPhone</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12.95</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-29</td>
      <td>Android</td>
      <td>2014-01-19</td>
      <td>0.0</td>
      <td>1</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.92</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-02-16</td>
      <td>iPhone</td>
      <td>2014-01-09</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.46</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-09</td>
      <td>iPhone</td>
      <td>2014-01-07</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>100.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9995</th>
      <td>2.11</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>2014-02-01</td>
      <td>iPhone</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>9996</th>
      <td>5.49</td>
      <td>4.9</td>
      <td>4.1</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-05-27</td>
      <td>iPhone</td>
      <td>2014-01-30</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>33.3</td>
    </tr>
    <tr>
      <th>9997</th>
      <td>2.49</td>
      <td>4.2</td>
      <td>4.6</td>
      <td>1.25</td>
      <td>Winterfell</td>
      <td>2014-05-24</td>
      <td>Android</td>
      <td>2014-01-15</td>
      <td>18.8</td>
      <td>9</td>
      <td>True</td>
      <td>90.6</td>
    </tr>
    <tr>
      <th>9998</th>
      <td>1.05</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-23</td>
      <td>Android</td>
      <td>2014-01-22</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>9999</th>
      <td>6.31</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-04-27</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>10000 rows × 12 columns</p>
</div>




```python

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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
      <th>Churn</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>5.0</td>
      <td>4.700000</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>2014-06-17</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-05-05</td>
      <td>True</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>5.0</td>
      <td>4.300000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-07</td>
      <td>False</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.9</td>
      <td>4.600000</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>2014-06-29</td>
      <td>False</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.9</td>
      <td>4.400000</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>2014-03-15</td>
      <td>True</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
      <td>True</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.2</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>2014-06-05</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-25</td>
      <td>False</td>
      <td>2014-01-24</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>0.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-05-22</td>
      <td>True</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>100.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>3.5</td>
      <td>3.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-15</td>
      <td>False</td>
      <td>2014-01-14</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>100.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>5.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-04-20</td>
      <td>True</td>
      <td>2014-01-18</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>0.0</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 13 columns</p>
</div>



## Clean Data


```python
df_clean = pd.read_csv('data/Churn_clean.csv', index_col=0)
df_clean.dropna(inplace=True)
df_clean['signup_date']=pd.to_datetime(df_clean['signup_date'])

features = ['avg_dist', 'avg_rating_by_driver', 'avg_rating_of_driver', 'avg_surge',
       'city', 'phone', 'signup_date', 'surge_pct',
       'trips_in_first_30_days', 'luxury_car_user', 'weekday_pct']
X = df_clean[features]
y = df_clean['Churn']
X
y
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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>5.0</td>
      <td>4.700000</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>True</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>5.0</td>
      <td>4.300000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.9</td>
      <td>4.600000</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.9</td>
      <td>4.400000</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>True</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.2</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-24</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>True</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>3.5</td>
      <td>3.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-14</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>5.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>True</td>
      <td>2014-01-18</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>49604 rows × 11 columns</p>
</div>






    0        False
    1         True
    2         True
    3        False
    4         True
             ...  
    49995    False
    49996     True
    49997     True
    49998     True
    49999     True
    Name: Churn, Length: 49604, dtype: bool




```python
X['phone'] = X['phone'].astype(bool)
```

    /Users/jacobmullins/opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.



```python
X['kings_landing'] = X['city'].apply(lambda x: x == "King's Landing")
X['astapor'] = X['city'].apply(lambda x: x == "Astapor")
X.drop(columns=['city'], inplace=True)
```

    /Users/jacobmullins/opt/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.



```python
X['signup_date'] = X['signup_date'].apply(lambda x: x.day)
```


```python
X
X.dtypes
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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>luxury_car_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>5.0</td>
      <td>4.700000</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>True</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>5.0</td>
      <td>4.300000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.9</td>
      <td>4.600000</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.9</td>
      <td>4.400000</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>True</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.2</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>False</td>
      <td>2014-01-25</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-24</td>
      <td>0.0</td>
      <td>1</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>5.0</td>
      <td>5.000000</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>True</td>
      <td>2014-01-31</td>
      <td>0.0</td>
      <td>0</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>3.5</td>
      <td>3.000000</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>False</td>
      <td>2014-01-14</td>
      <td>0.0</td>
      <td>2</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>5.0</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>True</td>
      <td>2014-01-18</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>49604 rows × 11 columns</p>
</div>






    avg_dist                         float64
    avg_rating_by_driver             float64
    avg_rating_of_driver             float64
    avg_surge                        float64
    city                              object
    phone                             object
    signup_date               datetime64[ns]
    surge_pct                        float64
    trips_in_first_30_days             int64
    luxury_car_user                     bool
    weekday_pct                      float64
    dtype: object




```python
#X_training = pd.read_csv('data/Churn_Xtrain.csv', index_col=0)
#X_test = pd.read_csv('data/Churn_Xtest.csv', index_col=0)
#y_training = pd.read_csv('data/Churn_ytrain.csv', index_col=0)
#y_test = pd.read_csv('data/Churn_ytest.csv', index_col=0)
#
#X_training.shape
#X_test.shape
#y_training.shape
#y_test.shape

X_training, X_test, y_training, y_test = train_test_split(X, y)
```

## EDA


```python
import seaborn as sns

def plot_correlation_matrix(X):
    corr = X.corr()
    ax = sns.heatmap(
        corr, 
        vmin=-1, vmax=1, center=0,
        cmap=sns.diverging_palette(20, 220, n=200),
        square=True
    )
    ax.set_xticklabels(
        ax.get_xticklabels(),
        rotation=45,
        horizontalalignment='right'
    );
    return 

def plot_logistic_regression(X, feature, y):
    pass

def get_p_values(X, y):
    pass
```


```python
plot_correlation_matrix(X_training)
plt.title('Feature Correlation')
plt.tight_layout()
plt.savefig('feature_correlations', dpi=240)
```




    Text(0.5, 1, 'Feature Correlation')




![png](output_13_1.png)


## Model


```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split

from sklearn.ensemble import RandomForestClassifier

from sklearn.inspection import plot_partial_dependence
```


```python
#logistic
def train_logistic_model(X, y):
    model = LogisticRegression()
    X_train, X_valid, y_train, y_valid = train_test_split(X, y, random_state=1)
    model.fit(X_train, y_train)
    #coeffs = model._coeffs
    y_predict = model.predict(X_valid)
    score = mean_squared_error(y_valid, y_predict)
    return score

#random forest
X_train, X_valid, y_train, y_valid = train_test_split(X_training, y_training)
y_train = y_train.values
y_valid = y_valid.values

def train_random_forest(X_train, y_train, X_valid, y_valid, num_trees=100):
    #X_train, X_valid, y_train, y_valid = train_test_split(X, y)
    rf = RandomForestClassifier(oob_score=True, n_estimators=num_trees)
    rf.fit(X_train, y_train)
    feature_importance = pd.DataFrame(rf.feature_importances_, index=X_train.columns)
    oob_score = rf.oob_score_
    
    return rf, feature_importance, oob_score
    
#def test_random_forest(X_train, y_train, X_valid, y_valid, num_trees=100):
#    model = train_random_forest(X_train, y_train, X_valid, y_valid, num_trees=num_trees)[0]
#    y_predict = model.predict(X_valid)
#    y_predict.reshape(-1, 1)
#    y_valid.reshape(-1, 1)
#    print(y_predict.shape, y_valid.shape)
#    score = model.score(y_valid, y_predict)
#    
#    return score
#      
```


```python

```


```python

```


```python
rf1, feature_importance, oob_score = train_random_forest(X_train, y_train, X_valid, y_valid)
feature_importance
score
oob_score
rf1
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>avg_dist</th>
      <td>0.203373</td>
    </tr>
    <tr>
      <th>avg_rating_by_driver</th>
      <td>0.108149</td>
    </tr>
    <tr>
      <th>avg_rating_of_driver</th>
      <td>0.075538</td>
    </tr>
    <tr>
      <th>avg_surge</th>
      <td>0.063987</td>
    </tr>
    <tr>
      <th>phone</th>
      <td>0.034142</td>
    </tr>
    <tr>
      <th>signup_date</th>
      <td>0.136856</td>
    </tr>
    <tr>
      <th>surge_pct</th>
      <td>0.075776</td>
    </tr>
    <tr>
      <th>trips_in_first_30_days</th>
      <td>0.074940</td>
    </tr>
    <tr>
      <th>luxury_car_user</th>
      <td>0.029972</td>
    </tr>
    <tr>
      <th>weekday_pct</th>
      <td>0.120915</td>
    </tr>
    <tr>
      <th>kings_landing</th>
      <td>0.055638</td>
    </tr>
    <tr>
      <th>astapor</th>
      <td>0.020714</td>
    </tr>
  </tbody>
</table>
</div>






    0.7688089670187888






    0.7641746111389864






    RandomForestClassifier(bootstrap=True, ccp_alpha=0.0, class_weight=None,
                           criterion='gini', max_depth=None, max_features='auto',
                           max_leaf_nodes=None, max_samples=None,
                           min_impurity_decrease=0.0, min_impurity_split=None,
                           min_samples_leaf=1, min_samples_split=2,
                           min_weight_fraction_leaf=0.0, n_estimators=100,
                           n_jobs=None, oob_score=True, random_state=None,
                           verbose=0, warm_start=False)




```python
#def partial_dependence(model, X, feature_index, classification=True):
#    '''
#    Parameters
#    ----------
#    model: fitted model
#        anything with .predict()
#    X: numpy array
#        data the model was trained on.
#    feature_index: int
#        feature to calculate partial dependence for
#    classification: boolean. 
#        True if the model is a classifier
#           (in which case, it must have .predict_proba()
#        False if the model is a regressor
#    Returns
#    -------
#    x_values: numpy array
#        x values to plot partial dependence over
#    pdp: numpy array
#        partial dependence values
#    example:
#    >> x, pdp = partial_dependence(model, X_train, 3, classification=False)
#    >> plt.plot(x, pdp)
#    '''
#    x_values = np.unique(X[:,feature_index])
#    pdp = np.zeros(x_values.shape)
#    for i, value in enumerate(x_values):
#        X_new = replace_column(X, feature_index, value)
#        if classification:
#            y_pred_prob = model.predict_proba(X_new)[:,1]
#            y_pred_prob = np.clip(y_pred_prob, 0.001, 0.999)
#            y_pred = np.log(y_pred_prob / (1 - y_pred_prob))
#        else:
#            y_pred = model.predict(X_new)
#        pdp[i] = y_pred.mean()
#    return (x_values, pdp)
#
#feature_indices = X_train.columns
#print(feature_indices)
#fig, axes = plt.subplots(4,3, figsize=(16,8), sharey=True)
#for ax, feat_ind in zip(axes.flatten(), feature_indices):
#    xx, pdp = partial_dependence(rf1, X_train, feat_ind)
#    ax.plot(xx, pdp)
#    ax.set_title(feature_names[feat_ind])
#plt.tight_layout()
```


```python
model = train_random_forest(X_train, y_train, X_valid, y_valid,num_trees=num)[0]
y_predict = model.predict(X_valid)
model.score(X_valid, y_valid)
```


```python
y_predict.shape
y_valid.shape
```




    (12401,)






    (12401,)




```python
num_trees = [50, 100, 250, 500, 1000]
scores=[]

for num in num_trees:
    model = train_random_forest(X_train, y_train, X_valid, y_valid,num_trees=num)[0]
    #y_predict = model.predict(X_valid)
    #y_predict.reshape(-1,1)
    #y_valid.reshape(-1,1)
    score = model.score(X_valid, y_valid)
    scores.append(score)
print(scores)
```

    [0.7681969680679497, 0.7751854639286099, 0.7769057090635415, 0.7774432856682078, 0.7764756477798086]



```python
sns.lineplot(x=num_trees, y=scores)
plt.xlabel('Number of Trees')
plt.ylabel('Mean Accuracy')
plt.title('Optimizing Number of Trees in Random Forest')
plt.tight_layout()
plt.savefig('MeanAccuracyPlot', dpi=240)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a58534290>






    Text(0.5, 0, 'Number of Trees')






    Text(0, 0.5, 'Mean Accuracy')






    Text(0.5, 1.0, 'Optimizing Number of Trees in Random Forest')




![png](output_24_4.png)


## Tune 


```python
final_rf, feature_importance, oob_score = train_random_forest(X_training, y_training, X_test, y_test, num_trees=500)
```


```python
feature_importance
oob_score
final_rf.score(X_test, y_test)
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>avg_dist</th>
      <td>0.207971</td>
    </tr>
    <tr>
      <th>avg_rating_by_driver</th>
      <td>0.108332</td>
    </tr>
    <tr>
      <th>avg_rating_of_driver</th>
      <td>0.072820</td>
    </tr>
    <tr>
      <th>avg_surge</th>
      <td>0.063629</td>
    </tr>
    <tr>
      <th>phone</th>
      <td>0.034464</td>
    </tr>
    <tr>
      <th>signup_date</th>
      <td>0.135938</td>
    </tr>
    <tr>
      <th>surge_pct</th>
      <td>0.077600</td>
    </tr>
    <tr>
      <th>trips_in_first_30_days</th>
      <td>0.072872</td>
    </tr>
    <tr>
      <th>luxury_car_user</th>
      <td>0.031577</td>
    </tr>
    <tr>
      <th>weekday_pct</th>
      <td>0.119234</td>
    </tr>
    <tr>
      <th>kings_landing</th>
      <td>0.055713</td>
    </tr>
    <tr>
      <th>astapor</th>
      <td>0.019848</td>
    </tr>
  </tbody>
</table>
</div>






    0.7736204069564282






    0.7734053705346343




```python

```


```python
ax = sns.scatterplot(data=feature_importance,legend=False)
ax.set_xticklabels(
    labels=X_valid.columns,
    rotation=90,
    horizontalalignment='right')
plt.tight_layout()
plt.savefig('FeatureImportance', dpi=240)
```




    [Text(0, 0, 'avg_dist'),
     Text(0, 0, 'avg_rating_by_driver'),
     Text(0, 0, 'avg_rating_of_driver'),
     Text(0, 0, 'avg_surge'),
     Text(0, 0, 'phone'),
     Text(0, 0, 'signup_date'),
     Text(0, 0, 'surge_pct'),
     Text(0, 0, 'trips_in_first_30_days'),
     Text(0, 0, 'luxury_car_user'),
     Text(0, 0, 'weekday_pct'),
     Text(0, 0, 'kings_landing'),
     Text(0, 0, 'astapor')]




![png](output_29_1.png)



```python
final_score = final_rf.score(X_test, y_test)
```


```python
final_score
```




    0.7734053705346343



# FINAL ACCURACY SCORE = 0.7742923957745343


```python

```
