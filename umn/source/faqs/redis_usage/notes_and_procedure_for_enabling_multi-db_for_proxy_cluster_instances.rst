:original_name: dcs-faq-210804001.html

.. _dcs-faq-210804001:

Notes and Procedure for Enabling Multi-DB for Proxy Cluster Instances
=====================================================================

Note the following constraints when you consider implementing multi-DB:

-  **Usage constraints:**

   #. The **SWAPDB** command does not support multi-DB.
   #. The **INFO KEYSPACE** command does not return data of multi-DB.
   #. To query the total number of keys in each database, use the customized **dbstats** command. CPU usage will surge on the node executing this command.
   #. LUA scripts do not support multi-DB.
   #. The **RANDOMKEY** command does not support multi-DB.
   #. **PUBLISH** cannot be used in Lua scripts.
   #. The database number ranges from 0 to 255.
   #. Proxy Cluster DCS Redis 3.0 instances do not support multi-DB.

-  **Performance constraints**

   #. The **FLUSHDB** command deletes keys one by one, which takes a long time and is slower than the open-source native implementation. The execution speed of the **FLUSHDB** command is the same as that of the **SCAN** command (which should be tested by the customer).
   #. The **DBSIZE** command is time-consuming. Do not use it in the code.
   #. If multi-DB is used, the performance of the **KEYS** and **SCAN** commands deteriorates by up to 50%.

-  **Other constraints**:

   The backend storage rewrites keys based on certain rules. Keys in the exported RDB file are not the original keys. However, the access through the Redis protocol is not affected.

Procedure for Enabling or Disabling Multi-DB
--------------------------------------------

By default, a Proxy Cluster instance is not enabled with multi-DB, but you can do as follows to enable multi-DB.

#. Log in to the DCS console.

#. Connect to the instance and run the **FLUSHALL** command to clear the instance data.

   .. note::

      Before enabling or disabling multi-DB, ensure that all instance data is cleared and no data is being written.

#. On the **Cache Manager** page of the DCS console, click the desired DCS instance.

#. Choose **Instance Configuration** > **Parameters**.

#. To enable multi-DB, click **Modify** in the row that contains parameter **multi-db**, and change its value to **yes**.

   To disable multi-DB, change the value to **no**.

#. Click **Save** and then confirm the modification. The instance does not need to be restarted.
