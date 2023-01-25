<div align="center">
<h1>

`Jinja2`

</h1>

**TEMPLATING ENGINE**

</div>

---

<p id="#"></p>

### Write Expression
```html
	<div>
		<h2>Hello {{ name }}</h2>
	</div>
```
[Back To Top](#)

### Write Statements
```html
<div>
	{% for item in items %}
		<li> {{ item }} </li>
	{% endfor %}
</div>
```
[Back To Top](#)

### Template Inheritance
```html
<!--For Import Layout-->
{% include "header.html" %}

<!--For Import + Send Data-->
<!--base.html-->
<main class="">
   {% block main %}
		
   {% endblock %}
</main>

<!--home.html-->
{% extends "base.html" %}
{% block main %}
	<div class="">
		<h2>Home Page</h2>
	</div>
{% endblock %}
```
[Back To Top](#)

### Add Static Files From `static` Folder
```html
{% extends "base.html" %}
{% block style %}
	<link rel="stylesheet" href={{ url_for("static",filename="css/home.css") }} type="" />
{% endblock %}

{% block main %}
	<div class="">
		<h2>Home Page</h2>
	</div>
{% endblock %}
```
[Back To Top](#)

<!--### 
```html

```
[Back To Top](#)

-->