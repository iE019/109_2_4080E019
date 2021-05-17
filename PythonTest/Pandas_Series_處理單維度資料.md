# Pandas_Series_處理單維度資料

實作日期 2021/05/16 ~ 2021/05/17

參考資料:[Pandas教學]資料分析必懂的 Pandas Series 處理單維度資料方法  
<https://www.learncodewithmike.com/2020/10/python-pandas-series-tutorial.html>

Google Colab 內建已有 pandas 套件，所以不用 pip install(安裝)  
pandas 套件，是一種常用的資料分析處理工具  
類似 Excel，能夠將儲存的 Data 進行統計、搜尋或修改等操作  
主要有兩種 data structure，分別是 Series 及 DataFrame   

Pandas Series 適用於處理單維度或單一 column(直欄)的 Data  

## 實作1
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

## 實作2
```python

```

## 執行結果
```

```

## 實作3
```python

```

## 執行結果
```

```

## 實作4
```python

```

## 執行結果
```

```

## 實作5
```python

```


## 執行結果
```

```

## 實作6
```python

```

## 實作7
```python

```


## 執行結果
```

```
