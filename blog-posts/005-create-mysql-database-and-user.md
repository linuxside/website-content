---
title: Create a MySQL/MariaDB database and user
date: 2021-10-05
updated: 2022-04-02
tags: cli, mysql
url: create-mysql-database-and-user
---

Set up a new database with a new user that has access to a specific database or all databases.

---

This tutorial will help you set up a new database with a new user that has access to a specific database or all databases.

**Note:** Make sure you change `new_mysql_database`, `new_mysql_user` and `new_mysql_password` with something of your own and [create a strong password](https://www.expressvpn.com/password-generator).

**Use the root user ONLY for administration purposes. By using the root user on production, you risk of having a system-wide security hole.**

1. Login to MySQL/MariaDB

**Note:** This command must be run as root, hence the `sudo` in front of it.

```bash
sudo mysql -u root -p
```

and press ENTER

2. Create the database

```sql
CREATE DATABASE new_mysql_database;
```

3. Create the user

```sql
CREATE USER 'new_mysql_user'@'localhost' IDENTIFIED BY 'new_mysql_password';
```

4. Grant all privileges to a specific database

```sql
GRANT ALL PRIVILEGES ON new_mysql_database.* TO 'new_mysql_user'@'localhost';
```

5. Grant all privileges to all databases (only if necessary)

```sql
GRANT ALL PRIVILEGES ON *.* TO 'new_mysql_user'@'localhost';
```

6. Grant usage privileges to all databases (only if necessary)

```sql
GRANT USAGE ON *.* TO 'new_mysql_user'@'localhost';
```

7. Flush the privileges

```sql
FLUSH PRIVILEGES;
```

8. Check the new user (optional)

```sql
SHOW GRANTS FOR 'new_mysql_user'@'localhost';
```

**Resources:**
- [Create a New User and Grant Permissions in MySQL](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql)
