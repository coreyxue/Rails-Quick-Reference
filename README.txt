Rails-Quick-Reference
=====================

#Setting Up Postgres
--------------------
#switch to user postgres, if do not know password run: "$sudo passwd postgres" to set the password
$ su - postgres
#enter psql env
$ psql
#create role
create role ROLENAME with createdb login password 'PASSWORD'
#switch back
$ su ubuntu

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

#Setup heroku
-------------
$ [sudo] gem install heroku
$ heroku keys:add

#Deploy to heroku
-----------------
$ git init
$ git add .
$ git commit -m "eh"
$ heroku create
$ git push heroku master
$ heroku run rake db:migrate
$ (heroku run rake db:seed)

#-- config gem file ---
source 'https://rubygems.org'
gem 'rails', '3.2.3'
group :development do
gem 'sqlite3'
end
# Gems used only for assets and not required
# in production environments by default.
group :assets do
gem 'sass-rails', '3.2.4'
gem 'coffee-rails', '3.2.2'
gem 'uglifier', '1.2.3'
end
gem 'jquery-rails', '2.0.0'
group :production do
gem 'pg'
end
--->$bundle install --without production
