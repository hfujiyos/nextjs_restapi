## Pythonプロジェクト作成
### Anaconda
* 仮想環境構築
  * Name : Nextjs_API
  * Package : Python 3.8.13

* ライブラリインストール
  ```
  $ pip install Django==3.1
  $ pip install django-cors-headers==3.4.0
  $ pip install djangorestframework==3.11.1
  $ pip install djangorestframework-simplejwt==4.6.0
  $ pip install PyJWT==2.0.0
  $ pip install djoser==2.0.3
  $ pip install python-decouple
  $ pip install dj-database-url
  $ pip install dj_static
  ```

### PyCharm
* プロジェクト rest_api を作成
  ```
  $ django-admin startproject rest_api .
  ```

* アプリケーション api を作成
  ```
  $ django-admin startapp api
  ```

## 開発環境
### ディレクトリ構成
* api
  * admin.py
  * models.py
  * serializers.py
  * urls.py
  * views.py
* rest_api
  * asgi.py
  * settings.py
  * urls.py
  * wsgi.py
* .env
* .gitignore
* manage.py
* Procfile
* requirements.txt
* requirements-dev.txt
* runtime.txt

### マイグレーション
* マイグレーション
  ```
  $ python manage.py makemigrations
  $ python manage.py migrate 
  ```

* superuser
  ```
  $ python manage.py createsuperuser
  Username: *****
  Email address: *****
  Password: *****
  ```

## デプロイ
### デプロイ設定
* rest_api/wsgi.py
  ```
  import os
  from dj_static import Cling
  from django.core.wsgi import get_wsgi_application

  os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'rest_api.settings')

  application = Cling(get_wsgi_application())
  ```
* requirements-dev.txt
  ```
  仮想環境にインストール済のモジュール一覧を作成
  $ pip freeze > requirements-dev.txt
  ```
* runtime.txt
  ```
  python-3.8.13
  ```
* requirement.txt
  ```
  -r requirements-dev.txt
  gunicorn
  psycopg2==2.8.6
  ```
* Procfile
  ```
  web: gunicorn rest_api.wsgi --log-file -
  ```
* restapi/settings.pyにURLを追記
  ```
  ALLOWED_HOSTS = ['nextjs-hpapi.herokuapp.com']
  ```

### Heroku CLI
  ```
  $ heroku git:remote -a nextjs-hpapi
  $ heroku config:push
  ```

## 本番環境
### Heroku Deploy
  ```
  $ git add .
  $ git commit -m "initial commit to heroku"
  $ git push heroku master
  ```

### マイグレーション
* マイグレーション
  ```
  $ heroku run python3 manage.py migrate
  ```

* superuser
  ```
  $ heroku run python3 manage.py createsuperuser
  Username: ************
  Email address: ************
  Password: ************
  ```
