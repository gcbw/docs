<!--

********************************************************************************

WARNING:

    DO NOT EDIT "mariadb/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "mariadb/" combined with a set of templates)

********************************************************************************

-->

# Quick reference

-	**Maintained by**:  
	[MariaDB developer community](https://github.com/MariaDB/mariadb-docker)

-	**Where to get help**:  
	[Database Adminstrators (Stack Exchange)](https://dba.stackexchange.com/questions/tagged/docker+mariadb), [MariaDB Knowledge Base](https://mariadb.com/kb/en/docker-and-mariadb/) ([Ask a Question here](https://mariadb.com/kb/en/docker-and-mariadb/ask) available).

Also see the ["Getting Help with MariaDB" article on the MariaDB Knowledge Base](https://mariadb.com/kb/en/getting-help-with-mariadb/).

# Supported tags and respective `Dockerfile` links

-	[`10.7.1-focal`, `10.7-focal`, `10.7.1`, `10.7`](https://github.com/MariaDB/mariadb-docker/blob/d4efdb8951f606fe2837e9cc4db37225a5b7a621/10.7/Dockerfile)
-	[`10.6.5-focal`, `10.6-focal`, `10-focal`, `focal`, `10.6.5`, `10.6`, `10`, `latest`](https://github.com/MariaDB/mariadb-docker/blob/d711333929498046f354e14430cbe65e4767fc63/10.6/Dockerfile)
-	[`10.5.13-focal`, `10.5-focal`, `10.5.13`, `10.5`](https://github.com/MariaDB/mariadb-docker/blob/8414e4ff9ebff49f28148a860d85131e11c049c6/10.5/Dockerfile)
-	[`10.4.22-focal`, `10.4-focal`, `10.4.22`, `10.4`](https://github.com/MariaDB/mariadb-docker/blob/435a47c85a80be384524051f23cc3e8f132c31ff/10.4/Dockerfile)
-	[`10.3.32-focal`, `10.3-focal`, `10.3.32`, `10.3`](https://github.com/MariaDB/mariadb-docker/blob/a98e19f16db72ff1f6148cd797a0cb53dacacef3/10.3/Dockerfile)
-	[`10.2.41-bionic`, `10.2-bionic`, `10.2.41`, `10.2`](https://github.com/MariaDB/mariadb-docker/blob/9c804d5875d9faa880133b7720fdf7ccf35d6393/10.2/Dockerfile)

# Quick reference (cont.)

-	**Where to file issues**:  
	Issues can be filed on [https://jira.mariadb.org/](https://jira.mariadb.org/) under the "MDEV" Project and "Docker" Component, or on [GitHub](https://github.com/MariaDB/mariadb-docker/issues)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/mariadb/), [`arm64v8`](https://hub.docker.com/r/arm64v8/mariadb/), [`ppc64le`](https://hub.docker.com/r/ppc64le/mariadb/), [`s390x`](https://hub.docker.com/r/s390x/mariadb/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/mariadb/` directory](https://github.com/docker-library/repo-info/blob/master/repos/mariadb) ([history](https://github.com/docker-library/repo-info/commits/master/repos/mariadb))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images repo's `library/mariadb` label](https://github.com/docker-library/official-images/issues?q=label%3Alibrary%2Fmariadb)  
	[official-images repo's `library/mariadb` file](https://github.com/docker-library/official-images/blob/master/library/mariadb) ([history](https://github.com/docker-library/official-images/commits/master/library/mariadb))

-	**Source of this description**:  
	[docs repo's `mariadb/` directory](https://github.com/docker-library/docs/tree/master/mariadb) ([history](https://github.com/docker-library/docs/commits/master/mariadb))

# What is MariaDB?

MariaDB Server is one of the most popular database servers in the world. It’s made by the original developers of MySQL and guaranteed to stay open source. Notable users include Wikipedia, DBS Bank, and ServiceNow.

The intent is also to maintain high compatibility with MySQL, ensuring a library binary equivalency and exact matching with MySQL APIs and commands. MariaDB developers continue to develop new features and improve performance to better serve its users.

![logo](https://raw.githubusercontent.com/docker-library/docs/fe985dcb24154456254e252d1fa4a2b6b656ee80/mariadb/logo.png)

# How to use this image

## Start a `mariadb` server instance

Starting a MariaDB instance with the latest version is simple:

```console
$ docker run --detach --name some-mariadb --env MARIADB_USER=example-user --env MARIADB_PASSWORD=my_cool_secret --env MARIADB_ROOT_PASSWORD=my-secret-pw  mariadb:latest
```

or:

```console
$ docker network create some-network 
$ docker run --detach --network some-network --name some-mariadb --env MARIADB_USER=example-user --env MARIADB_PASSWORD=my_cool_secret --env MARIADB_ROOT_PASSWORD=my-secret-pw  mariadb:latest
```

... where `some-network` is a newly created network (other than `bridge` as the default network), `some-mariadb` is the name you want to assign to your container, `my-secret-pw` is the password to be set for the MariaDB root user. See the list above for relevant tags to match your needs and environment.

## Connect to MariaDB from the MySQL/MariaDB command line client

The following command starts another `mariadb` container instance and runs the `mysql` command line client against your original `mariadb` container, allowing you to execute SQL statements against your database instance:

```console
$ docker run -it --network some-network --rm mariadb mysql -hsome-mariadb -uexample-user -p
```

... where `some-mariadb` is the name of your original `mariadb` container (connected to the `some-network` Docker network).

This image can also be used as a client for non-Docker or remote instances:

```console
$ docker run -it --rm mariadb mysql -h <server container IP> -u example-user -p
```

That will give you a standard MariaDB prompt. You can test it with:

```console
MariaDB [(none)]> SELECT VERSION();
```

... which should give you the version. You can then use `exit` to leave the MariaDB command line client and the client container.

More information about the MariaDB command-line client can be found in the [MariaDB Knowledge Base](https://mariadb.com/kb/en/mysql-command-line-client/)

## ... via [`docker stack deploy`](https://docs.docker.com/engine/reference/commandline/stack_deploy/) or [`docker-compose`](https://github.com/docker/compose)

Example `stack.yml` for `mariadb`:

```yaml
# Use root/example as user/password credentials
version: '3.1'

services:

  db:
    image: mariadb
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
```

[![Try in PWD](https://github.com/play-with-docker/stacks/raw/cff22438cb4195ace27f9b15784bbb497047afa7/assets/images/button.png)](http://play-with-docker.com?stack=https://raw.githubusercontent.com/docker-library/docs/9efeec18b6b2ed232cf0fbd3914b6211e16e242c/mariadb/stack.yml)

Run `docker stack deploy -c stack.yml mariadb` (or `docker-compose -f stack.yml up`), wait for it to initialize completely, and visit `http://swarm-ip:8080`, `http://localhost:8080`, or `http://host-ip:8080` (as appropriate).

## Container shell access and viewing MariaDB logs

The `docker exec` command allows you to run commands inside a Docker container. The following command line will give you a bash shell inside your `mariadb` container:

```console
$ docker exec -it some-mariadb bash
```

The log is available through Docker's container log:

```console
$ docker logs some-mariadb
```

## Using a custom MariaDB configuration file

The startup configuration is specified in the file `/etc/mysql/my.cnf`, and that file in turn includes any files found in the `/etc/mysql/conf.d` directory that end with `.cnf`. Settings in files in this directory will augment and/or override settings in `/etc/mysql/my.cnf`. If you want to use a customized MariaDB configuration, you can create your alternative configuration file in a directory on the host machine and then mount that directory location as `/etc/mysql/conf.d` inside the `mariadb` container.

If `/my/custom/config-file.cnf` is the path and name of your custom configuration file, you can start your `mariadb` container like this (note that only the directory path of the custom config file is used in this command):

```console
$ docker run --name some-mariadb -v /my/custom:/etc/mysql/conf.d -e MARIADB_ROOT_PASSWORD=my-secret-pw -d mariadb:latest
```

This will start a new container `some-mariadb` where the MariaDB instance uses the combined startup settings from `/etc/mysql/my.cnf` and `/etc/mysql/conf.d/config-file.cnf`, with settings from the latter taking precedence.

### Configuration without a `cnf` file

Many configuration options can be passed as flags to `mysqld`. This will give you the flexibility to customize the container without needing a `cnf` file. For example, if you want to change the default encoding and collation for all tables to use UTF-8 (`utf8mb4`) just run the following:

```console
$ docker run --name some-mariadb -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mariadb:latest --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

If you would like to see a complete list of available options, just run:

```console
$ docker run -it --rm mariadb:latest --verbose --help
```

## Environment Variables

When you start the `mariadb` image, you can adjust the initialization of the MariaDB instance by passing one or more environment variables on the `docker run` command line. Do note that none of the variables below will have any effect if you start the container with a data directory that already contains a database: any pre-existing database will always be left untouched on container startup.

From tag 10.2.38, 10.3.29, 10.4.19, 10.5.10 onwards, and all 10.6 tags, the `MARIADB_*` equivalent variables are provided. `MARIADB_*` variants will always be used in preference to `MYSQL_*` variants.

One of `MARIADB_ROOT_PASSWORD`, `MARIADB_ALLOW_EMPTY_ROOT_PASSWORD`, or `MARIADB_RANDOM_ROOT_PASSWORD` (or equivalents, including `*_FILE`), is required. The other environment variables are optional.

### `MARIADB_ROOT_PASSWORD` / `MYSQL_ROOT_PASSWORD`

This specifies the password that will be set for the MariaDB `root` superuser account. In the above example, it was set to `my-secret-pw`.

### `MARIADB_ALLOW_EMPTY_ROOT_PASSWORD` / `MYSQL_ALLOW_EMPTY_PASSWORD`

Set to a non-empty value, like `yes`, to allow the container to be started with a blank password for the root user. *NOTE*: Setting this variable to `yes` is not recommended unless you really know what you are doing, since this will leave your MariaDB instance completely unprotected, allowing anyone to gain complete superuser access.

### `MARIADB_RANDOM_ROOT_PASSWORD` / `MYSQL_RANDOM_ROOT_PASSWORD`

Set to a non-empty value, like `yes`, to generate a random initial password for the root user. The generated root password will be printed to stdout (`GENERATED ROOT PASSWORD: .....`).

### `MARIADB_ROOT_HOST` / `MYSQL_ROOT_HOST`

This is the hostname part of the root user created. By default this is `%`, however it can be set to any default [MariaDB allowed hostname component](https://mariadb.com/kb/en/create-user/#host-name-component).

### `MARIADB_DATABASE` / `MYSQL_DATABASE`

This variable allows you to specify the name of a database to be created on image startup.

### `MARIADB_USER` / `MYSQL_USER`, `MARIADB_PASSWORD` / `MYSQL_PASSWORD`

These are used in conjunction to create a new user and to set that user's password. Both user and password variables are required for a user to be created. This user will be granted all access ([corresponding to `GRANT ALL`](https://mariadb.com/kb/en/grant/#the-all-privileges-privilege)) to the `MARIADB_DATABASE` database.

Do note that there is no need to use this mechanism to create the root superuser, that user gets created by default with the password specified by the `MARIADB_ROOT_PASSWORD` / `MYSQL_ROOT_PASSWORD` variable.

### `MARIADB_INITDB_SKIP_TZINFO` / `MYSQL_INITDB_SKIP_TZINFO`

By default, the entrypoint script automatically loads the timezone data needed for the `CONVERT_TZ()` function. If it is not needed, any non-empty value disables timezone loading.

## Docker Secrets

As an alternative to passing sensitive information via environment variables, `_FILE` may be appended to the previously listed environment variables, causing the initialization script to load the values for those variables from files present in the container. In particular, this can be used to load passwords from Docker secrets stored in `/run/secrets/<secret_name>` files. For example:

```console
$ docker run --name some-mysql -e MARIADB_ROOT_PASSWORD_FILE=/run/secrets/mysql-root -d mariadb:latest
```

Currently, this is only supported for `MARIADB_ROOT_PASSWORD`, `MARIADB_ROOT_HOST`, `MARIADB_DATABASE`, `MARIADB_USER`, and `MARIADB_PASSWORD` (and `MYSQL_*` equivalents of these).

# Initializing a fresh instance

When a container is started for the first time, a new database with the specified name will be created and initialized with the provided configuration variables. Furthermore, it will execute files with extensions `.sh`, `.sql`, `.sql.gz`, and `.sql.xz` that are found in `/docker-entrypoint-initdb.d`. Files will be executed in alphabetical order. `.sh` files without file execute permission are sourced rather than executed. You can easily populate your `mariadb` services by [mounting a SQL dump into that directory](https://docs.docker.com/engine/tutorials/dockervolumes/#mount-a-host-file-as-a-data-volume) and provide [custom images](https://docs.docker.com/reference/builder/) with contributed data. SQL files will be imported by default to the database specified by the `MARIADB_DATABASE` / `MYSQL_DATABASE` variable.

# Caveats

## Where to Store Data

Important note: There are several ways to store data used by applications that run in Docker containers. We encourage users of the `mariadb` images to familiarize themselves with the options available, including:

-	Let Docker manage the storage of your database data [by writing the database files to disk on the host system using its own internal volume management](https://docs.docker.com/engine/tutorials/dockervolumes/#adding-a-data-volume). This is the default and is easy and fairly transparent to the user. The downside is that the files may be hard to locate for tools and applications that run directly on the host system, i.e. outside containers.
-	Create a data directory on the host system (outside the container) and [mount this to a directory visible from inside the container](https://docs.docker.com/engine/tutorials/dockervolumes/#mount-a-host-directory-as-a-data-volume). This places the database files in a known location on the host system, and makes it easy for tools and applications on the host system to access the files. The downside is that the user needs to make sure that the directory exists, and that e.g. directory permissions and other security mechanisms on the host system are set up correctly.

The Docker documentation is a good starting point for understanding the different storage options and variations, and there are multiple blogs and forum postings that discuss and give advice in this area. We will simply show the basic procedure here for the latter option above:

1.	Create a data directory on a suitable volume on your host system, e.g. `/my/own/datadir`.
2.	Start your `mariadb` container like this:

	```console
	$ docker run --name some-mariadb -v /my/own/datadir:/var/lib/mysql -e MARIADB_ROOT_PASSWORD=my-secret-pw -d mariadb:latest
	```

The `-v /my/own/datadir:/var/lib/mysql` part of the command mounts the `/my/own/datadir` directory from the underlying host system as `/var/lib/mysql` inside the container, where MariaDB by default will write its data files.

## No connections until MariaDB init completes

If there is no database initialized when the container starts, then a default database will be created. While this is the expected behavior, this means that it will not accept incoming connections until such initialization completes. This may cause issues when using automation tools, such as `docker-compose`, which start several containers simultaneously.

## Usage against an existing database

If you start your `mariadb` container instance with a data directory that already contains a database (specifically, a `mysql` subdirectory), the `$MARIADB_ROOT_PASSWORD` variable should be omitted from the run command line; it will in any case be ignored, and the pre-existing database will not be changed in any way.

## Creating database dumps

Most of the normal tools will work, although their usage might be a little convoluted in some cases to ensure they have access to the `mysqld` server. A simple way to ensure this is to use `docker exec` and run the tool from the same container, similar to the following:

```console
$ docker exec some-mariadb sh -c 'exec mysqldump --all-databases -uroot -p"$MARIADB_ROOT_PASSWORD"' > /some/path/on/your/host/all-databases.sql
```

## Restoring data from dump files

For restoring data. You can use the `docker exec` command with the `-i` flag, similar to the following:

```console
$ docker exec -i some-mariadb sh -c 'exec mysql -uroot -p"$MARIADB_ROOT_PASSWORD"' < /some/path/on/your/host/all-databases.sql
```

# License

View [license information](https://mariadb.com/kb/en/library/licensing-faq/) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `mariadb/` directory](https://github.com/docker-library/repo-info/tree/master/repos/mariadb).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
