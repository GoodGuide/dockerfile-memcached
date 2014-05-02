goodguide-docker-memcached
======================


Base docker image to run a Memcached server


Usage
-----

To create the image `goodguide/memcached`, execute the following command on the root of this repo:

	docker build -t goodguide/memcached .

To run the image and bind to port 11211:

	docker run -d -p 11211:11211 goodguide/memcached

The first time that you run your container, a new user `memcached` with all privileges
will be created in Memcached with a random password. To get the password, check the logs
of the container by running:

	docker logs <CONTAINER_ID>

You will see an output like the following:

	========================================================================
    You can now connect to this Memcached server using:

          USERNAME:admin      PASSWORD:h0znMbk3RkM8

	Please remember to change the above password as soon as possible!
	========================================================================

In this case, `h0znMbk3RkM8` is the password assigned to the `admin` user.

Done!


Setting a specific password for the admin account
-------------------------------------------------

If you want to use a preset password instead of a random generated one, you can
set the environment variable `MEMCACHED_PASS` to your specific password when running the container:

	docker run -d -p 5432:5432 -e MEMCACHED_PASS="mypass" goodguide/memcached


Testing with Python
-------------------

First, install `bmemcached`. To do this, use pip or easy_install:

    pip install python-binary-memcached

Testing `goodguide/memcached`:

```python
>>> import bmemcached
>>> client = bmemcached.Client(('localhost:49154',),'admin','h0znMbk3RkM8')
>>> client.set('key','value')
True
>>> print client.get('key')
value
```

Mounting a file volume
---------------------------------

Coming soon!


Migrating an existing Memcached server
----------------------------------

Coming soon!
