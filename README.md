# Tiny Library Information Management System

## Introduction

**Now it's on development.**

The repository is a Database Curriculum Design.

It's based on _**Python**_, _**Django**_ and _**MySQL**_.

## File Structure
<details>
<summary>File Structure Info</summary>

```
LibraryInfoManager
├── ConnectionTemplate.py
├── Django
│   ├── Book
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── BookType
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── Borrow
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── Django
│   │   ├── asgi.py
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── template
│   │   │   ├── base.html
│   │   │   ├── footer.html
│   │   │   ├── header.html
│   │   │   └── static
│   │   │       ├── MainPanel.html
│   │   │       ├── ManageBook.html
│   │   │       ├── ManageBookType.html
│   │   │       ├── ManageBorrow.html
│   │   │       ├── ManagePublisher.html
│   │   │       ├── ManageUsers.html
│   │   │       ├── OrderBook.html
│   │   │       ├── SignIn.html
│   │   │       ├── SignUp.html
│   │   │       └── UserProfile.html
│   │   ├── urls.py
│   │   └── wsgi.py
│   ├── MainPanel
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── manage.py
│   ├── Publisher
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   ├── urls.py
│   │   └── views.py
│   └── Users
│       ├── apps.py
│       ├── forms.py
│       ├── __init__.py
│       ├── models.py
│       ├── tests.py
│       ├── urls.py
│       └── views.py
├── InitDBToolkit.py
├── Initialize.bat
├── Initialize.sh
├── lib
│   ├── encrypt.py
│   └── utils.py
├── LICENSE
├── README.md
├── requirements.txt
├── SQLs
│   ├── InitDatabase.sql
│   └── InitData.sql
└── Test.py

12 directories, 73 files
```
</details>

## Table Structure

> The Bold properties are primary keys. And the Italic properties are foreign keys.

- Publisher(**PublisherID**, publisher_name)
- BookType(**BookTypeID**, book_type_name)
- Book(**ISBN**, book_name, author, location, status, _book_type_id_, _publisher_id_)
- Users(**UserID**, name, nickname, password, tel, is_admin, is_staff, is_active, last_login, trustworthiness, max_borrow_day, max_borrow_count)
- Borrow(**OperationID**, borrow_time, status, give_back_time, _book_id_, _user_id_)

<details>

```sql
mysql> desc Publisher;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| PublisherID    | int         | NO   | PRI | NULL    | auto_increment |
| publisher_name | varchar(40) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> desc BookType;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| BookTypeID     | int         | NO   | PRI | NULL    | auto_increment |
| book_type_name | varchar(40) | NO   |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
2 rows in set (0.01 sec)

mysql> desc Book;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| ISBN         | varchar(20) | NO   | PRI | NULL    |       |
| book_name    | varchar(40) | NO   |     | NULL    |       |
| author       | varchar(40) | NO   |     | NULL    |       |
| location     | varchar(20) | NO   |     | NULL    |       |
| status       | varchar(5)  | NO   |     | NULL    |       |
| book_type_id | int         | NO   | MUL | NULL    |       |
| publisher_id | int         | NO   | MUL | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
7 rows in set (0.00 sec)

mysql> desc Users;
+------------------+---------------+------+-----+---------+----------------+
| Field            | Type          | Null | Key | Default | Extra          |
+------------------+---------------+------+-----+---------+----------------+
| UserID           | int           | NO   | PRI | NULL    | auto_increment |
| name             | varchar(40)   | NO   |     | NULL    |                |
| nickname         | varchar(20)   | NO   |     | NULL    |                |
| password         | varchar(1024) | NO   |     | NULL    |                |
| tel              | varchar(11)   | NO   |     | NULL    |                |
| is_admin         | tinyint(1)    | NO   |     | NULL    |                |
| is_staff         | tinyint(1)    | NO   |     | NULL    |                |
| is_active        | tinyint(1)    | NO   |     | NULL    |                |
| last_login       | datetime(6)   | NO   |     | NULL    |                |
| trustworthiness  | int           | YES  |     | NULL    |                |
| max_borrow_day   | int           | YES  |     | NULL    |                |
| max_borrow_count | int           | YES  |     | NULL    |                |
+------------------+---------------+------+-----+---------+----------------+
12 rows in set (0.01 sec)

mysql> desc Borrow;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| OperationID    | int         | NO   | PRI | NULL    | auto_increment |
| borrow_time    | datetime(6) | NO   |     | NULL    |                |
| status         | varchar(8)  | NO   |     | NULL    |                |
| give_back_time | datetime(6) | NO   |     | NULL    |                |
| book_id        | varchar(20) | NO   | MUL | NULL    |                |
| user_id        | int         | NO   | MUL | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
6 rows in set (0.00 sec)
```

<summary>The Structure of each table</summary>
</details>

## Credit System

> The max value of the credit is 100, and the min value is 0.

- When the book(s) got damaged, the user would lose 25. 
- When the book(s) got lost, the user have to compensate for the book. If not, he/she will get 0 credit. 
- When the book(s) got back late, the user would lose 10. And of course, if he/she didn't give back for too long, this scene would be seen as the book(s) got lost. 
- Only when the book(s) got back, the user could get 1.

**What's the Credit used for?**:

The credit can effect the max count of book(s) you can borrow and the longest time you can borrow book(s) for as well.

$$
\begin{aligned}
UserMaxCount &= \lfloor \frac{credit}{100} \times MaxCount \rfloor \\
UserLongestTime &= \lfloor \frac{credit}{100} \times LongestTime \rfloor
\end{aligned}
$$


## Usage

To use it, you shall run InitDBToolkit first. 

The next step is to Initial the database, run `sh Initialize.sh` in Linux System or double click `Initialize.bat` in Windows System.

Then run `python Django/manage.py runserver`.

_**(On development so that the left are unconsidered.)**_