:original_name: dcs-migrate-0220411.html

.. _dcs-migrate-0220411:

Online Full Migration of Redis from Another Cloud with redis-shake
==================================================================

redis-shake is an open-source Redis migration tool. Its **rump** mode allows you to obtain the full data of a source Redis using the **SCAN** command and write the data to a target Redis. This migration solution does not involve the **SYNC** or **PSYNC** command and can be widely used for migration between self-built Redis and cloud Redis.

This section describes how to use the **rump** mode of redis-shake to migrate the full Redis data of another cloud service vendor at a time online to DCS.


.. figure:: /_static/images/en-us_image_0000001252755478.png
   :alt: **Figure 1** Data flow in this solution

   **Figure 1** Data flow in this solution

Prerequisites
-------------

-  A :ref:`DCS Redis instance <dcs-ug-0312003>` has been created on the target cloud.
-  An ECS has been created on the target cloud for running redis-shake.
-  The ECS is in the same VPC as the DCS Redis instance and bound with an EIP.
-  The **rump** mode does not support incremental data migration. To keep data consistency, stop writing data to the source Redis before migration.
-  This solution applies only to same-database mapping and does not apply to inter-database mapping.
-  If the source Redis has multiple databases (there are databases other than DB0), and your DCS instance is a cluster, this solution cannot be used. (Cluster DCS instances support only DB0.)

Procedure
---------

#. Install Nginx on the ECS and the source forwarding server. The following describes how to install Nginx on an ECS running CentOS 7.x. The commands vary depending on the OS.

   a. Add Nginx to the Yum repository.

      .. code-block::

         sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

   b. Check whether Nginx has been added successfully.

      .. code-block::

         yum search nginx

   c. Install Nginx.

      .. code-block::

         sudo yum install -y nginx

   d. Install the stream module.

      .. code-block::

         yum install nginx-mod-stream --skip-broken

   e. Start Nginx and set it to run automatically upon system startup.

      .. code-block::

         sudo systemctl start nginx.service
         sudo systemctl enable nginx.service

   f. In the address box of a browser, enter the server address (the EIP of the ECS) to check whether Nginx is installed successfully.

      If the following page is displayed, Nginx has been installed successfully.

      |image1|

#. Add the source forwarding server to the whitelist of the source Redis.

#. Configure a security group for the source forwarding server.

   a. Obtain the EIP of the ECS.
   b. In the inbound rule of the security group of the source forwarding server, add the EIP of the ECS, and open the port that ECS's requests come through. The following takes port 6379 as an example.

#. Configure Nginx forwarding for the source forwarding server.

   a. Log in to the Linux source forwarding server and run the following commands to open and modify the configuration file:

      .. code-block::

         cd /etc/nginx
         vi nginx.conf

   b. Example forwarding configuration:

      .. code-block::

         stream {
             server {
                 listen 6379;
                 proxy_pass {source_instance_address}:{port};
             }
            }

      **6379** is the listening port of the source forwarding server. *{source_instance_address}* and *{port}* are the connection address and port of the source Redis instance.

      This configuration allows you to access the source Redis through the local listening port 6379 of the source forwarding server.

      This configuration must be added exactly where it is shown in the following figure.


      .. figure:: /_static/images/en-us_image_0000001299155037.png
         :alt: **Figure 2** Configuration location

         **Figure 2** Configuration location

   c. Restart Nginx.

      .. code-block::

         service nginx restart

   d. Verify whether Nginx has been started.

      .. code-block::

         netstat -an|grep 6379

      If the port is being listened, Nginx has been started successfully.


      .. figure:: /_static/images/en-us_image_0000001299513869.png
         :alt: **Figure 3** Verification result

         **Figure 3** Verification result

#. Configure Nginx forwarding for the ECS.

   a. Log in to the Linux ECS and run the following commands to open and modify the configuration file:

      **cd /etc/nginx**

      **vi nginx.conf**

   b. Configuration example:

      .. code-block::

         stream {
             server {
                 listen 6666;
                 proxy_pass {source_ecs_address}:6379;
             }
            }

      **6666** is ECS's listening port, *{source_ecs_address}* is the public IP address of the source forwarding server, and **6379** is the listening port of the source forwarding server Nginx.

      This configuration allows you to access the source forwarding server through the local listening port 6666 of the ECS.

      This configuration must be added exactly where it is shown in the following figure.


      .. figure:: /_static/images/en-us_image_0000001299274493.png
         :alt: **Figure 4** Configuration location

         **Figure 4** Configuration location

   c. Restart Nginx.

      .. code-block::

         service nginx restart

   d. Verify whether Nginx has been started.

      .. code-block::

         netstat -an|grep 6666

      If the port is being listened, Nginx has been started successfully.


      .. figure:: /_static/images/en-us_image_0000001299354449.png
         :alt: **Figure 5** Verification result

         **Figure 5** Verification result

#. Run the following command on the ECS to test the network connection of port 6666:

   .. code-block::

      redis-cli -h {target_ecs_address} -p 6666 -a {password}

   *{target_ecs_address}* is the EIP of the ECS, **6666** is the listening port of the ECS, and *{password}* is the source Redis password. If there is no password, leave it blank.


   .. figure:: /_static/images/en-us_image_0000001252915210.png
      :alt: **Figure 6** Connection example

      **Figure 6** Connection example

#. Prepare the migration tool redis-shake.

   a. Log in to the ECS.

   b. Download redis-shake. Version 2.0.3 is used as an example. You can use `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__ as required.

      .. code-block::

         wget https://github.com/tair-opensource/RedisShake/releases/download/release-v2.0.3-20200724/redis-shake-v2.0.3.tar.gz

   c. Decompress the redis-shake file.

      .. code-block::

         tar -xvf redis-shake-v2.0.3.tar.gz

#. Configure the redis-shake configuration file.

   a. Go to the directory generated after the decompression.

      .. code-block::

         cd redis-shake-v2.0.3

   b. Modify the **redis-shake.conf** configuration file.

      .. code-block::

         vim redis-shake.conf

      Modify the source Redis configuration.

      -  source.type

         Type of the source Redis instance. Use **standalone** for single-node, master/standby, and Proxy Cluster, and **cluster** for cluster instances.

      -  source.address

         EIP of the ECS and the mapped port of the source forwarding server (ECS's listening port 6666). Separate the EIP and port number with a colon (:).

      -  source.password_raw

         Password of the source Redis instance. If no password is set, you do not need to set this parameter.

      Modify the target DCS configuration.

      -  target.type

         Type of the DCS Redis instance. Use **standalone** for single-node, master/standby, and Proxy Cluster, and **cluster** for cluster instances.

      -  target.address

         Colon (:) separated connection address and port of the DCS Redis instance.

      -  target.password_raw

         Password of the DCS Redis instance. If no password is set, you do not need to set this parameter.

   c. Press **Esc** to exit the editing mode and enter **:wq!**. Press **Enter** to save the configuration and exit the editing interface.

#. Run the following command to start redis-shake and migrate data in the **rump** (online in full) mode:

   .. code-block::

      ./redis-shake.linux -conf redis-shake.conf -type rump


   .. figure:: /_static/images/en-us_image_0000001252755498.png
      :alt: **Figure 7** Migration process

      **Figure 7** Migration process


   .. figure:: /_static/images/en-us_image_0000001253234262.png
      :alt: **Figure 8** Migration result

      **Figure 8** Migration result

#. After the migration is complete, use redis-cli to connect to the source and target Redis instances to check whether the data is complete.

   a. Connect to the source and target Redis instances, respectively.

      For details, see :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

   b. Run the **info keyspace** command to check the values of **keys** and **expires**.

   c. Calculate the differences between the values of **keys** and **expires** of the source Redis and the target Redis. If the differences are the same, the data is complete and the migration is successful.

#. Delete the redis-shake configuration file.

.. |image1| image:: /_static/images/en-us_image_0000001253074986.png
