:original_name: dcs-ug-211202002.html

.. _dcs-ug-211202002:

Connecting to Redis on predis (PHP)
===================================

This section describes how to connect to Redis on predis. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__
-  If the ECS runs the Linux OS, ensure that the PHP compilation environment has been installed on the ECS.

Connecting to Redis on predis
-----------------------------

#. .. _dcs-ug-211202002__en-us_topic_0000001184480402_li1655151054317:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Install the PHP development package and CLI tool. Run the following **yum** command:

   .. code-block::

      yum install php-devel php-common php-cli

#. After the installation is complete, check the version number to ensure that the installation is successful.

   .. code-block::

      php --version

#. Download the Predis package to the **/usr/share/php** directory.

   a. Run the following command to download the Predis source file:

      .. code-block::

         wget https://github.com/predis/predis/archive/refs/tags/v2.2.2.tar.gz

      .. note::

         This version is used as an example. To download Predis clients of other versions, visit the Redis or PHP official website.

   b. Run the following commands to decompress the source Predis package:

      .. code-block::

         tar -zxvf predis-2.2.2.tar.gz

   c. Rename the decompressed Predis directory **predis** and move it to **/usr/share/php/**.

      .. code-block::

         mv predis-2.2.2 predis

#. Edit a file used to connect to Redis.

   -  Example of using **redis.php** to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance:

      .. code-block::

         <?php
             require 'predis/autoload.php';
             Predis\Autoloader::register();
             $client = new Predis\Client([
               'scheme' => 'tcp' ,
               'host'     => '{redis_instance_address}' ,
               'port'     =>{port} ,
               'password' => '{password}'
             ]);
             $client->set('foo', 'bar');
             $value = $client->get('foo');
             echo $value;
         ?>

   -  Example code for using **redis-cluster.php** to connect to Redis Cluster:

      .. code-block::

         <?php
            require 'predis/autoload.php';
                 $servers = array(
                  'tcp://{redis_instance_address}:{port}'
                 );
                $options = array('cluster' => 'redis');
                $client = new Predis\Client($servers, $options);
                $client->set('foo', 'bar');
                $value = $client->get('foo');
                echo $value;
         ?>

   *{redis_instance_address}* indicates the actual IP address/domain name of the DCS instance and *{port}* is the actual port number of DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-211202002__en-us_topic_0000001184480402_li1655151054317>`. Change them as required. *{password}* indicates the password used to log in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation. If password-free access is required, delete the line that contains "password".

#. Run the **php redis.php** command to access the DCS instance.
