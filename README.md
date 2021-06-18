# how-to-install-postgresql-on-ubuntu-20.04
how to install postgresql on ubuntu 20.04

## Install postgresql

```
sudo apt update
sudo apt install postgresql postgresql-contrib
```

check status postgresql
```
sudo service postgresql status
sudo pg_isready
```

access postgresql: You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
```
sudo -u postgres psql
\conninfo
\q
```
### change password posgtres
```
sudo -u postgres psql
alter user postgres password '261997';
psql -U postgres -h localhost
```



### create new user (should open postgres dashboard and click create user)
```
sudo -u postgres psql
CREATE USER nghiahsgs WITH PASSWORD '20101997';
CREATE DATABASE test_db;
GRANT ALL PRIVILEGES ON DATABASE test_db to nghiahsgs;
```

```
sudo -u postgres createuser --interactive
```

## Install pgAdmin4
```
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```
it will install apache2, ...pgadmin4
This script will configure Apache2 to serve the pgAdmin4 web application which involves enabling the WSGI module and configuring the pgAdmin application to mount at pgadmin4 on the webserver 
```
sudo apt install pgadmin4
sudo /usr/pgadmin4/bin/setup-web.sh
```

```
http://SERVER_IP/pgadmin4
```

#login
```
nghiahsgs@gmail.com
261997
```


#info server
```
user: postgres
pass: 261997
```

## Allow postgresql can connect remotely
```
cd /etc/postgresql/12/main
vi postgresql.conf
listen_addresses = '*'
wq
```

```
cd /etc/postgresql/12/main

vi pg_hba.conf
#host    all             all             127.0.0.1/32            md5
host    all             all             0.0.0.0/0            md5
wq
```

```
sudo service postgresql restart
```
