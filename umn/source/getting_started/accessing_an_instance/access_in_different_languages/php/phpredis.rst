:original_name: dcs-ug-0312009.html

.. _dcs-ug-0312009:

phpredis
========

Access a DCS Redis instance through phpredis on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

.. note::

   The operations described in this section apply only to single-node, master/standby, and Proxy Cluster instances. To use phpredis to connect to a Redis Cluster instance, see the `phpredis description <https://github.com/phpredis/phpredis#readme>`__.

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the GCC compilation environment has been installed on the ECS.

Procedure
---------

#. .. _dcs-ug-0312009__en-us_topic_0148195315_li8233164074413:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Log in to the ECS.

   The following uses CentOS as an example to describe how to access an instance through phpredis.

#. Install GCC-C++ and Make compilation components.

   **yum install gcc-c++ make**

#. Install the PHP development package and CLI tool.

   Run the following **yum** command to install the PHP development package:

   **yum install php-devel php-common php-cli**

   After the installation is complete, run the following command to query the PHP version and check whether the installation is successful:

   **php --version**

#. Install the phpredis client.

   a. Download the source phpredis package.

      **wget http://pecl.php.net/get/redis-5.3.7.tgz**

      This version is used as an example. To download phpredis clients of other versions, visit the Redis or PHP official website.

   b. Decompress the source phpredis package.

      **tar -zxvf redis-5.3.7.tgz**

      **cd redis-5.3.7**

   c. Command before compilation.

      **phpize**

   d. Configure the **php-config** file.

      **./configure --with-php-config=/usr/bin/php-config**

      The location of the file varies depending on the OS and PHP installation mode. You are advised to locate the directory where the file is saved before the configuration.

      **find / -name php-config**

   e. Compile and install the phpredis client.

      **make && make install**

   f. After the installation, add the **extension** configuration in the **php.ini** file to reference the Redis module.

      **vim /etc/php.ini**

      Add the following configuration:

      .. code-block::

         extension = "/usr/lib64/php/modules/redis.so"

      .. note::

         The **redis.so** file may be saved in a different directory from **php.ini**. Run the following command to locate the directory:

         **find / -name php.ini**

   g. Save the configuration and exit. Then, run the following command to check whether the extension takes effect:

      **php -m \|grep redis**

      If the command output contains **redis**, the phpredis client environment has been set up.

#. Access the DCS instance by using phpredis.

   a. Edit a **redis.php** file.

      .. code-block::

         <?php
             $redis_host = "{redis_instance_address}";
             $redis_port = 6379;
             $user_pwd = "{password}";
             $redis = new Redis();
             if ($redis->connect($redis_host, $redis_port) == false) {
                die($redis->getLastError());
             }
             if ($redis->auth($user_pwd) == false) {
                 die($redis->getLastError());
             }
             if ($redis->set("welcome", "Hello, DCS for Redis!") == false) {
                 die($redis->getLastError());
             }
             $value = $redis->get("welcome");
             echo $value;
             $redis->close();
         ?>

      *{redis_instance_address}* indicates the IP address/domain name of DCS instance and *6379* is an example port number of DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312009__en-us_topic_0148195315_li8233164074413>`. Change the IP address/domain name and port as required. *{password}* indicates the password used to log in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation. If password-free access is enabled, shield the **if** statement for password authentication.

   b. Run the **php redis.php** command to access the DCS instance.
