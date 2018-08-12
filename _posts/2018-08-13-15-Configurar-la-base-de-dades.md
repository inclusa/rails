---
layout: post # Sustituye el layout si lo usas uno diferente
title: 15 Configurar la base de dades # Nombre generado automáticamente
---

Hi ha tres maneres de configurar la base de dades:

- library_development
- library_production
- library_test

Per a inicialitzar la base de dades necessitem privilegis de **root**.

# Configurar la base de dades en MySQL

```bash
ysql> create database library_development;
Query OK, 1 row affected (0.01 sec)

mysql> grant all privileges on library_development.*
to 'root'@'localhost' identified by 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

# Configurar database.yml

`dtabase.yml` roman a `library/config`.

```bash
development:
   adapter: mysql
   database: library_development
   username: root
   password: [password]
   host: localhost
	
test:
   adapter: mysql
   database: library_test
   username: root
   password: [password]
   host: localhost
   
production:
   adapter: mysql
   database: library_production
   username: root
   password: [password]
   host: localhost
```

# Configurar la base de date per a PostgreSQL

Creem l'usuari:

```bash
sudo -u postgres createuser rubyuser -s
```

Elegim un password:

```bash
sudo -u postgres psql

postgres=# \password rubyuser
```

Creem una base de dades de desenvolupament:

```bash
postgres=# CREATE DATABASE library_development OWNER rubyuser;

CREATE DATABASE
```

Creem una base de dades de producció:

```bash
postgres=# CREATE DATABASE library_development OWNER rubyuser;

CREATE DATABASE
```

Creem la base de dades de test:

```bash
postgres=# CREATE DATABASE library_test OWNER rubyuser;

CREATE DATABASE
```

Per tal de tancar PostgreSQL cal presionar `Ctrl + D`.

# Configurar database.yml

Trobarem aquest arxiu ací: `library/config`.

Contindrà aquesta informació:

```bash
default: &default
   adapter: postgresql
   encoding: unicode

development:
   adapter: postgresql
   encoding: unicode
   database: library_development
   username: rubyuser
   password: <Password for rubyuser>

test:
   adapter: postgresql
   encoding: unicode
   database: library_test
   username: rubyuser
   password: <Password for rubyuser>

production:
   adapter: postgresql
   encoding: unicode
   database: library_production
   username: rubyuser
   password: <Password for rubyuser>
```


