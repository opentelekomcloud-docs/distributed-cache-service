:original_name: dcs-ug-210820001.html

.. _dcs-ug-210820001:

Switching DCS Instance IP Addresses
===================================

Scenario
--------

Currently, you cannot change the instance type when using the specification modification function. To modify instance specifications while changing the instance type, you can perform IP switching after data migration. By switching IP addresses, you can also change the AZ used by an instance.

-  After online data migration is complete, you can switch the IP addresses.
-  The IP addresses can be rolled back as required after the switching.

.. note::

   -  This function is supported by DCS Redis 4.0 instances and later.
   -  IP switching is supported only when both the source and target instances are DCS instances in the cloud.

Prerequisites
-------------

-  Obtain information about the source and target instances. For details about preparing a target instance, see :ref:`Step 2: Prepare the Target DCS Redis Instance <dcs-ug-0312038__en-us_topic_0179456698_dcs-migration-190703003_section1128152020384>`.
-  Ensure that the source and target instances can communicate with each other. For details, see :ref:`Step 3: Check the Network <dcs-ug-0312038__section858595915281>`.
-  The target and source instances must use the same port.
-  IP switching can be performed only when the following conditions are met:

   -  Both the source and target instances are DCS Redis instances.

   -  :ref:`Table 1 <dcs-ug-210820001__en-us_topic_0000001148100324_table09121148162513>` lists the supported IP switching scenarios.

      .. _dcs-ug-210820001__en-us_topic_0000001148100324_table09121148162513:

      .. table:: **Table 1** IP switching scenarios

         +---------------------------------------------------------------------+---------------------------------------------------------------------+
         | Source                                                              | Target                                                              |
         +=====================================================================+=====================================================================+
         | Single-node, master/standby, read/write splitting, or Proxy Cluster | Single-node, master/standby, read/write splitting, or Proxy Cluster |
         +---------------------------------------------------------------------+---------------------------------------------------------------------+

Precautions for IP Switching
----------------------------

#. Online migration will stop during the switching.
#. Instances will be read-only for one minute and disconnected for several seconds during the switching.
#. The target and source instances must use the same port.
#. If your application cannot reconnect to Redis or handle exceptions, you may need to restart the application after the IP switching.
#. If the source and target instances are in different subnets, the subnet information will be updated after the switching.
#. If the source is a master/standby instance, the IP address of the standby node will not be switched. Ensure that this IP address is not used by your applications.
#. If your applications use a domain name to connect to Redis, the domain name will be used for the source instance. Select **Yes** for **Switch Domain Name**.
#. Ensure that the passwords of the source and target instances are the same. If they are different, verification will fail after the switching.
#. If a whitelist is configured for the source instance, ensure that the same whitelist is configured for the target instance before switching IP addresses.

Switching IP Addresses
----------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner of the management console and select the region where your instance is located.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Online Migration Task**.

#. Enter the task name and description.

#. Configure the VPC, subnet, and security group for the migration task.

   The VPC, subnet, and security group facilitate the migration. Ensure that the migration resources can access the source and target Redis instances.

#. Configure the migration task by referring to :ref:`Configuring the Online Migration Task <dcs-ug-0312038__section1329517563912>`. Select **Full + Incremental** for **Migration Type**.

#. On the **Online Migration** page, when the migration task status changes to **Incremental migration in progress**, choose **More** > **Switch IP** in the **Operation** column.

#. In the **Switch IP** dialog box, select whether to switch the domain name.

   .. note::

      -  If a domain name is used, switch it or you must modify the domain name on the client.
      -  If no domain name is used, the DNS of the instances will be updated.

#. Click **OK**. The IP address switching task is submitted successfully. When the status of the migration task changes to **IP switched**, the IP address switching is complete.

Rolling Back IP Addresses
-------------------------

If you want to change the instance IP address to the original IP address, perform the following operations:

#. Log in to the DCS console.
#. Click |image2| in the upper left corner of the management console and select the region where your instance is located.
#. In the navigation pane, choose **Data Migration**.
#. On the **Online Migration** page, locate the row that contains the migration task in the **IP switched** state, choose **More** > **Roll Back IP**.
#. In the confirmation dialog box, click **Yes**. The IP address rollback task is submitted successfully. When the task status changes to **IP rolled back**, the rollback is complete.

.. |image1| image:: /_static/images/en-us_image_0148195246.png
.. |image2| image:: /_static/images/en-us_image_0148195246.png
