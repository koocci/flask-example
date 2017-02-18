# Examples of Flask

---

Flask 개발 Example 모음
(Examples of `Flask`)

---
## reference

+ [Flask 메인 참고 자료](https://realpython.com/blog/python/flask-by-example-part-1-project-setup/)
+ [Flask 보조 참고 자료](http://flask-docs-kr.readthedocs.io/ko/latest/foreword.html)

---
### 001 - install && setting

+ [homebrew, pip 설치](http://freeprog.tistory.com/58)
    - python package index
+ [virtualenv 설치](https://virtualenv.pypa.io/en/latest/installation/)
    - python 가상 개발환경
    - env 환경 설정
+ 기본 파일 설정
    - `touch app.py .gitignore README.md requirements.txt`
+ `Flask` 설치, requirements.txt에 freeze
    - pip install Flask
    - pip freeze > requirements.txt
+ app.py 코딩 후, 실행확인
+ heroky 계정을 터미널에 실행
    - `heroku login`
+ `Procfile` 파일 생성 후 작성
+ `gunicorn` 설치 후 `requirements` freeze
    - `pip install gunicorn`
+ heroku가 사용할 [Python Runtime](https://devcenter.heroku.com/articles/python-runtimes)을 실행하기 위해 `runtime.txt`를 만들고 파이썬 버젼 작성
+ [heroku 연결](https://devcenter.heroku.com/articles/heroku-cli)
+ heroku에 `Personal apps` 만들기 (pro, stage) 이 후, git 연결
+ pro, stage workflow 이해
+ `config`파일 설정
+ [autoenv](https://github.com/kennethreitz/autoenv) 설정
+ 저장소별 config 설정 (Local, stage, pro) `APP_SETTINGS`
+ config 설정 확인
    - `app.config.from_object(os.environ['APP_SETTINGS'])`
+ heroku 실행으로 결과 확인
    - `heroku run python app.py --app YOUR-APP`

---
### 002 - Postgres, SQLAlchemy, and Alembic

+ env 설정 확인
+ [postgres 설치](https://www.codementor.io/devops/tutorial/getting-started-postgresql-server-mac-osx)
+ psycopg2 설치 - (sudo)pip install psycopg2
    - Python library 로, Python에서 PostgreSQL를 활용하게 해주는 library
+ Flask-SQLAlchemy 설치 - (sudo) pip install Flask-SQLAlchemy
    - DB 툴
+ Flask-Migrate 설치 - (sudo) pip install Flask-Migrate
    - handles SQLAlchemy database migrations for Flask applications using Alembic
+ requirement.txt 추가 - `pip freeze > requirements.txt`
+ config에 `SQLALCHEMY_DATABASE_URI` 추가
+ `DATABASE_URL` 환경 변수 설정
+ `models.py` 파일 생성
    - PostgreSQL `dialects` -> the system SQLAlchemy uses to communicate with various types of DBAPI implementations and databases.
    - `JSON columns` -> postgres 에서는 새로운 것이고, SQLAlchemy이 제공하는 모든 DB에서 가능한 것이 아니므로, 따로 import 해준다.
    - `Result class` -> results 라는 table name 을 주고, attributes를 정의
    - `__init__()`, `__repr__()` 정의
+ `Alembic` 사용을 위해, manage.py 생성
    - A database migration tool for SQLAlchemy.
    - `Migrate` 와 `MigrateCommand`를 수행하기 위해 `Manager` 를 import
    - `app` 과 `db`를 import해 사용할 수 있게 함.
    - 이후, `migrate instance`를 만들고, `manager instance`를 만든다.
    - `db` command 를 `manager`에 추가하면, command line 으로 `migrations`을 사용할 수 있다.
+ 위 참조문서와는 다르게 `Flask-Script`에서, `flask.ext.somthing`은 deprecated 됬으므로, `flask_something`으로 바꿔서 적용한다. 그렇지 않으면 밑, `migrations`과정에 문제가 생길 수 있다.
+ `Alembic`을 init하기 위해 migrations 를 실행  (command line `python manage.py db init` 실행)
    - `migrations` 파일 자동 생성됨
    - `migrations`파일 내부 `versions` 확인 (migration파일이 만들어 질 곳)
+ `python manage.py db migrate` 실행 (migration 파일 생성)
+ `python manage.py db upgrade` 실행
    -[Text 오류 개선](http://stackoverflow.com/questions/39997252/flask-python-manage-py-db-upgrade-raise-error)
+ `psql` 로 DB 현황 확인
+ heroku 환경변수적용 확인 - (heroku config --app YOUR-STAGE-APP)
+ heroku 내 환경변수 설정 (`hobby-dev`는 heroku의 free tier다.)
    - `heroku addons:create heroku-postgresql:hobby-dev --app YOUR-STAGE-APP`
+ heroku 환경변수적용 다시 확인 - (heroku config --app YOUR-STAGE-APP)
    - `DATABASE_URL` 추가된 것 확인
+ git push stage master
+ heroku 내 migration 적용
    - `heroku run python manage.py db upgrade --app YOUR-STAGE-APP`
    - 미리 로컬에서 migration 파일은 만들었으므로, upgrade만 하면 된다.
+ 돌아가는게 확인이 되면, pro 에도 똑같이 적용한다.
+ `heroku pg:psql --app YOUR-APP` 으로 해당 앱의 postgres에 접속할 수 있다.
+ 적용된 버전
    - alembic==0.8.10
    - click==6.7
    - Flask==0.12
    - Flask-Migrate==2.0.3
    - Flask-Script==2.0.5
    - Flask-SQLAlchemy==2.1
    - gunicorn==19.6.0
    - itsdangerous==0.24
    - Jinja2==2.9.5
    - Mako==1.0.6
    - MarkupSafe==0.23
    - psycopg2==2.6.2
    - python-editor==1.0.3
    - SQLAlchemy==1.1.5
    - Werkzeug==0.11.15
+ postgres 버전
    - postgres (PostgreSQL) 9.6.2

---
## 제작

+ 구진현
    - [blog](https://koocci.github.io)
    - [github](https://github.com/koocci)

---
## Update

+ 2017 / 02 / 16
    - install && setting 완료
+ 2017 / 02 / 18
    - Postgres, SQLAlchemy, and Alembic 완료

---
## 개발환경

+ macOS Sierra 10.12.1
