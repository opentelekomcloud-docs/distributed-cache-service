:original_name: dcs-ug-0312012.html

.. _dcs-ug-0312012:

Connecting to Redis on ioredis (Node.js)
========================================

This section describes how to access a Redis instance on ioredis. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

Notes and Constraints
---------------------

The operations described in this section apply only to single-node, master/standby, and Proxy Cluster instances. To access a Redis Cluster instance on ioredis, see `Node.js Redis client description <https://github.com/NodeRedis/cluster-key-slot>`__.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.

-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__

-  The Linux ECS must have GNU Compiler Collection (GCC) installed. To query the GCC version, run the **gcc --version** command.

   Run the following command to install GCC on the ECS if needed, CentOS is used as an example:

   .. code-block::

      yum install -y make
      yum install -y pcre-devel
      yum install -y zlib-devel
      yum install -y libevent-devel
      yum install -y openssl-devel
      yum install -y gcc-c++

Connecting to Redis on ioredis
------------------------------

-  For a client server running Ubuntu (Debian series), see :ref:`For Client Servers Running Ubuntu (Debian Series) <dcs-ug-0312012__en-us_topic_0148195323_section10247113513274>`.
-  For a client server running CentOS (Red Hat series), see :ref:`For client servers running CentOS (Red Hat series) <dcs-ug-0312012__en-us_topic_0148195323_section485881815286>`.

.. _dcs-ug-0312012__en-us_topic_0148195323_section10247113513274:

For Client Servers Running Ubuntu (Debian Series)
-------------------------------------------------

#. .. _dcs-ug-0312012__en-us_topic_0148195323_li41311414288:

   View the IP address/domain name and port of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Install Node.js.

   .. code-block::

      apt install nodejs-legacy

   If the preceding command does not work, run the following commands:

   .. code-block::

      wget https://nodejs.org/dist/v4.28.5/node-v4.28.5.tar.gz --no-check-certificate
      tar -xvf node-v4.28.5.tar.gz
      cd node-v4.28.5
      ./configure
      make
      make install

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

   **host** indicates the example IP address/domain name of the DCS instance and **port** indicates the port of the DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312012__en-us_topic_0148195323_li41311414288>`. Change them as required. **\*****\*** indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation. Omit the password setting in the command for a password-free instance.

#. Run the sample script to access the chosen DCS Redis instance.

   .. code-block::

      node ioredisdemo.js

.. _dcs-ug-0312012__en-us_topic_0148195323_section485881815286:

For client servers running CentOS (Red Hat series)
--------------------------------------------------

#. .. _dcs-ug-0312012__en-us_topic_0148195323_li10535549122814:

   View the IP address/domain name and port of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Install Node.js.

   .. code-block::

      yum install nodejs

   If the preceding command does not work, run the following commands:

   .. code-block::

      wget https://nodejs.org/dist/v4.28.5/node-v4.28.5.tar.gz --no-check-certificate
      tar -xvf node-v4.28.5.tar.gz
      cd node-v4.28.5
      ./configure
      make
      make install

   After the installation is complete, run the **node -v** command to query the Node.js version to check whether the installation is successful.

#. Install the node package manager (npm).

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

   **host** indicates the example IP address/domain name of the DCS instance and **port** indicates the port of the DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312012__en-us_topic_0148195323_li10535549122814>`. Change them as required. **\*****\*** indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation. Omit the password setting in the command for a password-free instance.

#. Run the sample script to access the chosen DCS Redis instance.

   .. code-block::

      node ioredisdemo.js
