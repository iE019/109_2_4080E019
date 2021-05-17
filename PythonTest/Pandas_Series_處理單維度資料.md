# Pandas_Series_處理單維度資料

實作日期 2021/05/16 ~ 2021/05/17

參考資料:[Pandas教學]資料分析必懂的 Pandas Series 處理單維度資料方法  
<https://www.learncodewithmike.com/2020/10/python-pandas-series-tutorial.html>

Google Colab 內建已有 pandas 套件，所以不用 pip install(安裝)  
pandas 套件，是一種常用的資料分析處理工具  
類似 Excel，能夠將儲存的 Data 進行統計、搜尋或修改等操作  
主要有兩種 data structure，分別是 Series 及 DataFrame   

Pandas Series 適用於處理單維度或單一 column(直欄)的 Data  

## 實作1_基本認識 Series
```python
import pandas as pd
# 匯入 pandas 套件，並且簡稱為 pa

smartphone = pd.Series(["ASUS", "Apple", "Sony", "HTC"])
# 建立物件 smartphone
# 使用 pandas 套件呼叫 Series method
# 參數 is List(串列)
# List is 使用中括號在單個變數中儲存多個項目
# 並且是可變的，這意味著創建 List 後，可以更改、添加和刪除 List 中的項目

print(smartphone)
# 將物件 smartphone 的 Data 以 Pandas Series 的格式列印出來
# 左側 is Data index(索引值)(預設從 0 開始)
# 右側 is Data content(內容)
# Data type is object(物件)
```

## 執行結果
```
0     ASUS
1    Apple
2     Sony
3      HTC
dtype: object
```

## 實作2_自訂 Data index Name
```python
import pandas as pd
 
smartphone = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
# 自訂 Data index Name

print(smartphone)
```

## 執行結果
```
Num.1     ASUS
Num.2    Apple
Num.3     Sony
Num.4      HTC
dtype: object

```

## 實作3_依據 Data index or index Name 取值
```python
import pandas as pd
 
smartphone = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
print(smartphone[1])  # 依據 Data index 取值(從0開始計算)
print(smartphone["Num.3"])  # 依據 Data index name 取值
```

## 執行結果
```
Apple
Sony
```

## 實作 4-1 _新增 Data_新增的 Data index 會又從 0 開始
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"])
smartphone2 = pd.Series(["OPPO","小米"])  # 新增的 Data
result = smartphone1.append(smartphone2)
# 物件 smartphone2 的 Data 加入到 物件 smartphone1 的尾端
# 並指定給物件 result
# 新增的 Data index 會又從0開始

print(result)
# 將物件 result 的所有 Data 以 Pandas Series 的格式列印出來
```

## 執行結果
```
0     ASUS
1    Apple
2     Sony
3      HTC
0     OPPO
1       小米
dtype: object
```

## 實作 4-2 _新增 Data_加入 ignore_index=True 指令，使新增的 Data index 會接續前1個的 index
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"])
smartphone2 = pd.Series(["OPPO","小米"])  # 新增的 Data
result = smartphone1.append(smartphone2, ignore_index=True)
# 物件 smartphone2 的 Data 加入到 物件 smartphone1 的尾端
# 並指定給物件 result
# 新增的 Data index 會 接續

print(result)
# 將物件 result 的所有 Data 以 Pandas Series 的格式列印出來
```


## 執行結果
```
0     ASUS
1    Apple
2     Sony
3      HTC
4     OPPO
5       小米
dtype: object
```

## 實作 4-3 _新增 Data_index Name 全用自訂的
```python
import pandas as pd
 
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
smartphone2 = pd.Series(["OPPO","小米"],
          index=["Num.5","Num.6"])  # 新增的 Data
result = smartphone1.append(smartphone2)
# 物件 smartphone2 的 Data 加入到 物件 smartphone1 的尾端
# 並指定給物件 result

print(result)
# 將物件 result 的所有 Data 以 Pandas Series 的格式列印出來
```


## 執行結果
```
Num.1     ASUS
Num.2    Apple
Num.3     Sony
Num.4      HTC
Num.5     OPPO
Num.6       小米
dtype: object
```


## 實作 5-1 _運用 index Name 修改 物件內 List 的 Data
```python
import pandas as pd

smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
smartphone1["Num.4"] = "OPPO"
# 運用 index Name 修改 物件內 List 的 Data

print(smartphone1)
```


## 執行結果
```
Num.1     ASUS
Num.2    Apple
Num.3     Sony
Num.4     OPPO
dtype: object

```

## 實作 5-2 _運用 index 修改 物件內 List 的 Data
```python
import pandas as pd
# 匯入 pandas 套件，並且簡稱為 pa

smartphone = pd.Series(["ASUS", "Apple", "Sony", "HTC"])

smartphone[2] = "OPPO"
# 運用 index 修改 物件內 List 的 Data

print(smartphone)

```

## 執行結果
```
0     ASUS
1    Apple
2     OPPO
3      HTC
dtype: object
```

## 實作6_計算共有多少筆項目
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
print("Data 筆數共有:")
print(smartphone1.size)  
# 計算共有多少筆項目
```


## 執行結果
```
Data 筆數共有:
4
```


## 實作7_將 String Data 都轉換為大寫字母
```python
import pandas as pd
 
smartphone1 = pd.Series(["asus", "apple", "sony", "htc"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

print(smartphone1.str.upper())  
# 將 String Data 都轉換為大寫字母
```


## 執行結果
```
Num.1     ASUS
Num.2    APPLE
Num.3     SONY
Num.4      HTC
dtype: object
```

## 實作8_將String Data 都轉換為小寫字母
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

print(smartphone1.str.lower())  
# 將String Data 都轉換為小寫字母
```


## 執行結果
```
Num.1     asus
Num.2    apple
Num.3     sony
Num.4      htc
dtype: object
```

## 實作9-1 _搜尋是否包含特定字串(固定版)
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])
            
print(smartphone1.str.contains("Ap"))  # 搜尋是否包含特定字串
# 左側 is Data index(索引值)
# 右側 is Data boolean values(True or False)
# Data type is bool(布林[邏輯資料型別])
```


## 執行結果
```
Num.1    False
Num.2     True
Num.3    False
Num.4    False
dtype: bool
```

## 實作9-2 _搜尋是否包含特定字串(使用者輸入版)
```python

```


## 執行結果
```

```
