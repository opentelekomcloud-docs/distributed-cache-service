:original_name: dcs-ug-0312011.html

.. _dcs-ug-0312011:

Connecting to Redis on redis-py (Python)
========================================

This section describes how to access a Redis instance on redis-py. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

.. note::

   Use redis-py to connect to single-node, master/standby, and Proxy Cluster instances and redis-py-cluster to connect to Redis Cluster instances.

   To access a Redis 7.0 instance, use a redis-py `4.3.0 <https://github.com/redis/redis-py/releases/tag/v4.3.0>`__ or later client. `5.0.0 <https://github.com/redis/redis-py/releases/tag/v5.0.0>`__ and later versions are recommended.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__
-  If the ECS runs the Linux OS, ensure that the Python compilation environment has been installed on the ECS.

Connecting to Redis on redis-py
-------------------------------

#. .. _dcs-ug-0312011__en-us_topic_0148195287_li450593110588:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

   The following uses CentOS as an example to describe how to access an instance using a Python client.

#. Access the DCS Redis instance.

   If the ECS OS does not provide Python, run the following **yum** command to install it:

   .. code-block::

      yum install python

   .. note::

      The Python version must be 3.6 or later. If the default Python version is earlier than 3.6, perform the following operations to change it:

      a. Run the **rm -rf python** command to delete the Python symbolic link.
      b. Run the **ln -s python**\ *X.X.X* **python** command to create another Python link. In the command, *X.X.X* indicates the Python version number.

   -  **For single-node, master/standby, or Proxy Cluster types:**

      a. Install Python and redis-py.

         #. If the system does not provide Python, run the **yum** command to install it.

         #. Run the following command to download and decompress the redis-py package:

            .. code-block::

               wget https://github.com/andymccurdy/redis-py/archive/master.zip
               unzip master.zip

         #. Go to the directory where the decompressed redis-py package is saved, and install redis-py.

            .. code-block::

               python setup.py install

            After the installation, run the **python** command. redis-py have been successfully installed if the following command output is displayed:


            .. figure:: /_static/images/en-us_image_0000001188005622.png
               :alt: **Figure 1** Running the python command

               **Figure 1** Running the python command

      b. Use the redis-py client to connect to the instance. In the following steps, commands are executed in CLI mode. (Alternatively, write the commands into a Python script and then execute the script.)

         #. Run the **python** command to enter the CLI mode. You have entered CLI mode if the following command output is displayed:


            .. figure:: /_static/images/en-us_image_0000001187846598.png
               :alt: **Figure 2** Entering the CLI mode

               **Figure 2** Entering the CLI mode

         #. Run the following command to access the chosen DCS Redis instance:

            .. code-block::

               r = redis.StrictRedis(host='XXX.XXX.XXX.XXX', port=6379, password='******');

            *XXX.XXX.XXX.XXX* indicates the IP address/domain name of the DCS instance and **6379** is an example port number of the instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312011__en-us_topic_0148195287_li450593110588>`. Change them as required. ``******`` indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

            You have successfully accessed the instance if the following command output is displayed. Enter commands to perform read and write operations on the database.


            .. figure:: /_static/images/en-us_image_0000001233126245.png
               :alt: **Figure 3** Redis connected successfully

               **Figure 3** Redis connected successfully

   -  **For the Redis Cluster type:**

      a. Install the redis-py-cluster client.

         #. Download the released version.

            .. code-block::

               wget https://github.com/Grokzen/redis-py-cluster/releases/download/2.1.3/redis-py-cluster-2.1.3.tar.gz

         #. Decompress the package.

            .. code-block::

               tar -xvf redis-py-cluster-2.1.3.tar.gz

         #. Go to the directory where the decompressed redis-py-cluster package is saved, and install redis-py-cluster.

            .. code-block::

               python setup.py install

      b. Access the DCS Redis instance by using redis-py-cluster.

         In the following steps, commands are executed in CLI mode. (Alternatively, write the commands into a Python script and then execute the script.)

         #. Run the **python** command to enter the CLI mode.

         #. Run the following command to access the chosen DCS Redis instance. If the instance does not have a password, exclude **password='******'** from the command.

            .. code-block::

               >>> from rediscluster import RedisCluster

               >>> startup_nodes = [{"host": "192.168.0.143", "port": "6379"},{"host": "192.168.0.144", "port": "6379"},{"host": "192.168.0.145", "port": "6379"},{"host": "192.168.0.146", "port": "6379"}]

               >>> rc = RedisCluster(startup_nodes=startup_nodes, decode_responses=True, password='******')

               >>> rc.set("foo", "bar")
               True
               >>> print(rc.get("foo"))
               'bar'
