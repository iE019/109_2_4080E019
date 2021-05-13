## 實作1
```python
import pandas as pd # 引用套件並縮寫為 pd

groups = ["Modern Web", "DevOps", "Cloud", "Big Data", "Security"]
men_number = [46, 8, 12, 12, 6]

men_number_dict = {"組別": groups,
                   "人數": men_number
}

men_number_df = pd.DataFrame(men_number_dict)

print(men_number_df) # 看看資料框的外觀

# 參考資料
# https://ithelp.ithome.com.tw/articles/10185182

```
## 實作1_執行結果
```
           組別  人數
0  Modern Web  46
1      DevOps   8
2       Cloud  12
3    Big Data  12
4    Security   6
```
## 實作1-2
```python
import pandas as pd

groups = ["Modern Web", "DevOps", "Cloud", "Big Data", "Security"]
ironmen = [46, 8, 12, 12, 6]

ironmen_dict = {"groups": groups,
                "men": ironmen
}

ironmen_df = pd.DataFrame(ironmen_dict)

print(ironmen_df[ironmen_df.loc[:,"men"] > 10]) # 選出人數超過 10 的 data frame

```

## 實作1-2_執行結果
```
       groups  men
0  Modern Web   46
2       Cloud   12
3    Big Data   12
```

## 實作2
```python
import pandas as pd
scores = [{"姓名":"小華", "數學":90, "國文":80},
      {"姓名":"小明", "數學":70, "國文":55},
      {"姓名":"小李", "數學":45, "國文":75}]
score_df = pd.DataFrame(scores)
print(score_df)

scores = {"姓名":["小華","小明","小李"],
      "國文":[80,55,75],
      "數學":[90,70,45]}
score_df = pd.DataFrame.from_dict(scores)
print(score_df)
```
## 實作2_執行結果
```
   姓名  數學  國文
0  小華  90  80
1  小明  70  55
2  小李  45  75
   姓名  國文  數學
0  小華  80  90
1  小明  55  70
2  小李  75  45
```

