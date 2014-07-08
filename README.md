# A Virtual Machine for Tinkering with ConceptQL

## Introduction

Inspired by https://github.com/rails/rails-dev-box, this project automates the setup of a development environment for working with ConceptQL.

## Requirements

* [VirtualBox](https://www.virtualbox.org)
* [Vagrant 1.6+](http://vagrantup.com)

## How To Build The Virtual Machine

Building the virtual machine is this easy:

    host $ git clone https://github.com/outcomesinsights/conceptql-dev-box.git
    host $ cd conceptql-dev-box
    host $ vagrant up

Wait a while (there's a lot of data to load and programs to install).

That's it.

If the base box is not present that command fetches it first. The setup itself takes about 3 minutes in my MacBook Air. After the installation has finished, you can access the virtual machine with

    host $ vagrant ssh
    Welcome to Ubuntu 14.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)
    ...
    vagrant@rails-dev-box:~$

## What's In The Box

* Git
* RVM
* Ruby 2.1.2 (binary RVM install)
* Bundler
* PostgreSQL 9.3
* Databases and users needed to run the Active Record test suite
* [Sequelizer](https://github.com/outcomesinsights/sequelizer)
* [ConceptQL](https://github.com/outcomesinsights/conceptql)
* [Test ConceptQL](https://github.com/outcomesinsights/test_conceptql)

## Recommended Workflow

The recommended workflow is

* edit in the host computer and

* test within the virtual machine.

Just clone your Rails fork into the rails-dev-box directory on the host computer:

    host $ ls
    README.md   Vagrantfile puppet
    host $ git clone git@github.com:<your username>/rails.git

Vagrant mounts that directory as _/vagrant_ within the virtual machine:

    vagrant@rails-dev-box:~$ ls /vagrant
    puppet  rails  README.md  Vagrantfile

Install gem dependencies in there:

    vagrant@rails-dev-box:~$ cd /vagrant/rails
    vagrant@rails-dev-box:/vagrant/rails$ bundle

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

## License

Released under the MIT License, Copyright (c) 2012–<i>ω</i> Xavier Noria.
