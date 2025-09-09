# PostgreSQL Setup on Ubuntu

[PostgreSQL](https://www.postgresql.org/) is a powerful open-source relational database. This guide covers installing PostgreSQL, creating a database, managing users, and connection strings.

---

## 1. Install PostgreSQL

```bash
sudo apt install -y postgresql postgresql-contrib
```

Enable and start the service:

```bash
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

Check status:

```bash
systemctl status postgresql
```

---

## 2. Access the PostgreSQL Shell

Switch to the default `postgres` user:

```bash
sudo -i -u postgres
```

Enter PostgreSQL:

```bash
psql
```

---

## 3. Create a Database and User

Inside the `psql` shell:

```sql
CREATE DATABASE mydb;
CREATE USER myuser WITH ENCRYPTED PASSWORD 'mypassword';
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;
\q
```

Exit back to your normal Ubuntu user:

```bash
exit
```

---

## 4. Connect with the New User

From Ubuntu:

```bash
psql -U myuser -d mydb -h localhost -W
```

- `-U myuser` → username
    
- `-d mydb` → database name
    
- `-h localhost` → host
    
- `-W` → prompt for password

---

## 5. Connection Strings

When connecting from your apps (Node.js, Python, etc.), you can use a connection string.

### PostgreSQL URI format

```
postgresql://<username>:<password>@<host>:<port>/<database>?schema=public
```

Example:

```
postgresql://myuser:mypassword@localhost:5432/mydb?schema=public
```

- `<username>` → your DB user (`myuser`)
    
- `<password>` → password (`mypassword`)
    
- `<host>` → server address (`localhost` or your EC2 public/private IP)
    
- `<port>` → PostgreSQL default port is `5432`
    
- `<database>` → database name (`mydb`)
    
- `?schema=public` → optional, if using ORMs that require schema

---

PostgreSQL is now installed, running, and ready for connections from both the shell and your applications.
