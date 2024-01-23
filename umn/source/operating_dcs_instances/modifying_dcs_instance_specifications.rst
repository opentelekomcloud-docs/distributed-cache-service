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

      +--------------+-----------------+-----------------+-------------------------+---------------+
      | Cache Engine | Single-Node     | Master/Standby  | Redis Cluster           | Proxy Cluster |
      +==============+=================+=================+=========================+===============+
      | Redis 3.0    | Scaling up/down | Scaling up/down | N/A                     | Scaling up    |
      +--------------+-----------------+-----------------+-------------------------+---------------+
      | Redis 4.0    | Scaling up/down | Scaling up/down | Scaling up              | N/A           |
      +--------------+-----------------+-----------------+-------------------------+---------------+
      | Redis 5.0    | Scaling up/down | Scaling up/down | Scaling up              | N/A           |
      +--------------+-----------------+-----------------+-------------------------+---------------+
      | Redis 6.0    | Scaling up/down | Scaling up/down | Scaling up/down, out/in | N/A           |
      +--------------+-----------------+-----------------+-------------------------+---------------+

   .. note::

      If the reserved memory of a DCS Redis 3.0 instance is insufficient, the scaling may fail when the memory is used up.

-  **Impact of scaling:**

   -  Single-node and master/standby

      -  A DCS Redis 4.0/5.0/6.0 instance will be disconnected for several seconds and remain read-only for about 1 minute.
      -  A DCS Redis 3.0 instance will be disconnected and remain read-only for 5 to 30 minutes.
      -  For scaling up, only the memory of the instance is expanded. The CPU processing capability is not improved.
      -  Data of single-node instances may be lost because they do not support data persistence. After scaling, check whether the data is complete and import data if required.
      -  Backup records of master/standby instances cannot be used after scaling down.

   -  Cluster

      -  If the shard quantity is not decreased, the instance can always be connected, but the CPU usage will increase, compromising performance by up to 20%, and the latency will increase during data migration.
      -  During scaling up, new Redis Server nodes are added, and data is automatically balanced to the new nodes.
      -  Nodes will be deleted if the shard quantity decreases. To prevent disconnection, ensure that the deleted nodes are not directly referenced in your application.
      -  Ensure that the used memory of each node is less than 70% of the maximum memory per node of the new flavor. Otherwise, you cannot perform the scale-in.
      -  If the memory becomes full during scaling due to a large amount of data being written, scaling will fail. Modify specifications during off-peak hours.
      -  Scaling involves data migration. The latency for accessing the key being migrated increases. For a Redis Cluster instance, ensure that the client can properly process the **MOVED** and **ASK** commands. Otherwise, requests will fail.
      -  Before scaling, perform cache analysis to ensure that no big keys (>= 512 MB) exist in the instance. Otherwise, scaling may fail.
      -  Backup records created before scaling cannot be restored.

-  **Notes on changing the number of replicas of a DCS Redis instance:**

   Deleting replicas interrupts connections. If your application cannot reconnect to Redis or handle exceptions, you need to restart the application after scaling.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.

4. Choose **More** > **Modify Specifications** in the row containing the DCS instance.

5. On the **Modify Specifications** page, select the desired specification.

6. Click **Submit** to start modifying the DCS instance.

   You can go to **Background Tasks** page to view the modification status. For more information, see :ref:`Viewing Background Tasks <dcs-ug-0312028>`.

   Specification modification of a single-node or master/standby DCS instance takes about 5 to 30 minutes to complete, while that of a cluster DCS instance takes a longer time. After an instance is successfully modified, it changes to the **Running** state.

   .. note::

      -  If the specification modification of a single-node DCS instance fails, the instance is temporarily unavailable for use. The specification remains unchanged. Some management operations (such as parameter configuration and specification modification) are temporarily not supported. After the specification modification is completed in the backend, the instance changes to the new specification and becomes available for use again.
      -  If the specification modification of a master/standby or cluster DCS instance fails, the instance is still available for use with its original specifications. Some management operations (such as parameter configuration, backup, restoration, and specification modification) are temporarily not supported. Remember not to read or write more data than allowed by the original specifications; otherwise, data loss may occur.
      -  After the specification modification is successful, the new specification of the instance takes effect.

.. |image1| image:: /_static/images/en-us_image_0000001194523049.png
