### Where to Store Data

> Important note: There are several ways to store data used by applications that run in Docker containers. We encourage users of the mysql images to familiarize themselves with the options available, including:

Let Docker manage the storage of your database data by writing the database files to disk on the host system using its own internal volume management⁠. This is the default and is easy and fairly transparent to the user. The downside is that the files may be hard to locate for tools and applications that run directly on the host system, i.e. outside containers.

Create a data directory on the host system (outside the container) and mount this to a directory visible from inside the container⁠. This places the database files in a known location on the host system, and makes it easy for tools and applications on the host system to access the files. The downside is that the user needs to make sure that the directory exists, and that e.g. directory permissions and other security mechanisms on the host system are set up correctly.

Create a data directory on a suitable volume on your host system, e.g. /my/own/datadir.

Start your mysql container like this:

> docker run --name some-mysql -v /my/own/datadir:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

```
docker run --name sswamyn-mysql8 -v /Users/swamysivasubramaniyan/home/repo/sql/learning_sql/mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-sql-pwd -d mysql:8.4.7
```
The -v /my/own/datadir:/var/lib/mysql part of the command mounts the /my/own/datadir directory from the underlying host system as /var/lib/mysql inside the container, where MySQL by default will write its data files.
source: https://hub.docker.com/_/mysql

