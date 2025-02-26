:original_name: dcs-migration-0312003.html

.. _dcs-migration-0312003:

Online Migration Between Instances
==================================

If the source and target instances are interconnected and the **SYNC** and **PSYNC** commands are supported by the source instance, data can be migrated online in full or incrementally from the source to the target.

.. note::

   During online migration, data is essentially synchronized in full to a new replica. Therefore, perform online migration during low-demand hours. Otherwise, source instance CPU usage may surge and latency may increase.

Notes and Constraints
---------------------

-  You cannot use public networks for online migration.
-  Before migrating data, read through :ref:`Migration Solution Notes <dcs-migration-090626002>` to learn about the DCS data migration function and select an appropriate target instance.
-  Migrating a later Redis instance to an earlier one may fail.
-  For earlier instances whose passwords contain single quotation marks ('), modify the password for online migration or try other methods.
-  By default, a cluster instance has only one DB (DB0). Before you migrate data from a multi-DB single-node or master/standby instance to a Redis Cluster instance, check whether any data exists on databases other than DB0. To ensure that the migration succeeds, move all data to DB0 by referring to :ref:`Online Migration with Rump <dcs-migration-090626001>`.
-  During online migration, you are advised to set **repl-timeout** on the source instance to 300s and **client-output-buffer-slave-hard-limit** and **client-output-buffer-slave-soft-limit** to 20% of the maximum memory of the instance.
-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.

-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`.

   If the data exists on the target instance, the replicated data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

Creating an Online Migration Task
---------------------------------

#. Log in to the DCS console.

   **If the source and target Redis are under different accounts, use the source account to log in to DCS.**

#. Click |image1| in the upper left corner of the console and select the region where your **source** instance is located.

   .. note::

      Only when the online migration task and the source Redis are under an account and in a region, the **SYNC** and **PSYNC** commands of the source Redis are allowed. Otherwise, online migration cannot be performed.

#. In the navigation pane, choose **Data Migration**. The migration task list is displayed.

#. Click **Create Online Migration Task**.

#. Enter the task name and description.

   The task name must start with a letter, contain 4 to 64 characters, and contain only letters, digits, hyphens (-), and underscores (_).

#. Configure the VPC, subnet, and security group for the migration task.

   .. note::

      -  Use the VPC of the source or target Redis.
      -  The online migration task uses a tenant IP address (**Migration ECS** displayed on the **Basic Information** page of the task.) If a whitelist is configured for the source or target instance, add the migration IP address to the whitelist or disable the whitelist.
      -  To allow the VM used by the migration task to access the source and target instances, set an outbound rule for the task's security group to allow traffic through the IP addresses and ports of the source and target instances. By default, all outbound traffic is allowed.

Checking the Network
--------------------

#. Check whether the source Redis instance, the target Redis instance, and the migration task are configured with the same VPC.

   If yes, go to :ref:`Configuring the Online Migration Task <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_section14919536272>`. If no, go to :ref:`2 <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li160420185217>`.

#. .. _dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li160420185217:

   Check whether the VPCs configured for the source Redis instance, the target Redis instance, and the migration task are connected to ensure that the VM resource of the migration task can access the source and target Redis instances.

   If yes, go to :ref:`Configuring the Online Migration Task <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_section14919536272>`. If no, go to :ref:`3 <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li423483319412>`.

#. .. _dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li423483319412:

   Perform the following operations to establish the network.

   -  If the source and target Redis instances are in the same DCS region, create a VPC peering connection by referring to "Peering Connection" in *Virtual Private Cloud (VPC) User Guide*.
   -  If the source and target Redis instances are in different DCS regions, create a connection by referring to the *Direct Connect User Guide*.

.. _dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_section14919536272:

Configuring the Online Migration Task
-------------------------------------

#. On the **Online Migration** tab page, click **Configure** in the row containing the online migration task you just created.

#. .. _dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li18777171715209:

   Select a migration type.

   Supported migration types are **Full** and **Full + Incremental**, which are described in :ref:`Table 1 <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_table55653322215>`.

   To :ref:`switch DCS instance IPs <dcs-migration-0312003__en-us_topic_0000001935864141_section12424655143818>` after instance migration, select **Full + Incremental** for the migration type.

   .. _dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_table55653322215:

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


   .. figure:: /_static/images/en-us_image_0000001955094688.png
      :alt: **Figure 1** Selecting the migration type

      **Figure 1** Selecting the migration type

#. Only if **Migration Type** is set to **Full + Incremental**, you can specify a bandwidth limit.

   The data synchronization rate can be kept around the bandwidth limit.

#. Specify **Auto-Reconnect**. If this option is enabled, automatic reconnections will be performed indefinitely in the case of a network exception.

   Full synchronization will be triggered and requires more bandwidth if incremental synchronization becomes unavailable. Exercise caution when enabling this option.

#. Configure **Source Redis** and **Target Redis**.

   a. Set **Source Redis Type** to **Redis in the cloud** and add **Source Redis Instance**.

   b. Configure **Target Redis Type** and **Target Redis Instance**:

      -  If the target Redis and migration task are in a VPC, or across VPCs over a network in a region, set **Target Redis Type** to **Redis in the cloud** and add **Target Redis Instance**.
      -  If the target Redis and migration task are in different regions, set **Target Redis Type** to **Self-hosted Redis** and add **Target Redis Instance**. If the target Redis is a Redis Cluster, enter the IP addresses and ports of all masters in the cluster and separate multiple addresses with commas (,). For example: **192.168.1.1:6379,192.168.0.0:6379**

   c. Configure **Source Redis Instance Password** and **Target Redis Instance Password**: If the instance is password-protected, click **Test Connection** to check whether the instance password is correct and whether the network is connected. If the instance is not password-protected, click **Test Connection** directly.

      Currently, the users created in :ref:`Managing Users <dcs-ug-221220>` are unavailable here.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

   If the migration fails, click the migration task and check the log on the **Migration Logs** page.

   .. note::

      -  Once full + incremental migration starts, it remains **Migrating** after full migration.
      -  To manually stop a migration task, select the check box on the left of the migration task and click **Stop** above the migration task.

Verifying the Migration
-----------------------

After the migration is complete, check data integrity in the following way.

#. Connect the source Redis and the target Redis. For details, see :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. Run the **info keyspace** command on the source and the target Redis to check the values of **keys** and **expires**.


   .. figure:: /_static/images/en-us_image_0000001990974029.png
      :alt: **Figure 2** Checking instance data

      **Figure 2** Checking instance data

#. Calculate the differences between the values of **keys** and **expires** of the source Redis and the target Redis. If the differences are the same, the data is complete and the migration is successful.

.. note::

   During full migration, source Redis data updated during the migration will not be migrated to the target instance.

.. _dcs-migration-0312003__en-us_topic_0000001935864141_section12424655143818:

(Optional) Switching DCS Instance IP Addresses
----------------------------------------------

The prerequisites for switching source and target Redis instance IP addresses are as follows. The target Redis can be accessed automatically on a client after the switch.

**Prerequisites:**

-  This function is supported by basic edition DCS Redis 4.0 instances and later, **but not by professional edition DCS Redis instances**.
-  For DCS Redis 3.0 instances, contact customer service to enable the whitelist for Redis 3.0 instance IP switches. The instance IP addresses can be switched only when the source instance is a DCS Redis 3.0 instance and the target instance is a basic edition DCS Redis 4.0, 5.0, or 6.0 instance.
-  The IP addresses of a source or target instance with public access enabled cannot be switched.
-  Instance IPs can be switched only for the source and target Redis that are single-node, master/standby, read/write splitting, or Proxy Cluster instances.
-  **Full + Incremental** must be selected in :ref:`2 <dcs-migration-0312003__en-us_topic_0000001935864141_en-us_topic_0292880550_dcs-migration-190703003_li18777171715209>`.
-  The source and target Redis instance ports must be consistent.

.. important::

   #. Online migration will stop during the switching.
   #. Instances will be read-only for one minute and disconnected for several seconds during the switching.
   #. If your application cannot reconnect to Redis or handle exceptions, you may need to restart the application after the IP switching.
   #. If the source and target instances are in different subnets, the subnet information will be updated after the switching.
   #. If the source is a master/standby instance, the IP address of the standby node will not be switched. Ensure that this IP address is not used by your applications.
   #. If your applications use a domain name to connect to Redis, the domain name will be used for the source instance. Select **Yes** for **Switch Domain Name**.
   #. Ensure that the passwords of the source and target instances are the same. If they are different, verification will fail after the switching.
   #. If a whitelist is configured for the source instance, ensure that the same whitelist is configured for the target instance before switching IP addresses.

#. On the **Data Migration** > **Online Migration** page, when the migration task status changes to **Incremental migration in progress**, choose **More** > **Switch IP** in the **Operation** column.

#. In the **Switch IP** dialog box, select whether to switch the domain name.

   .. note::

      -  If a Redis domain name is used on the client, switch it or you must modify the domain name on the client.
      -  If the domain name switch is not selected, only the instance IP addresses will be switched.

#. Click **OK**. The IP address switching task is submitted successfully. When the status of the migration task changes to **IP switched**, the IP address switching is complete.

   To restore the IPs, choose **More** > **Roll Back IP** in the operation column. The IPs are rolled back when the task is in the **Successful** state.

.. |image1| image:: /_static/images/en-us_image_0000001962038446.png
