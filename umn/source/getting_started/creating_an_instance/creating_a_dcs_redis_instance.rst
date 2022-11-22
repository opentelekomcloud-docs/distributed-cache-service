:original_name: dcs-ug-0326008.html

.. _dcs-ug-0326008:

Creating a DCS Redis Instance
=============================

You can create one or more DCS Redis instances with the required computing capabilities and storage space based on service requirements.

.. note::

   The system automatically schedules the task every 3 minutes for checking whether resources are available or sold out.


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

      Currently, 3.0, 4.0, and 5.0 versions are supported.

      .. note::

         -  When creating a Proxy Cluster instance, you can only select version 3.0.
         -  When creating a Redis Cluster instance, you can select versions 4.0 or 5.0.

   c. Set **Instance Type** to **Single-node**, **Master/Standby**, **Proxy Cluster** or **Redis Cluster**.

   d. Set **CPU Architecture** to **x86**.

   e. Set **Replicas**. The default value is **2** (including the master).

      This parameter is displayed only when you select Redis 4.0 or Redis 5.0 and the instance type is master/standby or Redis Cluster.

   f. Select an AZ.

      If the instance type is master/standby, Proxy Cluster, or Redis Cluster, **Standby AZ** is displayed. Select a standby AZ for the standby node of the instance.

      .. note::

         -  To accelerate access, deploy your instance and your application in the same AZ.
         -  There are multiple AZs in each region. If resources are insufficient in an AZ, the AZ will be unavailable. In this case, select another AZ.

   g. **Instance Specification**:

      The remaining quota is displayed on the console.

      To apply to increase quota, click **Increase quota** below the specifications.

#. Configure the instance network parameters.

   a. For **VPC**, select a created VPC, subnet, and specify the IP address.

      You can choose to obtain an automatically assigned IP address or manually specify an IP address that is available in the selected subnet.

      For a DCS Redis 4.0 or 5.0 instance, you can specify a port numbering in the range from 1 to 65535. If no port is specified, the default port 6379 will be used. For a DCS Redis 3.0 instance, the port cannot be customized. Port 6379 will be used.

   b. Select a security group.

      A security group is a set of rules that control access to ECSs. It provides access policies for mutually trusted ECSs with the same security protection requirements in the same VPC.

      This parameter is displayed only for DCS Redis 3.0 instances. DCS Redis 4.0 and 5.0 instances are based on VPC endpoints and do not support security groups. To control access to a DCS Redis 4.0 or 5.0 instance, configure a whitelist after instance creation. For details, see :ref:`Managing IP Address Whitelist <dcs-ug-190812001>`.

#. Set the instance password.

   This password is used for accessing the DCS Redis instance.

   .. note::

      For security purposes, you must enter an instance-specific password when you are accessing the DCS Redis instance. Keep your instance password secure and change it periodically.

      The password must meet the following requirements:

      -  Cannot be left blank.
      -  Can contain 8 to 32 characters.
      -  Must contain at least three of the following character types:

         -  Lowercase letters
         -  Uppercase letters
         -  Digits
         -  special characters (:literal:`\`~!@#$^&*()-_=+\\|{}:,<.>/?`)

#. Click **More Settings** to display more configurations, including auto backup.

   a. Specify **Name** and **Description**.

      The value of **Name** can contain 4 to 64 characters.

   b. Choose whether to enable **Auto Backup**.

      This parameter is displayed only when the instance type is master/standby or cluster. You can enable and schedule automated backup now or after the instance is created. For more information on how to configure a backup policy, see :ref:`Backing Up and Restoring DCS Instances <dcs-ug-0312030>`.

   c. Rename critical commands.

      **Command Renaming** is displayed for Redis 4.0 and 5.0. Currently, you can only rename the **COMMAND**, **KEYS**, **FLUSHDB**, **FLUSHALL**, and **HGETALL** commands.

   d. Specify the maintenance window.

      Choose a window for DCS O&M personnel to perform maintenance on your instance. You will be contacted before any maintenance activities are performed.

#. Click **Create Now**.

   The displayed page shows the instance information you have specified.

#. Confirm the instance information and click **Submit**.

#. Return to the **Cache Manager** page to view and manage your DCS instances.

   a. Creating a single-node or master/standby DCS Redis 3.0 instance takes 5 to 15 minutes. Creating a cluster DCS Redis 3.0 instance takes 30 minutes.

      .. note::

         DCS Redis 4.0 and 5.0 instances are containerized and can be created within seconds.

   b. After a DCS instance has been successfully created, it enters the **Running** state by default.

   .. note::

      -  If the new DCS instance failed to be created, delete the unsuccessful instance creation task by following the procedure in :ref:`Deleting Instance Creation Tasks That Have Failed to Run <dcs-ug-0326014>`. Then, create the DCS instance again. If the DCS instance still fails to be created, contact customer service.
      -  There is the management plane and the tenant plane. The tenant plane is also called the pod zone. During the creation of a DCS instance, a VM is created in the pod zone. If the instance creation fails, the instance status changes to **Faulty**, and the error message "Failed to connect to the instance. Network exceptions may have occurred in the pod zone." is displayed, indicating that the management plane cannot be connected to the tenant plane.

.. |image1| image:: /_static/images/en-us_image_0266235412.png
