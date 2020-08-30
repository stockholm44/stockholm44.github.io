
# 파일경로 패키지 경로 관련 노트북 정리

### 파일경로 관련 궁금한 것
1. 파일로드할때의 종류.
    1. 절대경로
    2. 상대경로.
2. 왜 파이썬에는 windows 경로 문자인 \ 가 인식이 안되는가?


# 1. 파일로드 할때의 종류
   ## A. 절대경로
- 그냥 절대경로로 읽으니 에러가 뜸.
    - OSError: Initializing from file failed
    - stackoverflow에 보니 permission이 안된다고 함.
- 해결법은 아래와 같이 engine='python'을 파라미터로 넘겨주니 됨.ㅋ
- 참고 사이트 https://programmersought.com/article/91811966388/


```python
import pandas as pd

file = 'C:/study_2018/python_study_2018/200830_파일경로 및 패키지 경로/b/b-2/input/train.csv'
df = pd.read_csv(file, sep=',', engine='python')
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



## B. 상대경로
- 일반적으로는 상대경로로 파일의 위치를 지정한다.
    - 캐글이나 쥬피터 노트북때도 상대경로로 한다.
- 단 기준위치가 명확해야 한다.
    - 기준위치를 알기 위해서는 os 라이브러리를 활용한다.
- 쥬피터 노트북을 사용할때는 일반적으로 작업폴더가 상대경로의 기준인데 즉 노트북파일의 위치가 기준이다. 

- 현재 파일의 경로 확인
    - os.getcwd() 활용


```python
import os
print(os.getcwd())
```

    C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2
    

### 여러 폴더에 있는 파일의 상대경로
- 현재 편집중인 노트북은 위와 같이 b-2 폴더에 존재
- train.csv를 아래의 총 5군데에 배치했다. 
    1. 'b-2' 
    2. 'c-1'
    3. 'b'
    4. 'a'
    5. 'a-1' 
- "현재 파일의 경로 = 작업디렉토리" 인 상황에서 각각의 train.csv 파일을 어떻게 읽는지 해보자.
    - train.csv는 각폴더이름을 뒤에 붙인 파일이름으로 수정했다. 
    - 잘열리는지 확인하자.
- 각 파일의 위치를 file에 저장하고 os.path.abspath() 함수로 절대위치를 확인하여 잘가져왔나 확인하자.



200830_파일경로 및 패키지 경로/
- ├── a/
- │   ├── a-1/
- │   │   └── train_a-1.csv
- │   ├── a-2/
- │   └── train_a.csv
- └── b/
-     ├── b-1/
-     │   └── train_b-1.csv
-     ├── b-2/
-     │   ├── .ipynb_checkpoints/
-     │   │   └── 200830_파일경로 및 패키지 경로-checkpoint.ipynb
-     │   ├── 200830.ipynb
-     │   ├── 200830_파일경로 및 패키지 경로.ipynb
-     │   ├── 2020-08-30-파이썬 파일경로관련.md.md
-     │   ├── c-1/
-     │   │   └── train_c-1.csv
-     │   ├── c-2/
-     │   ├── folder_tree.jpg
-     │   ├── image/
-     │   │   └── folder_tree.jpg
-     │   ├── input/
-     │   │   ├── test.csv
-     │   │   └── train.csv
-     │   └── train_b-2.csv
-     └── train_b.csv



#### 1. b-2 폴더
- 현재 폴더의 파일을 가져오는 것은 제일 쉽다. 
- 그냥 파일이름만 넘기면 된다.


```python
# b-2폴더(현재 작업폴더)의 파일 불러오기
file = 'train_b-2.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

    C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2\train_b-2.csv
    




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



#### 2. c-1 폴더
- 현재 폴더의 하위 폴더 부터 살짝헷갈린다. 
- 그냥 '/c-1/train_c-1.csv'로 하면 파일이 없다고 한다. 
- 현재 폴더를 뜻하는 점한개를 붙힌 후 './c-1/train_c-1.csv'와 같이 경로를 지정해줘야한다.


```python
# c-1폴더(하위 폴더)의 파일 불러오기
file = './c-1/train_c-1.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2\c-1\train_c-1.csv

<br />




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



#### 3. b 폴더
- 이제 조금씩 헷갈린다.
- 현재폴더가 점 한개. 그럼 상위는 점 두개다.
- 마치 90년대 자주 사용한 MS-DOS 명령어에서 cd.은 현재폴더, cd..은 상위폴더로 갔던 그 시대의 느낌을 살려보자.


```python
# b폴더(상위폴더)의 파일 불러오기
file = '../train_b.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

    C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\train_b.csv
    




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



#### 4. a 폴더
- 설명하기도 어려운 경로다. 
- b-2의 아빠는 b, 할아버지폴더는 '200830_파일경로 및 패키지 경로'인데. 그 자식중 하나인 a폴더의 파일을 불러온다.
- 즉 삼촌 폴더다.
- 그냥 점을 늘리는 것으로 실수할 수 있다.(나도 실수했다.)
- '.../a/train.csv'는 틀리다. '...'(점 3개)이란 문법은 없다. 아까 MS-DOS 시절을 생각해보자고 했다.
- '..'이 상위폴더면 2단계상위는?? '../../'이다.
- 이렇게 헷갈리게 폴더구조를 만들지 말자. 하위에 넣으면 간단하다. 이것은 그냥 이런경우도 있을수 있으므로 참고만 하자.


```python
# a폴더(상위*2의 하위폴더)의 파일 불러오기
file = '../../a/train_a.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

    C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\a\train_a.csv
    




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



#### 5. a-1 폴더
- 4번 a 폴더가 난관이었고 그 하위인 a-1은 오히려 간단하다.


```python
# a-1폴더(상위*2의 하위*2 폴더)의 파일 불러오기
file = '../../a/a-1/train_a-1.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

    C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\a\a-1\train_a-1.csv
    




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



#### ※ 추가 보너스
- 작업폴더를 바꾸려면? os.chdir() 사용한다.
    - 마치 도스 시절의 'cd 폴더명'과 같은 느낌.
    
    
- 작업폴더가 바뀌면 위의 파일 읽어오는것도 작업폴더기준으로 바뀌게 된다. 


```python
print("현재작업폴더 : {}".format(os.getcwd()))

# 작업폴더를 C:\로 변경
os.chdir("C:/")
print("변경후작업폴더 : {}".format(os.getcwd()))
```

    현재작업폴더 : C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2
    변경후작업폴더 : C:\
    


```python
# 변경된 작업폴더의 파일 불러오기
file = 'train_c-drive.csv'
print(os.path.abspath(file))
pd.read_csv(file, sep=',').head(1)
```

    C:\train_c-drive.csv
    




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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



## 2. 왜 파이썬에는 windows 경로 문자인 \ 가 인식이 안되는가?
- \가 file str안에 인식안되는 이유는 간단하다.
    - 바로 \가 Escape Character이기 때문이다.
    - 참고링크 : https://docs.python.org/2.0/ref/strings.html
    - \n, \t, \\등 str에서 특수한 기능을하는 escape sequence의 시작 문자이기 때문에 단순 \는 다음문자가 무엇인가에 따라 전혀 다른 뜻이 된다.
    - 예를 들면 'C:\test\'로 경로를 입력하면 가운데 \t를 tab으로 인식하게 된다.
    - 그래서 경로를 위해 문자를 파이썬에서는 백슬래쉬 2개인 \\(='\')나 포워드슬래시 /로 구분한다.
    - (※ \ : BACKSLASH, / : FORWARDSLASH -> 영어사전참고함)

- 윈도우 경로를 그럼 어떻게 인식하게 효율적으로하는가?
    - A. 경로 str앞에 r붙이기
    - B. str.replace 함수이용하기

#### A. 윈도우형식 파일경로 str 앞에 r 붙이기
- r을 붙이면 escape sequence가 무시되어 경로 그대로를 반환한다.
- \로 입력한것들이 다 \\로 변환됨을 알 수 있다.


```python
파일경로 = r'C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2'
파일경로
```




    'C:\\study_2018\\python_study_2018\\200830_파일경로 및 패키지 경로\\b\\b-2'



#### B. str.replace() 함수 이용하기
- 안된다. SyntaxError: EOL while scanning string literal 라고 에러가 뜬다.
- '\' 자체도 인식이 안된다.ㅜ
- 그냥 A방법만 사용하자


```python
파일경로_before = 'C:\study_2018\python_study_2018\200830_파일경로 및 패키지 경로\b\b-2'
print('변경 전 파일경로 :', 파일경로_before)
파일경로_after = 파일경로_before.replace('\', '/')
print('변경 후 파일경로 :', 파일경로_after)
```


      File "<ipython-input-116-d18034d88900>", line 3
        파일경로_after = 파일경로_before.replace('\', '/')
                                                  ^
    SyntaxError: EOL while scanning string literal
    

