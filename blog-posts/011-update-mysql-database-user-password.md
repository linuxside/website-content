---
title: Update MySQL/MariaDB user password
date: 2022-04-15
updated: 2022-10-18
tags: cli, mysql
url: update-mysql-database-user-password
---

Identify a MySQL/MariaDB user and change its password.

---

From time to time, it is advised to change user's passwords as a security measure.

> If you have reason to believe your password has been stolen, you should change it, and make sure you change it on all of your accounts where you use the same or a similar password.  
> ...  
> If you think you might have just given your password to a phishing website, change it. If your current password is weak, change it. If it will make you feel better or if you just feel like it’s time for a change, then by all means go ahead and change your password.
{: class="blockquote bg-light text-muted mt-5 px-3 pt-3 pb-1"}

*-- [Time to rethink mandatory password changes](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2016/03/time-rethink-mandatory-password-changes){class="text-info"}*{class="text-muted d-block mb-5"}

1. Login to MySQL/MariaDB

**Note:** This command must be run as root, hence the `sudo` in front of it.

```bash
sudo mysql -u root -p
```

and press ENTER

2. List all users

```sql
SELECT User, Host FROM mysql.user;
```

Sample output:

```text
+---------------------+-----------+
| User                | Host      |
+---------------------+-----------+
| mysql_user          | localhost |
| debian-sys-maint    | localhost |
| mysql.infoschema    | localhost |
| mysql.session       | localhost |
| mysql.sys           | localhost |
| root                | localhost |
+---------------------+-----------+
9 rows in set (0.00 sec)
```

In our case, the user is `mysql_user`.

3. Update the user password

```sql
ALTER USER 'mysql_user'@'localhost' IDENTIFIED BY 'new_mysql_password';
```

Make sure you change the `mysql_user` with a user that you have and the `new_mysql_password` with a [strong password](https://www.expressvpn.com/password-generator).

**Resources:**
- [Create a new MySQL user and grant permissions]({{ route('blog_post', {'url': 'create-mysql-database-and-user'}) }})
- [When is Flush Privileges in MySQL really needed?](https://stackoverflow.com/a/47155873/9618184)
