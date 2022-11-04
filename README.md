REDMINE INSTALLTION

IN TERMINAL CREATE SPECIAL FOLDER FOR REDMINE USING FOLLOWING COMMOND
```
cd /var/
sudo mkdir data
cd data/
sudo mkdir redmine
cd redmine 
```
download the redmine version of your choice.

https://www.redmine.org/projects/redmine/wiki/Download

```
sudo chown -R User /var/data/redmine 
```
copy files from redmine downloaded folder var/data/redmine/remine folder

Install mysql and other packages
```
sudo apt install mysql-server mysql-client apache2 build-essential patch ruby-dev zlib1g-dev liblzma-dev libmysqlclient-dev libmagickwand-dev 
```

```
sudo -i
mysql
mysql> CREATE DATABASE redmine CHARACTER SET utf8mb4;
mysql>CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'password';
mysql>GRANT ALL ON redmine.* TO 'redmine'@'localhost';
```

copy database.ymlexample content in database.yml
```
cd config 
touch database.yml
```
database.yml
```
production:
  adapter: mysql2
  database: redmine
  host: localhost
  username: redmine 
  password: "password"
  # Use "utf8" instead of "utfmb4" for MySQL prior to 5.7.7
  encoding: utf8mb4
```
```
bundle install
bundle exec rake generate_secret_token
RAILS_ENV=production  bundle exec rake db:migrate
RAILS_ENV=production bundle exec rake redmine:load_default_data
```
To start rails server :
```
bundle exec rails server -b 127.0.0.1 -e production
```
