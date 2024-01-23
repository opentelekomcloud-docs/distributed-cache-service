:original_name: dcs-migration-190703003.html

.. _dcs-migration-190703003:

Online Migration of Self-Hosted Redis
=====================================

Application Scenarios
---------------------

If the source and target instances are interconnected and the **SYNC** and **PSYNC** commands are supported by the source instance, data can be migrated online in full or incrementally from the source to the target.

.. caution::

   -  If the **SYNC** and **PSYNC** commands are disabled on the source Redis instance, enable them before performing online migration. Otherwise, the migration fails. If you use a DCS Redis instance for online migration, the **SYNC** command is automatically enabled.
   -  You cannot use public networks for online migration.
   -  During online migration, you are advised to set **repl-timeout** on the source instance to 300s and **client-output-buffer-limit** to 20% of the maximum memory of the instance.
   -  The source must be Redis 3.0 or later.

Impacts on Services
-------------------

During online migration, data is essentially synchronized in full to a new replica. Therefore, perform online migration during low-demand hours.

Prerequisites
-------------

-  Before migrating data, read through :ref:`Migration Tools and Schemes <dcs-migration-090626002>` to learn about the DCS data migration function and select an appropriate target instance.
-  By default, a cluster instance has only one DB (DB0). Before you migrate data from a multi-DB single-node or master/standby instance to a Redis Cluster instance, check whether any data exists on databases other than DB0. To ensure that the migration succeeds, move all data to DB0 by referring to :ref:`Online Migration with Rump <dcs-migration-090626001_0>`.

Step 1: Obtain the Source Redis Address
---------------------------------------

Obtain the IP address/domain name and port number of the source Redis instance.

Step 2: Prepare the Target DCS Redis Instance
---------------------------------------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.

-  If you already have a DCS Redis instance, you do not need to create one again, but you need to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`.

   If the target instance data is not cleared before the migration and the source and target instances contain the same key, the key in the target instance will be overwritten by the key in the source instance after the migration.

Step 3: Check the Network
-------------------------

#. Check whether the source Redis instance, the target Redis instance, and the migration task are configured with the same VPC.

   If yes, go to :ref:`Step 4: Create an Online Migration Task <dcs-migration-190703003__section157769524519>`. If no, go to :ref:`2 <dcs-migration-190703003__li160420185217>`.

#. .. _dcs-migration-190703003__li160420185217:

   Check whether the VPCs configured for the source Redis instance, the target Redis instance, and the migration task are connected to ensure that the VM resource of the migration task can access the source and target Redis instances.

   If yes, go to :ref:`Step 4: Create an Online Migration Task <dcs-migration-190703003__section157769524519>`. If no, go to :ref:`3 <dcs-migration-190703003__li423483319412>`.

#. .. _dcs-migration-190703003__li423483319412:

   Perform the following operations to establish the network.

   -  If the source and target Redis instances are in the same DCS region, create a VPC peering connection by referring to "VPC Peering Connection" in the *Virtual Private Cloud User Guide*.
   -  If the source and target Redis instances are on different clouds or in different regions, create a connection by referring to the *Direct Connect User Guide*.

.. _dcs-migration-190703003__section157769524519:

Step 4: Create an Online Migration Task
---------------------------------------

#. Log in to the DCS console.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Online Migration Task**.

#. Enter the task name and description.

#. Configure the VPC, subnet, and security group for the migration task.

   The VPC, subnet, and security group facilitate the migration. Ensure that the migration resources can access the source and target Redis instances.

   .. note::

      -  The online migration task uses a tenant IP address (**Migration ECS** displayed on the **Basic Information** page of the task.) If a whitelist is configured for the source or target instance, add the migration IP address to the whitelist or disable the whitelist.
      -  To allow the VM used by the migration task to access the source and target instances, set an outbound rule for the task's security group to allow traffic through the IP addresses and ports of the source and target instances. By default, all outbound traffic is allowed.

Step 5: Configure the Online Migration Task
-------------------------------------------

#. On the **Online Migration** tab page, click **Configure** in the row containing the online migration task you just created.

#. Select a migration type.

   Supported migration types are **Full** and **Full + Incremental**, which are described in :ref:`Table 1 <dcs-migration-190703003__table55653322215>`.

   .. _dcs-migration-190703003__table55653322215:

   .. table:: **Table 1** Migration type description

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Migration Type                    | Description                                                                                                                                                                                                                                                                                                                                                                                                           |
      +===================================+=======================================================================================================================================================================================================================================================================================================================================================================================================================+
      | Full                              | Suitable for scenarios where services can be interrupted. Data is migrated at one time. **Source instance data updated during the migration will not be migrated to the target instance.**                                                                                                                                                                                                                            |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Full + incremental                | Suitable for scenarios requiring minimal service downtime. The incremental migration parses logs to ensure data consistency between the source and target instances.                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                       |
      |                                   | Once the migration starts, it remains **Migrating** until you click **Stop** in the **Operation** column. After the migration is stopped, data in the source instance will not be lost, but data will not be written to the target instance. When the transmission network is stable, the delay of incremental migration is within seconds. The actual delay depends on the transmission quality of the network link. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0291862872.png
      :alt: **Figure 1** Selecting the migration type

      **Figure 1** Selecting the migration type

#. Configure source Redis and target Redis.

   a. The Redis type can be **Redis in the cloud** or **Self-hosted Redis** as required.

      -  **Redis in the cloud**: a DCS Redis instance (source or target) that is in the same VPC as the migration task. If you select this option, specify a DCS Redis instance.
      -  **Self-hosted Redis**: a DCS Redis instance, Redis in another cloud, or self-hosted Redis. If you select this option, enter Redis addresses.

   b. If the instance is password-protected, click **Test Connection** to check whether the instance password is correct and whether the network is connected. If the instance is not password-protected, click **Test Connection** directly.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

   .. note::

      -  Once incremental migration starts, it remains **Migrating** until you click **Stop**.
      -  To stop a migration task, select the check box on the left of the migration task and click **Stop** above the instance list.
      -  After data migration, duplicate keys will be overwritten.

   If the migration fails, click the migration task and check the log on the **Migration Logs** page.

Verifying the Migration
-----------------------

After the migration is complete, use redis-cli to connect the source and target Redis instances to check data integrity.

#. Connect to the source Redis and the target Redis.

#. Run the **info keyspace** command to check the values of **keys** and **expires**.

   |image1|

#. Calculate the differences between the values of **keys** and **expires** of the source Redis and the target Redis. If the differences are the same, the data is complete and the migration is successful.

During full migration, source Redis data updated during the migration will not be migrated to the target instance.

.. |image1| image:: /_static/images/en-us_image_0293255709.png
