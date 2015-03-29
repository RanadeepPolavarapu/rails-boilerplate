rails-boilerplate
=====================
A Ruby on Rails (RoR) boilerplate for quick rails app creation.

# Installation Steps

Step 1 - Install Core Essentials  
--------------------
    sudo apt-get -y update
    sudo apt-get -y upgrade
    sudo apt-get -y install build-essential git 

Step 2 - Install Python Prerequisites
---------------------------------------
Install fail2ban as well while we're at it for security:  

    sudo apt-get -y install python-pip python3-pip python-dev python3-dev virtualenv fail2ban

Step 3 - Install Ruby
--------------------
Install Ruby Version Manager ([rvm](https://rvm.io/)):  

	gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
	curl -sSL https://get.rvm.io | bash -s stable

List all known *Rubies* (versions and compilers of Ruby):  

	rvm list known

Install a version of Ruby:

	root@dev:~# rvm install 2.2.0
	Searching for binary rubies, this might take some time.
	No binary rubies available for: ubuntu/14.04/i386/ruby-2.2.0.
	Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
	Checking requirements for ubuntu.
	Requirements installation successful.
	Installing Ruby from source to: /usr/local/rvm/rubies/ruby-2.2.0, this may take a while depending on your cpu(s)...
	ruby-2.2.0 - #downloading ruby-2.2.0, this may take a while depending on your connection...
	ruby-2.2.0 - #extracting ruby-2.2.0 to /usr/local/rvm/src/ruby-2.2.0....
	ruby-2.2.0 - #applying patch /usr/local/rvm/patches/ruby/2.2.0/fix_installing_bundled_gems.patch.
	ruby-2.2.0 - #configuring.........................................................
	ruby-2.2.0 - #post-configuration..
	ruby-2.2.0 - #compiling...............................................................................
	ruby-2.2.0 - #installing............................
	ruby-2.2.0 - #making binaries executable..
	ruby-2.2.0 - #downloading rubygems-2.4.6
	ruby-2.2.0 - #extracting rubygems-2.4.6.....
	ruby-2.2.0 - #removing old rubygems.........
	ruby-2.2.0 - #installing rubygems-2.4.6.....................
	ruby-2.2.0 - #gemset created /usr/local/rvm/gems/ruby-2.2.0@global
	ruby-2.2.0 - #importing gemset /usr/local/rvm/gemsets/global.gems...........................................................
	ruby-2.2.0 - #generating global wrappers........
	ruby-2.2.0 - #gemset created /usr/local/rvm/gems/ruby-2.2.0
	ruby-2.2.0 - #importing gemsetfile /usr/local/rvm/gemsets/default.gems evaluated to empty gem list
	ruby-2.2.0 - #generating default wrappers........
	ruby-2.2.0 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
	Install of ruby-2.2.0 - #complete 
	Ruby was built without documentation, to build it run: rvm docs generate-ri
	Making gemset ruby-2.2.0 pristine............................................................
	Making gemset ruby-2.2.0@global pristine..............................................................
	root@dev:~#

Do a Ruby version check:  

	root@dev:~$ ruby -v
	ruby 2.2.0p0 (2014-12-25 revision 49005) [i686-linux]

NOTE: Ruby installation takes a couple minutes. It is not as quick as Golang and Node.js so be patient.

To upgrade RVM itself do:

	rvm get stable
	rvm cleanup all


Step 4 - Install Rails
-----------------------
Install Ruby on Rails with no Ruby Documentation (`rdoc`) or Ruby Interactive (`ri`):
	
	sudo gem install --no-rdoc --no-ri rails

Step 5 - Install PostgreSQL
----------------------------
Feel free to use MySQL however, I highly prefer PostgreSQL.

	sudo apt-get install postgresql postgresql-contrib libpq-dev

Create a custom `railsadmin` user in PostgreSQL and specify a custom password:  
Use `dropuser` if you mess up.  

    postgres@dev:~$ createuser -P railsadmin
    Enter password for new role: 
    Enter it again: 
    postgres@dev:~$ 

Create a PostgreSQL Database:

	postgres@dev:~$ psql
	psql (9.4.1)
	Type "help" for help.

	postgres=# CREATE DATABASE myrailsapp;
	CREATE DATABASE
	postgres=# \l
	                                  List of databases
	    Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
	------------+----------+----------+-------------+-------------+-----------------------
	 myrailsapp | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
	 postgres   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
	 template0  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
	            |          |          |             |             | postgres=CTc/postgres
	 template1  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
	            |          |          |             |             | postgres=CTc/postgres
	(4 rows)

	postgres=# GRANT ALL PRIVILEGES ON DATABASE myrailsapp TO postgres;
	GRANT
	postgres=# GRANT ALL PRIVILEGES ON DATABASE myrailsapp TO railsadmin;
	GRANT
	postgres=# \l
	                                   List of databases
	    Name    |  Owner   | Encoding |   Collate   |    Ctype    |    Access privileges    
	------------+----------+----------+-------------+-------------+-------------------------
	 myrailsapp | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =Tc/postgres           +
	            |          |          |             |             | postgres=CTc/postgres  +
	            |          |          |             |             | railsadmin=CTc/postgres
	 postgres   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
	 template0  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres            +
	            |          |          |             |             | postgres=CTc/postgres
	 template1  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres            +
	            |          |          |             |             | postgres=CTc/postgres
	(4 rows)

