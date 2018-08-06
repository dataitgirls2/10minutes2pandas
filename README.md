
# Pandas 10분 완성

*역자 주 : 본 자료는 10 Minutes to Pandas(하단 원문 링크 참조)의 한글 번역 자료로, 번역은 데잇걸즈2 프로그램 교육생 모두가 함께 진행하였습니다. 데잇걸즈2는 과학기술정보통신부와 한국정보화진흥원이 주관하는 SW여성인재 빅데이터 분석 교육과정으로, 상세한 소개는 [홈페이지](http://dataitgirls2.pagedemo.co/)를 참조 부탁 드립니다.* <br>
*본 자료의 저작권은 Creative Common License 기준으로 CC BY-NC-ND(저작자표시 - 비영리 - 변경금지)인 점을 참조하여 주세요.* <br><br>
*This documentation is a Korean translation material of '10 Minutes to Pandas'. Every members of DATAITGIRLS2 program participated in the translation. If you want to know about DATAITGIRLS2 program, please visit [DATAITGIRLS2 program's homepage](http://dataitgirls2.pagedemo.co/).*<br>
*The copyright conditions of this documentation are CC BY-NC-ND on Creative Common License basis.* <br><br>

*역자 주(참조 자료) : [10 Minuts to Pandas 원문](https://pandas.pydata.org/pandas-docs/stable/10min.html), [판다스 개발자의 PyCon Korea 2016 발표 : Keynote](https://www.youtube.com/watch?v=O5uFF1H0R0M), [Pandas 10분 완성 원문의 인터넷 강의 영상](https://vimeo.com/59324550), [Pandas Cheat Sheet](http://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)* <br><br><br>


이 소개서는 주로 신규 사용자를 대상으로 한 판다스에 대한 간략한 소개입니다. 더 복잡한 방법은 [Cookbook](https://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook) 에서 볼 수 있습니다.


일반적으로 다음과 같이 불러옵니다.


```python
import pandas as pd
```


```python
import numpy as np
```


```python
import matplotlib.pyplot as plt
```

## Object Creation (객체 생성)

[데이터 구조 소개 섹션](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dsintro)을 참조하세요.

pandas는 값을 가지고 있는 리스트를 통해 [시리즈](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html#pandas.Series)를 만들고, 정수로 만들어진 인덱스를 기본값으로 불러올 것입니다.


```python
s = pd.Series([1,3,5,np.nan,6,8])
```


```python
s
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



datetime 인덱스와 레이블이 있는 열을 가지고 있는 NumPy 배열을 전달하여 데이터프레임을 만듭니다.


```python
dates = pd.date_range('20130101', periods=6)
```


```python
dates
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df = pd.DataFrame(np.random.randn(6,4), index=dates, columns=list('ABCD'))
```


```python
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.387345</td>
      <td>-0.443100</td>
      <td>-0.540677</td>
      <td>-0.370186</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.222998</td>
      <td>-1.308863</td>
      <td>0.433432</td>
      <td>0.409407</td>
    </tr>
  </tbody>
</table>
</div>



시리즈와 같은 것으로 변환될 수 있는 객체들의 dict로 구성된 데이터프레임을 만듭니다.


```python
df2 = pd.DataFrame({'A' : 1.,
                    'B' : pd.Timestamp('20130102'),
                    'C' : pd.Series(1,index=list(range(4)),dtype='float32'),
                    'D' : np.array([3] * 4,dtype='int32'),
                    'E' : pd.Categorical(["test","train","test","train"]),
                    'F' : 'foo' })
```


```python
df2
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>



데이터프레임 결과물의 열은 다양한 데이터 타입(dtypes)으로 구성됩니다.


```python
df2.dtypes
```




    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object



IPython을 이용하고 계시다면, (공용 속성을 포함한) 열 이름에 대한 Tap 자동완성 기능이 자동으로 활성화됩니다. <br>
다음은 완성될 속성에 대한 부분집합(subset)입니다. 

*역자 주 : 아래 제시된 코드의 경우, IPython이 아닌 환경(Google Colaboratory, Jupyter 등)에서는 사용이 불가능한 코드인 점에 주의하세요.*


```python
# df2.<TAB>
```

*역자 주 : IPython에서 실행하면 다음과 같은 결과값이 나옵니다.*

```
df2.A                  df2.bool
df2.abs                df2.boxplot
df2.add                df2.C
df2.add_prefix         df2.clip
df2.add_suffix         df2.clip_lower
df2.align              df2.clip_upper
df2.all                df2.columns
df2.any                df2.combine
df2.append             df2.combine_first
df2.apply              df2.compound
df2.applymap           df2.consolidate
df2.D
```

보시다시피, A, B, C 그리고 D 열이 Tab 자동완성 기능으로 실행됩니다. 물론 E도 있습니다. 나머지 속성들은 간결하게 잘라버렸습니다. 

## Viewing Data(데이터 확인하기)

[Basic Section](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics)을 참조하세요.

데이터프레임의 가장 윗 줄과 마지막 줄을 확인하고 싶을 때에 사용하는 방법은 다음과 같습니다. <br>

*역자 주 <br>
괄호()안에는 숫자가 들어갈 수도 있고 안 들어갈 수도 있습니다. <br>
숫자가 들어간다면, 윗/마지막 줄의 특정 줄을 불러올 수 있습니다. <br>
숫자가 들어가지 않다면, 기본값인 5로 처리됩니다.*

*예시 <br>
df.tail(3) - 끝에서 마지막 3줄을 불러옴 <br>
df.tail() - 끝에서 마지막 5줄 불러옴*


```python
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.387345</td>
      <td>-0.443100</td>
      <td>-0.540677</td>
      <td>-0.370186</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(3)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.387345</td>
      <td>-0.443100</td>
      <td>-0.540677</td>
      <td>-0.370186</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.222998</td>
      <td>-1.308863</td>
      <td>0.433432</td>
      <td>0.409407</td>
    </tr>
  </tbody>
</table>
</div>



인덱스(Index), 열(Column) 그리고 NumPy 데이터에 대한 세부 정보를 봅니다.


```python
df.index
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df.columns
```




    Index(['A', 'B', 'C', 'D'], dtype='object')




```python
df.values
```




    array([[ 1.20366414,  0.03519932, -0.51651206, -1.65195383],
           [-0.93589333,  0.85494382, -0.81497074, -0.33344655],
           [-2.36422326, -2.18746816,  1.01892836,  1.25290739],
           [-2.21401998,  0.36188549, -0.390074  , -0.49700376],
           [ 1.38734459, -0.44310022, -0.54067692, -0.37018639],
           [ 0.22299798, -1.30886252,  0.43343249,  0.40940659]])



[describe()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.describe.html#pandas.DataFrame.describe)는 데이터의 대략적인 통계적 정보 요약을 보여줍니다.


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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.450022</td>
      <td>-0.447900</td>
      <td>-0.134979</td>
      <td>-0.198379</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.647755</td>
      <td>1.127290</td>
      <td>0.706005</td>
      <td>0.972158</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>-0.814971</td>
      <td>-1.651954</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-1.894488</td>
      <td>-1.092422</td>
      <td>-0.534636</td>
      <td>-0.465299</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.356448</td>
      <td>-0.203950</td>
      <td>-0.453293</td>
      <td>-0.351816</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.958498</td>
      <td>0.280214</td>
      <td>0.227556</td>
      <td>0.223693</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.387345</td>
      <td>0.854944</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
  </tbody>
</table>
</div>



데이터를 전치합니다.


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
      <th>2013-01-01 00:00:00</th>
      <th>2013-01-02 00:00:00</th>
      <th>2013-01-03 00:00:00</th>
      <th>2013-01-04 00:00:00</th>
      <th>2013-01-05 00:00:00</th>
      <th>2013-01-06 00:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>1.203664</td>
      <td>-0.935893</td>
      <td>-2.364223</td>
      <td>-2.214020</td>
      <td>1.387345</td>
      <td>0.222998</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.035199</td>
      <td>0.854944</td>
      <td>-2.187468</td>
      <td>0.361885</td>
      <td>-0.443100</td>
      <td>-1.308863</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.516512</td>
      <td>-0.814971</td>
      <td>1.018928</td>
      <td>-0.390074</td>
      <td>-0.540677</td>
      <td>0.433432</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-1.651954</td>
      <td>-0.333447</td>
      <td>1.252907</td>
      <td>-0.497004</td>
      <td>-0.370186</td>
      <td>0.409407</td>
    </tr>
  </tbody>
</table>
</div>



축 별로 정렬합니다.


```python
df.sort_index(axis=1, ascending=False)
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
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.651954</td>
      <td>-0.516512</td>
      <td>0.035199</td>
      <td>1.203664</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.333447</td>
      <td>-0.814971</td>
      <td>0.854944</td>
      <td>-0.935893</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>1.252907</td>
      <td>1.018928</td>
      <td>-2.187468</td>
      <td>-2.364223</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.497004</td>
      <td>-0.390074</td>
      <td>0.361885</td>
      <td>-2.214020</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.370186</td>
      <td>-0.540677</td>
      <td>-0.443100</td>
      <td>1.387345</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.409407</td>
      <td>0.433432</td>
      <td>-1.308863</td>
      <td>0.222998</td>
    </tr>
  </tbody>
</table>
</div>



값 별로 정렬합니다.


```python
df.sort_values(by='B')
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.222998</td>
      <td>-1.308863</td>
      <td>0.433432</td>
      <td>0.409407</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.387345</td>
      <td>-0.443100</td>
      <td>-0.540677</td>
      <td>-0.370186</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
    </tr>
  </tbody>
</table>
</div>



## Selection (선택)

주석(Note) : 선택과 설정을 위한 Python / Numpy의 표준화된 표현들이 직관적이며, 코드 작성을 위한 양방향 작업에 유용하지만 우리는 Pandas에 최적화된 데이터 접근 방법인 .at, .iat, .loc 및 .iloc 을 추천합니다. 

[데이터 인덱싱 및 선택](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing) 문서와 [다중 인덱싱 / 심화 인덱싱](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced) 문서를 참조하세요.

### Getting (데이터 얻기)

df.A 와 동일한 Series를 생성하는 단일 열을 선택합니다.


```python
df['A']
```




    2013-01-01    1.203664
    2013-01-02   -0.935893
    2013-01-03   -2.364223
    2013-01-04   -2.214020
    2013-01-05    1.387345
    2013-01-06    0.222998
    Freq: D, Name: A, dtype: float64



행을 분할하는 []를 통해 선택합니다.


```python
df[0:3]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['20130102':'20130104']
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
    </tr>
  </tbody>
</table>
</div>



### Selection by Label (Label 을 통한 선택)

[Label을 통한 선택](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-label)에서 더 많은 내용을 확인하세요.

라벨을 사용하여 횡단면을 얻습니다.


```python
df.loc[dates[0]]
```




    A    1.203664
    B    0.035199
    C   -0.516512
    D   -1.651954
    Name: 2013-01-01 00:00:00, dtype: float64



라벨을 사용하여 여러 축(의 데이터)을 얻습니다.


```python
df.loc[:,['A','B']]
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.387345</td>
      <td>-0.443100</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.222998</td>
      <td>-1.308863</td>
    </tr>
  </tbody>
</table>
</div>



양쪽 종단점을 포함한 라벨 슬라이싱을 봅니다.


```python
df.loc['20130102':'20130104', ['A','B']]
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
    </tr>
  </tbody>
</table>
</div>



반환되는 객체의 차원를 줄입니다.


```python
df.loc['20130102',['A','B']]
```




    A   -0.935893
    B    0.854944
    Name: 2013-01-02 00:00:00, dtype: float64



스칼라 값을 얻습니다.


```python
df.loc[dates[0],'A']
```




    1.2036641391265706



스칼라 값을 더 빠르게 구하는 방법입니다. (앞선 메소드와 동일합니다.)


```python
df.at[dates[0],'A']
```




    1.2036641391265706



### Selection by Position (위치로 선택하기)

자세한 내용은 [위치로 선택하기](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-integer)를 참고해주세요.

넘겨받은 정수의 위치를 기준으로 선택합니다.


```python
df.iloc[3]
```




    A    0.834505
    B    0.029459
    C    0.543112
    D   -1.471167
    Name: 2013-01-04 00:00:00, dtype: float64



정수(로 표기된) 슬라이스들을 통해, numpy/python과 유사하게 작동합니다.


```python
df.iloc[3:5,0:2]
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
    </tr>
  </tbody>
</table>
</div>



정수(로 표기된) 위치값의 리스트들을 통해, numpy/python의 스타일과 유사해집니다.


```python
df.iloc[[1,2,4],[0,2]]
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
      <th>A</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>0.791482</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.394338</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>-0.839317</td>
    </tr>
  </tbody>
</table>
</div>



명시적으로 행을 나누고자 하는 경우입니다.


```python
df.iloc[1:3,:]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>0.791482</td>
      <td>-0.699104</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>1.669255</td>
    </tr>
  </tbody>
</table>
</div>



명시적으로 열을 나누고자 하는 경우입니다.


```python
df.iloc[:,1:3]
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
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.228990</td>
      <td>-0.412877</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.316784</td>
      <td>0.791482</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.117943</td>
      <td>-0.394338</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.029459</td>
      <td>0.543112</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>2.139297</td>
      <td>-0.839317</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.026487</td>
      <td>0.471119</td>
    </tr>
  </tbody>
</table>
</div>



명시적으로 (특정한) 값을 얻고자 하는 경우입니다.


```python
df.iloc[1,1]
```




    -0.31678422882681939



스칼라 값을 빠르게 얻는 방법입니다. (위의 방식과 동일합니다.)


```python
df.iat[1,1]
```




    -0.31678422882681939



### Boolean Indexing

데이터를 선택하기 위해 단일 열의 값을 사용합니다.


```python
df[df.A > 0]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>1.669255</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
      <td>0.543112</td>
      <td>-1.471167</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
      <td>-0.839317</td>
      <td>0.107340</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.766095</td>
      <td>-0.026487</td>
      <td>0.471119</td>
      <td>0.227956</td>
    </tr>
  </tbody>
</table>
</div>



Boolean 조건을 충족하는 데이터프레임에서 값을 선택합니다.


```python
df[df > 0]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.791482</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.669255</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
      <td>0.543112</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
      <td>NaN</td>
      <td>0.107340</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.766095</td>
      <td>NaN</td>
      <td>0.471119</td>
      <td>0.227956</td>
    </tr>
  </tbody>
</table>
</div>



필터링을 위한 메소드 [isin()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.isin.html#pandas.Series.isin)을 사용합니다.


```python
df2 = df.copy()
```


```python
df2['E'] = ['one', 'one', 'two', 'three', 'four', 'three']
```


```python
df2
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.285004</td>
      <td>-0.228990</td>
      <td>-0.412877</td>
      <td>-0.801001</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>0.791482</td>
      <td>-0.699104</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>1.669255</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
      <td>0.543112</td>
      <td>-1.471167</td>
      <td>three</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
      <td>-0.839317</td>
      <td>0.107340</td>
      <td>four</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.766095</td>
      <td>-0.026487</td>
      <td>0.471119</td>
      <td>0.227956</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2[df2['E'].isin(['two','four'])]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>1.669255</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
      <td>-0.839317</td>
      <td>0.107340</td>
      <td>four</td>
    </tr>
  </tbody>
</table>
</div>



### Setting (설정)

새 열을 설정하면 데이터가 인덱스 별로 자동 정렬됩니다.



```python
s1 = pd.Series([1,2,3,4,5,6], index=pd.date_range('20130102', periods=6))
```


```python
s1
```




    2013-01-02    1
    2013-01-03    2
    2013-01-04    3
    2013-01-05    4
    2013-01-06    5
    2013-01-07    6
    Freq: D, dtype: int64




```python
df['F'] = s1
```

라벨에 의해 값을 설정합니다.


```python
df.at[dates[0],'A'] = 0
```

위치에 의해 값을 설정합니다.


```python
df.iat[0,1] = 0
```

NumPy 배열을 사용한 할당에 의해 값을 설정합니다.


```python
df.loc[:,'D'] = np.array([5] * len(df))
```

위 설정대로 작동한 결과입니다.


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.412877</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>0.791482</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
      <td>0.543112</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.646337</td>
      <td>2.139297</td>
      <td>-0.839317</td>
      <td>5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.766095</td>
      <td>-0.026487</td>
      <td>0.471119</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



where 연산을 설정합니다.


```python
df2 = df.copy()
```


```python
df2[df2 > 0] = -df2
```


```python
df2
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.412877</td>
      <td>-5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>-0.791482</td>
      <td>-5</td>
      <td>-1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>-5</td>
      <td>-2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.834505</td>
      <td>-0.029459</td>
      <td>-0.543112</td>
      <td>-5</td>
      <td>-3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.646337</td>
      <td>-2.139297</td>
      <td>-0.839317</td>
      <td>-5</td>
      <td>-4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-1.766095</td>
      <td>-0.026487</td>
      <td>-0.471119</td>
      <td>-5</td>
      <td>-5.0</td>
    </tr>
  </tbody>
</table>
</div>



## Missing Data (결측치)

pandas는 결측치를 표현하기 위해 주로 np.nan 값을 사용합니다. 이 방법은 기본 설정값이지만 계산에는 포함되지 않습니다. <br>
[Missing Data section](https://pandas.pydata.org/pandas-docs/stable/missing_data.html#missing-data)를 참조하세요.

Reindexing으로 지정된 축 상의 인덱스를 변경/추가/삭제할 수 있습니다. Reindexing은 데이터의 복사본을 반환합니다.


```python
df1 = df.reindex(index=dates[0:4], columns=list(df.columns) + ['E'])
```


```python
df1.loc[dates[0]:dates[1],'E'] = 1
```


```python
df1
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.364223</td>
      <td>-2.187468</td>
      <td>1.018928</td>
      <td>1.252907</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.214020</td>
      <td>0.361885</td>
      <td>-0.390074</td>
      <td>-0.497004</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



결측치를 가지고 있는 행들을 지웁니다.


```python
df1.dropna(how='any')
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.203664</td>
      <td>0.035199</td>
      <td>-0.516512</td>
      <td>-1.651954</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.935893</td>
      <td>0.854944</td>
      <td>-0.814971</td>
      <td>-0.333447</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



결측치를 채워 넣습니다.


```python
df1.fillna(value=5)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.412877</td>
      <td>5</td>
      <td>5.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>0.791482</td>
      <td>5</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.812184</td>
      <td>-0.117943</td>
      <td>-0.394338</td>
      <td>5</td>
      <td>2.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.834505</td>
      <td>0.029459</td>
      <td>0.543112</td>
      <td>5</td>
      <td>3.0</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



nan인 값에 Boolean(을 통한) 표식을 얻습니다.

*역자 주 : 데이터프레임의 모든 값이 Boolean 형태로 표시되도록 하며, nan인 값에만 True가 표시되게 하는 함수입니다.*


```python
pd.isna(df1)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



## Operation (연산)

[이진(Binary) 연산의 기본 섹션](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-binop)을 참조하세요.

### Stats (통계)

일반적으로 결측치를 제외한 후 연산됩니다.

기술통계를 수행합니다.


```python
df.mean()
```




    A    0.442648
    B    0.284590
    C    0.026530
    D    5.000000
    F    3.000000
    dtype: float64



다른 축에서 동일한 연산을 수행합니다.


```python
df.mean(1)
```




    2013-01-01    1.146781
    2013-01-02    1.014293
    2013-01-03    1.459981
    2013-01-04    1.881415
    2013-01-05    2.189263
    2013-01-06    2.442146
    Freq: D, dtype: float64



정렬이 필요하며, 차원이 다른 객체로 연산해보겠습니다. 또한, pandas는 지정된 차원을 따라 자동으로 브로드 캐스팅됩니다.

*역자 주 : broadcast란 numpy에서 유래한 용어로, n차원이나 스칼라 값으로 연산을 수행할 때 도출되는 결과의 규칙을 설명하는 것을 의미합니다.*


```python
s = pd.Series([1,3,5,np.nan,6,8], index=dates).shift(2)
```


```python
s
```




    2013-01-01    NaN
    2013-01-02    NaN
    2013-01-03    1.0
    2013-01-04    3.0
    2013-01-05    5.0
    2013-01-06    NaN
    Freq: D, dtype: float64




```python
df.sub(s, axis='index')
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.187816</td>
      <td>-1.117943</td>
      <td>-1.394338</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.165495</td>
      <td>-2.970541</td>
      <td>-2.456888</td>
      <td>2.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-4.353663</td>
      <td>-2.860703</td>
      <td>-5.839317</td>
      <td>0.0</td>
      <td>-1.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Apply (적용)

데이터에 함수를 적용합니다.


```python
df.apply(np.cumsum)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.412877</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.403231</td>
      <td>-0.316784</td>
      <td>0.378605</td>
      <td>10</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.591046</td>
      <td>-0.434727</td>
      <td>-0.015733</td>
      <td>15</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.243458</td>
      <td>-0.405268</td>
      <td>0.527380</td>
      <td>20</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.889795</td>
      <td>1.734029</td>
      <td>-0.311938</td>
      <td>25</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>2.655891</td>
      <td>1.707541</td>
      <td>0.159182</td>
      <td>30</td>
      <td>15.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.apply(lambda x: x.max() - x.min())
```




    A    3.169326
    B    2.456081
    C    1.630800
    D    0.000000
    F    4.000000
    dtype: float64



### Histogramming (히스토그래밍)

더 많은 내용은 [Histogramming and Discretization (히스토그래밍과 이산화)](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-discretization) 항목을 참조하세요.


```python
s = pd.Series(np.random.randint(0, 7, size=10))
```


```python
s
```




    0    0
    1    0
    2    3
    3    0
    4    3
    5    2
    6    5
    7    5
    8    2
    9    3
    dtype: int32




```python
s.value_counts()
```




    3    3
    0    3
    5    2
    2    2
    dtype: int64



### String Methods (문자열 메소드)

Series는 다음의 코드와 같이 문자열 처리 메소드 모음(set)을 가지고 있습니다. <br>
이 모음은 배열의 각 요소를 쉽게 조작할 수 있도록 만들어주는 문자열의 속성에 포함되어 있습니다.

문자열의 패턴 일치 확인은 기본적으로 정규 표현식을 사용하며, 몇몇 경우에는 항상 정규 표현식을 사용함에 유의하십시오.

좀 더 자세한 내용은 [벡터화된 문자열 메소드](https://pandas.pydata.org/pandas-docs/stable/text.html#text-string-methods) 부분에서 확인할 수 있습니다.


```python
s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])
```


```python
s.str.lower()
```




    0       a
    1       b
    2       c
    3    aaba
    4    baca
    5     NaN
    6    caba
    7     dog
    8     cat
    dtype: object



## Merge (병합)

### Concat (연결)

결합(join) / 병합(merge) 형태의 연산에 대한 인덱스, 관계 대수 기능을 위한 다양한 형태의 논리를 포함한 Series, 데이터프레임, Panel 객체를 손쉽게 결합할 수 있도록 하는 다양한 기능을 pandas 에서 제공합니다. 

[Merging](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging) 부분을 참조하세요. 

[concat()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.concat.html#pandas.concat)으로 pandas 객체를 연결합니다. 


```python
df = pd.DataFrame(np.random.randn(10, 4))
```


```python
df
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.619545</td>
      <td>0.438321</td>
      <td>0.045161</td>
      <td>-0.090580</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.607351</td>
      <td>-0.460920</td>
      <td>1.086252</td>
      <td>0.069311</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.505874</td>
      <td>-0.147020</td>
      <td>0.762800</td>
      <td>-1.948289</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.893628</td>
      <td>-1.387833</td>
      <td>1.010362</td>
      <td>1.073543</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.007528</td>
      <td>-0.380234</td>
      <td>0.466893</td>
      <td>0.189073</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.173880</td>
      <td>-0.164525</td>
      <td>1.020937</td>
      <td>0.641751</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.550514</td>
      <td>-0.796966</td>
      <td>-0.071519</td>
      <td>-0.493431</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.250619</td>
      <td>-1.676189</td>
      <td>-1.722703</td>
      <td>-0.639210</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.119734</td>
      <td>-0.599197</td>
      <td>2.282847</td>
      <td>0.403409</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.233205</td>
      <td>-0.569511</td>
      <td>-0.780681</td>
      <td>0.654899</td>
    </tr>
  </tbody>
</table>
</div>




```python
# break it into pieces
pieces = [df[:3], df[3:7], df[7:]]
```


```python
pd.concat(pieces)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.619545</td>
      <td>0.438321</td>
      <td>0.045161</td>
      <td>-0.090580</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.607351</td>
      <td>-0.460920</td>
      <td>1.086252</td>
      <td>0.069311</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.505874</td>
      <td>-0.147020</td>
      <td>0.762800</td>
      <td>-1.948289</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.893628</td>
      <td>-1.387833</td>
      <td>1.010362</td>
      <td>1.073543</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.007528</td>
      <td>-0.380234</td>
      <td>0.466893</td>
      <td>0.189073</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.173880</td>
      <td>-0.164525</td>
      <td>1.020937</td>
      <td>0.641751</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.550514</td>
      <td>-0.796966</td>
      <td>-0.071519</td>
      <td>-0.493431</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.250619</td>
      <td>-1.676189</td>
      <td>-1.722703</td>
      <td>-0.639210</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.119734</td>
      <td>-0.599197</td>
      <td>2.282847</td>
      <td>0.403409</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.233205</td>
      <td>-0.569511</td>
      <td>-0.780681</td>
      <td>0.654899</td>
    </tr>
  </tbody>
</table>
</div>



### Join (결합)

SQL 방식으로 병합합니다. [데이터베이스 스타일 결합](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-join) 부분을 참고하세요.


```python
left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})
```


```python
left
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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on= 'key')
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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



다른 예시입니다.


```python
left = pd.DataFrame({'key' : ['foo', 'bar'], 'lval' : [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'bar'], 'rval': [4, 5]})
```


```python
left
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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right 
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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on= 'key')
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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



### Append (추가)

데이터프레임에 행을 추가합니다. [Appending](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-concatenation) 부분을 참조하세요.


```python
df = pd.DataFrame(np.random.randn(8, 4), columns=['A', 'B', 'C', 'D'])
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.299919</td>
      <td>-1.472544</td>
      <td>-0.707566</td>
      <td>-0.365660</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.187241</td>
      <td>1.968653</td>
      <td>0.824469</td>
      <td>0.358518</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.034656</td>
      <td>0.829071</td>
      <td>-0.378907</td>
      <td>0.293894</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.414106</td>
      <td>2.328096</td>
      <td>-1.367931</td>
      <td>0.228907</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.914727</td>
      <td>-0.052547</td>
      <td>-0.583842</td>
      <td>-0.231221</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.178399</td>
      <td>-1.257682</td>
      <td>0.560755</td>
      <td>0.005913</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.507263</td>
      <td>0.446625</td>
      <td>-0.014416</td>
      <td>0.345235</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.367934</td>
      <td>0.292150</td>
      <td>1.821888</td>
      <td>-2.561016</td>
    </tr>
  </tbody>
</table>
</div>




```python
s = df.iloc[3]
```


```python
df.append(s, ignore_index=True)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.299919</td>
      <td>-1.472544</td>
      <td>-0.707566</td>
      <td>-0.365660</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.187241</td>
      <td>1.968653</td>
      <td>0.824469</td>
      <td>0.358518</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.034656</td>
      <td>0.829071</td>
      <td>-0.378907</td>
      <td>0.293894</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.414106</td>
      <td>2.328096</td>
      <td>-1.367931</td>
      <td>0.228907</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.914727</td>
      <td>-0.052547</td>
      <td>-0.583842</td>
      <td>-0.231221</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.178399</td>
      <td>-1.257682</td>
      <td>0.560755</td>
      <td>0.005913</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.507263</td>
      <td>0.446625</td>
      <td>-0.014416</td>
      <td>0.345235</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.367934</td>
      <td>0.292150</td>
      <td>1.821888</td>
      <td>-2.561016</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.414106</td>
      <td>2.328096</td>
      <td>-1.367931</td>
      <td>0.228907</td>
    </tr>
  </tbody>
</table>
</div>



## Grouping (그룹화)

**그룹화**는 다음 단계 중 하나 이상을 포함하는 과정을 가리킵니다.

- 몇몇 기준에 따라 여러 그룹으로 데이터를 **분할(Splitting)**
- 각 그룹에 독립적으로 함수를 **적용(Applying)**
- 결과물들을 하나의 데이터 구조로  **결합(Combining)**

자세한 내용은 [그룹화](https://pandas.pydata.org/pandas-docs/stable/groupby.html#groupby) 부분을 참조하세요.


```python
df = pd.DataFrame(
    {
        'A' : ['foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'foo'],
        'B' : ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],
        'C' : np.random.randn(8),
        'D' : np.random.randn(8)
    })
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>0.297352</td>
      <td>-1.025981</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>one</td>
      <td>0.796546</td>
      <td>1.127086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>1.645520</td>
      <td>-0.659429</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>three</td>
      <td>1.328364</td>
      <td>0.263898</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foo</td>
      <td>two</td>
      <td>0.531388</td>
      <td>0.859260</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>two</td>
      <td>2.099372</td>
      <td>-0.720175</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foo</td>
      <td>one</td>
      <td>-0.038247</td>
      <td>-0.295680</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foo</td>
      <td>three</td>
      <td>0.351615</td>
      <td>0.543172</td>
    </tr>
  </tbody>
</table>
</div>



(생성된 데이터프레임을) 그룹화한 후 각 그룹에 [sum()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sum.html#pandas.DataFrame.sum) 함수를 적용합니다.


```python
df.groupby('A').sum()
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
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>4.224282</td>
      <td>0.670809</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>2.787628</td>
      <td>-0.578657</td>
    </tr>
  </tbody>
</table>
</div>



여러 열을 기준으로 그룹화하면 계층적 인덱스가 형성됩니다. 여기에도 sum 함수를 적용할 수 있습니다.


```python
df.groupby(['A','B']).sum()
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
      <th></th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



## Reshaping (변형)

[계층적 인덱싱](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced-hierarchical) 및 [변형](https://pandas.pydata.org/pandas-docs/stable/reshaping.html#reshaping-stacking) 부분을 참조하세요.

### Stack (스택)


```python
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz',
                     'foo', 'foo', 'qux', 'qux'],
                    ['one', 'two', 'one', 'two',
                     'one', 'two', 'one', 'two']]))
```


```python
index = pd.MultiIndex.from_tuples(tuples, names=['first', 'second'])
```


```python
df = pd.DataFrame(np.random.randn(8, 2), index=index, columns=['A', 'B'])
```


```python
df2  =  df[:4]
```


```python
df2
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
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-0.726072</td>
      <td>-1.436126</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.211388</td>
      <td>1.305562</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>0.399729</td>
      <td>-1.519716</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.278913</td>
      <td>0.079106</td>
    </tr>
  </tbody>
</table>
</div>



[stack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.stack.html#pandas.DataFrame.stack) 메소드는 데이터프레임 열들의 계층을 "압축"합니다.


```python
stacked = df2.stack()
```


```python
stacked
```




    first  second   
    bar    one     A   -0.726072
                   B   -1.436126
           two     A    0.211388
                   B    1.305562
    baz    one     A    0.399729
                   B   -1.519716
           two     A   -0.278913
                   B    0.079106
    dtype: float64



"Stack된" 데이터프레임 또는 (MultiIndex를 인덱스로 사용하는) Series인 경우, [stack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.stack.html#pandas.DataFrame.stack)의 역 연산은 [unstack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.unstack.html#pandas.DataFrame.unstack)이며, 기본적으로 **마지막 계층**을 unstack합니다.


```python
stacked.unstack()
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
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-0.726072</td>
      <td>-1.436126</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.211388</td>
      <td>1.305562</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>0.399729</td>
      <td>-1.519716</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.278913</td>
      <td>0.079106</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(1)
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
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>-0.726072</td>
      <td>0.211388</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.436126</td>
      <td>1.305562</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>0.399729</td>
      <td>-0.278913</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.519716</td>
      <td>0.079106</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(0)
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
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>-0.726072</td>
      <td>0.399729</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.436126</td>
      <td>-1.519716</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>0.211388</td>
      <td>-0.278913</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.305562</td>
      <td>0.079106</td>
    </tr>
  </tbody>
</table>
</div>



### Pivot Tables (피벗 테이블)

[피벗 테이블](https://pandas.pydata.org/pandas-docs/stable/reshaping.html#reshaping-pivot) 부분을 참조하세요.


```python
df = pd.DataFrame({'A' : ['one', 'one', 'two', 'three'] * 3,
                   'B' : ['A', 'B', 'C'] * 4,
                   'C' : ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,
                   'D' : np.random.randn(12),
                   'E' : np.random.randn(12)})
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>A</td>
      <td>foo</td>
      <td>-0.776195</td>
      <td>1.198841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.317653</td>
      <td>-1.110124</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>C</td>
      <td>foo</td>
      <td>1.848317</td>
      <td>0.050875</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>A</td>
      <td>bar</td>
      <td>1.678460</td>
      <td>-0.206626</td>
    </tr>
    <tr>
      <th>4</th>
      <td>one</td>
      <td>B</td>
      <td>bar</td>
      <td>-0.509394</td>
      <td>0.740372</td>
    </tr>
    <tr>
      <th>5</th>
      <td>one</td>
      <td>C</td>
      <td>bar</td>
      <td>0.128912</td>
      <td>-0.491783</td>
    </tr>
    <tr>
      <th>6</th>
      <td>two</td>
      <td>A</td>
      <td>foo</td>
      <td>1.251120</td>
      <td>-1.181534</td>
    </tr>
    <tr>
      <th>7</th>
      <td>three</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.292120</td>
      <td>0.299805</td>
    </tr>
    <tr>
      <th>8</th>
      <td>one</td>
      <td>C</td>
      <td>foo</td>
      <td>1.371375</td>
      <td>-0.603625</td>
    </tr>
    <tr>
      <th>9</th>
      <td>one</td>
      <td>A</td>
      <td>bar</td>
      <td>1.291114</td>
      <td>-1.712893</td>
    </tr>
    <tr>
      <th>10</th>
      <td>two</td>
      <td>B</td>
      <td>bar</td>
      <td>0.897307</td>
      <td>-0.651877</td>
    </tr>
    <tr>
      <th>11</th>
      <td>three</td>
      <td>C</td>
      <td>bar</td>
      <td>0.082510</td>
      <td>-0.336216</td>
    </tr>
  </tbody>
</table>
</div>



이 데이터로부터 피벗 테이블을 매우 쉽게 생성할 수 있습니다.


```python
pd.pivot_table(df, values='D', index=['A', 'B'], columns=['C'])
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
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>1.291114</td>
      <td>-0.776195</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.509394</td>
      <td>-0.317653</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.128912</td>
      <td>1.371375</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>1.678460</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>-0.292120</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.082510</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>1.251120</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.897307</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>1.848317</td>
    </tr>
  </tbody>
</table>
</div>



## Time Series (시계열)

pandas는 자주 일어나는 변환(예시 : 5분마다 일어나는 데이터에 대한 2차 데이터 변환) 사이에 수행하는 리샘플링 연산을 위한 간단하고, 강력하며, 효율적인 함수를 제공합니다. 이는 재무(금융) 응용에서 매우 일반적이지만 이에 국한되지는 않습니다. [시계열](https://pandas.pydata.org/pandas-docs/stable/timeseries.html#timeseries) 부분을 참고하세요.


```python
rng = pd.date_range('1/1/2012', periods=100, freq='S')
```


```python
ts = pd.Series(np.random.randint(0, 500, len(rng)), index=rng)
```


```python
ts.resample('5Min').sum()
```




    2012-01-01    25654
    Freq: 5T, dtype: int32



시간대를 표현합니다.


```python
rng = pd.date_range('3/6/2012 00:00', periods=5, freq='D')
```


```python
ts = pd.Series(np.random.randn(len(rng)), rng)
```


```python
ts
```




    2012-03-06   -1.170229
    2012-03-07    0.995390
    2012-03-08   -2.433136
    2012-03-09   -1.579099
    2012-03-10   -0.139682
    Freq: D, dtype: float64




```python
ts_utc = ts.tz_localize('UTC')
```


```python
ts_utc
```




    2012-03-06 00:00:00+00:00   -1.170229
    2012-03-07 00:00:00+00:00    0.995390
    2012-03-08 00:00:00+00:00   -2.433136
    2012-03-09 00:00:00+00:00   -1.579099
    2012-03-10 00:00:00+00:00   -0.139682
    Freq: D, dtype: float64



다른 시간대로 변환합니다.


```python
ts_utc.tz_convert('US/Eastern')
```




    2012-03-05 19:00:00-05:00   -1.170229
    2012-03-06 19:00:00-05:00    0.995390
    2012-03-07 19:00:00-05:00   -2.433136
    2012-03-08 19:00:00-05:00   -1.579099
    2012-03-09 19:00:00-05:00   -0.139682
    Freq: D, dtype: float64



시간 표현 ↔ 기간 표현으로 변환합니다.


```python
rng = pd.date_range('1/1/2012', periods=5, freq='M')
```


```python
ts = pd.Series(np.random.randn(len(rng)), index=rng)
```


```python
ts
```




    2012-01-31    0.080979
    2012-02-29    0.075085
    2012-03-31   -0.076771
    2012-04-30    0.819286
    2012-05-31   -0.542812
    Freq: M, dtype: float64




```python
ps = ts.to_period()
```


```python
ps
```




    2012-01    0.080979
    2012-02    0.075085
    2012-03   -0.076771
    2012-04    0.819286
    2012-05   -0.542812
    Freq: M, dtype: float64




```python
ps.to_timestamp()
```




    2012-01-01    0.080979
    2012-02-01    0.075085
    2012-03-01   -0.076771
    2012-04-01    0.819286
    2012-05-01   -0.542812
    Freq: MS, dtype: float64



기간 ↔ 시간 변환은 편리한 산술 기능들을 사용할 수 있도록 만들어줍니다. 다음 예제에서, 우리는 11월에 끝나는 연말 결산의 분기별 빈도를 분기말 익월의 월말일 오전 9시로 변환합니다.


```python
prng = pd.period_range('1990Q1', '2000Q4', freq='Q-NOV')
```


```python
ts = pd.Series(np.random.randn(len(prng)), prng)
```


```python
ts.index = (prng.asfreq('M', 'e') + 1).asfreq('H', 's') + 9
```


```python
ts.head()
```




    1990-03-01 09:00    0.018325
    1990-06-01 09:00    1.330483
    1990-09-01 09:00    1.122604
    1990-12-01 09:00    0.288536
    1991-03-01 09:00    1.161760
    Freq: H, dtype: float64



## Categoricals (범주화)

pandas는 데이터프레임 내에 범주형 데이터를 포함할 수 있습니다. [범주형 소개](https://pandas.pydata.org/pandas-docs/stable/categorical.html#categorical) 와 [API 문서](https://pandas.pydata.org/pandas-docs/stable/api.html#api-categorical) 부분을 참조하세요.


```python
df = pd.DataFrame({"id":[1,2,3,4,5,6], "raw_grade":['a', 'b', 'b', 'a', 'a', 'e']})
```

가공하지 않은 성적을 범주형 데이터로 변환합니다.


```python
df["grade"] = df["raw_grade"].astype("category")
```


```python
df["grade"]
```




    0    a
    1    b
    2    b
    3    a
    4    a
    5    e
    Name: grade, dtype: category
    Categories (3, object): [a, b, e]



범주에 더 의미 있는 이름을 붙여주세요. (Series.cat.categories로 할당하는 것이 적합합니다!)


```python
df["grade"].cat.categories = ["very good", "good", "very bad"]
```

범주의 순서를 바꾸고 동시에 누락된 범주를 추가합니다. (Series.cat에 속하는 메소드는 기본적으로 새로운 Series를 반환합니다.)


```python
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "medium", "good", "very good"])
```


```python
df["grade"]
```




    0    very good
    1         good
    2         good
    3    very good
    4    very good
    5     very bad
    Name: grade, dtype: category
    Categories (5, object): [very bad, bad, medium, good, very good]



정렬은 사전 순서가 아닌, 해당 범주에서 지정된 순서대로 배열합니다.

*역자 주 : 131번에서 very bad, bad, medium, good, very good 의 순서로 기재되어 있기 때문에 정렬 결과도 해당 순서대로 배열됩니다.*


```python
df.sort_values(by="grade")
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
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>



범주의 열을 기준으로 그룹화하면 빈 범주도 표시됩니다.


```python
df.groupby("grade").size()
```




    grade
    very bad     1
    bad          0
    medium       0
    good         2
    very good    3
    dtype: int64



## Plotting

[Plotting](https://pandas.pydata.org/pandas-docs/stable/visualization.html#visualization) 부분을 참조하세요.


```python
ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))
```


```python
ts = ts.cumsum()
```


```python
ts.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x9974fd0>



데이터프레임에서 [plot()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html#pandas.DataFrame.plot) 메소드는 라벨이 존재하는 모든 열을 그릴 때 편리합니다.


```python
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,
                  columns=['A', 'B', 'C', 'D'])  
```


```python
df = df.cumsum()
```


```python
plt.figure(); df.plot(); plt.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x9b10208>



## Getting Data In/Out (데이터 입/출력)

### CSV

[csv 파일에 씁니다.](https://pandas.pydata.org/pandas-docs/stable/io.html#io-store-in-csv)


```python
df.to_csv('foo.csv')
```

[csv 파일을 읽습니다.](https://pandas.pydata.org/pandas-docs/stable/io.html#io-read-csv-table)


```python
pd.read_csv('foo.csv')
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
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>-1.170941</td>
      <td>0.688051</td>
      <td>-0.383810</td>
      <td>0.837035</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>-1.325416</td>
      <td>0.061442</td>
      <td>-1.080497</td>
      <td>0.281412</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>-0.687276</td>
      <td>0.916830</td>
      <td>-2.839985</td>
      <td>1.852432</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>-1.288728</td>
      <td>-0.242376</td>
      <td>-3.791390</td>
      <td>1.309750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>-0.937522</td>
      <td>-0.779122</td>
      <td>-5.202554</td>
      <td>2.219908</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2000-01-06</td>
      <td>-2.136242</td>
      <td>-0.693236</td>
      <td>-6.256821</td>
      <td>3.015780</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2000-01-07</td>
      <td>-1.412520</td>
      <td>-2.517668</td>
      <td>-5.712015</td>
      <td>3.805923</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000-01-08</td>
      <td>-0.049283</td>
      <td>-1.716615</td>
      <td>-7.405345</td>
      <td>4.770589</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000-01-09</td>
      <td>0.592184</td>
      <td>-0.617583</td>
      <td>-7.339519</td>
      <td>3.694828</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2000-01-10</td>
      <td>1.378037</td>
      <td>0.110647</td>
      <td>-5.297688</td>
      <td>3.467191</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000-01-11</td>
      <td>2.474387</td>
      <td>-0.083230</td>
      <td>-4.153509</td>
      <td>3.091714</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000-01-12</td>
      <td>1.621882</td>
      <td>0.016834</td>
      <td>-7.112481</td>
      <td>1.237205</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000-01-13</td>
      <td>1.246822</td>
      <td>-1.368471</td>
      <td>-5.531885</td>
      <td>0.338128</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2000-01-14</td>
      <td>1.978975</td>
      <td>-0.527194</td>
      <td>-5.112244</td>
      <td>1.466986</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2000-01-15</td>
      <td>1.450342</td>
      <td>0.450082</td>
      <td>-4.731543</td>
      <td>3.673504</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2000-01-16</td>
      <td>1.948955</td>
      <td>1.059912</td>
      <td>-6.297084</td>
      <td>4.191426</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2000-01-17</td>
      <td>2.035009</td>
      <td>2.273572</td>
      <td>-6.637326</td>
      <td>3.746256</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2000-01-18</td>
      <td>1.550255</td>
      <td>3.503449</td>
      <td>-6.578056</td>
      <td>4.099211</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2000-01-19</td>
      <td>1.864008</td>
      <td>4.212954</td>
      <td>-7.183693</td>
      <td>2.888867</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2000-01-20</td>
      <td>-0.075277</td>
      <td>5.007933</td>
      <td>-7.093309</td>
      <td>4.735946</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000-01-21</td>
      <td>-1.140021</td>
      <td>6.814976</td>
      <td>-6.716311</td>
      <td>5.306338</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2000-01-22</td>
      <td>1.162872</td>
      <td>6.534765</td>
      <td>-6.110653</td>
      <td>5.233384</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2000-01-23</td>
      <td>1.760717</td>
      <td>5.714708</td>
      <td>-4.054118</td>
      <td>4.785703</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2000-01-24</td>
      <td>0.536450</td>
      <td>5.849652</td>
      <td>-3.765441</td>
      <td>3.989357</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2000-01-25</td>
      <td>0.506539</td>
      <td>6.692062</td>
      <td>-4.821839</td>
      <td>3.023168</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2000-01-26</td>
      <td>0.958889</td>
      <td>6.568955</td>
      <td>-4.259598</td>
      <td>2.421934</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2000-01-27</td>
      <td>-0.172696</td>
      <td>4.921587</td>
      <td>-4.413335</td>
      <td>2.314551</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2000-01-28</td>
      <td>0.165740</td>
      <td>5.134014</td>
      <td>-3.341849</td>
      <td>1.133864</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2000-01-29</td>
      <td>0.093579</td>
      <td>4.991880</td>
      <td>-4.020020</td>
      <td>2.081721</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000-01-30</td>
      <td>0.424503</td>
      <td>4.328352</td>
      <td>-3.503704</td>
      <td>2.303425</td>
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
      <th>970</th>
      <td>2002-08-28</td>
      <td>-9.441308</td>
      <td>-10.407354</td>
      <td>60.908649</td>
      <td>-3.372065</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2002-08-29</td>
      <td>-10.022290</td>
      <td>-10.300304</td>
      <td>59.022868</td>
      <td>-4.729307</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2002-08-30</td>
      <td>-10.771862</td>
      <td>-10.121161</td>
      <td>59.190720</td>
      <td>-4.776657</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2002-08-31</td>
      <td>-11.397452</td>
      <td>-10.721580</td>
      <td>59.955429</td>
      <td>-4.837409</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2002-09-01</td>
      <td>-12.606183</td>
      <td>-12.794658</td>
      <td>60.073882</td>
      <td>-6.897691</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2002-09-02</td>
      <td>-11.490124</td>
      <td>-12.763907</td>
      <td>60.835452</td>
      <td>-6.677909</td>
    </tr>
    <tr>
      <th>976</th>
      <td>2002-09-03</td>
      <td>-11.985902</td>
      <td>-12.161442</td>
      <td>60.848448</td>
      <td>-6.248310</td>
    </tr>
    <tr>
      <th>977</th>
      <td>2002-09-04</td>
      <td>-12.581613</td>
      <td>-11.248297</td>
      <td>60.504354</td>
      <td>-6.408271</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2002-09-05</td>
      <td>-13.733525</td>
      <td>-10.625722</td>
      <td>58.903688</td>
      <td>-5.788621</td>
    </tr>
    <tr>
      <th>979</th>
      <td>2002-09-06</td>
      <td>-13.257015</td>
      <td>-10.091945</td>
      <td>58.625660</td>
      <td>-4.776391</td>
    </tr>
    <tr>
      <th>980</th>
      <td>2002-09-07</td>
      <td>-12.855639</td>
      <td>-8.795421</td>
      <td>59.073399</td>
      <td>-4.017372</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2002-09-08</td>
      <td>-11.482862</td>
      <td>-9.402805</td>
      <td>58.042510</td>
      <td>-3.530595</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2002-09-09</td>
      <td>-10.850022</td>
      <td>-9.553852</td>
      <td>57.214538</td>
      <td>-4.053349</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2002-09-10</td>
      <td>-12.208049</td>
      <td>-9.259484</td>
      <td>58.237309</td>
      <td>-3.971102</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2002-09-11</td>
      <td>-12.401630</td>
      <td>-9.367988</td>
      <td>58.999006</td>
      <td>-3.615675</td>
    </tr>
    <tr>
      <th>985</th>
      <td>2002-09-12</td>
      <td>-14.382630</td>
      <td>-7.615701</td>
      <td>61.633138</td>
      <td>-2.822245</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2002-09-13</td>
      <td>-14.385503</td>
      <td>-5.825456</td>
      <td>62.643005</td>
      <td>-2.631831</td>
    </tr>
    <tr>
      <th>987</th>
      <td>2002-09-14</td>
      <td>-14.670608</td>
      <td>-6.534945</td>
      <td>63.046983</td>
      <td>-2.521697</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2002-09-15</td>
      <td>-15.424981</td>
      <td>-6.552120</td>
      <td>64.461886</td>
      <td>-3.493400</td>
    </tr>
    <tr>
      <th>989</th>
      <td>2002-09-16</td>
      <td>-13.875303</td>
      <td>-7.511547</td>
      <td>64.741750</td>
      <td>-4.255253</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2002-09-17</td>
      <td>-13.574444</td>
      <td>-7.407093</td>
      <td>64.003745</td>
      <td>-3.096605</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2002-09-18</td>
      <td>-13.843896</td>
      <td>-7.287694</td>
      <td>64.860323</td>
      <td>-3.211695</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2002-09-19</td>
      <td>-13.444606</td>
      <td>-8.069938</td>
      <td>66.156664</td>
      <td>-3.679680</td>
    </tr>
    <tr>
      <th>993</th>
      <td>2002-09-20</td>
      <td>-14.319578</td>
      <td>-6.771972</td>
      <td>64.871045</td>
      <td>-4.633304</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2002-09-21</td>
      <td>-15.126463</td>
      <td>-7.993281</td>
      <td>65.080881</td>
      <td>-3.497950</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>-14.717619</td>
      <td>-8.359075</td>
      <td>65.765170</td>
      <td>-5.577461</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>-13.763743</td>
      <td>-8.046417</td>
      <td>66.821624</td>
      <td>-5.256422</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>-15.111257</td>
      <td>-5.814779</td>
      <td>66.104899</td>
      <td>-6.185853</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>-14.890142</td>
      <td>-5.402545</td>
      <td>65.420458</td>
      <td>-5.578971</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>-14.917314</td>
      <td>-5.732310</td>
      <td>63.944766</td>
      <td>-6.181776</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



### HDF5

[HDFStores](https://pandas.pydata.org/pandas-docs/stable/io.html#io-hdf5)에 읽고 씁니다.

HDF5 Store에 씁니다.


```python
df.to_hdf('foo.h5','df')
```

HDF5 Store에서 읽어옵니다.


```python
pd.read_hdf('foo.h5','df')
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-1.170941</td>
      <td>0.688051</td>
      <td>-0.383810</td>
      <td>0.837035</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>-1.325416</td>
      <td>0.061442</td>
      <td>-1.080497</td>
      <td>0.281412</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>-0.687276</td>
      <td>0.916830</td>
      <td>-2.839985</td>
      <td>1.852432</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>-1.288728</td>
      <td>-0.242376</td>
      <td>-3.791390</td>
      <td>1.309750</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>-0.937522</td>
      <td>-0.779122</td>
      <td>-5.202554</td>
      <td>2.219908</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>-2.136242</td>
      <td>-0.693236</td>
      <td>-6.256821</td>
      <td>3.015780</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-1.412520</td>
      <td>-2.517668</td>
      <td>-5.712015</td>
      <td>3.805923</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-0.049283</td>
      <td>-1.716615</td>
      <td>-7.405345</td>
      <td>4.770589</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>0.592184</td>
      <td>-0.617583</td>
      <td>-7.339519</td>
      <td>3.694828</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>1.378037</td>
      <td>0.110647</td>
      <td>-5.297688</td>
      <td>3.467191</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>2.474387</td>
      <td>-0.083230</td>
      <td>-4.153509</td>
      <td>3.091714</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>1.621882</td>
      <td>0.016834</td>
      <td>-7.112481</td>
      <td>1.237205</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>1.246822</td>
      <td>-1.368471</td>
      <td>-5.531885</td>
      <td>0.338128</td>
    </tr>
    <tr>
      <th>2000-01-14</th>
      <td>1.978975</td>
      <td>-0.527194</td>
      <td>-5.112244</td>
      <td>1.466986</td>
    </tr>
    <tr>
      <th>2000-01-15</th>
      <td>1.450342</td>
      <td>0.450082</td>
      <td>-4.731543</td>
      <td>3.673504</td>
    </tr>
    <tr>
      <th>2000-01-16</th>
      <td>1.948955</td>
      <td>1.059912</td>
      <td>-6.297084</td>
      <td>4.191426</td>
    </tr>
    <tr>
      <th>2000-01-17</th>
      <td>2.035009</td>
      <td>2.273572</td>
      <td>-6.637326</td>
      <td>3.746256</td>
    </tr>
    <tr>
      <th>2000-01-18</th>
      <td>1.550255</td>
      <td>3.503449</td>
      <td>-6.578056</td>
      <td>4.099211</td>
    </tr>
    <tr>
      <th>2000-01-19</th>
      <td>1.864008</td>
      <td>4.212954</td>
      <td>-7.183693</td>
      <td>2.888867</td>
    </tr>
    <tr>
      <th>2000-01-20</th>
      <td>-0.075277</td>
      <td>5.007933</td>
      <td>-7.093309</td>
      <td>4.735946</td>
    </tr>
    <tr>
      <th>2000-01-21</th>
      <td>-1.140021</td>
      <td>6.814976</td>
      <td>-6.716311</td>
      <td>5.306338</td>
    </tr>
    <tr>
      <th>2000-01-22</th>
      <td>1.162872</td>
      <td>6.534765</td>
      <td>-6.110653</td>
      <td>5.233384</td>
    </tr>
    <tr>
      <th>2000-01-23</th>
      <td>1.760717</td>
      <td>5.714708</td>
      <td>-4.054118</td>
      <td>4.785703</td>
    </tr>
    <tr>
      <th>2000-01-24</th>
      <td>0.536450</td>
      <td>5.849652</td>
      <td>-3.765441</td>
      <td>3.989357</td>
    </tr>
    <tr>
      <th>2000-01-25</th>
      <td>0.506539</td>
      <td>6.692062</td>
      <td>-4.821839</td>
      <td>3.023168</td>
    </tr>
    <tr>
      <th>2000-01-26</th>
      <td>0.958889</td>
      <td>6.568955</td>
      <td>-4.259598</td>
      <td>2.421934</td>
    </tr>
    <tr>
      <th>2000-01-27</th>
      <td>-0.172696</td>
      <td>4.921587</td>
      <td>-4.413335</td>
      <td>2.314551</td>
    </tr>
    <tr>
      <th>2000-01-28</th>
      <td>0.165740</td>
      <td>5.134014</td>
      <td>-3.341849</td>
      <td>1.133864</td>
    </tr>
    <tr>
      <th>2000-01-29</th>
      <td>0.093579</td>
      <td>4.991880</td>
      <td>-4.020020</td>
      <td>2.081721</td>
    </tr>
    <tr>
      <th>2000-01-30</th>
      <td>0.424503</td>
      <td>4.328352</td>
      <td>-3.503704</td>
      <td>2.303425</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-08-28</th>
      <td>-9.441308</td>
      <td>-10.407354</td>
      <td>60.908649</td>
      <td>-3.372065</td>
    </tr>
    <tr>
      <th>2002-08-29</th>
      <td>-10.022290</td>
      <td>-10.300304</td>
      <td>59.022868</td>
      <td>-4.729307</td>
    </tr>
    <tr>
      <th>2002-08-30</th>
      <td>-10.771862</td>
      <td>-10.121161</td>
      <td>59.190720</td>
      <td>-4.776657</td>
    </tr>
    <tr>
      <th>2002-08-31</th>
      <td>-11.397452</td>
      <td>-10.721580</td>
      <td>59.955429</td>
      <td>-4.837409</td>
    </tr>
    <tr>
      <th>2002-09-01</th>
      <td>-12.606183</td>
      <td>-12.794658</td>
      <td>60.073882</td>
      <td>-6.897691</td>
    </tr>
    <tr>
      <th>2002-09-02</th>
      <td>-11.490124</td>
      <td>-12.763907</td>
      <td>60.835452</td>
      <td>-6.677909</td>
    </tr>
    <tr>
      <th>2002-09-03</th>
      <td>-11.985902</td>
      <td>-12.161442</td>
      <td>60.848448</td>
      <td>-6.248310</td>
    </tr>
    <tr>
      <th>2002-09-04</th>
      <td>-12.581613</td>
      <td>-11.248297</td>
      <td>60.504354</td>
      <td>-6.408271</td>
    </tr>
    <tr>
      <th>2002-09-05</th>
      <td>-13.733525</td>
      <td>-10.625722</td>
      <td>58.903688</td>
      <td>-5.788621</td>
    </tr>
    <tr>
      <th>2002-09-06</th>
      <td>-13.257015</td>
      <td>-10.091945</td>
      <td>58.625660</td>
      <td>-4.776391</td>
    </tr>
    <tr>
      <th>2002-09-07</th>
      <td>-12.855639</td>
      <td>-8.795421</td>
      <td>59.073399</td>
      <td>-4.017372</td>
    </tr>
    <tr>
      <th>2002-09-08</th>
      <td>-11.482862</td>
      <td>-9.402805</td>
      <td>58.042510</td>
      <td>-3.530595</td>
    </tr>
    <tr>
      <th>2002-09-09</th>
      <td>-10.850022</td>
      <td>-9.553852</td>
      <td>57.214538</td>
      <td>-4.053349</td>
    </tr>
    <tr>
      <th>2002-09-10</th>
      <td>-12.208049</td>
      <td>-9.259484</td>
      <td>58.237309</td>
      <td>-3.971102</td>
    </tr>
    <tr>
      <th>2002-09-11</th>
      <td>-12.401630</td>
      <td>-9.367988</td>
      <td>58.999006</td>
      <td>-3.615675</td>
    </tr>
    <tr>
      <th>2002-09-12</th>
      <td>-14.382630</td>
      <td>-7.615701</td>
      <td>61.633138</td>
      <td>-2.822245</td>
    </tr>
    <tr>
      <th>2002-09-13</th>
      <td>-14.385503</td>
      <td>-5.825456</td>
      <td>62.643005</td>
      <td>-2.631831</td>
    </tr>
    <tr>
      <th>2002-09-14</th>
      <td>-14.670608</td>
      <td>-6.534945</td>
      <td>63.046983</td>
      <td>-2.521697</td>
    </tr>
    <tr>
      <th>2002-09-15</th>
      <td>-15.424981</td>
      <td>-6.552120</td>
      <td>64.461886</td>
      <td>-3.493400</td>
    </tr>
    <tr>
      <th>2002-09-16</th>
      <td>-13.875303</td>
      <td>-7.511547</td>
      <td>64.741750</td>
      <td>-4.255253</td>
    </tr>
    <tr>
      <th>2002-09-17</th>
      <td>-13.574444</td>
      <td>-7.407093</td>
      <td>64.003745</td>
      <td>-3.096605</td>
    </tr>
    <tr>
      <th>2002-09-18</th>
      <td>-13.843896</td>
      <td>-7.287694</td>
      <td>64.860323</td>
      <td>-3.211695</td>
    </tr>
    <tr>
      <th>2002-09-19</th>
      <td>-13.444606</td>
      <td>-8.069938</td>
      <td>66.156664</td>
      <td>-3.679680</td>
    </tr>
    <tr>
      <th>2002-09-20</th>
      <td>-14.319578</td>
      <td>-6.771972</td>
      <td>64.871045</td>
      <td>-4.633304</td>
    </tr>
    <tr>
      <th>2002-09-21</th>
      <td>-15.126463</td>
      <td>-7.993281</td>
      <td>65.080881</td>
      <td>-3.497950</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>-14.717619</td>
      <td>-8.359075</td>
      <td>65.765170</td>
      <td>-5.577461</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>-13.763743</td>
      <td>-8.046417</td>
      <td>66.821624</td>
      <td>-5.256422</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>-15.111257</td>
      <td>-5.814779</td>
      <td>66.104899</td>
      <td>-6.185853</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>-14.890142</td>
      <td>-5.402545</td>
      <td>65.420458</td>
      <td>-5.578971</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>-14.917314</td>
      <td>-5.732310</td>
      <td>63.944766</td>
      <td>-6.181776</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>



### Excel
[MS Excel](https://pandas.pydata.org/pandas-docs/stable/io.html#io-excel)에 읽고 씁니다. 

엑셀 파일에 씁니다. 



```python
df.to_excel('foo.xlsx', sheet_name='Sheet1')
```

엑셀 파일을 읽어옵니다.


```python
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-1.170941</td>
      <td>0.688051</td>
      <td>-0.383810</td>
      <td>0.837035</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>-1.325416</td>
      <td>0.061442</td>
      <td>-1.080497</td>
      <td>0.281412</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>-0.687276</td>
      <td>0.916830</td>
      <td>-2.839985</td>
      <td>1.852432</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>-1.288728</td>
      <td>-0.242376</td>
      <td>-3.791390</td>
      <td>1.309750</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>-0.937522</td>
      <td>-0.779122</td>
      <td>-5.202554</td>
      <td>2.219908</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>-2.136242</td>
      <td>-0.693236</td>
      <td>-6.256821</td>
      <td>3.015780</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-1.412520</td>
      <td>-2.517668</td>
      <td>-5.712015</td>
      <td>3.805923</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-0.049283</td>
      <td>-1.716615</td>
      <td>-7.405345</td>
      <td>4.770589</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>0.592184</td>
      <td>-0.617583</td>
      <td>-7.339519</td>
      <td>3.694828</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>1.378037</td>
      <td>0.110647</td>
      <td>-5.297688</td>
      <td>3.467191</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>2.474387</td>
      <td>-0.083230</td>
      <td>-4.153509</td>
      <td>3.091714</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>1.621882</td>
      <td>0.016834</td>
      <td>-7.112481</td>
      <td>1.237205</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>1.246822</td>
      <td>-1.368471</td>
      <td>-5.531885</td>
      <td>0.338128</td>
    </tr>
    <tr>
      <th>2000-01-14</th>
      <td>1.978975</td>
      <td>-0.527194</td>
      <td>-5.112244</td>
      <td>1.466986</td>
    </tr>
    <tr>
      <th>2000-01-15</th>
      <td>1.450342</td>
      <td>0.450082</td>
      <td>-4.731543</td>
      <td>3.673504</td>
    </tr>
    <tr>
      <th>2000-01-16</th>
      <td>1.948955</td>
      <td>1.059912</td>
      <td>-6.297084</td>
      <td>4.191426</td>
    </tr>
    <tr>
      <th>2000-01-17</th>
      <td>2.035009</td>
      <td>2.273572</td>
      <td>-6.637326</td>
      <td>3.746256</td>
    </tr>
    <tr>
      <th>2000-01-18</th>
      <td>1.550255</td>
      <td>3.503449</td>
      <td>-6.578056</td>
      <td>4.099211</td>
    </tr>
    <tr>
      <th>2000-01-19</th>
      <td>1.864008</td>
      <td>4.212954</td>
      <td>-7.183693</td>
      <td>2.888867</td>
    </tr>
    <tr>
      <th>2000-01-20</th>
      <td>-0.075277</td>
      <td>5.007933</td>
      <td>-7.093309</td>
      <td>4.735946</td>
    </tr>
    <tr>
      <th>2000-01-21</th>
      <td>-1.140021</td>
      <td>6.814976</td>
      <td>-6.716311</td>
      <td>5.306338</td>
    </tr>
    <tr>
      <th>2000-01-22</th>
      <td>1.162872</td>
      <td>6.534765</td>
      <td>-6.110653</td>
      <td>5.233384</td>
    </tr>
    <tr>
      <th>2000-01-23</th>
      <td>1.760717</td>
      <td>5.714708</td>
      <td>-4.054118</td>
      <td>4.785703</td>
    </tr>
    <tr>
      <th>2000-01-24</th>
      <td>0.536450</td>
      <td>5.849652</td>
      <td>-3.765441</td>
      <td>3.989357</td>
    </tr>
    <tr>
      <th>2000-01-25</th>
      <td>0.506539</td>
      <td>6.692062</td>
      <td>-4.821839</td>
      <td>3.023168</td>
    </tr>
    <tr>
      <th>2000-01-26</th>
      <td>0.958889</td>
      <td>6.568955</td>
      <td>-4.259598</td>
      <td>2.421934</td>
    </tr>
    <tr>
      <th>2000-01-27</th>
      <td>-0.172696</td>
      <td>4.921587</td>
      <td>-4.413335</td>
      <td>2.314551</td>
    </tr>
    <tr>
      <th>2000-01-28</th>
      <td>0.165740</td>
      <td>5.134014</td>
      <td>-3.341849</td>
      <td>1.133864</td>
    </tr>
    <tr>
      <th>2000-01-29</th>
      <td>0.093579</td>
      <td>4.991880</td>
      <td>-4.020020</td>
      <td>2.081721</td>
    </tr>
    <tr>
      <th>2000-01-30</th>
      <td>0.424503</td>
      <td>4.328352</td>
      <td>-3.503704</td>
      <td>2.303425</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-08-28</th>
      <td>-9.441308</td>
      <td>-10.407354</td>
      <td>60.908649</td>
      <td>-3.372065</td>
    </tr>
    <tr>
      <th>2002-08-29</th>
      <td>-10.022290</td>
      <td>-10.300304</td>
      <td>59.022868</td>
      <td>-4.729307</td>
    </tr>
    <tr>
      <th>2002-08-30</th>
      <td>-10.771862</td>
      <td>-10.121161</td>
      <td>59.190720</td>
      <td>-4.776657</td>
    </tr>
    <tr>
      <th>2002-08-31</th>
      <td>-11.397452</td>
      <td>-10.721580</td>
      <td>59.955429</td>
      <td>-4.837409</td>
    </tr>
    <tr>
      <th>2002-09-01</th>
      <td>-12.606183</td>
      <td>-12.794658</td>
      <td>60.073882</td>
      <td>-6.897691</td>
    </tr>
    <tr>
      <th>2002-09-02</th>
      <td>-11.490124</td>
      <td>-12.763907</td>
      <td>60.835452</td>
      <td>-6.677909</td>
    </tr>
    <tr>
      <th>2002-09-03</th>
      <td>-11.985902</td>
      <td>-12.161442</td>
      <td>60.848448</td>
      <td>-6.248310</td>
    </tr>
    <tr>
      <th>2002-09-04</th>
      <td>-12.581613</td>
      <td>-11.248297</td>
      <td>60.504354</td>
      <td>-6.408271</td>
    </tr>
    <tr>
      <th>2002-09-05</th>
      <td>-13.733525</td>
      <td>-10.625722</td>
      <td>58.903688</td>
      <td>-5.788621</td>
    </tr>
    <tr>
      <th>2002-09-06</th>
      <td>-13.257015</td>
      <td>-10.091945</td>
      <td>58.625660</td>
      <td>-4.776391</td>
    </tr>
    <tr>
      <th>2002-09-07</th>
      <td>-12.855639</td>
      <td>-8.795421</td>
      <td>59.073399</td>
      <td>-4.017372</td>
    </tr>
    <tr>
      <th>2002-09-08</th>
      <td>-11.482862</td>
      <td>-9.402805</td>
      <td>58.042510</td>
      <td>-3.530595</td>
    </tr>
    <tr>
      <th>2002-09-09</th>
      <td>-10.850022</td>
      <td>-9.553852</td>
      <td>57.214538</td>
      <td>-4.053349</td>
    </tr>
    <tr>
      <th>2002-09-10</th>
      <td>-12.208049</td>
      <td>-9.259484</td>
      <td>58.237309</td>
      <td>-3.971102</td>
    </tr>
    <tr>
      <th>2002-09-11</th>
      <td>-12.401630</td>
      <td>-9.367988</td>
      <td>58.999006</td>
      <td>-3.615675</td>
    </tr>
    <tr>
      <th>2002-09-12</th>
      <td>-14.382630</td>
      <td>-7.615701</td>
      <td>61.633138</td>
      <td>-2.822245</td>
    </tr>
    <tr>
      <th>2002-09-13</th>
      <td>-14.385503</td>
      <td>-5.825456</td>
      <td>62.643005</td>
      <td>-2.631831</td>
    </tr>
    <tr>
      <th>2002-09-14</th>
      <td>-14.670608</td>
      <td>-6.534945</td>
      <td>63.046983</td>
      <td>-2.521697</td>
    </tr>
    <tr>
      <th>2002-09-15</th>
      <td>-15.424981</td>
      <td>-6.552120</td>
      <td>64.461886</td>
      <td>-3.493400</td>
    </tr>
    <tr>
      <th>2002-09-16</th>
      <td>-13.875303</td>
      <td>-7.511547</td>
      <td>64.741750</td>
      <td>-4.255253</td>
    </tr>
    <tr>
      <th>2002-09-17</th>
      <td>-13.574444</td>
      <td>-7.407093</td>
      <td>64.003745</td>
      <td>-3.096605</td>
    </tr>
    <tr>
      <th>2002-09-18</th>
      <td>-13.843896</td>
      <td>-7.287694</td>
      <td>64.860323</td>
      <td>-3.211695</td>
    </tr>
    <tr>
      <th>2002-09-19</th>
      <td>-13.444606</td>
      <td>-8.069938</td>
      <td>66.156664</td>
      <td>-3.679680</td>
    </tr>
    <tr>
      <th>2002-09-20</th>
      <td>-14.319578</td>
      <td>-6.771972</td>
      <td>64.871045</td>
      <td>-4.633304</td>
    </tr>
    <tr>
      <th>2002-09-21</th>
      <td>-15.126463</td>
      <td>-7.993281</td>
      <td>65.080881</td>
      <td>-3.497950</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>-14.717619</td>
      <td>-8.359075</td>
      <td>65.765170</td>
      <td>-5.577461</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>-13.763743</td>
      <td>-8.046417</td>
      <td>66.821624</td>
      <td>-5.256422</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>-15.111257</td>
      <td>-5.814779</td>
      <td>66.104899</td>
      <td>-6.185853</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>-14.890142</td>
      <td>-5.402545</td>
      <td>65.420458</td>
      <td>-5.578971</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>-14.917314</td>
      <td>-5.732310</td>
      <td>63.944766</td>
      <td>-6.181776</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>



## Gotchas (잡았다!)

연산을 수행하기 위해 시도하면 다음과 같은 예외 상황을 볼 수도 있습니다.


```python
if pd.Series([False, True, False]):
    print("I was true")
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-153-9cae3ab0f79f> in <module>()
    ----> 1 if pd.Series([False, True, False]):
          2     print("I was true")
    

    C:\Users\Admin\Anaconda3\lib\site-packages\pandas\core\generic.py in __nonzero__(self)
        951         raise ValueError("The truth value of a {0} is ambiguous. "
        952                          "Use a.empty, a.bool(), a.item(), a.any() or a.all()."
    --> 953                          .format(self.__class__.__name__))
        954 
        955     __bool__ = __nonzero__
    

    ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().


이러한 경우에는, any(), all() or empty 등을 사용해서 무엇을 원하는지를 선택(반영)해주어야 합니다.


```python
if pd.Series([False, True, False])is not None:
      print("I was not None")
```

설명과 무엇을 해야하는지에 대해서는 [비교](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-compare) 부분을 참조하세요.

[Gotchas](https://pandas.pydata.org/pandas-docs/stable/gotchas.html#gotchas) 부분도 참조하세요.
