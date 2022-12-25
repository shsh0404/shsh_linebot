## 【程式設計】用LINEBot改善校園生活
### 安裝Django及line-bot-sdk
```
$ pip install Django
$ pip install line-bot-sdk
$ pip install virtualenv
```
### 開啟第一個Django專案
```
$ cd C:/
$ django-admin startproject "專案名稱"
$ cd "專案名稱"
```
### 建立虛擬環境
```
#建立虛擬環境方式
$ virtualenv "虛擬環境名稱"

#啟動虛擬環境方式
$ .\"虛擬環境名稱"\Scripts\activate
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
進入ngrok官網下載ngrok.exe
