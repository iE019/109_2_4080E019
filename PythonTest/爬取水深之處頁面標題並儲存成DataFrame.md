# 爬取水深之處頁面標題並儲存成DataFrame

實作日期: 2021/05/17

參考資料:解析Python網頁爬蟲如何有效整合Pandas套件提升資料處理效率
<https://www.learncodewithmike.com/2020/11/python-web-scraping-with-pandas.html>

```python
def myTest(subject):
  web_Url = requests.get("http://www.luke54.org/index.php?option=com_jumi&view=application&fileid=41&cat=" + subject) 
  # 將此水深之處頁面的 HTML碼 抓取出來

  soup = BeautifulSoup(web_Url.text,"html.parser") 
  # 將網頁資料以 html.parser 來解析

  sel = soup.select("div.item-title a") 
  # 抓取HTML標籤中的 <div class="item-title"></div> 中的<a>標籤存入變數sel裡

  result = []
  for title_string in sel:
    result.append((title_string.text, title_string["href"]))
  print("-----------------------------------") # 分隔線
  
  df = pd.DataFrame(result, columns=["標題", "網址"])
  print(df)
  print("")

delay_choices = [1, 3, 5, 7]  #延遲的秒數
delay = random.choice(delay_choices)  #隨機選取秒數
# 目的: 降低網頁爬蟲被偵測封鎖的機率

Outside_subject = ["真理","見證","時事","詩歌","影片"]
# 給文字敘述用的主題

Inside_subject = ["truth","testimony","current","hymns","video"]
# 給網址用的主題

for num in range((len(Outside_subject))):
  print("顯示此週主題為_"+ Outside_subject[num] +"_的最新文章標題:")
  myTest(Inside_subject[num]) # 呼叫 myTest method 
  time.sleep(delay) # 隨機延遲個幾秒


```

## 執行結果

```
顯示此週主題為_見證_的最新文章標題:
-----------------------------------
                                                  標題                                          網址
0                       婚姻家庭｜【 願你吸引我，我們就快跑跟隨你！ 】水深之處  http://www.luke54.org/view/1060/12649.html
1                     福音見證｜【失明，是因我業障太深？不，主耶穌救了我】水深之處  http://www.luke54.org/view/1060/12639.html
2                校園學業｜【國中英文只考2分，卻能考上成功大學 葉爸爸說故事】水深之處  http://www.luke54.org/view/1062/12614.html
3           【可以當貴婦，卻選擇不再當貴婦】我地上的父親雖然走了，但是我天上的父親來了...  http://www.luke54.org/view/1060/12183.html
4                         【但那誠實愛主的人，禍福都不問...】黃昱庭姊妹見證  http://www.luke54.org/view/1060/12070.html
5  【如何在高手如雲的公司中，事業蒸蒸日上？又沒有壓力？】王嘉陵姊妹 以IBM公司副總裁的職位，...  http://www.luke54.org/view/1060/12062.html
6                         【趕鬼法師竟成基督徒】范凱彥弟兄─原來耶穌是最大的！  http://www.luke54.org/view/1062/12051.html
7                                          【婚姻的信心之路】  http://www.luke54.org/view/1060/12046.html
8    【基督徒如何聰明工作、蒙福人生？】先搞清楚什麼是人生大事，作一個真正聰明的人 柯是鈐弟兄的見證  http://www.luke54.org/view/1060/12042.html
9                   【你是否有真正的平安?】到了鬼門開的日子，怕疫情又怕鬼，怎麼辦？  http://www.luke54.org/view/1060/12018.html

顯示此週主題為_時事_的最新文章標題:
-----------------------------------
                                                  標題                                          網址
0  時事感言｜【日本311大地震，一位基督徒蒙拯救的故事。在各樣環境中，你都能跟主耶穌禱告！】水深之處  http://www.luke54.org/view/1060/12643.html
1             時事感言｜【以色列普珥節：一段精彩絕倫聖經中「逆轉勝」─ 以斯帖記】水深之處  http://www.luke54.org/view/1060/12597.html
2  時事感言｜【外星人存在嗎？聖經怎麼說？ 帶您看美國NASA毅力號：來自火星的景象與風聲  】...  http://www.luke54.org/view/1060/12594.html
3                       【生命中的公轉，年末的十件事】空中的鸛鳥，知道來去的定期  http://www.luke54.org/view/1060/12355.html
4            【動物園食蟻獸「小紅」回家囉！】別在外漂流不得飽了，回家吧！神愛你，正在等你！  http://www.luke54.org/view/1060/12313.html
5                                 【神為人預備不盡的機會】新年新月新日  http://www.luke54.org/view/1060/12299.html
6  【虛空的人生 vs 美福的人生】「神的手」的阿根廷足球人物，馬拉度納（Diego Marad...  http://www.luke54.org/view/1060/12290.html
7       【感恩節 thanksgiving 】只有神才是「萬福泉源」，一切祝福最後都是來自神自己  http://www.luke54.org/view/1060/12287.html
8                            【人生如同在風暴海上的一艘船】大海教會我們的事  http://www.luke54.org/view/1060/12286.html
9                   【從哈米吉頓大戰之豫言，看今日世界局勢】李俊輝弟兄 國際觀點分析  http://www.luke54.org/view/1060/12261.html

顯示此週主題為_詩歌_的最新文章標題:
-----------------------------------
                                                  標題                                          網址
0  【最聞名的詩歌：Amazing Grace 驚人恩典 】背後動人的故事，約翰牛頓從無賴變為基...  http://www.luke54.org/view/1062/12081.html
1                                           詩人與詩歌：宣信  http://www.luke54.org/view/1060/10599.html
2                                    悄悄的，菲比成了主偷走的寶貝。  http://www.luke54.org/view/1060/10231.html
3                          【來學日文新詩歌】Jesus Lord Jesus  http://www.luke54.org/view/1062/10164.html
4                                   【信主的價值】施孝榮弟兄分享見證  http://www.luke54.org/view/1062/10057.html
5                            得勝得勝，阿利路亞－SOLSO 水流之音聖樂團   http://www.luke54.org/view/1062/9640.html
6                             愛使浪子回家 - SOLSO 水流之音聖樂團   http://www.luke54.org/view/1062/9630.html
7                               永活救主 － SOLSO 水流之音聖樂團   http://www.luke54.org/view/1062/9623.html
8                           我神我愛我的永分 - SOLSO 水流之音聖樂團   http://www.luke54.org/view/1062/9597.html
9                            惟知道我所信的是誰－SOLSO 水流之音聖樂團   http://www.luke54.org/view/1062/9575.html

顯示此週主題為_影片_的最新文章標題:
-----------------------------------
                                                  標題                                          網址
0                校園學業｜【國中英文只考2分，卻能考上成功大學 葉爸爸說故事】水深之處  http://www.luke54.org/view/1062/12614.html
1             【人到底為什麼活著？】為金錢、學問、享樂、成就嗎？聖經啟示一個真正的原因~~  http://www.luke54.org/view/1060/12102.html
2                         【趕鬼法師竟成基督徒】范凱彥弟兄─原來耶穌是最大的！  http://www.luke54.org/view/1062/12051.html
3  【106歲的爺爺，告訴你】信主有甚麼好處？   我說：「好處太多！」他喜樂平安，一無所缺的原...  http://www.luke54.org/view/1062/11988.html
4                                        【動畫小卡】男孩與釘子  http://www.luke54.org/view/1062/10495.html
5                            〖水深知識+〗孕婦必看麻醉風暴之無痛分娩打不打  http://www.luke54.org/view/1062/10431.html
6                                      【動畫小卡】改變生命的橘子  http://www.luke54.org/view/1062/10067.html
7                                   【信主的價值】施孝榮弟兄分享見證  http://www.luke54.org/view/1062/10057.html
8                           【真理短講】基督不只來作生命，祂更要作我們的人位   http://www.luke54.org/view/1062/9895.html
9                            【在賭城槍案中為妻子犧牲的丈夫－桑尼．梅爾頓】   http://www.luke54.org/view/1062/9823.html

```
