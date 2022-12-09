# Task 7: Implementing the Persistance Layer with MySQL

## Description

For this task, we'll be implementing the database of your application using MySQL.

## Walkthrough

### Step 1: Using MySQL Workbench to implement the database structure

> #### Useful Resources for this step
>
> - [MySQL Workbench Tutorial: complete guide to the RDBMS tool](https://www.educative.io/blog/mysql-workbench-tutorial)

In this step, we'll create a EER Model to represent the application data layer.

1. Create a database in your MySQL workbench called either "items" or "posts"

   <img src="https://i.gyazo.com/0ffaf27f9a9d93a950a9940100d32ec6.png">


### Step 2: Create the credentials that you will give to Spring Data JPA in Task 8

In this step, we'll add a user on the MySQL server that we will allow Spring Data JPA to use in order to create and manage our table/entries.

1.  In your MySQL workbench, add a new user with administrator permissions. Remember the password you set as you will need it for our next task.

    <img src="https://i.gyazo.com/aa3dab20b72deb7006786c913f004311.png" />

### Step 3: Finalize the columns that each entry in your database will have.

1. What fields do you need for every entry in your database table? We will need to know this before continuing on to the next task.


<strong>Results:</strong>

Congratulations! Now you should be able to see a database called either item or post in your MySQL workbench as well as a user with DBA (DataBase Administrator) permissions.
