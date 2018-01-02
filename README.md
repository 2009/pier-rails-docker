# Docker Compose for PIER Rails applications

## Setup

Clone and build the `ruby-mysql-socket` image:

```
git clone git@github.com:2009/ruby-mysql-socket.git
cd ruby-mysql-socket
docker build -t ruby-mysql-socket .
```

Clone the database repo and start it running:

```
git clone git@github.com:2009/mariadb-docker.git mariadb
cd mariadb
docker-compose up -d
```

> NOTE: Mysql data is stored in the `mysql` directory, you can copy
> existing mysql data `/var/lib/mysql` to this folder.

Clone the elasticsearch repo and start it running:

```
git clone git@github.com:2009/elasticsearch-docker-compose.git elasticsearch
cd elasticsearch
docker-compose up -d
```

Copy the `docker-compose.yml` file into the root of the rails
application and update the external port by changing `3000:3000`
to `<desired-port-to-access-app>:3000`.

## Running

First bring up the app containers (mariadb must be started first):

```
docker-compose up -d
```

Now we can run commands in the docker container by using the following:

```
docker-compose exec app bundle install
docker-compose exec app rails s -b 0.0.0.0
docker-compose exec bundle exec rake db:migrate
```

## Fresh container instance

```
docker-compose down
```
