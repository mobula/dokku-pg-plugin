PostgreSQL w/ PostGIS plugin for Dokku
--------------------------------------

> **Warning:** This plugin is under development and still only tested with the below dependencies

Based on [kloadut](https://github.com/Kloadut)'s **dokku-pg-plugin**: https://github.com/Kloadut/dokku-pg-plugin

Compared to kloadut's version:

  * commands follow the Heroku command format as much as possible, i.e, `dokku pg:create <db>` instead of `dokku postgres:create <db>`
  * Adds **postgis 2.1** support (in default branch `postgis2.1)
    - [x] Dockerfile
    - [ ] Dokku commands

> ###### Note
> Each database will be created in its own container.
> For single container, see jeffutter's https://github.com/jeffutter/dokku-postgresql-plugin


Requirements
------------
* Docker version `1.1.2` or higher
* Dokku version `0.2.3` or higher - Project: https://github.com/progrium/dokku


Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/mobula/dokku-pg-plugin postgresql
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
$ dokku pg:create foo            # Server side
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
