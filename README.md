Setup a boiler plate Rails instance quickly with Vagrant and Ansible. The Ansible playbooks can also be used to deploy to a real production server in a similar fashion.


## Getting started

The following steps to provision a *development* instance of **newapp**.  

Clone this repo to a new vagrant-newapp folder:
```
git clone https://github.com/yorkulibraries/vagrant-newapp.git vagrant-newapp
```

Change into the vagrant-newapp directory:
```
cd vagrant-newapp
```

Clone the [ansible-rails](https://github.com/yorkulibraries/ansible-rails) project:
```
git clone https://github.com/yorkulibraries/ansible-rails.git
```

Install the Ansible dependencies.

```
ansible-galaxy install -r requirements.yml
```

Bring up the box with RAILS_ENV=development (this is the default):

```
vagrant up
```

Watch for any error/failed tasks. If all is good then the instance is ready to use for testing.


Edit /etc/hosts and add an entry like followed so you can access the app from a browser at http://newapp.me.ca/

```
192.168.56.168 newapp.me.ca
```

## Verifying emails are sent in development

In development environment, mails are "caught" by MailCatcher. You can see all the emails by going to the MailCatcher web interface at http://newapp.me.ca:1080/


## Making changes

**NOTE: Assuming you have provisioned the box with the default RAILS_ENV=development.**

The directory **/home/newapp/newapp** in the box is a *symlink* to **/vagrant/newapp**, which is a synced folder in the your local machine's **vagrant-newapp** folder.
You can make changes on your local machine in **vagrant-newapp/newapp** folder and it is changed in the vagrant box too. 

## Running unit tests

**NOTE: Assuming you have provisioned the box with the default RAILS_ENV=development.**

SSH into the box as user **newapp**
```
ssh newapp@127.0.0.1 -p2222
cd newapp
RAILS_ENV=test bundle exec rake db:reset
RAILS_ENV=test bundle exec rake test
```
