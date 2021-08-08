# MeetingMinutes

## 2021/07/23 分工
 - Front-end Instructions: [TSMC Design System](https://zeroheight.com/5e50b6e36/p/957ef9-instructions)
 - 希望大家都能寫到code, 暫時先前後各３人, 再動態調整
 - 前端: 彥存/有璿/紹寧 (Vue.js)
 - 後端: 書文/銘仁/盛暉 (Python Flask + MairaDB)


## 2021/07/26 Mentor 碎碎念ＱＱ
- 在設計schema的階段, 可以用一些[免費的工具](https://online.visual-paradigm.com/tw/diagrams/solutions/free-erd-tool/)畫ER Model 幫助思考,後續做ppt時也可以放
- DB的部分
 1. 可以照之前說的, 先用json當假資料, 等確定後端API可以正確的回傳資料給前端, 再串接DB
 2. 後續嘗試架一套[MariaDB](https://mariadb.org/), 最近公司在導入它取代Oracle, 參考[這篇](https://mariadb.com/resources/blog/how-to-connect-python-programs-to-mariadb/)
 3. AWS有MariaDB的service, 若後續有時間, 也可以改用AWS的服務,應該會是個不錯的經驗, 參考[這篇](https://aws.amazon.com/tw/getting-started/hands-on/create-mariadb-db/)
- 程式碼本身是最好的comment, 寫出可讀性高的程式, 比寫一堆comment更重要(Ex: 變數/方法的命名不要亂取), 但複雜的地方仍可以用comment輔助說明
- git依照不同的功能切feature branch進行開發, 該功能開發完畢後, 要開PR (Pull request) 回develop branch<br>希望大家盡可能都去看PR, 有建議或疑問都可以在PR上留言討論, 互相學習, git的概念可以參考[這篇](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)
-(如果有時間)希望能實作自動化測試的部分

## 2021/07/26 進度update
- 前端
```
以Nodejs跟bootstrapVue建立網站初版
新增登入頁面，註冊頁面，預約疫苗頁面（有璿）
```

## 2021/07/27 Discussion

1.   User story：
     
     For 員工：
     * 我想要可以預約施打疫苗
     * 預約時 我希望可以得知我能施打哪種疫苗已即可施打時間
     * 預約成功後我希望可以收到預約成功(施打)通知
     * 預約完成後我希望可以隨時查詢或修改我的預約
     * 我希望可以看到各廠區的施打比例
     
     For 主管：
     * 除了員工的功能，我希望可以查看我底下員工的施打狀況
     
     For 健康中心or施打人員：
     * 當為某員工施打成功後，我希望能登記回報他的施打資訊
     
2.   前後端功能討論：

     API需求：(目標先完成員工的基本功能)
     a. 註冊時，將使用者資訊儲存到DB
     b. 登入時，前端傳送使用者帳密，後端回傳帳密是否有效
     c. 預約時，將使用者預約資訊儲存到DB
     d. 查看預約資訊時，前端丟出使用著工號，後端回傳已儲存之預約資訊
     e. 回傳各廠區施打比例資料


## 2021/07/28 Mentor suggestion

- 前端跟後端各開一個github repo
- 登入跟後續每一發request的身份驗證這個可以先做, 註冊等其他主功能告一段落後再開始進行
- 簡單的身份驗證做法：
    1. 前端將帳號＆加密過的密碼傳給後端, 後端跟DB內的資料比對(DB直接存密文）
    2. 如果帳號密碼對了, 後端使用based64 encode一個token給前端, 設在cookie上
    3. 後續的操作, 前端都要帶這個cookie(token)給後端, 身份驗證 

## 2021/07/31 進度update
- 前端
```
修改router.js會先將網頁導向login頁面，並新增加密功能於Login.vue（有璿）
本週嘗試與後端串接
新增其他功能頁面
```
- 後端
```
下禮拜一晚上9點前完成以下：
盛輝: 會用flask-sqlalchemy連結mariadb，做出四張table，讓後端可以使用
銘仁: 做出登記預約的function
書文: 登入驗證，研究UserSchema和session的使用邏輯
```

## 2021/08/02 進度update

- 前端
```
登入API串接完成（有璿）
新增：
1. 查看預約資訊頁面（彥存）
2. 圖表統計頁面（彥存初版 紹寧修）
3. 健康中心標記施打完成頁面（紹寧）
4. 左側各網頁欄位修改（紹寧）
```
- 後端
```
新增 :
1. 登入功能已和前端串接完成 (書文)
2. 預約、查詢、刪除預約完成基本功能 (銘仁)
3. DB架構初版 (盛暉)
預計要完成的功能 :
1. 施打狀況計算
2. 考量疫苗數量的預約系統
```

## 2021/08/04 discussion

改用mongoDB cloud: 方便串接時前端不須自己建立DB在自己的電腦

前端：
```
完成登出API串接(有璿)
待做事項：
1. 註冊頁面新增部門欄位(方便之後圖表統計用)(彥存)
2. 預約疫苗新增日期欄位(彥存)
3. 修改查看預約資訊頁面：不須有修改功能，直接於預約資訊後面新增delete button，並提醒使用者須重新預約(彥存)
4. 修改健康中心頁面：改成顯示今日預約者，並在該資訊後面新增"已施打" button，按完之後對這筆資料做顯示上的修改 以分辨施打與否(紹寧)
5. 將user id存到localStorage，在其他頁面才能得到使用者資訊(有璿)
6. 嘗試處理使用者身分與權限問題(有璿)
```

## 2021/08/07 進度update
- 前端
```
登入API串接修改（有璿）
修改預約頁面(彥存)
修改查看預約資訊頁面（彥存）
修改圖表統計頁面（紹寧）
修改健康中心頁面（紹寧）
儲存userId跟identity於localStorage 且偵測到localStorage被修改時會自動改回原本的data(避免用其他人的id偷看資料)(有璿)
隱藏側欄health center連結(之後再處理讓他連擁有健康中心網址也進不去)(有璿)
```
## 2021/08/08 login issue explanation by mentor
- Problem background:
```
1. 後端使用flask-login套件做登入狀態管理
2. 後端已用postman測試過, 先call login API再call其他加上@login_required的API, 可以正確卡關
3. 但前端跟後端串接發現, 即使login過, 後續的request打過去, 均被視為未登入
```

![image](https://github.com/TSMCHappyClick/MeetingMinutes/blob/main/images/request-header.png)

- 為什麼使用postman時正常, 但前端串接會失敗:
```
1. call login api時, response header會多一個set-cookie, session=xxx
2. 使用postman時, 這個cookie會自動被更新至request header, 因此下一發request會帶上此cookie
3. cookie不允許跨domain access, 前端的domain與後端不同, 所以set-cookie失敗
```

![image](https://github.com/TSMCHappyClick/MeetingMinutes/blob/main/images/response-set-header.png)

- How to fix? (frontend) 
```
1. 將AP也deploy至heroku, 這樣就會與後端擁有相同domain (*.herokuapp.com)
    1.1. 刪除package-lock.json ＆ yarn.lock
    1.2. 加上static.json (內容跟官網sample一樣即可)
    1.3. vue.config.js加上outputDir: 'dist/HappyClick/'
2. 在main.js加上 => axios.defaults.withCredentials = true
```
- How to fix? I  (backend)

```
1. after_request加上, 解決cors site的問題
response.headers.add('Access-Control-Allow-Origin', 'https://happy-click-gui.herokuapp.com')
response.headers.add('Access-Control-Allow-Headers',
                     'Access-Control-Allow-Headers, Access-Control-Allow-Origin, Origin, Accept, '
                     'X-Requested-With, Content-Type, '
                     'Access-Control-Request-Method, Access-Control-Request-Headers')
response.headers.add('Access-Control-Allow-Credentials', 'true')
response.headers.add('Access-Control-Allow-Methods', 'GET, PUT, POST, DELETE')

2. 更改ap config, 解決samesite問題
app.config.update(
    SESSION_COOKIE_SECURE=True,
    SESSION_COOKIE_HTTPONLY=True,
    SESSION_COOKIE_SAMESITE='None',
)
```

- Reference:
  <br/>
  [Cors and Samesite](https://medium.com/d-d-mag/%E5%92%8C-cors-%E8%B7%9F-cookie-%E6%89%93%E4%BA%A4%E9%81%93-dd420ccc7399)
  <br/>
  [Flase set cookie](https://flask.palletsprojects.com/en/2.0.x/security/#set-cookie-options)