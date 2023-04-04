# 【自主學習】Python 的學習與應用 - 利用 LINE Bot 幫助校園生活
##  LINE Developers
### 建立LINE官方帳號
![14](https://user-images.githubusercontent.com/121269120/209457730-145c9bfc-d070-4601-ac80-7b54d4f9b770.png)
### 獲取LINE Channel secret、access token
![15](https://user-images.githubusercontent.com/121269120/209457828-ce66be6e-e884-44b5-b82f-0913962f6e2d.png)
![16](https://user-images.githubusercontent.com/121269120/209457848-a893efdc-261c-4e2c-ba62-cea79107e4eb.png)
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
![1](https://user-images.githubusercontent.com/121269120/209457953-6826d258-5765-416a-888d-76acf3051e39.png)
#### 在INSTALLED_APPS內新增剛剛建立的APP名稱
![2](https://user-images.githubusercontent.com/121269120/209457955-16580a6e-6b91-43ac-99df-0a1a6dec1774.png)
#### 在TEMPLATES中新增templates的資料夾路徑
![3](https://user-images.githubusercontent.com/121269120/209457957-f18f7ee4-8317-4353-93fc-60e21687a772.png)
#### 設定語系、時區
![4](https://user-images.githubusercontent.com/121269120/209457959-90a42b4f-e594-4d21-b330-2d9be902b1af.png)
#### 新增static路徑
![5](https://user-images.githubusercontent.com/121269120/209457962-e9e4d4e6-8b5f-4f96-99e5-04b3a078340d.png)
#### 在開發階段Allowed_Host先設定為*即可
![6](https://user-images.githubusercontent.com/121269120/209457964-74f1e6db-2956-43b7-81c7-e1e16374061f.png)
#### 更改urls.py
![7](https://user-images.githubusercontent.com/121269120/209457968-e519299a-068f-4086-9852-9ebb39e91506.png)
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
## LINE Notify爬蟲
### 登入LINE Notify，發行權杖，將權杖記錄下來
![12](https://user-images.githubusercontent.com/121269120/209457446-45c0c71e-803a-4376-9786-0bff1f414003.png)
### 爬蟲
```
from bs4 import BeautifulSoup  # 從 bs4 大套件中選取其中一個 BeautifulSoup 功能
import requests          

def linebot(url):         # 自訂函數

  data = requests.get(url)   # 模擬伺服器使用 get 取得資料

  soup = BeautifulSoup(data.text,"html.parser")   # 匯入模組

  sel = soup.select("td.col-md-9 a")        # 只取每篇貼文的標題

  msg = " "
  
  for item in sel:
    msg += item.text + "\n"     
  return msg


def LineNotify(token, msg):         # 連接 LineNotify

    headers = {
        "Authorization": "Bearer " + token,
        "Content-Type": "application/x-www-form-urlencoded"
    }

    params = {
        "message": msg
    }

    r = requests.post("https://notify-api.line.me/api/notify", headers=headers, params=params)

 
if __name__ == "__main__":

    token = "你的LINE Notify權杖token"  # 從LINE Notify取得的權杖(token)

    url = "https://www.shsh.ylc.edu.tw/"          # 要爬蟲的網址

    msg = "最新消息：\n" + linebot(url)          # 要在LINE上跳出的提示訊息

    LineNotify(token, msg)
```
### 定時爬蟲
#### 開啟windows的工作排程器
![13](https://user-images.githubusercontent.com/121269120/209457637-d4fcec85-f0eb-49c9-a6d9-2c512178431c.png)
#### 建立工作並新增程式(py.檔)路徑
![17](https://user-images.githubusercontent.com/121269120/209457881-850a069b-33e6-4fa0-bcf5-cabf89b827d5.png)
#### 設定工作觸發時間
![18](https://user-images.githubusercontent.com/121269120/209457916-8d0bf276-f89c-4365-9ceb-951ed8bc7d76.png)
**這樣就完成 LINEBot Notify 校網爬蟲的設定了喔！**
