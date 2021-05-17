# Pandas_Series_處理單維度資料

實作日期 2021/05/16 ~ 2021/05/17

參考資料:[Pandas教學]資料分析必懂的 Pandas Series 處理單維度資料方法  
<https://www.learncodewithmike.com/2020/10/python-pandas-series-tutorial.html>

Google Colab 內建已有 pandas 套件，所以不用 pip install(安裝)  
pandas 套件，是一種常用的資料分析處理工具  
類似 Excel，能夠將儲存的 Data 進行統計、搜尋或修改等操作  
主要有兩種 data structure，分別是 Series 及 DataFrame   

Pandas Series 適用於處理 單維度 or 單一 column(直欄)的 Data  

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

## 實作9-1 _搜尋是否包含 自己預設 的特定 String
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

print(smartphone1.str.contains("Ap"))  
# 搜尋是否包含 自己預設 的特定 String
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

## 實作9-2 _搜尋是否包含 User input 的特定 String
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

User_input = input("請輸入關鍵字:")

print(smartphone1.str.contains(User_input))  
# 搜尋是否包含 User input 的特定 String
# 左側 is Data index(索引值)
# 右側 is Data boolean values(True or False)
# Data type is bool(布林[邏輯資料型別])
```


## 執行結果
```
請輸入關鍵字:AS
Num.1     True
Num.2    False
Num.3    False
Num.4    False
dtype: bool
```

## 實作10_運用 cat(sep="、") method_自訂用來 連接 Data 中的每個項目的符號
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

print(smartphone1.str.cat(sep="、"))  
# 運用自訂的 頓號 連接 Data 中的每個項目
```

## 執行結果
```
ASUS、Apple、Sony、HTC
```


## 實作11_運用 replace method 取代為 指定的 Data
```python
import pandas as pd
 
smartphone1 = pd.Series(["ASUS", "Apple", "Sony", "HTC"], 
            index=["Num.1", "Num.2", "Num.3", "Num.4"])

print(smartphone1.str.replace("Sony", "OPPO"))  
# 將 Sony 取代為 OPPO
```

## 執行結果
```
Num.1     ASUS
Num.2    Apple
Num.3     OPPO
Num.4      HTC
dtype: object
```


## 實作12_數值運算
```python
import pandas as pd
 
numbers = pd.Series([10, 25, 35, 5, 77, 55])

print("最大值:")
print(numbers.max())  
# 運用 m() method 列印出物件 numbers Data 中的最大值

print("------------------------")

print("最小值:")
print(numbers.min())
# 運用 min() method 列印出物件 numbers Data 中的最小值

print("------------------------")

print("總和=")
print(numbers.sum())
# 運用 sum() method 列印出物件 numbers Data 的總和

print("------------------------")

print("平均值=")
print(numbers.mean()) 
# 運用 mean() method 列印出物件 numbers Data 的平均值

print("------------------------")

print("物件 numbers Data 中最大的2個數值:")
print(numbers.nlargest(2))  
# nlargest 讀法是 n  largest : 找出 n 個最大值
# 列印出物件 numbers Data 中最大的2個數值
# 左側 is index
# 右側 is value
# Data type:int(整數)

print("------------------------")

print("物件 numbers Data 中最小的3個數值:")
print(numbers.nsmallest(3))  
# nlargest 讀法是 n smallest: 找出 n 個最小值
# 列印出物件 numbers Data 中最小的3個數值
# 左側 is index
# 右側 is value
# Data type:int(整數)
```

## 執行結果
```
最大值:
77
------------------------
最小值:
5
------------------------
總和=
207
------------------------
平均值=
34.5
------------------------
物件 numbers Data 中最大的2個數值:
4    77
5    55
dtype: int64
------------------------
物件 numbers Data 中最小的3個數值:
3     5
0    10
1    25
dtype: int64
```
