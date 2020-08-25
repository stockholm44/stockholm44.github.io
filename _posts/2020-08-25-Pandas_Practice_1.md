
# pandas#1

- Pandas는 python 계의 엑셀! 하지만 엑셀이 더쉽긴하다 ㅋㅋ
- numpy의 ref.이므로 numpy기능을 그대로 제공.
- indexing 전처리등에 많이씀
- 필요없는데이타 날리기, 머지등을 하기 쉽다.

#### 1. Numpy, Pandas 임포트하기


```python
import pandas as pd
import numpy as np
```

#### 2. 파일로부터 DataFrame 만들기
- csv 파일은  data_url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data'
- separate는 빈공간으로 지정.('\s+') 
- Column은 없는걸로(header=None)
- df_data 변수에 할당


```python
data_url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data' #Data URL
df_data = pd.read_csv(data_url, sep='\s+', header = None) #csv 타입 데이터 로드, separate는 빈공간으로 지정하고, Column은 없음
```

#### 3. df_data의 head 보기


```python
df_data.head()
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00632</td>
      <td>18.0</td>
      <td>2.31</td>
      <td>0</td>
      <td>0.538</td>
      <td>6.575</td>
      <td>65.2</td>
      <td>4.0900</td>
      <td>1</td>
      <td>296.0</td>
      <td>15.3</td>
      <td>396.90</td>
      <td>4.98</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.02731</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>6.421</td>
      <td>78.9</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242.0</td>
      <td>17.8</td>
      <td>396.90</td>
      <td>9.14</td>
      <td>21.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.02729</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>7.185</td>
      <td>61.1</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242.0</td>
      <td>17.8</td>
      <td>392.83</td>
      <td>4.03</td>
      <td>34.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.03237</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>6.998</td>
      <td>45.8</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222.0</td>
      <td>18.7</td>
      <td>394.63</td>
      <td>2.94</td>
      <td>33.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.06905</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>7.147</td>
      <td>54.2</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222.0</td>
      <td>18.7</td>
      <td>396.90</td>
      <td>5.33</td>
      <td>36.2</td>
    </tr>
  </tbody>
</table>
</div>



- pandas는 series, datafme으로 구성.
- series는 한개 column에 해당
- series를 모은게 dataframera


## Series
Series도 index가 있긴한데 별로 신경안쓰는편.

#### 4. Series와 DataFrame을 pandas 입력없이 되게 import 하기.


```python
from pandas import Series, DataFrame
```

#### 5. 아래 리스트데이터를 시리즈로 변환. example_obj 변수에 Series로 할당
- list_data = [1,2,3,4,5]


```python
list_data = [1,2,3,4,5]
example_obj = Series(data = list_data)
example_obj
```




    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64



#### 6. 아래 list_data를 데이터로, list_name을 인덱스로 시리즈로 불러들이기
- list_data = [1,2,3,4,5]  
- list_name = list('abced')
- 변수이름은 example_obj으로 저장



```python
list_data = [1,2,3,4,5]
list_name = list('abced')
example_obj = Series(data = list_data, index=list_name)
example_obj
```




    a    1
    b    2
    c    3
    e    4
    d    5
    dtype: int64



#### 7. Dict 타입으로도 시리즈만들어보자.
- 아래 dict_data로 시리즈 만들기. 
- 데이터타입은 np.float32
- 시리즈이름은 "example_data" ※변수이름이 아님.
- 변수이름은 example_obj


```python
dict_data = {"a":1, "b":2, "c":3, "d":4, "e":5}
example_obj = Series(dict_data, dtype=np.float32, name="example_data")
example_obj
```




    a    1.0
    b    2.0
    c    3.0
    d    4.0
    e    5.0
    Name: example_data, dtype: float32



#### 8. 위에서만든 시리즈 인덱스 'a'의 값 확인.
- 시리즈에서 Data접근하기할때는 index로 접근. 
- 하지만 dataframe에서는 동일문법이 컬럼을 선택할 때 쓰기 때문에 헷갈린다. 


```python
example_obj["a"]
```




    1.0



# Dataframe
- 기본적으로 matrix를 가정. row, column으로 접근가능하나 좀 귀찮...
- numpy의 subclass라 그쪽기능 거의다 사용가능.

#### 9. DataFrame만들기
- 데이터는 raw_data로,
- raw_data = {'first_name': ['Jason', 'Molly', 'Tina', 'Jake', 'Amy'],
        'last_name': ['Miller', 'Jacobson', 'Ali', 'Milner', 'Cooze'],
        'age': [42, 52, 36, 24, 73],
        'city': ['San Francisco', 'Baltimore', 'Miami', 'Douglas', 'Boston']}

- 컬럼은 아래 컬럼으로 
- cols = ['first_name', 'last_name', 'age', 'city']



```python
raw_data = {'first_name': ['Jason', 'Molly', 'Tina', 'Jake', 'Amy'],
        'last_name': ['Miller', 'Jacobson', 'Ali', 'Milner', 'Cooze'],
        'age': [42, 52, 36, 24, 73],
        'city': ['San Francisco', 'Baltimore', 'Miami', 'Douglas', 'Boston']}
df = pd.DataFrame(raw_data, columns = ['first_name', 'last_name', 'age', 'city'])
df
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
      <th>first_name</th>
      <th>last_name</th>
      <th>age</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Miller</td>
      <td>42</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>Jacobson</td>
      <td>52</td>
      <td>Baltimore</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>Ali</td>
      <td>36</td>
      <td>Miami</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>Milner</td>
      <td>24</td>
      <td>Douglas</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>Cooze</td>
      <td>73</td>
      <td>Boston</td>
    </tr>
  </tbody>
</table>
</div>



#### 10. column 이름 바꾸기
- ["First_Name", "Family_Name", "Age", "Born"]로 컬럼이름 바꾸기


```python
df.columns = ["First_Name", "Family_Name", "Age", "Born"]
df
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
      <th>First_Name</th>
      <th>Family_Name</th>
      <th>Age</th>
      <th>Born</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Miller</td>
      <td>42</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>Jacobson</td>
      <td>52</td>
      <td>Baltimore</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>Ali</td>
      <td>36</td>
      <td>Miami</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>Milner</td>
      <td>24</td>
      <td>Douglas</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>Cooze</td>
      <td>73</td>
      <td>Boston</td>
    </tr>
  </tbody>
</table>
</div>



#### 11. raw_data의 특정 컬럼으로만 데이터 프레임만들기
- 요기부터 집중!
- 특별 column 만가져올수 있다. 이게 numpy와 다른점.
- 저위 raw_data에서 age, city 컬럼만으로 데이터프레임만들기


```python
pd.DataFrame(raw_data, columns = ['age', 'city'])
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
      <th>age</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>42</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>1</th>
      <td>52</td>
      <td>Baltimore</td>
    </tr>
    <tr>
      <th>2</th>
      <td>36</td>
      <td>Miami</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Douglas</td>
    </tr>
    <tr>
      <th>4</th>
      <td>73</td>
      <td>Boston</td>
    </tr>
  </tbody>
</table>
</div>



#### 12. 기존에 없던 새로운 column으로 만들기
- 기존에 없던 새로운 column으로 만들면 Nan으로 들어감,
- ['first_name', 'last_name', 'age', 'city', 'debt']


```python
df = DataFrame(raw_data, columns = ['first_name', 'last_name', 'age', 'city', 'debt'])
```

#### 13. 데이터프레임의 Column을 선택하여 Series로 추출가능.
- 두가지 방법으로 불러오자.first_name 컬럼만 시리즈로 가져오자
    1. 대괄호써서.
    2. 점만써서
    


```python
#1
df['first_name'] 
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-f706a29788ea> in <module>
          1 #1
    ----> 2 df['first_name']
    

    NameError: name 'df' is not defined



```python
df.first_name
```




    (0    Jason
     1    Molly
     2     Tina
     3     Jake
     4      Amy
     Name: first_name, dtype: object, 0    Jason
     1    Molly
     2     Tina
     3     Jake
     4      Amy
     Name: first_name, dtype: object)



- Dataframe의 값 접근법
    1. loc - index location -> 인덱스 이름으로 반환
    2. iloc - index position -> 인덱스 순서번호로 반환

#### 14. 시리즈 만들기
- s 변수에 시리즈 할당
- 인덱스는 [49,48,47,46,45, 1, 2, 3, 4, 5]
- 값은 np.nan으로 채움.


```python
s = pd.Series(np.nan, index=[49,48,47,46,45, 1, 2, 3, 4, 5])
s
```




    49   NaN
    48   NaN
    47   NaN
    46   NaN
    45   NaN
    1    NaN
    2    NaN
    3    NaN
    4    NaN
    5    NaN
    dtype: float64



#### 15. 14번의 시리즈에서 3번째 위치 전까지를 뽑기
- index 3번째 위치까지를 시리즈로 뽑기


```python
s.iloc[:3] 
```




    49   NaN
    48   NaN
    47   NaN
    dtype: float64



#### 16. 인덱스가 3인놈 까지를 뽑기
- index가 3인 위치까지의 인덱스 값들을 시리즈로 뽑기(인덱스 순서가 3이 아님)


```python
s.loc[:3]
```




    49   NaN
    48   NaN
    47   NaN
    46   NaN
    45   NaN
    1    NaN
    2    NaN
    3    NaN
    dtype: float64



- Column 에 새로운 데이터 할당 -> 이것 굉장히 많이씀.
- 있는 data를 갖고 새로운 feature를 만들때 많이 사용함.

#### 17. 데이터프레임만들기
- 데이터프레임 이름은 df
- 데이터는 raw_data
- 컬럼은  ['first_name', 'last_name', 'age', 'city', 'debt']


```python
df = DataFrame(raw_data, columns = ['first_name', 'last_name', 'age', 'city', 'debt'])
```

#### 18. 새 Column 에 새로운 데이터 할당 
- df의 debt컬럼을 age가 40 초과면 True, 아니면 False로 값 넣기
- 새컬럼 만들때도 df.xx 혹은 df['xx']의 두가지 방법이 있다. 
- .으로 만들시에는 ''가 필요없고  []로 만들때는 ''가 필요하다.


```python
df.debt = df.age>40
df
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
      <th>first_name</th>
      <th>last_name</th>
      <th>age</th>
      <th>city</th>
      <th>debt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Miller</td>
      <td>42</td>
      <td>San Francisco</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>Jacobson</td>
      <td>52</td>
      <td>Baltimore</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>Ali</td>
      <td>36</td>
      <td>Miami</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>Milner</td>
      <td>24</td>
      <td>Douglas</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>Cooze</td>
      <td>73</td>
      <td>Boston</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



#### 19. df 행렬 변환



```python
df.T
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>first_name</th>
      <td>Jason</td>
      <td>Molly</td>
      <td>Tina</td>
      <td>Jake</td>
      <td>Amy</td>
    </tr>
    <tr>
      <th>last_name</th>
      <td>Miller</td>
      <td>Jacobson</td>
      <td>Ali</td>
      <td>Milner</td>
      <td>Cooze</td>
    </tr>
    <tr>
      <th>age</th>
      <td>42</td>
      <td>52</td>
      <td>36</td>
      <td>24</td>
      <td>73</td>
    </tr>
    <tr>
      <th>city</th>
      <td>San Francisco</td>
      <td>Baltimore</td>
      <td>Miami</td>
      <td>Douglas</td>
      <td>Boston</td>
    </tr>
    <tr>
      <th>debt</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



#### 20. df의 전체값들을 array로 뽑기
- 행단위로 묶이다 보니 dtype은 당연히 object로 뽑힘.
- 전체 타입이 일정하면 그 일정한 타입으로 뽑힘.


```python
df.values
```




    array([['Jason', 'Miller', 42, 'San Francisco', True],
           ['Molly', 'Jacobson', 52, 'Baltimore', True],
           ['Tina', 'Ali', 36, 'Miami', False],
           ['Jake', 'Milner', 24, 'Douglas', False],
           ['Amy', 'Cooze', 73, 'Boston', True]], dtype=object)



#### 21. df를 csv 형태데이터로 변환
- 나중에 csv로 저장하려고 하면 ()안에 파일이름을 넣어주면됨.


```python
df.to_csv()
```




    ',first_name,last_name,age,city,debt\n0,Jason,Miller,42,San Francisco,True\n1,Molly,Jacobson,52,Baltimore,True\n2,Tina,Ali,36,Miami,False\n3,Jake,Milner,24,Douglas,False\n4,Amy,Cooze,73,Boston,True\n'



#### 22. df의 column 삭제


```python
del df["debt"]
```

#  Selection & Drop
- numpy떄의 indexing과 같은 기능.


#### 23. excel 파일을 데이터프레임으로 불러오기
- 변수이름 df
- rawdata는 C:/djangocym/study_2018/lab_bla/data/excel-comp-data.xlsx


```python
df = pd.read_excel("C:/djangocym/study_2018/lab_bla/data/excel-comp-data.xlsx")
df.head()
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
      <th>account</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>211829</td>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>New Jaycob</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>320563</td>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
      <td>Port Khadijah</td>
      <td>NorthCarolina</td>
      <td>38365</td>
      <td>95000</td>
      <td>45000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>648336</td>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>New Lilianland</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>109996</td>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
      <td>Hyattburgh</td>
      <td>Maine</td>
      <td>46021</td>
      <td>45000</td>
      <td>120000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>121213</td>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>Shanahanchester</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
  </tbody>
</table>
</div>



#### 24. 지정 column의 값들 보기
- df에서 account 컬럼의 첫 3개줄만 불러오기


```python
df["account"].head(3)
```




    0    211829
    1    320563
    2    648336
    Name: account, dtype: int64



#### 25. 지정 columns(복수)의 값들 보기
- account, street, state의 첫 3개 값들 가져오기


```python
df[["account", "street", "state"]].head(3)
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
      <th>account</th>
      <th>street</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>211829</td>
      <td>34456 Sean Highway</td>
      <td>Texas</td>
    </tr>
    <tr>
      <th>1</th>
      <td>320563</td>
      <td>1311 Alvis Tunnel</td>
      <td>NorthCarolina</td>
    </tr>
    <tr>
      <th>2</th>
      <td>648336</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>Iowa</td>
    </tr>
  </tbody>
</table>
</div>



#### Selection with index number
- 대괄호안에 원래 str을 넣으면 column을 가져오는데 숫자를 넣으면 row로 가져옴.
- 좀 일관성이 없다. 
- 그래서 되도록 대괄호는 column 위주로만 하기

#### 26. df의 3행만 불러오기(대괄호로일단 해보자.)


```python
df[:3] 
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
      <th>account</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>211829</td>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>New Jaycob</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>320563</td>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
      <td>Port Khadijah</td>
      <td>NorthCarolina</td>
      <td>38365</td>
      <td>95000</td>
      <td>45000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>648336</td>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>New Lilianland</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
  </tbody>
</table>
</div>



#### 27. df의 account컬럼의 3줄값만 가져오기


```python
df["account"][:3]
```




    0    211829
    1    320563
    2    648336
    Name: account, dtype: int64



#### series selection - 웃기다면 웃기고 재미있다면 재밌는 기능
- index값을 넣으면 index값들의 data를 가져옴.

#### 28. 변수 account_series에 df의 account 컬럼의 시리즈를 할당.


```python
account_series = df["account"]
```

#### 29. account_series의 3행까지 가져오기


```python
account_series[:3]
```




    0    211829
    1    320563
    2    648336
    Name: account, dtype: int64



#### 30. account_series의 1, 5, 2행가져오기
- 여러 index 사용시에는 []안에 반복형 변수로 넣어야함.(주로 리스트로함.) 
- 즉 [[x, y, xz]] 같이ㅋ


```python
account_series[[1,5,2]] 
```




    1    320563
    5    132971
    2    648336
    Name: account, dtype: int64



#### Boolean index
- 많이 쓰는 기능
- 일정 조건에 맞으면 True, 아니면 False를 반환
- 간단한 문법으로 확인이 가능하여 좀 쓰는듯함. 

#### 31. 위의 account_series에서 250,000 이하만 가져오기


```python
account_series[account_series<250000]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-3-90ba745ed8b6> in <module>
    ----> 1 account_series[account_series<250000]
    

    NameError: name 'account_series' is not defined


#### index 변경
- 인덱스를 그냥 숫자가 아닌 다른 예를들면 주민번호, 학번으로 변경가능

#### 32. df의 account컬럼을 인덱스로 만들기.
- account컬럼을 인덱스로 만들기.
- 컬럼에 남아있는 account 컬럼은 지워줘라.


```python
df.index = df["account"]
del df['account']
df.head()
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
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
    <tr>
      <th>account</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>211829</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>New Jaycob</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>320563</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
      <td>Port Khadijah</td>
      <td>NorthCarolina</td>
      <td>38365</td>
      <td>95000</td>
      <td>45000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>648336</th>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>New Lilianland</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>109996</th>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
      <td>Hyattburgh</td>
      <td>Maine</td>
      <td>46021</td>
      <td>45000</td>
      <td>120000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>121213</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>Shanahanchester</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
  </tbody>
</table>
</div>



#### Basic, loc, iloc Selection
- 각각의 장단이 있다. 
- []를 이용한 Basic한 방법은 컬럼은 컬럼명, index는 숫자로 가능하지만 헷갈리는 문법
- loc, iloc은 확실히 이름 only 혹은 순서 only로 명확하게 지정이 가능하나 둘을 섞어서는 힘듬,.

#### 33. df의 name, street 컬럼의 첫 2개행 가져오기


```python
df[["name","street"]][:2]
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
      <th>name</th>
      <th>street</th>
    </tr>
    <tr>
      <th>account</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>211829</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
    </tr>
    <tr>
      <th>320563</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
    </tr>
  </tbody>
</table>
</div>



#### 34. loc을 통해서 가져오기
- index 211829,320563, column은 name, street


```python
df.loc[[211829,320563],["name","street"]]
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
      <th>name</th>
      <th>street</th>
    </tr>
    <tr>
      <th>account</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>211829</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
    </tr>
    <tr>
      <th>320563</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
    </tr>
  </tbody>
</table>
</div>



#### 35. iloc을 통해서 가져오기
- name, street 컬럼의 10개열가져오기


```python
df[["name", "street"]].iloc[:10]
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
      <th>name</th>
      <th>street</th>
    </tr>
    <tr>
      <th>account</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>211829</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
    </tr>
    <tr>
      <th>320563</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
    </tr>
    <tr>
      <th>648336</th>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
    </tr>
    <tr>
      <th>109996</th>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
    </tr>
    <tr>
      <th>121213</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
    </tr>
    <tr>
      <th>132971</th>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
    </tr>
    <tr>
      <th>145068</th>
      <td>Casper LLC</td>
      <td>340 Consuela Bridge Apt. 400</td>
    </tr>
    <tr>
      <th>205217</th>
      <td>Kovacek-Johnston</td>
      <td>91971 Cronin Vista Suite 601</td>
    </tr>
    <tr>
      <th>209744</th>
      <td>Champlin-Morar</td>
      <td>26739 Grant Lock</td>
    </tr>
    <tr>
      <th>212303</th>
      <td>Gerhold-Maggio</td>
      <td>366 Maggio Grove Apt. 998</td>
    </tr>
  </tbody>
</table>
</div>



#### 36. index 변경 
- df의 인덱스를 0~15로 변경(range로 할당)
- 머지가 없을경우에는 제일편함.(?)


```python
df.index=list(range(0,15))
df.head()
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
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>New Jaycob</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
      <td>Port Khadijah</td>
      <td>NorthCarolina</td>
      <td>38365</td>
      <td>95000</td>
      <td>45000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>New Lilianland</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
      <td>Hyattburgh</td>
      <td>Maine</td>
      <td>46021</td>
      <td>45000</td>
      <td>120000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>Shanahanchester</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
  </tbody>
</table>
</div>



#### data drop
- column단위면 del인데 row단위면 drop과 row Num적어줌.
- drop의 parameter에 축설정이 있다. axis=0(행단위), axis=1(컬럼단위)
- axis의 디폴트가 0이므로 행지울때는 행만 넣어도 되나 컬럼단위를 지울때는 axis=1 꼭 넣어야함..
- drop함수는 변수자체를 변형하지 않기 때문에 변수자체를 변경할때는 아래 2가지로 함.
    - parameter에 inplace=True 추가 
    - df=df.drop(xx)와 같이 변수 재할당.

#### 37. df의 index 값이 1인 행 없에기


```python
df.drop(1) # index 1 row 없에기
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
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>New Jaycob</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>New Lilianland</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
      <td>Hyattburgh</td>
      <td>Maine</td>
      <td>46021</td>
      <td>45000</td>
      <td>120000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>Shanahanchester</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
      <td>Jeremieburgh</td>
      <td>Arkansas</td>
      <td>62785</td>
      <td>150000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Casper LLC</td>
      <td>340 Consuela Bridge Apt. 400</td>
      <td>Lake Gabriellaton</td>
      <td>Mississipi</td>
      <td>18008</td>
      <td>62000</td>
      <td>120000</td>
      <td>70000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Kovacek-Johnston</td>
      <td>91971 Cronin Vista Suite 601</td>
      <td>Deronville</td>
      <td>RhodeIsland</td>
      <td>53461</td>
      <td>145000</td>
      <td>95000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Champlin-Morar</td>
      <td>26739 Grant Lock</td>
      <td>Lake Juliannton</td>
      <td>Pennsylvania</td>
      <td>64415</td>
      <td>70000</td>
      <td>95000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Gerhold-Maggio</td>
      <td>366 Maggio Grove Apt. 998</td>
      <td>North Ras</td>
      <td>Idaho</td>
      <td>46308</td>
      <td>70000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Goodwin, Homenick and Jerde</td>
      <td>649 Cierra Forks Apt. 078</td>
      <td>Rosaberg</td>
      <td>Tenessee</td>
      <td>47743</td>
      <td>45000</td>
      <td>120000</td>
      <td>55000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Hahn-Moore</td>
      <td>18115 Olivine Throughway</td>
      <td>Norbertomouth</td>
      <td>NorthDakota</td>
      <td>31415</td>
      <td>150000</td>
      <td>10000</td>
      <td>162000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Frami, Anderson and Donnelly</td>
      <td>182 Bertie Road</td>
      <td>East Davian</td>
      <td>Iowa</td>
      <td>72686</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Walsh-Haley</td>
      <td>2624 Beatty Parkways</td>
      <td>Goodwinmouth</td>
      <td>RhodeIsland</td>
      <td>31919</td>
      <td>55000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>McDermott PLC</td>
      <td>8917 Bergstrom Meadow</td>
      <td>Kathryneborough</td>
      <td>Delaware</td>
      <td>27933</td>
      <td>150000</td>
      <td>120000</td>
      <td>70000</td>
    </tr>
  </tbody>
</table>
</div>



#### 38. df의 0, 1, 2, 3 행 없에기
- 여러개도 drop 가능
- 단 반복형변수(iterable variable)로 넣어줘야함. (예를들면 리스트)


```python
df.drop([0,1, 2,3])
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
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>Shanahanchester</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
      <td>Jeremieburgh</td>
      <td>Arkansas</td>
      <td>62785</td>
      <td>150000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Casper LLC</td>
      <td>340 Consuela Bridge Apt. 400</td>
      <td>Lake Gabriellaton</td>
      <td>Mississipi</td>
      <td>18008</td>
      <td>62000</td>
      <td>120000</td>
      <td>70000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Kovacek-Johnston</td>
      <td>91971 Cronin Vista Suite 601</td>
      <td>Deronville</td>
      <td>RhodeIsland</td>
      <td>53461</td>
      <td>145000</td>
      <td>95000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Champlin-Morar</td>
      <td>26739 Grant Lock</td>
      <td>Lake Juliannton</td>
      <td>Pennsylvania</td>
      <td>64415</td>
      <td>70000</td>
      <td>95000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Gerhold-Maggio</td>
      <td>366 Maggio Grove Apt. 998</td>
      <td>North Ras</td>
      <td>Idaho</td>
      <td>46308</td>
      <td>70000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Goodwin, Homenick and Jerde</td>
      <td>649 Cierra Forks Apt. 078</td>
      <td>Rosaberg</td>
      <td>Tenessee</td>
      <td>47743</td>
      <td>45000</td>
      <td>120000</td>
      <td>55000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Hahn-Moore</td>
      <td>18115 Olivine Throughway</td>
      <td>Norbertomouth</td>
      <td>NorthDakota</td>
      <td>31415</td>
      <td>150000</td>
      <td>10000</td>
      <td>162000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Frami, Anderson and Donnelly</td>
      <td>182 Bertie Road</td>
      <td>East Davian</td>
      <td>Iowa</td>
      <td>72686</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Walsh-Haley</td>
      <td>2624 Beatty Parkways</td>
      <td>Goodwinmouth</td>
      <td>RhodeIsland</td>
      <td>31919</td>
      <td>55000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>McDermott PLC</td>
      <td>8917 Bergstrom Meadow</td>
      <td>Kathryneborough</td>
      <td>Delaware</td>
      <td>27933</td>
      <td>150000</td>
      <td>120000</td>
      <td>70000</td>
    </tr>
  </tbody>
</table>
</div>



- 결측치가 많거나 할때 사용. drop 자체를 사용할일이 없을수 있다.
- 흠.. 아니다 drop은 마니쓴다

#### axis 축을 기준으로 drop
- drop이용하여 city column 없에기(axis=1)사용.
- 하지만 보통은 del df[col]을 더 많이 쓰는듯. 
- 하지만 나는 drop을 문법의 일관성을 위해 Drop을 더 마니씀.

#### 39. city column을 drop으로 없에기


```python
df.drop("city",axis=1).head() # 축을기준으로 없에라.
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
      <th>name</th>
      <th>street</th>
      <th>state</th>
      <th>postal-code</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kerluke, Koepp and Hilpert</td>
      <td>34456 Sean Highway</td>
      <td>Texas</td>
      <td>28752</td>
      <td>10000</td>
      <td>62000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Walter-Trantow</td>
      <td>1311 Alvis Tunnel</td>
      <td>NorthCarolina</td>
      <td>38365</td>
      <td>95000</td>
      <td>45000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bashirian, Kunde and Price</td>
      <td>62184 Schamberger Underpass Apt. 231</td>
      <td>Iowa</td>
      <td>76517</td>
      <td>91000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D'Amore, Gleichner and Bode</td>
      <td>155 Fadel Crescent Apt. 144</td>
      <td>Maine</td>
      <td>46021</td>
      <td>45000</td>
      <td>120000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bauch-Goldner</td>
      <td>7274 Marissa Common</td>
      <td>California</td>
      <td>49681</td>
      <td>162000</td>
      <td>120000</td>
      <td>35000</td>
    </tr>
  </tbody>
</table>
</div>



- 재밌는건..보여주는것만 없어지는거지 원래 df를 열어보면 그대로 있당.
- 왜냐면 pandas에서는 데이터 핸들링할때 원본데이터를 쉽게 삭제하지 않음.
- 원본데이터를 바꾸려면 inplace=True를 넣어야힘. False로 하면 해당 df를 copy한버전에서 삭제해서 임시로 보여주는거.

# Dataframe Operations

#### Series Operation
- index를 기준으로 연산수행
- 겹치는 index가 없을 경우 Nan값으로 변환
- numpy의 broadcasting 과는 좀 다름.
- index의 이름이 같은것끼리 더해줌.아래의 e의경우 2개인데 각각에 동일 e를 더해줌

#### 40. s1, s2에 시리즈 각각 할당 후 더하기.
- s1은 1~5까지 값, 인덱스는 a,b,c,d,e
- s2는 5~10까지 값, 인덱스는 b,c,e,d,e,f로
- s1과 s2 더하기 두가지방법.( 1) add함수, 2) 그냥 +)


```python
s1 = Series(range(1,6), index=list("abcde"))
s1
s2=Series(range(5,11), index=list("bcedef"))
s1.add(s2)
s1+s2
```




    a     NaN
    b     7.0
    c     9.0
    d    12.0
    e    12.0
    e    14.0
    f     NaN
    dtype: float64



#### Dataframe operation
- df는 column과 index를 모두 고려
- add operation을 쓰면 Nan값 0으로 변환
- operation type -> add, sub, div, mul

#### 41. 데이터프레임 df1, df2에 할당하고 그 둘 더하기.
- df1은 np.arange로 0~8까지 하고 3X3으로 변환한 값을 dataframe으로, 컬럼은 a,b,c
- df2은 np.arange로 0~15까지 하고 4X4으로 변환한 값을 dataframe으로, 컬럼은 a,b,c,d
- df1과 df2 두개 더하기 2가지방법. 
    1. 걍 +로 
    2. add 함수로, 단 쉐입이 다르므로 빈칸과 더할때는 0을 더하는 옵션인 fill_value 파라미터 0으로 하자.


```python
df1=DataFrame(np.arange(9).reshape(3,3),columns=list("abc"))
df1
df2=DataFrame(np.arange(16).reshape(4,4),columns=list("abcd"))
df2
```


```python
#1
df1+df2
```


```python
#2
df1.add(df2,fill_value=0)
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.0</td>
      <td>16.0</td>
      <td>18.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12.0</td>
      <td>13.0</td>
      <td>14.0</td>
      <td>15.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 42. Series + Dataframe(Broadcasting)
- 판다스 datae들의 연산은 Broadcasting의 개념이 들어감.
    - 행, 열단위로 계산이 되는건데 정확한 개념은 강의 참고.
- df에 데이터프레임 할당. np.arange로 0~15를 4X4로. 컬럼은 abcd를 각 4개로 할당.
- s에 시리즈 할당. np.arange로 10~13, 컬럼 abcd를 각 4개로
- df와 s (Column 기준)
    1. +로
    2. add함수로, axis= 뭐로할까!?


```python
df = DataFrame(np.arange(16).reshape(4,4),columns=list('abcd'))
df
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
s = Series(np.arange(10,14),index=list('abcd'))
s
```




    a    10
    b    11
    c    12
    d    13
    dtype: int32




```python
df+s # Column을 기준으로 broadcasting이 일어남.
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>12</td>
      <td>14</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14</td>
      <td>16</td>
      <td>18</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18</td>
      <td>20</td>
      <td>22</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22</td>
      <td>24</td>
      <td>26</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.add(s, axis=1) # 축을 지정해주면 그거 기준으로 broadcasting일어남.
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>12</td>
      <td>14</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14</td>
      <td>16</td>
      <td>18</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18</td>
      <td>20</td>
      <td>22</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22</td>
      <td>24</td>
      <td>26</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>



# Lambda, map, apply 
-  요기가 좀 재밌고 실용적!!!
- 굉장히 편하게 pandas에서 적용가능


#### 43. lambda로 series에 함수적용
- s1에 0~10 시리즈로 할당
- s1의 모든값에 제곱하기


```python
s1 = Series(np.arange(10))
s1.map(lambda x: x**2).head(5)
```




    0     0
    1     1
    2     4
    3     9
    4    16
    dtype: int64



#### 44. 값 대체에 map 사용.
- 아래 딕셔너리 z를 s1에 적용해서 변경
- 값들 대체할때 꽤쉽게 가능.
- z = {1: 'A', 2: 'B', 3: 'C'}


```python
z = {1: 'A', 2: 'B', 3: 'C'}
s1.map(z).head(5)
```




    0    NaN
    1      A
    2      B
    3      C
    4    NaN
    dtype: object



#### 45. 시리즈에다가 시리즈를 매핑하여 변경
- s1에 0~9 시리즈로 할당
- s2는 10~19 시리즈로 할당
- s1에 s2를 맵핑하여 값 대체



```python
s1 = Series(np.arange(10))
s1
```




    0    0
    1    1
    2    2
    3    3
    4    4
    5    5
    6    6
    7    7
    8    8
    9    9
    dtype: int32




```python
s2=Series(np.arange(10,20))
s2
```




    0    10
    1    11
    2    12
    3    13
    4    14
    5    15
    6    16
    7    17
    8    18
    9    19
    dtype: int32




```python
s1.map(s2) 
```




    0    10
    1    11
    2    12
    3    13
    4    14
    5    15
    6    16
    7    17
    8    18
    9    19
    dtype: int32



- 요렇게 시리즈끼리 맵핑가능

#### 아래와 같이 Wage파일을 읽고 sex의 male에 0, female에 1로 맵핑하라(두가지 방법)

#### 46. 변수 df에 아래 wage 파일을 불러들여라.
- C:/djangocym/study_2018/lab_bla/data/wages.csv
- 다른 parameter 없음
- 'sex' 컬럼의 unique() 확인해라


```python
# 아래예제와 같이 sex에 따라서 one-hot 매길수 있다. dict타입으로 mapping
df = pd.read_csv("C:/djangocym/study_2018/lab_bla/data/wages.csv")
df.head()
df.sex.unique()
```




    array(['male', 'female'], dtype=object)



#### 47. 위의 df의 'sex'컬럼의 값을 숫자로 맵핑해라
- sex_code 컬럼에 male은 0, female은 1로 값 매핑.
- 두가지 방법으로 하라.
    - map으로 mail:0, femail:1 dict를 매핑
    - replace로 mail:0, femail:1 dict를 매핑


```python
#1
df["sex_code"] =  df.sex.map({"male":0, "female":1}) # 제일많이쓰는 테크닉. 데이터 컨버젼. 아래와 같이 replace도가능
df.head(5)
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
      <th>earn</th>
      <th>height</th>
      <th>sex</th>
      <th>race</th>
      <th>ed</th>
      <th>age</th>
      <th>sex_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>79571.299011</td>
      <td>73.89</td>
      <td>male</td>
      <td>white</td>
      <td>16</td>
      <td>49</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>96396.988643</td>
      <td>66.23</td>
      <td>female</td>
      <td>white</td>
      <td>16</td>
      <td>62</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48710.666947</td>
      <td>63.77</td>
      <td>female</td>
      <td>white</td>
      <td>16</td>
      <td>33</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>80478.096153</td>
      <td>63.22</td>
      <td>female</td>
      <td>other</td>
      <td>16</td>
      <td>95</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82089.345498</td>
      <td>63.08</td>
      <td>female</td>
      <td>white</td>
      <td>17</td>
      <td>43</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#2
df.sex_code = df.sex.replace({"male":0, "female":1})
df.head()
# -> inplace=True쓰고 sex_code지우면 완전히 대체도 가능. 예제로 쓰장.!! del index["sex_code"]
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
      <th>earn</th>
      <th>height</th>
      <th>sex</th>
      <th>race</th>
      <th>ed</th>
      <th>age</th>
      <th>sex_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>79571.299011</td>
      <td>73.89</td>
      <td>male</td>
      <td>white</td>
      <td>16</td>
      <td>49</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>96396.988643</td>
      <td>66.23</td>
      <td>female</td>
      <td>white</td>
      <td>16</td>
      <td>62</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48710.666947</td>
      <td>63.77</td>
      <td>female</td>
      <td>white</td>
      <td>16</td>
      <td>33</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>80478.096153</td>
      <td>63.22</td>
      <td>female</td>
      <td>other</td>
      <td>16</td>
      <td>95</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82089.345498</td>
      <td>63.08</td>
      <td>female</td>
      <td>white</td>
      <td>17</td>
      <td>43</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# Apply for DataFrame

- map과 달리 series전체 column에 해당함수를 적용
- 입력값이 series데이터로 입력받아 handling 가능.
- 연산할때 보통 쓰는듯.
- 컬럼의 통계치 사용시 많이씀.
- 재밌는거 좀더 할 수 있긴함. ㅋ

#### 48. 위의 df에서 earn, height, age 컬럼만 df_info라는 dataframe만들자.


```python
df_info = df[["earn", "height","age"]]
df_info.head()
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
      <th>earn</th>
      <th>height</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>79571.299011</td>
      <td>73.89</td>
      <td>49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>96396.988643</td>
      <td>66.23</td>
      <td>62</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48710.666947</td>
      <td>63.77</td>
      <td>33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>80478.096153</td>
      <td>63.22</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82089.345498</td>
      <td>63.08</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>



#### 49. 최대값과 최소값의 차
- 람다로 민맥스 차이함수 만들고 이를 apply로 적용


```python
f = lambda x : x.max() - x.min()
df_info.apply(f)
```




    earn      318047.708444
    height        19.870000
    age           73.000000
    dtype: float64



#### 50. sum 함수적용
- sum 함수를 apply로 적용.
- df자체 내장 sum함수사용.


```python
#1
df_info.apply(sum)
```




    earn      4.474344e+07
    height    9.183125e+04
    age       6.250800e+04
    dtype: float64




```python
#2
df_info.sum()
```




    earn      4.474344e+07
    height    9.183125e+04
    age       6.250800e+04
    dtype: float64



#### 51. f라는 함수를 만들고 df_info에 apply해보자.
- min, max, mean 값을 반환하는 f함수만들고 이를 apply하자.
- 이렇게 함수로 지정해서 Series를 반환하게 할 수 있도있게 잼나게 사용가능.



```python
def f(x):
    return Series([x.min(), x.max(), x.mean()],
                    index=["min", "max", "mean"])
df_info.apply(f)
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
      <th>earn</th>
      <th>height</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>min</th>
      <td>-98.580489</td>
      <td>57.34000</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>317949.127955</td>
      <td>77.21000</td>
      <td>95.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>32446.292622</td>
      <td>66.59264</td>
      <td>45.328499</td>
    </tr>
  </tbody>
</table>
</div>



- Applymap for dataframe -> series단위가 아닌 element 단위함수를 적용함.
- series단위에 apply를 적용시킬때와 같은효과
- apply는 통계데이터를 뽑을때, applymap은 전체 데이터를 바꿀 유용하다는 특징 기억.

#### 52. df의 요약정보를 보자.(describe)
 - built-in func
 - Numeric type 데이터의 요약정보를 보여줌.


```python
df.describe()
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
      <th>earn</th>
      <th>height</th>
      <th>ed</th>
      <th>age</th>
      <th>sex_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1379.000000</td>
      <td>1379.000000</td>
      <td>1379.000000</td>
      <td>1379.000000</td>
      <td>1379.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>32446.292622</td>
      <td>66.592640</td>
      <td>13.354605</td>
      <td>45.328499</td>
      <td>0.622915</td>
    </tr>
    <tr>
      <th>std</th>
      <td>31257.070006</td>
      <td>3.818108</td>
      <td>2.438741</td>
      <td>15.789715</td>
      <td>0.484832</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-98.580489</td>
      <td>57.340000</td>
      <td>3.000000</td>
      <td>22.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>10538.790721</td>
      <td>63.720000</td>
      <td>12.000000</td>
      <td>33.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>26877.870178</td>
      <td>66.050000</td>
      <td>13.000000</td>
      <td>42.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>44506.215336</td>
      <td>69.315000</td>
      <td>15.000000</td>
      <td>55.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>317949.127955</td>
      <td>77.210000</td>
      <td>18.000000</td>
      <td>95.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



#### unique
- series data의 유일한 값을 list를 반환.
- 카테고리형데이터가 몇개인지 모를때 같은경우
- (성별말고 단과대학같은 많은애들.
- 이놈들을 enumerate해서 dict로 하면 각카테고리별 딕트만들수있다.
- 이걸 map혹은 replace로 숫자로 치환가능)

#### 53. df의 race에 대한 unique 값을 확인하라


```python
df.race.unique() # 유일한 인종의 값 List
```




    array(['white', 'other', 'hispanic', 'black'], dtype=object)



#### 54. 위 인종의 값들을 dict로 대입하여 array로 만들어라
- 1) enumerate이용
- 2) 그냥 dict 적용


```python
#1
np.array(dict(enumerate(df["race"].unique()))) # dict type으로 index
```




    array({0: 'white', 1: 'other', 2: 'hispanic', 3: 'black'}, dtype=object)




```python
#2
np.array({0:'white', 1:'other', 2:'hispanic', 3:'black'}, dtype=object)
```




    array({0: 'white', 1: 'other', 2: 'hispanic', 3: 'black'}, dtype=object)



#### 위의 #1 방식(enumerate)의 array dict에서 value와 key 표시하자.


```python
value=list(map(int, np.array(list(enumerate(df["race"].unique())))[:, 0].tolist()))

key = np.array(list(enumerate(df["race"].unique())), dtype=str)[:,1].tolist()
value, key
# -> label index값과 label 값 각각추출
 # -> 위와 같이 여러 방법이 있당.
```




    ([0, 1, 2, 3], ['white', 'other', 'hispanic', 'black'])


