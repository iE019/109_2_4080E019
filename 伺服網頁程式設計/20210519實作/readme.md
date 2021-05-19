# 20210519 實作

參考資料  
Python Flask Tutorial: Full-Featured Web App Part 5 - Package Structure  
<https://www.youtube.com/watch?v=44PvX0Yv368&list=RDCMUCCezIgC97PvUuR4_gbFUs5g&t=1s>

## 之前要安裝的套件
```
pip install flask

pip install flask-wtf

pip install email_validator

pip install flask-sqlalchemy
```
## 此次的變化
```
app.py 改名成 run.py

在 flaskTest01資料夾內，新建 1個 flaskblog 資料夾
將 除了 run.py、__pycache__ 都存入 flaskblog 資料夾裡

原本的 __pycache__ 刪除

__pycache__ 之後會自動建檔在 flaskblog 資料夾裡

```

## 終端機裡的操作
```
顯示架構:
tree



```

## 執行
```
python run.py
```
