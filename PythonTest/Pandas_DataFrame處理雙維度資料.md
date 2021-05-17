# Pandas_DataFrame 處理雙維度資料

實作日期 2021/05/16 ~ 2021/5/17

參考資料:[Pandas教學]資料分析必懂的Pandas DataFrame處理雙維度資料方法
<https://www.learncodewithmike.com/2020/11/python-pandas-dataframe-tutorial.html>

目前進度: 第7大點

Google Colab 內建已有 pandas 套件所以不用 pip install (安裝)
pandas 套件，是一種常用的資料分析處理工具
類似 Excel，能夠將儲存的 Data 進行統計、搜尋或修改等操作
主要有兩種資料結構，分別是 Series 及 DataFrame

DataFrame 主要用來處理 雙維度的 Data
也就是具有 row(橫列)與 column(直欄)的 Table(表格)式資料集
所以，經常應用於讀取CSV檔案、網頁表格或資料庫等，來進行其中的資料分析或處理


## 實作1_基本認識DataFrame
```python
import pandas as pd
# 匯入 pandas 套件，並且簡稱為 pd
 
grades1 = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades1
# Dictionaries 是使用大括號括起來，並具有 Key(鍵) And Value(值)
# 每一組 key: [value1,value2...] 代表一直欄的 Data
# 以一直欄又一直欄的方式儲存 Data
 
df = pd.DataFrame(grades1)
# df 是 dataframe 的簡寫
# DataFrame method 內，參數放入 Dictionaries 的 Data
  
print("使用 Dictionaries 來建立 df：")
print(df)
# 左側 is index(索引值)
# 上方 Key is Pandas DataFrame 的 column Name
# 右側 Value is column Data
 
print("-------------------------")
# 分隔線
 

grades2 = [
    ["Peter", 80, 63],
    ["Mary", 75, 90],
    ["Mark", 93, 85],
    ["John", 86, 70]
]
# 建立 an Array(陣列) 並命名為 grades2
# 每組中括號的 Data 代表 一橫列 Data
 
df2 = pd.DataFrame(grades2)
# DataFrame method 內，參數放入 Array 的 Data
 
print("使用 Array 來建立 df：")
print(df2)
# 左側 And 上方 is index
# 右側 is column Data
```

## 執行結果
```
使用 Dictionaries 來建立 df：
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
-------------------------
使用 Array 來建立 df：
       0   1   2
0  Peter  80  63
1   Mary  75  90
2   Mark  93  85
3   John  86  70
```

## 實作2_自訂 index Name And column Name
```python
import pandas as pd
 
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# 每一組 key: [value1,value2...] 代表一直欄的 Data

 
df = pd.DataFrame(grades)
# 使用 pandas 套件呼叫 DataFrame method ，參數放入 Dictionaries 的 Data
# 並指定給物件 df

df.index = ["s1", "s2", "s3", "s4"]  
# 自訂 index Name

df.columns = ["student_name", "math_score", "chinese_score"]  
# 自訂 column Name

print(df)
# 左側 is index Name
# 上方 is column Name
# 右側 is column Data
```

## 執行結果
```
 student_name  math_score  chinese_score
s1        Peter          80             63
s2         Mary          75             90
s3         Mark          93             85
s4         John          86             70
```

## 實作3_head() 、tail() method 的運用
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# 每一組 key: [value1,value2...] 代表一直欄的 Data
 
df = pd.DataFrame(grades)
print("原來的df")
print(df)
 
print("-------------------------------------")
 
df2 = df.head(2)
print("取得最前面的兩筆資料")
print(df2)

print("------------------------------------")
 
df3 = df.tail(3)
print("取得最後面的三筆資料")
print(df3)
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
-------------------------------------
取得最前面的兩筆資料
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
------------------------------------
取得最後面的三筆資料
   name  math  chinese
1  Mary    75       90
2  Mark    93       85
3  John    86       70
```

## 實作4_在中括號中指定"column Name" or "Data index"，來取得所需的 資料集
```python
import pandas as pd
 
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
 
df = pd.DataFrame(grades)
 
print("取得單一欄位資料(type is Series)")
print(df["name"])
# 使用一個中括號，不會顯示 column Name
 
print("------------------------------------")
 
print("取得單一欄位資料(type is DataFrame)")
print(df[["name"]])
# 使用兩個中括號，會顯示有 column Name
 
print("------------------------------------")
 
print("取得多欄位資料(type is DataFrame)")
print(df[["name", "chinese"]])
 
print("------------------------------------")
 
print("取得索引值0~2的資料")
print(df[0:3])
```

## 執行結果
```
取得單一欄位資料(type is Series)
0    Peter
1     Mary
2     Mark
3     John
Name: name, dtype: object
------------------------------------
取得單一欄位資料(type is DataFrame)
    name
0  Peter
1   Mary
2   Mark
3   John
------------------------------------
取得多欄位資料(type is DataFrame)
    name  chinese
0  Peter       63
1   Mary       90
2   Mark       85
3   John       70
------------------------------------
取得索引值0~2的資料
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
```

## 實作5_ at() 、iat()、loc()、iloc() method 的運用
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# key:["value1","value2"...]
# key is column Name
# value is column Data 

df = pd.DataFrame(grades)
# 將 Dictionaries grades Data 指定給物件 df
 
print("原來的df")
print(df)
 
print("------------------------------------")
 
print("運用 at() method 取得 index  is 1 的 math column Data")
print(df.at[1, "math"])
# 運用 Data indaex And column Name 來取得 單一值
print("------------------------------------")

print("運用 at() method 取得 index is 2 的 chinese column Data")
print(df.at[2, "chinese"])
print("------------------------------------")

print("運用 iat() method 取得 第1列第2欄(從第0列0欄開始) 的 Data")
print(df.iat[1, 2])
# 運用 Data indaex And column順序 來取得 單一值
print("------------------------------------")

print("運用 iat() method 取得 第2列第1欄 的 Data")
print(df.iat[2, 1])
print("------------------------------------")

print("取得 Data index is 1 And 3 的 name And chinese column 資料集")
print(df.loc[[1, 3], ["name", "chinese"]])
# 運用 Data indaex And column Name 來取得 資料集
print("------------------------------------")

print("取得 Data index is 1 And 3 的第一個及第三個欄位資料集")
print(df.iloc[[1, 3], [0, 2]])
# 運用 Data indaex And column順序 來取得 資料集
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
------------------------------------
運用 at() method 取得 index  is 1 的 math column Data
75
------------------------------------
運用 at() method 取得 index is 2 的 chinese column Data
85
------------------------------------
運用 iat() method 取得 第1列第2欄(從第0列0欄開始) 的 Data
90
------------------------------------
運用 iat() method 取得 第2列第1欄 的 Data
93
------------------------------------
取得 Data index is 1 And 3 的 name And chinese column 資料集
   name  chinese
1  Mary       90
3  John       70
------------------------------------
取得 Data index is 1 And 3 的第一個及第三個欄位資料集
   name  chinese
1  Mary       90
3  John       70
```

## 實作6_運用 insert()  新增 Data
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# key:["value1","value2"...]
# key is column Name
# value is column Data 

df = pd.DataFrame(grades)
# 將 Dictionaries grades Data 指定給物件 df
 
print("原來的df")
print(df)
 
print("------------------------------------")

df.insert(2, column="Engilsh", value=[88, 72, 74, 98])
print("在第2欄的位置新增一個 column Data")
print(df)

print("------------------------------------")

new_df = df.append({
    "name": "Henry",
    "math": 60,
    "chinese": 62
}, ignore_index=True)
# ignore_index=True 代表是接續之前的 index
# if 沒有加 ignore_index=True，新橫列 Data 的 index 會又從0開始
 
print("新增一筆資料")
print(new_df)
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
------------------------------------
在第2欄的位置新增一個 column Data
    name  math  Engilsh  chinese
0  Peter    80       88       63
1   Mary    75       72       90
2   Mark    93       74       85
3   John    86       98       70
------------------------------------
新增一筆資料
    name  math  Engilsh  chinese
0  Peter    80     88.0       63
1   Mary    75     72.0       90
2   Mark    93     74.0       85
3   John    86     98.0       70
4  Henry    60      NaN       62
```

## 實作7_合併 df 來新增 Data
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# key:["value1","value2"...]
# key is column Name
# value is column Data 

df1 = pd.DataFrame(grades)
# 將 Dictionaries grades Data 指定給物件 df
 
print("原來的df")
print(df1)
 
print("------------------------------------")

df2 = pd.DataFrame({
    "name": ["Henry"],
    "math": [60],
    "chinese": [62]
})
 
new_df = pd.concat([df1, df2], ignore_index=True)
print("合併df來新增資料")
print(new_df)
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
------------------------------------
合併df來新增資料
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
4  Henry    60       62
```

## 實作8_修改 Data
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# key:["value1","value2"...]
# key is column Name
# value is column Data 

df = pd.DataFrame(grades)
# 將 Dictionaries grades Data 指定給物件 df
 
print("原來的df")
print(df)
 
print("------------------------------------")
df.at[1, "math"] = 100  #修改 index is 1 的 math column Data
df.iat[1, 0] = "Lily"  #修改 第1列0欄(從第0列第0欄開始) 的 column Data
print("修改後的df")
print(df)
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
------------------------------------
修改後的df
    name  math  chinese
0  Peter    80       63
1   Lily   100       90
2   Mark    93       85
3   John    86       70
```

## 實作9_ 刪除 Data
```python
import pandas as pd
 
grades = {
    "name": ["Peter", "Mary", "Mark", "John"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
# 建立 a Dictionaries(字典) 並命名為 grades
# key:["value1","value2"...]
# key is column Name
# value is column Data 

df = pd.DataFrame(grades)
# 將 Dictionaries grades Data 指定給物件 df
 
print("原來的df")
print(df)
 
print("------------------------------------")

df2 = df.drop(["math"], axis=1)
# drop(column Name, axis=1)：
# 刪除指定column Name 的 column，並且會回傳一個新的Pandas DataFrame資料集
print("刪除math欄位")
print(df2)

print("------------------------------------")

df3 = df.drop([0, 3], axis=0)  # 刪除 index is 0 And 3 的 Data
print("刪除第一筆及第四筆資料")
print(df3)
```

## 執行結果
```
原來的df
    name  math  chinese
0  Peter    80       63
1   Mary    75       90
2   Mark    93       85
3   John    86       70
------------------------------------
刪除math欄位
    name  chinese
0  Peter       63
1   Mary       90
2   Mark       85
3   John       70
------------------------------------
刪除第一筆及第四筆資料
   name  math  chinese
1  Mary    75       90
2  Mark    93       85
```

## 實作10_刪除空值
```python
import pandas as pd
import numpy as np
 
 
grades = {
    "name": ["Peter", "Mary", np.NaN, "John"],
    "city": ["Taipei", np.NaN, "Kaohsiung", "Taichung"],
    "math": [80, 75, 93, 86],
    "chinese": [63, 90, 85, 70]
}
 
df = pd.DataFrame(grades)
print("原來的df")
print(df)
 
print("------------------------------------")
 
new_df = df.dropna()
print("刪除空值後的df")
print(new_df)
```

## 執行結果
```
原來的df
     name       city  math  chinese
0    Mike     Taipei    80       63
1  Sherry        NaN    75       90
2     NaN  Kaohsiung    93       85
3    John   Taichung    86       70
======================================
刪除空值後的df
   name      city  math  chinese
0  Mike    Taipei    80       63
3  John  Taichung    86       70
```

## 實作11_刪除重複值
```python
import pandas as pd
 
 
grades = {
    "name": ["Peter", "Peter", "Mary", "John"],
    "city": ["Taipei", "Taipei", "Kaohsiung", "Taichung"],
    "math": [80, 80, 93, 86],
    "chinese": [80, 80, 93, 86]
}
 
df = pd.DataFrame(grades)
print("原來的df")
print(df)
 
print("------------------------------------")
 
new_df = df.drop_duplicates()
print("刪除重複值後的df")
print(new_df)
```

## 執行結果
```
原來的df
    name       city  math  chinese
0  Peter     Taipei    80       80
1  Peter     Taipei    80       80
2   Mary  Kaohsiung    93       93
3   John   Taichung    86       86
------------------------------------
刪除重複值後的df
    name       city  math  chinese
0  Peter     Taipei    80       80
2   Mary  Kaohsiung    93       93
3   John   Taichung    86       86
```

## 實作12
```python

```

## 執行結果
```

```



