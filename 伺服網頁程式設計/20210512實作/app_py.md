# 20210512 實作

參考資料  
Python Flask Tutorial: Full-Featured Web App Part 4 - Database with Flask-SQLAlchemy  
<https://www.youtube.com/watch?v=cYWiDiIUxQc&list=RDCMUCCezIgC97PvUuR4_gbFUs5g>

## 之前要安裝的套件
```
pip install flask

pip install flask-wtf

pip install email_validator
```

## 新安裝的套件(和資料庫有關)
```
pip install flask-sqlalchemy
```

## app.py
```python
from datetime import datetime
from flask import Flask, render_template, url_for, flash, redirect
from flask_sqlalchemy import SQLAlchemy
from forms import RegistrationForm, LoginForm

app = Flask(__name__)
app.config['SECRET_KEY'] = '141f1bb188e7c1f5b94b81fe209d5e12'
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///site.db'
db = SQLAlchemy(app)


class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(20), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
    image_file = db.Column(db.String(20), nullable=False, default='default.jpg')
    password = db.Column(db.String(60), nullable=False)
    posts = db.relationship('Post', backref='author', lazy=True)

    def __repr__(self):
        return f"User('{self.username}', '{self.email}', '{self.image_file}')"


class Post(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    date_posted = db.Column(db.DateTime, nullable=False, default=datetime.utcnow)
    content = db.Column(db.Text, nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)

    def __repr__(self):
        return f"Post('{self.title}', '{self.date_posted}')"


posts = [
    {
        'author': 'Corey Schafer',
        'title': 'Blog Post 1',
        'content': 'First post content',
        'date_posted': 'April 20, 2018'
    },
    {
        'author': 'Jane Doe',
        'title': 'Blog Post 2',
        'content': 'Second post content',
        'date_posted': 'April 21, 2018'
    }
]


@app.route("/")
@app.route("/home")
def home():
    return render_template('home.html', posts=posts)


@app.route("/about")
def about():
    return render_template('about.html', title='About')


@app.route("/register", methods=['GET', 'POST'])
def register():
    form = RegistrationForm()
    if form.validate_on_submit():
        flash(f'Account created for {form.username.data}!', 'success')
        return redirect(url_for('home'))
    return render_template('register.html', title='Register', form=form)


@app.route("/login", methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        if form.email.data == 'admin@blog.com' and form.password.data == 'password':
            flash('You have been logged in!', 'success')
            return redirect(url_for('home'))
        else:
            flash('Login Unsuccessful. Please check username and password', 'danger')
    return render_template('login.html', title='Login', form=form)


if __name__ == '__main__':
    app.run(debug=True)

```

## 說明:

```
db = SQLAlchemy(app)
# 建立物件
```

```
id = db.Column(db.Integer, primary_key=True)
# 唯一性
```

```
username = db.Column(db.String(20), unique=True, nullable=False)
# 長度 20  
```

```
nullable=False
# 不能是空的

```

```
posts = db.relationship('Post', backref='author', lazy=True)
# 關聯 一對多
# 一個作者可以發多個貼文
```

```
user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
# 一個貼文只能有1個作者
```

## 終端機的操作
```
(myflask01) C:\Users\KSUIE>cd ..

(myflask01) C:\Users>cd ..

(myflask01) C:\>D:

(myflask01) D:\>cd MyFlask2021

(myflask01) D:\MyFlask2021>cd 4080E019

(myflask01) D:\MyFlask2021\4080E019>cd flaskTest01

(myflask01) D:\MyFlask2021\4080E019\flaskTest01>python
Python 3.8.8 (default, Apr 13 2021, 15:08:03) [MSC v.1916 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from app import db
C:\Users\KSUIE\anaconda3_NEW\envs\myflask01\lib\site-packages\flask_sqlalchemy\__init__.py:872: FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled by default in the future.  Set it to True or False to suppress this warning.
  warnings.warn(FSADeprecationWarning(
>>> db.create_all()
>>> user_1 = User(username='Corey', email='C@demo.com', password='psssword')
>>> db.session.add(user_1)
>>> user_2 = User(username='JohnDoe', email='jd@demo.com', password='psssword')
>>> db.session.add(user_2)
>>> db.session.commit()
>>> User.query.all()
[User('Corey', 'C@demo.com', 'default.jpg'), User('JohnDoe', 'jd@demo.com', 'default.jpg')]
>>> User.query.first()
User('Corey', 'C@demo.com', 'default.jpg')
>>> User.query.filter_by(username='Corey').all()
[User('Corey', 'C@demo.com', 'default.jpg')]
>>> User.query.filter_by(username='Corey').first()
User('Corey', 'C@demo.com', 'default.jpg')
>>> user = User.query.filter_by(username='Corey').first()
>>> user
User('Corey', 'C@demo.com', 'default.jpg')
>>> user.id
1
>>> user = User.query.get(1)
>>> user
User('Corey', 'C@demo.com', 'default.jpg')
>>> user.posts
[]
>>> db.drop_all()
>>> db.create_all()
>>> User.query.all()
[]
>>> Post.query.all()
[]
>>>
```

### 設定&執行
```
1. 設定要執行的 flask 檔案

 set FLASK_APP=app.py

2. 執行設定後的 flask 檔案

 flask run
 
 ```
