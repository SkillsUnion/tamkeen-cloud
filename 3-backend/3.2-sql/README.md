# 3.2: SQL

## Learning Objectives

1. Define SQL and explain its role as a query language for relational databases.
2. Describe the fundamental concepts of relational databases, including tables, relations, and data representation.
3. Demonstrate the ability to set up and use psql, the PostgreSQL command-line client.
4. Execute basic SQL commands to create tables, insert data, and query information from a PostgreSQL database.
5. Analyze the structure of SQL table creation commands, including column definitions, data types, and constraints.

## Introduction

SQL (Structured Query Language) is a robust, mature and the most popular query language for relational databases. We use SQL to store, manage, and retrieve data from relational databases, aka SQL databases.

A relational database is a database composed of "relations", also known as tables. Tables are like spreadsheet tables with headers in the first row, each identifying the data that will be in its respective column.&#x20;

A primary strength of relational databases is their ability to represent relationships in data. For example, in a social media app I might have a `users` table and a `posts` table, and a relational database would be able to represent that each post belongs to a user, and that a user has many posts.

## PostgreSQL

PostgreSQL (aka "Postgres") is a popular and robust SQL dialect that is both lightweight and feature-rich. Other popular SQL dialects include MySQL (heavy, feature-rich) and SQLite (light, less feature-rich).

Postgres is also a database server application that we will use to store and retrieve data for our apps using the Postgres language. Postgres is typically run on its own server in production for modularity (multiple apps may want to access this DB) and security (different security rules for our DB vs API server).

## Intro to Database Servers

Database servers run applications that allow programs to manipulate the data inside them. In this module we'll learn how to create, manage, and deploy database servers. Note that this is separate from managing the _data_ inside the database, which is done by the SQL language. How SQL interacts with the database server hard drive depends on the particular SQL implementation.

Part of setting up a database is setting up database schema, i.e. what tables and columns are in the database. Web applications typically do not manipulate database schema in response to user actions; application code depends on database schema, but the schema is not defined by the application.

![The data in the database is stored separately from the application code](<../../.gitbook/assets/spaces_-MHpn6_lq7F3sPVKqyNy_uploads_git-blob-b91d82b347ba55676fd0db8808960cae14874017_SQL database.jpeg>)

Unlike with the `data.json` file we used prior to SQL, the data inside our database will _not_ be part of the application repo. Database servers are often on separate machines from web application servers, such that they can be accessed by multiple applications. We will see this when we use Heroku, but for now, we will keep our database server on the same machine as our Express app.

![The PostgreSQL server is typically on a separate machine from the web application that accesses it. ](../../.gitbook/assets/spaces_-MHpn6_lq7F3sPVKqyNy_uploads_git-blob-cdcc69229a31bfe19ec50389a5880edc8509b390_Postgres.jpeg)

Managing the database server application, e.g. ports, backups, version upgrades, is typically considered developer operations or DevOps and can be a separate role from application development.

## Intro to PostgreSQL

Postgres implements the SQL language in order to store and retrieve data from a set of files on the hard drive.

Postgres is a server application that uses its own TCP/IP protocol, usually on port 5432 (although this is configurable). Requests are sent to the server that contain the SQL language queries for the server to process. The result of the queries is sent back to the client.

Postgres is a software implementation of a database system. So far we've only dealt with a database at a conceptual level, and using that database though SQL.

However, a database system is the actual implementation of something that runs SQL and keeps the data. Each system implements the SQL language slightly differently, keeps the data on the disk in a slightly different way, and gets the data back out differently.

The database system ensures fundamental database properties like <a href="https://en.wikipedia.org/wiki/ACID" target="_blank">ACID</a> (atomicity, consistency, isolation, durability). A database system needs to account for circumstances like when two opposing queries happen at the same time, or like when a long running INSERT query fails while executing, due to something like power failure. The system doesn't solve these problems, but it is guaranteed to behave in a consistent manner each time.

A database system also includes functionality like automatic data backup and database indexes for increasing query speed.

## psql setup

psql is the Postgres command-line client to access our databases. To help us learn SQL we will use `psql` to manipulate our databases with SQL commands. In later modules we will use a SQL client that allows us to manipulate our databases using a GUI.

### Mac

Install <a href="https://postgresapp.com" target="_blank">postgres.app</a>. Open the application and follow the setup instructions on the website. Do the optional step to configure `$PATH` to use included command line tools.

{% include youtube.html id="cEOe6WRAhRE" %}
Installing Postgres Mac


### Ubuntu (for Windows users in WSL and EC2 Installation)

Install Postgres

```
sudo apt update
sudo apt upgrade
sudo apt install postgresql
sudo apt install postgresql-client
```

Set the Postgres server to start in the background:

```
sudo service postgresql start
```

Set password-less login by opening pg_hba.conf and copying the below contents into it.&#x20;

<mark style="color:red;">**Note**</mark>

The command below assumes you've installed postgresql version 12, **you may need to alter the commands to accommodate a newer version of postgres** depending on which version you've installed.

```bash
// Postgres Version 12
sudo chmod 777 /etc/postgresql/12/main/pg_hba.conf

// Postgres Version 14
sudo chmod 777 /etc/postgresql/14/main/pg_hba.conf
```

```bash
# "sudo" runs the command as the root user
# "$(which code)" gets the location of the VSCode application locally

sudo "$(which code)" /etc/postgresql/12/main/pg_hba.conf
```

If the above command doesn't work, try running VSCode without `sudo`.

For the next command to work you will need to have the code command installed on your machine.

```bash
# Open pg_hba.conf in VSCode

// Postgres Version 12
code /etc/postgresql/12/main/pg_hba.conf
```

The above will open a new VSCode window.

`pg_hba.conf` contents to copy: (replace the whole file contents with the lines below)

```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# IPv4 local connections:
local    all            all                                     trust
host     all            all             127.0.0.1/32            trust
# IPv6 local connections:
host     all            all             ::1/128                 trust
```

Restart Postgres to get the new configs:

```
sudo service postgresql restart
```

Login as the user `postgres` - the default root user for the Postgres database. This system user was created when you installed Postgres.

```
sudo su postgres
psql postgres
```



## Basic SQL Commands

When creating your database within PostgreSQL you will need to be armed with some knowledge, namely the ability to create tables, insert information and subsequently query that dataset. In this section we will explore how we can interface with our database through the command line interface.



#### Starting PostgreSQL (Mac)

The first step is to start your PostgreSQL server and open a CLI window. For Mac users goto the applications toolbar and find this logo:

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>PostgreSQL logo</p></figcaption></figure>

Click on it, it will start up the PostgreSQL server and it will open a window that is similar to below, you may need to click start on when selecting a Postgres instance:

<figure><img src="../../.gitbook/assets/Screenshot 2023-01-04 at 10.16.47 AM.png" alt=""><figcaption><p>PostgreSQL Mac GUI</p></figcaption></figure>

From this panel select a database, here we have highlighted the fruit database, once you click on it a terminal window will appear:

<figure><img src="../../.gitbook/assets/Screenshot 2023-01-04 at 10.19.21 AM.png" alt=""><figcaption><p>PostgreSQL terminal window</p></figcaption></figure>

From this window we can interface with Postgres using SQL as well as PostgreSQL commands. We are currently accessing the fruit database and will only be able to query tables within that database from here.&#x20;



#### Starting PostgreSQL (Ubuntu - Windows)

To interface with PostgreSQL through your command line (Ubuntu) first open a new Ubuntu instance, then execute these commands:

```
sudo service postgresql start
sudo su postgres
psql postgres
```



In both Mac and Windows what we are doing is starting the PostgreSQL server on our computer, then we are making a connection to a particular database on the server. The commands above first start the PostgreSQL service, specifies that we are running PostgreSQL commands and then connects to the default PostgreSQL database.

#### Making your user

Create a user and database named after your Ubuntu user.&#x20;

Use the Postgres `CRATE USER` command to create a new Postgres database user that is named the same as your current user.

```
CREATE USER <my_user> WITH SUPERUSER CREATEDB CREATEROLE LOGIN;
```

Create a default Postgres database named after your current user. We will use DBs named after our usernames to test SQL syntax. Once we start building applications with SQL, we will name our DBs after our applications.

```
CREATE DATABASE <my_user>;
```

#### Common PostgreSQL commands

When you have connected to a PostgreSQL database you can easily list all of your databases, users or current tables:

List all of the databases on this PostgreSQL server:

```
\l
```

When you run this command in the current window you will get a table that contains all of the current databases and pertinent information regarding it.



Change the current window to another database:

```
\c <db-name>

// example command below

\c samoshaughnessy
```

The command above would change the current window to another database, in this case one named samoshaughnessy, this users database.



Another useful command is to list out all of the tables within the current database context.

```
\dt
```

The command above will generate a table which contains information about each table.



To list out all of the users you can use the command below:

```
\du
```



In order to create a new database you can use the command below:

```
CREATE DATABASE new_database;
```

You can alter the name of the databases by chnage the value `new_database` to your desired database name.&#x20;

#### Creating a table

After connecting to the appropriate database we can use the CREATE TABLE statement to develop a new table within the database. In the example below we will create a new table named students that contains a few columns regarding student information. Try to create this table within the users database.

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    mobile INT,
    gender BOOLEAN
    );
    
```

This command generates a table that contains five columns, an auto-incrementing identity column, id, two character columns first_name, last_name. This is followed by two additional columns mobile and gender which have the datatype of integer and boolean respectively. We are generating columns by naming the column, then adding a datatype with any column constraints that we need to implement. You can alter the datatype and constraints by changing the arguments to the code above. To see what PostgreSQL datatypes you can insert please checkout <a href="https://www.postgresql.org/docs/current/datatype.html" target="_blank">this documentation</a>. If you want to checkout the constraints <a href="https://www.postgresql.org/docs/current/ddl-constraints.html" target="_blank">click here</a>.

#### <mark style="color:red;">SQL NOTE</mark>

It should be noted that we must end the command with a semicolon otherwise PostgreSQL will not register that the command is complete.



#### Data Insertion

Inserting data into tables is the next step in database creation, the code below demonstrates an insertion query that will add a new row of data into the previously generated student table.


```sql
INSERT INTO students (first_name, last_name, mobile, gender) VALUES ('Foong', 'Leung', 9987712, true);
```


We entered a new student into the database, notice how we didn't need to insert an id, this is due to the SERIAL constraint we added when creating our table. These id's act a <a href="https://www.postgresql.org/docs/15/ddl-constraints.html#DDL-CONSTRAINTS-PRIMARY-KEYS" target="_blank">Primary Keys</a> which are vital unique identifiers for our rows of data. The  information that is required is the data that will be placed in our columns for this row, the two strings, a number and  the final value a boolean, true, true represents male within this table structure.

You can add in additional rows of information one at a time or you can insert multiple values like the command below.


```sql
INSERT INTO students (first_name, last_name, mobile, gender) VALUES ('Sam', 'O"Shaughnessy', 2781192, true), ('Neo', 'Yuan', 4366813, true) ;
```




#### Data Querying

When working with databases, it is important that you can query information such that you're able to manipulate, retrieve and delete data. You are able to do this from your command line interface and this is the next step in hands on database management. Querying data is dependant on specificity and targeting the correct information. You can select information from a database by table, row or under a condition, we will showcase a few of these commands below.


```sql
// Selecting by Table
SELECT * FROM students;
// This will return all of the enteries from the students table

SELECT first_name, last_name FROM students;
// This will return all of the data within the columns first_name and last_name from the students table

// Selecting by Row
SELECT * FROM students WHERE id = 1;
// This will return the row with an id of 1 from the students table

// Selecting by Condition
SELECT * FROM students WHERE gender = false;
// This will return all of the rows where gender is false.
```




To alter existing data within the tables you can use the UPDATE or DELETE commands paired with the WHERE claus that we saw in the previous code block. It should be noted that you can use logical operations like greater than or less than, read more about this <a href="https://www.postgresql.org/docs/current/functions-comparison.html" target="_blank">here</a>. Checkout the code block below to see how you can update and remove information inside a table.




```sql
// Update a row by ID
UPDATE students SET first_name = 'Neo Kai', mobile = 86739984 WHERE id = 3;

// Update a row by column value
UPDATE students SET first_name = 'Neo Kai', mobile = 86739984 WHERE first_name = 'Neo';

// Deleting data using id
DELETE FROM students WHERE id = 1;

// Deleting data using condition
DELETE FROM students WHERE gender = true; 
```




#### SQL relationships&#x20;

Creating tables and inserting data allows you to create some structure for data within your database. To really showcase meaningful information within a database, tables should have relationships and in more complex instances data could depend on other sets. To showcase this we will develop another table student_addresses.




```sql
CREATE TABLE student_addresses (
    id SERIAL PRIMARY KEY,
    student_id INT,
    address VARCHAR(255),
    CONSTRAINT fk_student_id
    FOREIGN KEY (student_id)
    REFERENCES students(id)    
);
```


The above command will generate a new table that contains three columns, an id, a student_id which is referencing data in our students table and our address column. In this instance we have to ensure that data is present within the students table before we can add any data into students_addresses this is because we are referencing an id within the students table for every entry within student_addresses. If you want to read more about foreign keys please look into <a href="https://www.javatpoint.com/postgresql-foreign-key" target="_blank">this set of documentation</a>.&#x20;

Once you have developed a database that contains multiple tables that have relationships you will be able to query with what are known as join clauses. Joins allow you to select from multiple tables, the returned information will only return the information that satisfies all of the criteria. To find out more about joins please look into this <a href="https://www.geeksforgeeks.org/sql-join-set-1-inner-left-right-and-full-joins/" target="_blank">set of documentation</a>. Check out the command below:


```sql
SELECT * FROM students JOIN student_addresses ON students.id = student_addresses.student_id WHERE gender = false;
```


This will produce the most common join the inner join. Which means you will only be returned records that have matching values within both tables. We have also added an additional claus further refining the search to only show the female students who have an address within the students_addresses table. It should be noted that the returned table that contains our information will not persist and you will need to run the query above to get the data.



## Post-Class Exercises: Codecademy Learn SQL

Complete all exercises in the following Codecademy lessons when they are assigned in the Rocket course schedule.

The following exercises introduce basic SQL syntax. We will not write much SQL during Rocket because we will rely on ORMs (Object-Relational Mappings) such as Sequelize to construct SQL using JavaScript for more robust applications. However, it is relevant to know SQL syntax and some companies test for it during interviews.

1. <a href="https://www.codecademy.com/courses/learn-sql/lessons/manipulation/exercises/sql" target="_blank">Manipulation</a>
2. <a href="https://www.codecademy.com/courses/learn-sql/lessons/queries/exercises/queries" target="_blank">Queries</a>
3. <a href="https://www.codecademy.com/courses/learn-sql/lessons/aggregate-functions/exercises/intro" target="_blank">Aggregate Functions</a>
4. <a href="https://www.codecademy.com/courses/learn-sql/lessons/multiple-tables/exercises/intro" target="_blank">Multiple Tables</a> (left joins, cross joins, unions and "with" syntax are more niche and less important for Bootcamp, but may be helpful in data analyst work)

## Additional Resources

1. Codecademy SQL cheatsheets for <a href="https://www.codecademy.com/learn/paths/learn-sql/tracks/learn-sql/modules/learn-sql-manipulation/cheatsheet" target="_blank">Manipulation</a>, <a href="https://www.codecademy.com/learn/paths/learn-sql/tracks/learn-sql/modules/learn-sql-queries/cheatsheet" target="_blank">Queries</a>, <a href="https://www.codecademy.com/learn/paths/learn-sql/tracks/learn-sql/modules/learn-sql-aggregate-functions/cheatsheet" target="_blank">Aggregate Functions</a> and <a href="https://www.codecademy.com/learn/paths/learn-sql/tracks/learn-sql/modules/learn-sql-multiple-tables/cheatsheet" target="_blank">Multiple Tables</a>
2. <a href="https://www.youtube.com/watch?v=gu980iXwY5c" target="_blank">This CS50 video</a> explains common SQL syntax
3. <a href="https://developer.okta.com/blog/2019/07/19/mysql-vs-postgres" target="_blank">Article on when to choose MySQL vs Postgres</a>
4. <a href="https://en.wikipedia.org/wiki/ACID" target="_blank">ACID properties</a> required of all production databases
