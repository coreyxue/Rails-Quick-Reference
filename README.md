Rails-Quick-Reference
=====================

#Setting Up Postgres
--------------------
#switch to user postgres, if do not know password run: "$sudo passwd postgres" to set the password
$su - postgres
#enter psql env
$psql
#create role
create role ROLENAME with createdb login password 'PASSWORD'
#switch back
$su ubuntu

#To create a new rails application using postgresql
---------------------------------------------------
$rails new myapp --database=postgresql

#modify yml file
development:
  adapter: postgresql
  encoding: unicode
  database: myapp_development
  host: localhost   #<-----important
  pool: 5
  username: ROLENAME
  password: PASSWORD

test:
  adapter: postgresql
  encoding: unicode
  database: myapp_test
  pool: 5
  username: ROLENAME
  password: PASSWORD

production:
  adapter: postgresql
  encoding: unicode
  database: myapp_production
  pool: 5
  username: ROLENAME
  password: PASSWORD
#create modle
rake db:migrate
  
#Deploy to heroku
-----------------
git init
git add .
git commit -m "eh"
heroku create
git push heroku master
heroku run rake db:migrate
(heroku run rake db:seed)
