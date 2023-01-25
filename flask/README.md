<h1 align="center">
Flask Notes
</h1>

<p id="index"></p>

* [Flask App Structure](#Structure)
* [Flask App](#App)
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
* [Flask Mail](#Mail)
* [Flask SQLite](#SQLite)
* [Flask SQLAlchemy](#SQLAlchemy)

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

<p id="Json"></p>

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
@app.route('/search/<name>')  
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

