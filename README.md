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





