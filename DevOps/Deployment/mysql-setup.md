MySQL Setup on Ubuntu

[MySQL](https://www.mysql.com/) is a widely-used relational database. This guide covers installing MySQL, creating a database and user, and connection strings for applications.

---

## 1. Install MySQL

```bash
sudo apt install -y mysql-server
```

Enable and start the service:

```bash
sudo systemctl enable mysql
sudo systemctl start mysql
```

Check status:

```bash
systemctl status mysql
```

---

## 2. Secure MySQL Installation

Run the security script:

```bash
sudo mysql_secure_installation
```

Follow the prompts to:

- Set root password (if not set)
    
- Remove anonymous users
    
- Disallow remote root login
    
- Remove test database
    
- Reload privilege tables

---

## 3. Access MySQL Shell

```bash
sudo mysql -u root -p
```

Enter the password you set during `mysql_secure_installation`.

---

## 4. Create a Database and User

Inside the MySQL shell:

```sql
CREATE DATABASE mydb;
CREATE USER 'myuser'@'%' IDENTIFIED BY 'mypassword';
GRANT ALL PRIVILEGES ON mydb.* TO 'myuser'@'%';
FLUSH PRIVILEGES;
EXIT;
```

- `%` allows connections from any host. You can restrict it to `localhost` if needed.
    

---

## 5. Connect with the New User

From Ubuntu:

```bash
mysql -u myuser -p -h localhost mydb
```

---

## 6. Connection Strings

When connecting from applications, use a MySQL URI.

### MySQL URI format

```
mysql://<username>:<password>@<host>:<port>/<database>
```

Example:

```
mysql://myuser:mypassword@localhost:3306/mydb
```

- `<username>` → DB user (`myuser`)
    
- `<password>` → password (`mypassword`)
    
- `<host>` → server address (`localhost` or your EC2 public/private IP)
    
- `<port>` → MySQL default port `3306`
    
- `<database>` → database name (`mydb`)

---

MySQL is now installed, running, and ready for app connections.
