# A Virtual Machine for Tinkering with ConceptQL

## Introduction

Inspired by [rails-dev-box](https://github.com/rails/rails-dev-box), this project automates the setup of a development environment for working with ConceptQL.

## Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant 1.6+](http://vagrantup.com)
* [Ansible 1.6+](http://www.ansible.com/home)
* Download the [OMOP Vocabulary Files](http://vocabbuild.omop.org/vocabulary-release) then **unzip them and rename them to conceptql-dev-box/omop_vocab**
    * I can't ship them myself because they contain "restricted" vocabularies like CPT codes
    * Sorry for the inconvenience!
* Download the following [Oracle Instant Client Files](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html) then **move them into oracle_instant_client_zip_files**:
  - instantclient-basic-linux.x64-11.2.0.4.0.zip
  - instantclient-sdk-linux.x64-11.2.0.4.0.zip
  - instantclient-sqlplus-linux.x64-11.2.0.4.0.zip


## How To Build The Virtual Machine

Building the virtual machine is this easy:

    host $ git clone https://github.com/outcomesinsights/conceptql-dev-box.git
    host $ cd conceptql-dev-box
    host $ vagrant up

Wait a while (there's a lot of data to load and programs to install).

That's it.

If there are any errors, retry the provisioning step:

    host $ vagrant provision

If it keeps failing at the same spot, [open up an issue](https://github.com/outcomesinsights/test_conceptql/issues/new)

After the installation has finished, you can access the virtual machine with

    host $ vagrant ssh
    Welcome to Ubuntu 14.04 LTS (GNU/Linux 3.13.0-30-generic x86_64)
    ...
    vagrant@conceptql-dev-box:~$

## What's In The Box

* Git
* RVM
* Ruby 2.1.2 (binary RVM install)
* Bundler
* PostgreSQL 9.3
* Databases and users needed to run the Active Record test suite
* [Sequelizer](https://github.com/outcomesinsights/sequelizer)
* [loadmop](https://github.com/outcomesinsights/loadmop)
* [ConceptQL](https://github.com/outcomesinsights/conceptql)
* [Test ConceptQL](https://github.com/outcomesinsights/test_conceptql)

## What to Play With

You may play with ConceptQL directly, or with its testing framework

### Playing with ConceptQL

ConceptQL comes with a command-line utility: `conceptql`.  This [Thor](http://whatisthor.com)-based script can be run by typing
    vagrant@conceptql-dev-box:/vagrant/conceptql$ bundle exec concepql

With no arguments, you'll get a list of the commands provided by the `conceptql` script.

The commands you run will execute against a sample of 250 patients' worth of synthetic data.

### Playing with ConceptQL's Tests

The other option is to run the tests in `/vagrant/test_conceptql`.  See [Test ConceptQL](https://github.com/outcomesinsights/test_conceptql) for instructions on how to run the tests.

## Recommended Workflow

The recommended workflow is

* edit in the host computer and

* test within the virtual machine.

Just clone your ConceptQL fork into the conceptql-dev-box directory on the host computer:

    host $ ls
    README.md   Vagrantfile puppet
    host $ git clone git@github.com:<your username>/conceptql.git

Vagrant mounts that directory as _/vagrant_ within the virtual machine:

    vagrant@conceptql-dev-box:~$ ls /vagrant
    ansible  conceptql test_conceptql omop_vocab README.md  Vagrantfile LICENSE.txt

Install gem dependencies in there:

    vagrant@conceptql-dev-box:~$ cd /vagrant/conceptql
    vagrant@conceptql-dev-box:/vagrant/conceptql$ bundle

We are ready to go to edit in the host, and test in the virtual machine.

This workflow is convenient because in the host computer you normally have your editor of choice fine-tuned, Git configured, and SSH keys in place.

## Virtual Machine Management

When done just log out with `^D` and suspend the virtual machine

    host $ vagrant suspend

then, resume to hack again

    host $ vagrant resume

Run

    host $ vagrant halt

to shutdown the virtual machine, and

    host $ vagrant up

to boot it again.

You can find out the state of a virtual machine anytime by invoking

    host $ vagrant status

Finally, to completely wipe the virtual machine from the disk **destroying all its contents**:

    host $ vagrant destroy # DANGER: all is gone

Please check the [Vagrant documentation](http://docs.vagrantup.com/v2/) for more information on Vagrant.

## Thanks
- Xavier Noria's [rails-dev-box](https://github.com/rails/rails-dev-box)
    - For the inspiration (and for being a great way to hack on Rails)!
- [Outcomes Insights, Inc.](http://outins.com)
    - Many thanks for allowing me to release a portion of my work as Open Source Software!
