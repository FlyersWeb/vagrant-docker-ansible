README
======

A vagrant shipped with a docker shipped with an ansible provisioning an nginx.

Introduction
------------

I've made a post on my blog about what would be my best development environment to start a fresh project. I tried to explain that it would be a mix of all that great stuff pushing up as of **vagrant** virtual machine, **docker** container system and **ansible** provisioning. To know more about it, go check http://goo.gl/ZRudPl.

Docker drawbacks
----------------

Docker is an amazing tool but I thing it as some drawbacks. First of all it do not works on every linux systems, you need a minimum kernel version. You'll also need to **install some extra kernel modules** for it to work. The other main drawback for docker is that the "provisioning" tool shipped by default **work only inside a docker image**. If someday you need to install your images outside a docker image you won't be able to do it.

How it works
------------

That is why I've created this project to show you how you can create a Vagrant virtual machine for your project. So what did this project contains :
  1. install an ``ubuntu trusty`` virtual machine shipped with docker (see Vagrantfile)
  2. share the docker-ansible-nginx folder containing a Dockerfile with an ``ubuntu vivid`` image.
  3. ship in this docker image the ``ansible playbook`` to install a ``nginx server`` inside of it
  4. allows you to edit only the playbook to ship what you want in your docker image or elsewhere

How to use it
-------------

Launch the vagrant and log in

```
vagrant up && vagrant ssh
```

Add the necessary ansible roles

```
cd docker-ansible-nginx
ansible-galaxy install geerlingguy.nginx -p .
```

Build your docker images

```
cd docker-ansible-nginx
docker build -t docker-ansible-nginx .
```

Run your image

```
docker run -it --rm docker-ansible-nginx
```

Conclusion
----------

This is just a demonstration of such a development environment. I recommend you to use a more stable docker container project such as [William-Yeh/docker-ansible](https://github.com/William-Yeh/docker-ansible).

By combining the best of these tools, you can easily create your necessary development environment for your projects. Using ansible allows you to deploy them with the same exact version on your production servers.

Have fun. Flyers.
