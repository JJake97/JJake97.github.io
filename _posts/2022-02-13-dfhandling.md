## DataFrame 다루기

### DataFrame indexing 문법

#### 이름으로 인덱싱
- 하나의 row 이름: df.loc["row_name"]

- row 이름의 리스트: df.loc[["row_name1", "row_name2", "row_name3"]]

- row 이름의 리스트 슬라이싱: df.loc['row_name2' : 'row_name3']

- 하나의 column 이름: df.loc[:, 'col_name1']

- column 이름의 리스트: df.loc[:, ['col_name2', 'col_name3', 'col_name4']

- column 이름의 리스트 인덱싱: df.loc[:, 'col_name5' : 'col_name6']

#### 위치로 인덱싱

- 하나의 row 위치: df.iloc[8]

- row 위치의 리스트: df.iloc[[4, 5, 3]]

- row 위치의 리스트 슬라이싱: df.iloc[2:5]

- 하나의 column 위치: df.iloc[:, 3]

- column 위치의 리스트: df.iloc[:, [3, 5, 6]]

- column 위치의 리스트 슬라이싱: df.iloc[:, [3:7]]

### 데이터 변형하기

- 데이터프레임에 값을 추가&제거하거나 없는 column을 생성해줄 수 있다

#### 조건에 따른 데이터 변형

- df.loc[조건1 & 조건2, 변경할 column] = 변경할 데이터 값


```python

```
