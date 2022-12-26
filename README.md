# MySQL-Django-Tutorial
Simple tutorial how create Django application, connect it to MySQL Database and perform MySQL queries in Django application.


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
![step3](images/step3.PNG)


## 4. Installing Django and MySQL client
4.1. Install Django packages
```
$ pip install django
```
![step4.1](images/step4.1.PNG)

4.2. Install MySQL client for python
```
$ pip install mysqlclient
```
![step4.2](images/step4.2.PNG)


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
$ create database categoryDB;
```
![step10.12](images/step10.345.PNG)

10.6. By clicking on update button we can see the new created database “categoryDB”

10.7. Double click on “categoryDB”
![step10.67](images/step10.67.PNG)

10.8. Create table called “Categories” and press the button
```
$ CREATE TABLE Categories (categoryID INT  NOT NULL, categoryName VARCHAR(50), categoryDescription CHAR(100), PRIMARY KEY (categoryID));
```

10.9. By pressing update button we can see that our table “Categories” is created
![step10.89](images/step10.89.PNG)

10.10. Add records “Categories” table 
```
$ INSERT INTO Categories (categoryID, categoryName,categoryDescription)
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




