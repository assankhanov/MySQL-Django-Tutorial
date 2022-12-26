<br />
<p align="center">
    <img src="images/logo.PNG" alt="Logo" width="290" height="128">
  </a>

  <h3 align="center">MySQL-Django-Tutorial</h3>
  <p align="center">
   Simple tutorial how create Django application, connect it to MySQL Database and perform MySQL queries in Django application.
  </p>
</p>

## 1. Download MySQL
- Go to this URL -> https://dev.mysql.com/downloads/mysql/
- Press “Go to download page” and download second installer


## 2. Install MySQL
- Lunch downloaded file (for example: mysql-installer-community-8.0.27.0.exe)
- Key points:
    - While choosing the setup type, select the “Developer Default” option
    - Enter the MySQL Root password which will be strong and which you can remember
![step2](images/step2.PNG)


## 3. Initializing a new virtual environment 
3.1. Create working directory 
(in this example it is a folder called “project”)

3.2. Open the working directory from PyCharm
 
3.3. Click on “Terminal” which is located at bottom left side in PyCharm

3.4. Create virtual environment called “projectEnv”

```
$ python3 -m venv .projectEnv
```

3.5. Activate the virtual environment

```
$ .projectEnv\Scripts\activate.bat
```

<img src="images/step3.PNG" alt="step3" width="525" height="349">

## 4. Installing Django and MySQL client
4.1. Install Django packages
```
$ pip install django
```
<img src="images/step4.1.PNG" alt="step4.1" width="255" height="41">


4.2. Install MySQL client for python
```
$ pip install mysqlclient
```
<img src="images/step4.2.PNG" alt="step4.2" width="274" height="41">

## 5. Create the new Django project
Start Django project called “category” using django-admin tool
```
$ django-admin startproject category 
```
After that our current working directory should look like this:

![step5](images/step5.PNG)


## 6. Change to project folder
6.1. Mark the project directory as root: Right click on project folder -> Mark Directory as -> Sources Root
![step6.1](images/step6.1.PNG)

6.2. Change into project directory in terminal
```
$ cd category 
```
![step6.2](images/step6.2.PNG)

## 7. Create the new Django application
Create Django application called “myApp”
```
$ python manage.py startapp myApp 
```

![step7](images/step7.PNG)

Then, our working directory will look like this:

![step7.2](images/step7.2.PNG)

## 8. Registering myApp application
Open settings.py file add the new created application myApp to INSTALLED_APPS

![step8](images/step8.PNG)


## 9. Testing the website framework 
9.1. Running database migrations:
```
$ python manage.py makemigrations 
```
```
$ python manage.py migrate
```

![step9](images/step9.1.PNG)

9.2. Running the server:
```
$ python manage.py runserver
```

The development server can be accessed at 
http://127.0.0.1:8000/
Here we can see that website framework was set up successfully: 
![step9](images/step9.3.PNG)


## 10. Creating MySQL Database
10.1. Open the MySQL Workbench and click on ⊕ button

10.2. Set up the connection name(here the name is “test”) and press ok
![step10.12](images/step10.12.PNG)

10.3. Double click on created connection “test” 

10.4. Enter the password of the root and click “OK”

10.5. Create database called “categoryDB” and press the button  
```
create database categoryDB;
```
![step10.12](images/step10.345.PNG)

10.6. By clicking on update button we can see the new created database “categoryDB”

10.7. Double click on “categoryDB”

![step10.67](images/step10.67.PNG)

10.8. Create table called “Categories” and press the button
```
CREATE TABLE Categories (categoryID INT  NOT NULL, categoryName VARCHAR(50), categoryDescription CHAR(100), PRIMARY KEY (categoryID));
```

10.9. By pressing update button we can see that our table “Categories” is created
![step10.89](images/step10.89.PNG)

10.10. Add records “Categories” table 
```
INSERT INTO Categories (categoryID, categoryName,categoryDescription)
VALUES (1, 'Beverages', 'Soft drinks, coffees, teas, beers, and ales'), (2, 'Condiments', 'Sweet and savory sauces, relishes, spreads, and seasonings'), (3, 'Confections', 'Desserts, candies, and sweet breads'),(4, 'Dairy Products', 'Cheeses'),(5, 'Grains/Cereals', 'Breads, crackers, pasta, and cereal'),(6, 'Meat/Poultry', 'Prepared meats'),(7, 'Produce', 'Dried fruit and bean curd'),(8, 'Seafood', 'Seaweed and fish');
```
![step10.10](images/step10.10.PNG)

10.11. In order to see the records in the table:
Right click on category->SelectRows
![step10.11](images/step10.11.PNG)


## 11. Connecting MySQL database to Django project

11.1. Open settings.py file and set up configurations of mySQL database “categoryDB”
![step11.1](images/step11.1.PNG)

11.2. Run database migrations:
```
$ python manage.py migrate
```

## 12. Defining custom SQL queries in views 
First, we need to set up the views.py. 
Define the function “display” as following:

views.py
```python
from django.shortcuts import render
from django.db import connection

def display(request):
    outputCategories = []
    outputOfQuery1 = []
    with connection.cursor() as cursor:
        sqlQueryCategories = "SELECT categoryid, categoryname, categorydescription FROM categories;"
        cursor.execute(sqlQueryCategories)
        fetchResultCategories = cursor.fetchall()

        sqlQuery1 = "SELECT categoryname, categorydescription FROM categories WHERE categoryid=7;"
        cursor.execute(sqlQuery1)
        fetchResultQuery1 = cursor.fetchall()

        connection.commit()
        connection.close()

        for temp in fetchResultCategories:
            eachRow = {'categoryid': temp[0], 'categoryname': temp[1], 'categorydescription': temp[2]}
            outputCategories.append(eachRow)

        for temp in fetchResultQuery1:
            eachRow = {'categoryname': temp[0], 'categorydescription': temp[1]}
            outputOfQuery1.append(eachRow)

    return render(request, 'myApp/index.html',{"categories": outputCategories, "output1": outputOfQuery1})
```

## 13. Creating templates
13.1. In settings.py add path to “templates” which will store the templates used by application 

13.2. In the myApp directory, create templates directory and inside of it create another directory which will have same name as the application

13.3. Then right click on new created directory “myApp”-> Press New->HTML File

13.4. Name it as “index” and press enter
![step13](images/step13.PNG)

13.5. Add the following to index.html

index.html
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Categories Database:</title>
</head>
<body>
<h2>Categories table</h2>
<table>
    <thead>
        <tr>
        <th>category id</th>
        <th>category name</th>
        <th>category description</th>
    </tr>
    </thead>
{% for category in categories %}
    <tr>
        <td>{{ category.categoryid }}</td>
        <td>{{ category.categoryname }}</td>
        <td>{{ category.categorydescription }}</td>
    </tr>
{% endfor %}
</table>
<br>
<br>
<h2>Example query result:</h2>
<table>
    <thead>
        <tr>
            <th>category name</th>
            <th>category description</th>
    </tr>
    </thead>
{% for i in output1 %}
    <tr>
        <td>{{ i.categoryname }}</td>
        <td>{{ i.categorydescription }}</td>
    </tr>
{% endfor %}
</table>
</body>
</html>
```

## 14. Creating URLs
After that,we need to create urls in urls.py to have access to views. 
Update the urls.py file as following:

urls.py
```python
from django.urls import path
from myApp import views

urlpatterns = [
    path('', views.display, name='index'),
]
```

## 15. Run the development server
Running the server:
```
$ python manage.py runserver
```
We should get following output:

![step15](images/stepfinal.PNG)