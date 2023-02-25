<h1 align="center">
Flask Notes
</h1>

<p id="index"></p>

* [Flask App Structure](#Structure)
* [Flask App](#App)
* [Setup Cors](#cors)
* [Url Building](#urlBuilding)
* [Json Response](#Json)
* [Send Status Code](#Status)
* [Set Cookie](#SetCookie)
* [Get Cokie](#GetCookie)
* [Session](#Session)
* [Get Form Data](#Form)
* [Get Json Data](#GetJson)
* [Get Query Parameter](#Query)
* [Get Route Parameter](#Route)
* [Redirect](#Redirect)
* [Error Handling](#Error)
* [Flash Message](#Flash)
* [Templates](#Templates)
* [Use .env](#.env)
* [Jwt](#Jwt)
* [Bcrypt](#Bcrypt)
* [File Uploading](#fileUploading)
* [Flask Mail](#Mail)
* [Flask SQLAlchemy](#SQLAlchemy)
* [Flask SQLite](#SQLite)
* [Flask MySQL](#MySQL)

<p id="Structure"></p>

## Flask App Structure
* MyBlogApp
	* main.py
	* static **Folder**
		* `images`
		* `css`
		* `js`
		* `fonts`
		* `etc`
	* templates **Folder**
		* `all html file`

<p id="App"></p>

## Flask App
```py
from flask import *  
app = Flask(__name__)  
  
@app.route('/')  
def admin():  
    return render_template('index.html')  

if __name__ =='__main__':  
    app.run(host="localhost",port=7000,debug = True)
```

[Back To Top](#index)

<p id="cors"></p>

## Flask Cors
* **pip install flask-cors**
* [Docs](https://flask-cors.corydolphin.com/en/latest/api.html#extension)
```py
from flask_cors import CORS,cross_origin

# Initialize app Object
app = Flask(__name__)  
# Set cors
CORS(app, resources=r'/api/*')

```
[Back To Top](#index)


<p id="Json"></p>

<p id="urlBuilding"></p>

## Url Building
```py
# success is a function
return redirect(url_for("success"))
```

[Back To Top](#index)

## Json Response
```py
return jsonify({"message":"Im josn response !"})
```

[Back To Top](#index)

<p id="Status"></p>

## Send Status Code
```py
return jsonify({"message":"Im josn response !"}),200
```

[Back To Top](#index)

<p id="SetCookie"></p>

## Set Cookie
```py
res = make_response("Cookie i set")  
res.set_cookie("username","frabbi43")
return res
```

[Back To Top](#index)

<p id="GetCookie"></p>

## Get Cookie
```py
cookie = request.cookies["username"]
```

[Back To Top](#index)

<p id="Session"></p>

## Session
```py
from flask import *  
app = Flask(__name__)  

# Key For Sign Session
app.secret_key = "abc"

@app.route('/')  
def home():  
    session["uname"] = "frabbi45"
    return "Session Stored"

@app.route('/get')  
def get():  
    value = session["uname"]
    return "Session :"+value

# for clear ession
session.pop('key', None)

if __name__ =='__main__':  
    app.run(host="localhost",port=7000,debug = True)
```

[Back To Top](#index)

<p id="Form"></p>

## Get Form Data
```py
@app.route('/register',methods=["GET","POST"])
def register():  
	if request.method == "POST":
		name = request.form["name"]
		age = request.form["age"]
```

[Back To Top](#index)

<p id="GetJson"></p>

## Get Json Data
```py
@app.route('/register',methods=["GET","POST"])
def register():  
   if request.method == "GET":
      return "Metnod not accepted"
   if request.method == "POST":
      data = request.json
      if "name" in data:
         return "Hello: "+data["name"]
      else:
         return "Please send valid data"
```

[Back To Top](#index)

<p id="Query"></p>

## Get Query Parameter
```py
@app.route('/search')  
def search():
   query_data = request.args
   if "id" in query_data:
      ID = query_data["id"]
      return "Id: "+ID
   else:
      return "Query Data Not Found"
```

[Back To Top](#index)

<p id="Route"></p>

## Get Route Parameter
```py
# here name is also called as slug
@app.route('/search/<string:name>')  
def search(name):
	if name:
		return "Hello, "+name
```

[Back To Top](#index)

<p id="Redirect"></p>

## Redirect
```py
@app.route('/login')  
def login():
	# home is function name
	return redirect(url_for("home"))
```

[Back To Top](#index)

<p id="Error"></p>

## Error Handling
* **400:** for bad requests
* **401:** for unauthorized access
* **403:** for forbidden
* **404:** for not found
* **406:** for not acceptable
* **415:** for unsupported media types
* **429:** for too many requests
```py
# Page Not Found Error/404
@app.errorhandler(404)
def page_not_found(e):
    return render_template("404.html")

# it is used to to handle error that made from client side
abort(403) # it will through error --> Forbidden

# Others Error
import werkzeug

@app.errorhandler(werkzeug.exceptions.BadRequest)
def handle_bad_request(e):
    return 'bad request!', 400
```

[Back To Top](#index)

<p id="Flash"></p>

## Flash Message
   * **main.py**
   ```py
   @app.route('/')  
   def home():  
       flash('Welcome Back','success')
       return render_template('home.html');  
       
   ```
   
   * **index.html**
   ```html
   {% with messages = get_flashed_messages(with_categories=true) %}
   {% if messages %}
   {% for category,message in messages %}
      
      <div class="m-3 alert alert-{{category}}">
         <span>{{ message }} Hello guys welcome to my home page</span>
      </div>
      
   {% endfor %}
   {% endif %}
   {% endwith %}   
   ```
[Back To Top](#index)

<p id="Templates"></p>

## Templates
```py
return redirect(url_for(render_template("home.html")))
return render_template("home.html")

@app.route('/test')  
def test():  
	data = {
		"name": "Smith" 
	}
   return render_template("home.html",data=data)  
```

[Back To Top](#index)

<p id=".env"></p>

## Use .env
* pip install decouple
* make `.env` file and write bellow `line`
	* URL=https://example.com
	* Access `URL` from python
		```py
		from decouple import config
		
		url = config("URI")
		```

[Back To Top](#index)

<p id="Jwt"></p>

## Use Jwt
```py
import jwt

encoded_jwt = jwt.encode({"username": "frabbi"}, "ilovecode", algorithm="HS256")
decoded_jwt = jwt.decode(encoded_jwt, "ilovecode", algorithms=["HS256"])
```

[Back To Top](#index)

<p id="Bcrypt"></p>

## Use Bcrypt
* pip3 install -U "bcrypt<4.0.0"
	```py
	import bcrypt
	
	password = b"super secret password"
	
	hashed = bcrypt.hashpw(password, bcrypt.gensalt())
	
	print(hashed)
	
	if bcrypt.checkpw(password, hashed):
		print("matched")
	else:
		print("not matched")
	
	```

[Back To Top](#index)

<p id="fileUploading"></p>

## File Uploading
```py
import os
from flask import Flask, flash, request, redirect, url_for, send_from_directory
from werkzeug.utils import secure_filename

UPLOAD_FOLDER = os.path.join(os.getcwd(),'uploads')
ALLOWED_EXTENSIONS = {'txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif'}

app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER
app.config["SECRET_KEY"] = "01isjkak"

def allowed_file(filename):
    return '.' in filename and \
           filename.rsplit('.', 1)[1].lower() in ALLOWED_EXTENSIONS

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        # check if the post request has the file part
        if 'file' not in request.files:
            flash('No file part')
            return redirect(request.url)
        file = request.files['file']
        # If the user does not select a file, the browser submits an
        # empty file without a filename.
        if file.filename == '':
            flash('No selected file')
            return redirect(request.url)
        if file and allowed_file(file.filename):
            filename = secure_filename(file.filename)
            file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
            return redirect(url_for('download_file', name=filename))
    return '''
    <!doctype html>
    <title>Upload new File</title>
    <h1>Upload new File</h1>
    <form method=post enctype=multipart/form-data>
      <input type=file name=file>
      <input type=submit value=Upload>
    </form>
    '''

@app.route('/uploads/<name>')
def download_file(name):
    return send_from_directory(app.config["UPLOAD_FOLDER"], name)

if __name__ == "__main__":
	app.run(debug=True)
```

[Back To Top](#index)

<p id="Mail"></p>

## Flask Mail
```py
from flask import *  
from flask_mail import Mail

# Initialize app Object
app = Flask(__name__)  
app.config.update(
		MAIL_SERVER="smtp.gmail.com",
		MAIL_PORT=465,
		MAIL_USE_SSL=True,
		MAIL_USERNAME= "",
		MAIL_PASSWORD= ""
	)
mail = Mail(app)

# Home Route
@app.route('/')  
def home():
	# Send Email
	mail.send_message("Title",sender="",recipients=[""],body="")
	return jsonify({"Message":"Email send successful."})

# Start App
if __name__ =='__main__':  
	app.run(debug = True)	
```

[Back To Top](#index)

<p id="SQLAlchemy"></p>

## Flask SQLAlchemy
* `What is SQLAlchemy?`
	<p>SQLAlchemy is the Python SQL toolkit and Object Relational Mapper that gives application developers the full power and flexibility of SQL.</p>
* `What is ORM?`
	<p>Object-Relational Mapping (ORM) is a technique that lets you query and manipulate data from a database using an object-oriented paradigm. When talking about ORM, most people are referring to a library that implements the Object-Relational Mapping technique, hence the phrase "an ORM".
	An ORM library is a completely ordinary library written in your language of choice that encapsulates the code needed to manipulate the data, so you don't use SQL anymore; you interact directly with an object in the same language you're using.</p>
* `What is Flask-SQLAlchemy?`
	<p>Flask-SQLAlchemy is an extension for Flask that adds support for SQLAlchemy to your application. It simplifies using SQLAlchemy with Flask by setting up common objects and patterns for using those objects, such as a session tied to each web request, models, and engines.</p>

[Back To Top](#index)

<p id="SQLite"></p>

## Flask SQLite
* ***pip install flask-sqlalchemy***
```py
from flask import *
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()
app = Flask(__name__)  
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///todos.db" # dbname
db.init_app(app)

# Define Databse Model
class Todos(db.Model):
	sno = db.Column(db.Integer, primary_key=True)
	title = db.Column(db.String, nullable=False)
	desc = db.Column(db.String, nullable=False)
	created_date = db.Column(db.DateTime, default=datetime.utcnow)
	
	def __init__(self,title,desc):
		self.title = title
		self.desc = desc
		
	def __repr__(self):
		return f"Title:{self.title}"

# Create Table
with app.app_context():
    db.create_all()

#================================
#	 CRUD --> Operation			 
#================================

# Create
todo = Todos("Learn Python","From codewithharry in one month")
db.session.add(todo)
db.session.commit()

# Read
sno = 1 # id
all_todos = Todos.query.all()
one_todo = Todos.query.filter_by(sno=sno).first()

# Update
todo = Todos.query.filter_by(sno=sno).first()
todo.title = "New Title"
todo.desc = "This is description"
db.session.commit()

# Delete
todo = Todos.query.filter_by(sno=sno).first()
db.session.delete(todo)
db.session.commit()
```

<p id="MySQL"></p>

[Back To Top](#index)

## Flask MySQL
* **pip install pymysql**
```py
import pymysql
from flask_sqlalchemy import SQLAlchemy

# Configure SQLAlchemy With MySQL
db = SQLAlchemy()
app.config["SQLALCHEMY_DATABASE_URI"] = f"mysql+pymysql://{db_user_name}:{db_user_pass}@{host_name}/{db_name}"
db.init_app(app)

# Define Database Model
class Users(db.Model):
	id = db.Column(db.Integer, primary_key=True)
	name = db.Column(db.String(25), nullable=False)
	
	def __init__(self,name,username,email,password,is_verified,otp,token):
		self.name = name
		
	def __repr__(self):
		return f"""
		name:{self.name},
		"""
	
# Create Table
with app.app_context():
    db.create_all()

# Read Data
AllPosts = Blogs.query.all()
featured_posts = Blogs.query.filter(Blogs.featured_post.contains(1)).all()
note = Notes.query.filter_by(username=username).first()
notes = Notes.query.filter_by(username=username).all()
# Read Some Column
db.session.query(SomeModel.col1)
Model.query(Model.col1,Model.col2)

# usages: note.id  --> note is an class object

# -----------
# create
# delete
# update
# ----------- View in sqlite !

```

[Back To Top](#index)
