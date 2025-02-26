:original_name: dcs-migration-190703003.html

.. _dcs-migration-190703003:

Migrating Self-Built Redis Online
=================================

If the source self-host and target instances are interconnected and the **SYNC** and **PSYNC** commands are supported by the source instance, data can be migrated online in full or incrementally from the source to the target DCS.

.. note::

   During online migration, data is essentially synchronized in full to a new replica. Therefore, perform online migration during low-demand hours. Otherwise, source instance CPU usage may surge and latency may increase.

Notes and Constraints
---------------------

-  If the **SYNC** and **PSYNC** commands are disabled by the source instance, enable them before migrating data. Otherwise, the migration fails.
-  You cannot use public networks for online migration.
-  During online migration, you are advised to set **repl-timeout** on the source instance to 300s and **client-output-buffer-slave-hard-limit** and **client-output-buffer-slave-soft-limit** to 20% of the maximum memory of the source instance.
-  The source must be Redis 3.0 or later.
-  For earlier instances whose passwords contain single quotation marks ('), modify the password for online migration or try other methods.
-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  Before migrating data, read through :ref:`Migration Tools and Schemes <dcs-migration-090626002>` to learn about the DCS data migration function and select an appropriate target instance.
-  By default, a cluster instance has only one DB (DB0). Before you migrate data from a multi-DB single-node or master/standby instance to a Redis Cluster instance, check whether any data exists on databases other than DB0. To ensure that the migration succeeds, move all data to DB0 by referring to :ref:`Online Migration with Rump <dcs-migration-090626001_0>`.
-  The IP address and port of the source Redis instance has been obtained.
-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.
-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

.. _dcs-migration-190703003__section157769524519:

Creating an Online Migration Task
---------------------------------

#. Log in to the DCS console using the account of the target DCS Redis instance.

#. Click |image1| in the upper left corner of the console and select the region where your target instance is located.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Online Migration Task**.

#. Enter the task name and description.

   The task name must start with a letter, contain 4 to 64 characters, and contain only letters, digits, hyphens (-), and underscores (_).

#. Configure the VPC, subnet, and security group for the migration task.

   .. note::

      -  **Select the same VPC as the target Redis. Ensure that the migration resource can access the target Redis instance.**
      -  The online migration task uses a tenant IP address (**Migration ECS** displayed on the **Basic Information** page of the task.) If a whitelist is configured for the source or target instance, add the migration IP address to the whitelist or disable the whitelist.
      -  To allow the VM used by the migration task to access the source and target instances, set an outbound rule for the task's security group to allow traffic through the IP addresses and ports of the source and target instances. By default, all outbound traffic is allowed.

Checking the Network
--------------------

#. Check whether the source Redis instance, the target Redis instance, and the migration task are configured with the same VPC.

   If yes, go to :ref:`Creating an Online Migration Task <dcs-migration-190703003__section157769524519>`. If no, go to :ref:`2 <dcs-migration-190703003__li160420185217>`.

#. .. _dcs-migration-190703003__li160420185217:

   Check whether the VPCs configured for the source Redis instance, the target Redis instance, and the migration task are connected to ensure that the VM resource of the migration task can access the source and target Redis instances.

   If yes, go to :ref:`Configuring the Online Migration Task <dcs-migration-190703003__section14919536272>`. If no, go to :ref:`3 <dcs-migration-190703003__li423483319412>`.

#. .. _dcs-migration-190703003__li423483319412:

   Perform the following operations to establish the network.

   -  If the VPC of the source and target Redis instances are of the same cloud vendor and in the same region, create a VPC peering connection by referring to "VPC Peering Connection" in the *Virtual Private Cloud User Guide*.
   -  If the source and target Redis instances are on different clouds or in different regions, create a connection using only Direct Connect. For details, see the *Direct Connect User Guide*.

.. _dcs-migration-190703003__section14919536272:

Configuring the Online Migration Task
-------------------------------------

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

#. Only if **Migration Type** is set to **Full + Incremental**, you can specify a bandwidth limit.

   The data synchronization rate can be kept around the bandwidth limit.

#. Specify **Auto-Reconnect**. If this option is enabled, automatic reconnections will be performed indefinitely in the case of a network exception.

   Full synchronization will be triggered and requires more bandwidth if incremental synchronization becomes unavailable. Exercise caution when enabling this option.

#. Configure **Source Redis** and **Target Redis**.

   a. Configure **Source Redis Type** and **Source Redis Instance**:

      Set **Redis in the cloud** for **Source Redis Type** and add **Source Redis Instance**.

      If the source Redis is a Redis Cluster, enter the IP addresses and ports of all masters in the cluster and separate multiple addresses with commas (,). For example: **192.168.1.1:6379,192.168.0.0:6379**

   b. Configure **Target Redis Type** and **Target Redis Instance**:

      Set **Redis in the cloud** for **Target Redis Type** and add **Target Redis Instance**.

   c. Configure **Source Redis Instance Password** and **Target Redis Instance Password**: If the instance is password-protected, click **Test Connection** to check whether the instance password is correct and whether the network is connected. If the instance is not password-protected, click **Test Connection** directly. If the test fails, check whether the password is correct, and whether the migration task network is connected.

      If a DCS Redis instance is used, the users created in :ref:`Managing Users <dcs-ug-221220>` are currently unavailable.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

   If the migration fails, click the migration task and check the log on the **Migration Logs** page.

   .. note::

      -  Once incremental migration starts, it remains **Migrating** after full migration.
      -  To manually stop a migration task, select the check box on the left of the migration task and click **Stop** above the migration task.

Verifying the Migration
-----------------------

Before data migration, if the target Redis has no data, check data integrity after the migration is complete in the following way:

#. Connect to the source Redis and the target Redis. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. Run the **info keyspace** command to check the values of **keys** and **expires**.

   |image2|

#. Calculate the differences between the values of **keys** and **expires** of the source Redis and the target Redis. If the differences are the same, the data is complete and the migration is successful.

During full migration, source Redis data updated during the migration will not be migrated to the target instance.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0293255709.png
