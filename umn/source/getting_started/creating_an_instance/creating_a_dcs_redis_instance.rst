:original_name: dcs-ug-0326008.html

.. _dcs-ug-0326008:

Creating a DCS Redis Instance
=============================

You can create one or more DCS Redis instances with the required computing capabilities and storage space based on service requirements.

.. note::

   The system automatically schedules the task every 3 minutes for checking whether resources are available or sold out.

Prerequisites
-------------

You have prepared :ref:`necessary resources <dcs-ug-0312004>`.


Creating a DCS Redis Instance
-----------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner of the management console and select a region and a project.

#. Click **Create DCS Instance**.

#. Select a region closest to your application to reduce latency and accelerate access.

#. Specify the following instance parameters based on the information collected in :ref:`Identifying Requirements <purchasepreparation>`.

   a. **Cache Engine**:

      Select **Redis**.

   b. **Version**:

      Currently, versions 3.0/4.0/5.0/6.0 are supported.

      .. note::

         -  When creating a Proxy Cluster instance, you can only select version 3.0.
         -  When creating a Redis Cluster instance, you can select versions 4.0, 5.0, or 6.0.
         -  The Redis version cannot be changed once the instance is created. To use a later Redis version, create another DCS Redis instance and then migrate data from the old instance to the new one.
         -  The method of connecting a client to a Redis Cluster instance is different from that of connecting a client to other types of instances. For details, see :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

   c. Set **Instance Type** to **Single-node**, **Master/Standby**, **Proxy Cluster** or **Redis Cluster**.

   d. Set **CPU Architecture** to **x86**.

   e. Set **Replicas**. The default value is **2** (including the master).

      This parameter is displayed only when you select Redis 4.0/5.0/6.0 and the instance type is master/standby or Redis Cluster.

   f. If **4.0** or later, and **Proxy Cluster** or **Redis Cluster** are selected, the **Sharding** parameter is displayed. Options:

      -  **Use default**: Use the default sharding specifications.
      -  **Customize**: Customize the size of each shard and then select corresponding instance specifications.

   g. Select an AZ.

      If the instance type is master/standby, Proxy Cluster, or Redis Cluster, **Standby AZ** is displayed. Select a standby AZ for the standby node of the instance.

      .. note::

         -  To accelerate access, deploy your instance and your application in the same AZ.
         -  There are multiple AZs in each region. If resources are insufficient in an AZ, the AZ will be unavailable. In this case, select another AZ.

   h. **Instance Specification**:

      The remaining quota is displayed on the console.

      To apply to increase quota, click **Increase quota** below the specifications.

#. Configure the instance network parameters.

   a. Select a VPC and a subnet.

   b. Configure the IP address.

      Redis Cluster instances only support automatically-assigned IP addresses. The other instance types support both automatically-assigned IP addresses and manually-specified IP addresses. You can manually specify an IP address available in your subnet.

      For a DCS Redis 4.0 or later instance, you can specify a port number in the range from 1 to 65535. If no port is specified, the default port 6379 will be used. For a DCS Redis 3.0 instance, the port cannot be customized. Port 6379 will be used.

   c. Select a security group.

      A security group is a set of rules that control access to ECSs. It provides access policies for mutually trusted ECSs with the same security protection requirements in the same VPC.

      This parameter is displayed only for DCS Redis 3.0 instances. DCS Redis 4.0/5.0/6.0 instances are based on VPC endpoints and do not support security groups. To control access to a DCS Redis 4.0/5.0/6.0 instance, configure a whitelist after instance creation. For details, see :ref:`Managing IP Address Whitelist <dcs-ug-190812001>`.

#. Set the instance password.

   -  Select **Yes** or **No** for **Password Protected**.

      .. note::

         -  Password-free access carries security risks. Exercise caution when selecting this mode.

   -  **Password** and **Confirm Password**: These parameters indicate the password of accessing the DCS Redis instance, and are displayed only when **Password Protected** is set to **Yes**.

      .. note::

         For security purposes, if password-free access is disabled, the system prompts you to enter an instance-specific password when you are accessing the DCS Redis instance. Keep your instance password secure and change it periodically.

#. Configure **Parameter Configuration**.

   You can select **Default Templates** or **Use custom template**.

   .. note::

      -  On the instance creation page, the default parameter templates are used by default.
      -  If you use a custom template, the selected cache engine version and instance type must match those of the template. For details about using custom templates, see :ref:`Creating a Custom Parameter Template <dcs-ug-210622003>`.

#. Choose whether to enable **Auto Backup**.

   This parameter is displayed only when the instance type is master/standby or cluster. For more information on how to configure a backup policy, see :ref:`Overview <en-us_topic_0079835992>`.

#. Specify the number of instances to create.

#. Enter an instance name.

   The value of **Name** contains at least 4 characters. When you create multiple instances at a time, the instances are named in the format of *custom name*\ ``-``\ *n*, where *n* starts from 000 and is incremented by 1. For example, if you create two instances and set **name** to **dcs_demo**, the two instances are respectively named as **dcs_demo-000** and **dcs_demo-001**.

#. Click **More Settings** to configure more parameters.

   a. Enter a description of the instance.

   b. Rename critical commands.

      **Command Renaming** is displayed for Redis 4.0 and later. Currently, you can only rename the **COMMAND**, **KEYS**, **FLUSHDB**, **FLUSHALL**, **HGETALL**, **SCAN**, **HSCAN**, **SSCAN**, and **ZSCAN** commands.

   c. Specify the maintenance window.

      Choose a window for DCS O&M personnel to perform maintenance on your instance. You will be contacted before any maintenance activities are performed.

#. Click **Create Now**.

   The displayed page shows the instance information you have specified.

#. Confirm the instance information and click **Submit**.

#. Return to the **Cache Manager** page to view and manage your DCS instances.

   a. Creating a single-node or master/standby DCS Redis 3.0 instance takes 5 to 15 minutes. Creating a cluster DCS Redis 3.0 instance takes 30 minutes.DCS Redis 4.0 and later instances are containerized and can be created within seconds.
   b. After a DCS instance has been successfully created, it enters the **Running** state by default.

   .. note::

      -  If the new DCS instance failed to be created, delete the unsuccessful instance creation task by following the procedure in :ref:`Deleting Instance Creation Tasks That Have Failed to Run <dcs-ug-0326014>`. Then, create the DCS instance again. If the DCS instance still fails to be created, contact customer service.
      -  There is the management plane and the tenant plane. The tenant plane is also called the pod zone. During the creation of a DCS instance, a VM is created in the pod zone. If the instance creation fails, the instance status changes to **Faulty**, and the error message "Failed to connect to the instance. Network exceptions may have occurred in the pod zone." is displayed, indicating that the management plane cannot be connected to the tenant plane.

.. |image1| image:: /_static/images/en-us_image_0266235412.png
