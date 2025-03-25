:original_name: dcs-ug-0312012.html

.. _dcs-ug-0312012:

Connecting to Redis on ioredis (Node.js)
========================================

This section describes how to access a Redis instance on ioredis. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

.. note::

   The operations described in this section apply only to single-node, master/standby, and Proxy Cluster instances. To access a Redis Cluster instance on ioredis, see `Node.js Redis client description <https://github.com/NodeRedis/cluster-key-slot>`__.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__
-  If the ECS runs the Linux OS, ensure that the GCC compilation environment has been installed on the ECS.

Connecting to Redis on ioredis
------------------------------

-  **For client servers running Ubuntu (Debian series):**

#. .. _dcs-ug-0312012__en-us_topic_0148195323_li5233248151213:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Install Node.js.

   .. code-block::

      apt install nodejs-legacy

   If the preceding command does not work, run the following commands:

   .. code-block::

      wget https://nodejs.org/dist/v0.12.4/node-v0.12.4.tar.gz --no-check-certificate
      tar -xvf node-v4.28.5.tar.gz
      cd node-v4.28.5
      ./configure
      make
      make install

   .. note::

      After the installation is complete, run the **node --version** command to query the Node.js version to check whether the installation is successful.

#. Install the node package manager (npm).

   .. code-block::

      apt install npm

#. Install the Redis client ioredis.

   .. code-block::

      npm install ioredis

#. Edit the sample script for connecting to a DCS Redis instance.

   Add the following content to the **ioredisdemo.js** script, including information about connection and data reading.

   .. code-block::

      var Redis = require('ioredis');
      var redis = new Redis({
        port: 6379,          // Redis port
        host: '192.168.0.196',   // Redis host
        family: 4,           // 4 (IPv4) or 6 (IPv6)
        password: '******',
        db: 0
      });
      redis.set('foo', 'bar');
      redis.get('foo', function (err, result) {
        console.log(result);
      });
      // Or using a promise if the last argument isn't a function
      redis.get('foo').then(function (result) {
        console.log(result);
      });
      // Arguments to commands are flattened, so the following are the same:
      redis.sadd('set', 1, 3, 5, 7);
      redis.sadd('set', [1, 3, 5, 7]);
      // All arguments are passed directly to the redis server:
      redis.set('key', 100, 'EX', 10);

   *host* indicates the example IP address/domain name of the DCS instance and *port* indicates the port number of the DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312012__en-us_topic_0148195323_li5233248151213>`. Change them as required. ``******`` indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

#. Run the sample script to access the chosen DCS Redis instance.

   .. code-block::

      node ioredisdemo.js

-  **For client servers running CentOS (Red Hat series):**

#. .. _dcs-ug-0312012__en-us_topic_0148195323_li11511175651212:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Install Node.js.

   .. code-block::

      yum install nodejs

   If the preceding command does not work, run the following commands:

   .. code-block::

      wget https://nodejs.org/dist/v0.12.4/node-v0.12.4.tar.gz --no-check-certificate
      tar -xvf node-v0.12.4.tar.gz
      cd node-v0.12.4
      ./configure
      make
      make install

   .. note::

      After the installation is complete, run the **node --version** command to query the Node.js version to check whether the installation is successful.

#. Install npm.

   .. code-block::

      yum install npm

#. Install the Redis client ioredis.

   .. code-block::

      npm install ioredis

#. Edit the sample script for connecting to a DCS Redis instance.

   Add the following content to the **ioredisdemo.js** script, including information about connection and data reading.

   .. code-block::

      var Redis = require('ioredis');
      var redis = new Redis({
        port: 6379,          // Redis port
        host: '192.168.0.196',   // Redis host
        family: 4,           // 4 (IPv4) or 6 (IPv6)
        password: '******',
        db: 0
      });
      redis.set('foo', 'bar');
      redis.get('foo', function (err, result) {
        console.log(result);
      });
      // Or using a promise if the last argument isn't a function
      redis.get('foo').then(function (result) {
        console.log(result);
      });
      // Arguments to commands are flattened, so the following are the same:
      redis.sadd('set', 1, 3, 5, 7);
      redis.sadd('set', [1, 3, 5, 7]);
      // All arguments are passed directly to the redis server:
      redis.set('key', 100, 'EX', 10);

   *host* indicates the example IP address/domain name of the DCS instance and *port* indicates the port number of the DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312012__en-us_topic_0148195323_li11511175651212>`. Change them as required. ``******`` indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

#. Run the sample script to access the chosen DCS Redis instance.

   .. code-block::

      node ioredisdemo.js
