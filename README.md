# 【程式設計】用LINEBot改善校園生活
##  LINE Developers
### 安裝Django及line-bot-sdk
```
pip install Django
pip install line-bot-sdk
pip install virtualenv
```
### 開啟第一個Django專案
```
cd C:/
django-admin startproject "專案名稱"
cd "專案名稱"
```
### 建立虛擬環境
```
# 建立虛擬環境方式
virtualenv "虛擬環境名稱"

# 啟動虛擬環境方式
.\"虛擬環境名稱"\Scripts\activate
```
### 建立Django APP
```
python manage.py startapp "APP名稱"
```
### 新增資料夾
```
md templates
md static
```
### 更改settings.py
#### 把LINE的Channel Access Token跟Channel Secret新增到Secret_Key之前
![image](https://github.com/shsh0404/44fun/blob/main/1.png)
#### 在INSTALLED_APPS內新增剛剛建立的APP名稱
![image](https://github.com/shsh0404/44fun/blob/main/2.png)
#### 在TEMPLATES中新增templates的資料夾路徑
![image](https://github.com/shsh0404/44fun/blob/main/3.png)
#### 設定語系、時區
![image](https://github.com/shsh0404/44fun/blob/main/4.png)
#### 新增static路徑
![image](https://github.com/shsh0404/44fun/blob/main/5.png)
#### 在開發階段Allowed_Host先設定為*即可
![image](https://github.com/shsh0404/44fun/blob/main/6.png)
#### 更改urls.py
![image](https://github.com/shsh0404/44fun/blob/main/7.png)
### 資料庫遷移初始化及建立管理者帳號
```
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```
### 執行runserver進行測試
```
python manage.py runserver
```
### 開啟Django網站後開啟瀏覽器
```
127.0.0.1:8000/admin
```
### 運用ngrok產生HTTPS URL
進入ngrok官網下載 ngrok.exe  
下載好後解壓縮，將 ngrok.exe放在專案資料夾的第一層(同 manage.py)  
在ngrok官網註冊帳號，註冊完畢並登入後，會看到一組自己的授權碼，將授權碼記錄下來
### 開啟runserver+ngrok進行LINEBOT測試
```
# 進入專案資料夾
cd "專案資料夾"

# 啟動虛擬環境，正確啟動後前面會有('虛擬環境名稱')
.\"虛擬環境名稱"\Scripts\activate

# 在虛擬環境安裝Django及LINE BOT SDK
pip install Django
pip install line-bot-sdk

# 初始化資料庫遷移
python manage.py makemigrations
python manage.py migrate

# 開啟Django內建伺服器指令
python manage.py runserver
```
開啟另一個命令提示字元，並輸入下列指令
```
./ngrok authtoken 'ngrok授權碼'
./ngrok http 8000
```
### 設置webhook URL
順利啟動ngrok後將https之後的url記錄下來，並到 LINE Developer 後台貼的 webhook URL 貼上  
在 webhook URL 後面加上 /callback
![8](https://user-images.githubusercontent.com/121269120/209457110-c034bff7-83e9-4eb6-b290-8099c774ed91.png)
**這樣就用 Django 完成 LINEBot 的設定了喔！**

##  訊息推播
### 設定加入好友的歡迎訊息
![9](https://user-images.githubusercontent.com/121269120/209457291-351cf760-aae4-4d51-8d76-ac4f2c1091a8.png)  
### 設定圖文選單
![11](https://user-images.githubusercontent.com/121269120/209457368-f53fc810-6c14-4750-b58c-1f647f6e1450.png)  
![10](https://user-images.githubusercontent.com/121269120/209457372-7d6c8449-682d-404d-a0a8-247c68bd3b6f.png)
## LINE Notify
### 登入LINE Notify，發行權杖，將權杖記錄下來
![12](https://user-images.githubusercontent.com/121269120/209457446-45c0c71e-803a-4376-9786-0bff1f414003.png)

