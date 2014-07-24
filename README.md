PostgreSQL plugin for Dokku
---------------------------

Project: https://github.com/progrium/dokku

**Warning: This plugin is under development and still only tested with the below dependencies**

Requirements
------------
* Docker version `1.1.2` or higher
* Dokku version `0.2.1` or higher

Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/Kloadut/dokku-pg-plugin postgresql
dokku plugins-install
```


Commands
--------
```
$ dokku help
    pg:create <db>                         Create a PostgreSQL container
    pg:delete <db>                         Delete specified PostgreSQL container
    pg:dump <db> > dump_file.sql           Dump database data
    pg:info <db>                           Display database informations
    pg:link <app> <db>                     Link an app to a PostgreSQL database
    pg:list                                Display list of PostgreSQL containers
    pg:logs <db>                           Display last logs from PostgreSQL container
    pg:restore <db> < dump_file.sql        Restore database data from a previous dump
    pg:psql <db>                           Open interactive shell
```

Simple usage
------------

Create a new DB:
```
$ dokku postgresql:create foo            # Server side
$ ssh dokku@server postgresql:create foo # Client side

-----> PostgreSQL container created: postgresql/foo

       Host: 172.17.42.1
       User: 'root'
       Password: 'RDSBYlUrOYMtndKb'
       Database: 'db'
       Public port: 49187
```

Deploy your app with the same name (client side):
```
$ git remote add dokku git@server:foo
$ git push dokku master

```

Link your app to the database
```bash
dokku pg:link app_name database_name
```


Advanced usage
--------------

Initialize the database with SQL statements:
```
cat init.sql | dokku pg:create <db>
```

Deleting database:
```
dokku pg:delete <db>
```

Linking an app to a specific database:
```
dokku pg:link <db> <app>
```

PostgreSQL logs (per database):
```
dokku pg:logs <db>
```

Database information:
```
dokku pg:info <db>
```

List of containers:
```
dokku pg:list
```

Dump a database:
```
dokku pg:dump <db> > foo.sql
```

Restore a database:
```
dokku pg:restore <db> < foo.sql
```

Open interactive shell:
```
dokku pg:psql <db>
```
