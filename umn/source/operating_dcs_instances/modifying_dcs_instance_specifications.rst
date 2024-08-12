:original_name: dcs-ug-0326011.html

.. _dcs-ug-0326011:

Modifying DCS Instance Specifications
=====================================

On the DCS console, you can scale a DCS Redis instance to a larger or smaller capacity.

.. note::

   -  **Modify instance specifications during off-peak hours.** If the modification failed in peak hours (for example, when memory or CPU usage is over 90% or write traffic surges), try again during off-peak hours.
   -  If your DCS instances are too old to support scaling, contact technical support to upgrade the instances.
   -  Services may be interrupted for seconds during the modification. Therefore, services connected to Redis must support reconnection.
   -  Modifying instance specifications does not affect the connection address, password, data, security group, and whitelist configurations of the instance.

Change of the Instance Type
---------------------------

-  **Supported instance type changes:**

   -  From single-node to master/standby: Supported by Redis 3.0, and not by Redis 4.0/5.0/6.0.

   -  From master/standby to Proxy Cluster: Supported by Redis 3.0, and not by Redis 4.0/5.0/6.0.

      If the data of a master/standby DCS Redis 3.0 instance is stored in multiple databases, or in non-DB0 databases, the instance cannot be changed to the Proxy Cluster type. A master/standby instance can be changed to the Proxy Cluster type only if its data is stored only on DB0.

   -  From cluster types to other types: Not supported.

-  **Impact of instance type changes:**

   -  From single-node to master/standby for a DCS Redis 3.0 instance:

      The instance cannot be connected for several seconds and remains read-only for about 1 minute.

   -  From master/standby to Proxy Cluster for a DCS Redis 3.0 instance:

      The instance cannot be connected and remains read-only for 5 to 30 minutes.

Scaling
-------

-  **The following table lists scaling options supported by different DCS instances.**

   .. table:: **Table 1** Scaling options supported by different DCS instances

      +--------------+-----------------+-----------------+------------------------------------------------------+---------------+
      | Cache Engine | Single-Node     | Master/Standby  | Redis Cluster                                        | Proxy Cluster |
      +==============+=================+=================+======================================================+===============+
      | Redis 3.0    | Scaling up/down | Scaling up/down | N/A                                                  | Scaling out   |
      +--------------+-----------------+-----------------+------------------------------------------------------+---------------+
      | Redis 4.0    | Scaling up/down | Scaling up/down | Scaling up/out, down/in, and replica quantity change | N/A           |
      +--------------+-----------------+-----------------+------------------------------------------------------+---------------+
      | Redis 5.0    | Scaling up/down | Scaling up/down | Scaling up/out, down/in, and replica quantity change | N/A           |
      +--------------+-----------------+-----------------+------------------------------------------------------+---------------+
      | Redis 6.0    | Scaling up/down | Scaling up/down | Scaling up/down, out/in, and replica quantity change | N/A           |
      +--------------+-----------------+-----------------+------------------------------------------------------+---------------+

   .. note::

      If the reserved memory of a DCS Redis 3.0 instance is insufficient, the scaling may fail when the memory is used up.

      Change the replica quantity and capacity separately.

-  **Impact of scaling**

   .. table:: **Table 2** Impact of scaling

      +---------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Instance Type                   | Scaling Type          | Impact                                                                                                                                                                                                                                                                                                                                                   |
      +=================================+=======================+==========================================================================================================================================================================================================================================================================================================================================================+
      | Single-node and master/standby  | Scaling up/down       | -  During scaling up, a DCS Redis 4.0/5.0/6.0 instance will be disconnected for several seconds and remain read-only for about 1 minute. During scaling down, connections will not be interrupted.                                                                                                                                                       |
      |                                 |                       | -  A DCS Redis 3.0 instance will be disconnected for several seconds and remain read-only for 5 to 30 minutes.                                                                                                                                                                                                                                           |
      |                                 |                       | -  For scaling up, only the memory of the instance is expanded. The CPU processing capability is not improved.                                                                                                                                                                                                                                           |
      |                                 |                       | -  Single-node DCS instances do not support data persistence. Scaling may compromise data reliability. After scaling, check whether the data is complete and import data if required. If there is important data, use a migration tool to migrate the data to other instances for backup.                                                                |
      |                                 |                       | -  For master/standby instances, backup records created before scale-down cannot be used after scale-down. If necessary, download the backup file in advance or back up the data again after scale-down.                                                                                                                                                 |
      +---------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Proxy Cluster and Redis Cluster | Scaling up/down       | -  Scaling out by adding shards:                                                                                                                                                                                                                                                                                                                         |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       |    -  **Scaling out does not interrupt connections but will occupy CPU resources, decreasing performance by up to 20%.**                                                                                                                                                                                                                                 |
      |                                 |                       |    -  If the shard quantity increases, new Redis Server nodes are added, and data is automatically balanced to the new nodes, increasing the access latency.                                                                                                                                                                                             |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       | -  Scaling in by reducing shards:                                                                                                                                                                                                                                                                                                                        |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       |    -  If the shard quantity decreases, nodes will be deleted. **Before scaling in a Redis Cluster instance, ensure that the deleted nodes are not directly referenced in your application, to prevent service access exceptions.**                                                                                                                       |
      |                                 |                       |    -  **Nodes will be deleted**, and connections will be interrupted. If your application cannot reconnect to Redis or handle exceptions, you may need to restart the application after scaling.                                                                                                                                                         |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       | -  Scaling up by shard size without changing the shard quantity:                                                                                                                                                                                                                                                                                         |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       |    -  **Insufficient memory of the node's VM will cause the node to migrate. Service connections may stutter and the instance may become read-only during the migration.**                                                                                                                                                                               |
      |                                 |                       |    -  Increasing the node capacity when the VM memory is sufficient does not affect services.                                                                                                                                                                                                                                                            |
      |                                 |                       |                                                                                                                                                                                                                                                                                                                                                          |
      |                                 |                       | -  Scaling down by reducing the shard size without changing the shard quantity has no impact.                                                                                                                                                                                                                                                            |
      |                                 |                       | -  To scale down an instance, ensure that the used memory of each node is less than 70% of the maximum memory per node of the new flavor.                                                                                                                                                                                                                |
      |                                 |                       | -  **The flavor changing operation may involve data migration, and the latency may increase. For a Redis Cluster instance, ensure that the client can process the MOVED and ASK commands. Otherwise, the request will fail.**                                                                                                                            |
      |                                 |                       | -  If the memory becomes full during scaling due to a large amount of data being written, scaling will fail.                                                                                                                                                                                                                                             |
      |                                 |                       | -  Before scaling, **check for big keys through Cache Analysis**. Redis has a limit on key migration. If the instance has any single key greater than 512 MB, scaling will fail when big key migration between nodes times out. The bigger the key, the more likely the migration will fail.                                                             |
      |                                 |                       | -  **Before scaling a Redis Cluster instance, ensure that automated cluster topology refresh is enabled.** If it is disabled, you will need to restart the client after scaling. For details about how to enable automated refresh if you use Lettuce, see :ref:`an example of using Lettuce to connect to a Redis Cluster instance <dcs-ug-211105002>`. |
      |                                 |                       | -  Backup records created before scaling cannot be used. If necessary, download the backup file in advance or back up the data again after scaling.                                                                                                                                                                                                      |
      +---------------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.

4. Choose **More** > **Modify Specifications** in the row containing the DCS instance.

5. On the **Modify Specifications** page, select the desired specification.

   .. note::

      For a master/standby DCS Redis 4.0/5.0 instance or a Redis Cluster DCS Redis 4.0/5.0/6.0 instance, you can choose to change by specification or replica quantity.

6. Set **Apply Change** to **Now** or **During maintenance**.

   Select **During maintenance** if the modification interrupts connections.

   .. table:: **Table 3** Scenarios where specification modification interrupts connections

      +---------------------------------------------------------+-----------------------------------------------------------------------+
      | Change                                                  | When Connections Are Interrupted                                      |
      +=========================================================+=======================================================================+
      | Scaling up a single-node or master/standby instance     | Memory is increased from a size smaller than 8 GB to 8 GB or larger.  |
      +---------------------------------------------------------+-----------------------------------------------------------------------+
      | Scaling down a Proxy Cluster and Redis Cluster instance | The number of shards is decreased.                                    |
      +---------------------------------------------------------+-----------------------------------------------------------------------+
      | Deleting replicas                                       | Replicas are deleted from a master/standby or Redis Cluster instance. |
      +---------------------------------------------------------+-----------------------------------------------------------------------+

   .. note::

      -  If the modification does not interrupt connections, it will be applied immediately even if you select **During maintenance**.
      -  The modification cannot be withdrawn once submitted. To reschedule a modification, you can change the maintenance window. The maintenance window can be changed up to three times.
      -  Modifications on DCS Redis 3.0 instances can only be applied immediately.
      -  If you apply the change during maintenance, the change starts at any time within the maintenance window, rather than at the start time of the window.
      -  If a large amount of data needs to be migrated when you scale down a cluster instance, the operation may not be completed within the maintenance window.

7. Click **Next**. In the dialog box that is displayed, click **Yes**.

8. Confirm the change details and view the risk check result.

   If any risk is found in the check, the instance may fail to be modified. For details, see :ref:`Table 4 <dcs-ug-0326011__table2414162318507>`.

   .. _dcs-ug-0326011__table2414162318507:

   .. table:: **Table 4** Risk check items

      +-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Check Item                                                                    | Reason for Check                                                                                                                                                                                                  | Solution                                                                                                                       |
      +===============================================================================+===================================================================================================================================================================================================================+================================================================================================================================+
      | Dataset memory distribution check                                             | Specification modification of a cluster instance involves data migration between nodes. If an instance has any key bigger than 512 MB, the modification will fail when big key migration between nodes times out. | :ref:`Analyze big keys <dcs-ug-190808001>` and :ref:`Handle big keys <dcs-faq-0521005>` before proceeding with the change.     |
      |                                                                               |                                                                                                                                                                                                                   |                                                                                                                                |
      | .. note::                                                                     | If the instance dataset memory is unevenly distributed among nodes and the difference is greater than 512 MB, the instance has a big key and the change may fail.                                                 |                                                                                                                                |
      |                                                                               |                                                                                                                                                                                                                   |                                                                                                                                |
      |    This check item applies only to Proxy Cluster and Redis Cluster instances. |                                                                                                                                                                                                                   |                                                                                                                                |
      +-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Memory usage check                                                            | If the memory usage of a node is greater than 90%, keys may be evicted or the change may fail.                                                                                                                    | If the memory usage is too high, optimize the memory by optimizing big keys, scanning for expired keys, or deleting some keys. |
      +-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Network input traffic check                                                   | The change may fail if the network input traffic is too heavy and the write buffer overflows.                                                                                                                     | Perform the change during off-peak hours.                                                                                      |
      |                                                                               |                                                                                                                                                                                                                   |                                                                                                                                |
      | .. note::                                                                     |                                                                                                                                                                                                                   |                                                                                                                                |
      |                                                                               |                                                                                                                                                                                                                   |                                                                                                                                |
      |    This check item applies only to single-node, and master/standby instances. |                                                                                                                                                                                                                   |                                                                                                                                |
      +-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | CPU usage check                                                               | If the node CPU usage within 5 minutes is greater than 90%, the change may fail.                                                                                                                                  | Perform the change during off-peak hours.                                                                                      |
      +-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+

9. Click **Submit** to start modifying the DCS instance.

   You can go to **Background Tasks** page to view the modification status. For more information, see :ref:`Viewing Background Tasks <dcs-ug-0312028>`.

   Specification modification of a single-node or master/standby DCS instance takes about 5 to 30 minutes to complete, while that of a cluster DCS instance takes a longer time. After an instance is successfully modified, it changes to the **Running** state.

   .. note::

      -  If the specification modification of a single-node DCS instance fails, the instance is temporarily unavailable for use. The specification remains unchanged. Some management operations (such as parameter configuration and specification modification) are temporarily not supported. After the specification modification is completed in the backend, the instance changes to the new specification and becomes available for use again.
      -  If the specification modification of a master/standby or cluster DCS instance fails, the instance is still available for use with its original specifications. Some management operations (such as parameter configuration, backup, restoration, and specification modification) are temporarily not supported. Remember not to read or write more data than allowed by the original specifications; otherwise, data loss may occur.
      -  After the specification modification is successful, the new specification of the instance takes effect.

.. |image1| image:: /_static/images/en-us_image_0000001194523049.png
