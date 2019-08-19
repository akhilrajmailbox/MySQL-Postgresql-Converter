# MySQL Postgresql Converter

[configuration](https://github.com/akhilrajmailbox/MySQL-Postgresql-Converter/blob/master/pdf-files/mysql-postgresql-converter.pdf)



## Example : migration of redmine mysql database to postgresql database (redmine-01)

( use these steps only after migrating mysql database to postgresql  database by using mysql2psql )

### Step-1

edit the configuration file of redmine
(change mysql configuration into postgresql)
#### nano /etc/redmine/default/database.yml


production: 
  adapter: postgresql 
  database: redmine 
  host: host 
  port: 5432 
  username: username
  password: passwd
  encoding: utf8 
  schema_search_path: public

### Step-2

#### cd [redmine home] 

need to add two depenencies for postgresql connection

```
nano Gemfile.local
```

`gem 'activerecord-postgresql-adapter'`
`gem 'pg'`

### Step-3

install dependency for new ruby version and update older version into ruby 2.x

```
apt-get install -y apache2 php5 libapache2-mod-php5 mysql-server php5-mysql libapache2-mod-perl2 libcurl4-openssl-dev libssl-dev apache2-prefork-dev libapr1-dev libaprutil1-dev libmysqlclient-dev libmagickcore-dev libmagickwand-dev curl git-core gitolite patch build-essential bison zlib1g-dev libssl-dev libxml2-dev libxml2-dev sqlite3 libsqlite3-dev autotools-dev libxslt1-dev libyaml-0-2 autoconf automake libreadline6-dev libyaml-dev libtool imagemagick apache2-utils ssh zip libicu-dev libssh2-1 libssh2-1-dev cmake libgpg-error-dev subversion libapache2-svn git nano tar unzip libdbd-pg-ruby

apt-get -y install  software-properties-common
add-apt-repository ppa:brightbox/ruby-ng 
apt-get update 
apt-get -y install ruby2.1 ruby-switch ruby2.1-dev ri2.1 libruby2.1 libssl-dev zlib1g-dev 
ruby-switch --set ruby2.1 
gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 

curl -sSL https://get.rvm.io | bash -s stable 
/bin/bash -l -c "rvm install 2.1.4"
```

#### update the gem and install postgresql adapter

```
gem update 
gem install bundler 
gem install pg 
gem install activerecord-postgresql-adapter
```

### Step-4

run the bundle install for connecting postgresql database

```
bundle install
```

### Step-5

start the service

```
service apache2 restart
```
