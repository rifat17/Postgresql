# Task List

- [ ] PostgreSQL Installation Process for Arch Linux and its derivatives.

# Getting Started
---
These instructions will help in installing Postgresql and running a Postgresql server in Arch Linux and its derivatives.

## Prerequisite

It's always a good idea to have an up to date system. We can update Arch Linux using the following command:

`sudo pacman -Syu`

## Installation

For Installing Postgresql on arch linux we can have to use the following command.

`sudo pacman -S postgresql`

## Initial configuration

To config a Postsql server we have to login as a `postgresql` user. To do that we have to use a simple command:

`sudo -iu postgres`
Now we have switched to postgresql user. After this step, we should be able to see posegresql user name as `postgres:~ $` , It might look slightly different based on terminal configuartion and shell.


Now we have to initialize a database cluster. Without the database cluster Pstgresql won't work. For that we have to use
`postgres:~ $ initdb -D /var/lib/postgres/data`
After successful execution of the command we will see the following lines of text

```
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgres/data ... ok
creating subdirectories ... ok
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting dynamic shared memory implementation ... posix
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

WARNING: enabling "trust" authentication for local connections
You can change this by editing pg_hba.conf or using the option -A, or
--auth-local and --auth-host, the next time you run initdb.

Success. You can now start the database server using:

    pg_ctl -D /var/lib/postgres/ -l logfile start
```

# Start the server
To Start postgresql server on Arch linux based distributions we have to use the following command.
`sudo systemctl enable --now postgresql.service`
This command will also bind postgresql service to startup so we don't have to restart the server again after a reboot.

## Create first user and database
Switched to postgresql user shown in [initial configuration](initial-configuration) and enter the following command to create the first user

`createuser --interactive`
Create a new database over which the above user has read/write privileges using the createdb command (execute this command from your login shell if the database user has the same name as your Linux user, otherwise add -O database-username to the following command):
`createdb myDatabaseName`

# Access the database shell
Become the postgres user. Start the primary database shell using psql command. Here you can do all your creation of databases/tables, deletion, set permissions, and run raw SQL commands. Use the -d option to connect to the database you created (without specifying a database, psql will try to access a database that matches your username).
`psql -d myDatabaseName`

## Optional configuration
For optional configuration such as Restricts access rights to the database superuser by default, please visit [https://wiki.archlinux.org/index.php/PostgreSQL#Optional_configuration](Arch wiki)

