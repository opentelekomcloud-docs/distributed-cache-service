:original_name: dcs-ug-190808001.html

.. _dcs-ug-190808001:

Analyzing Big Keys and Hot Keys
===============================

By performing big key analysis and hot key analysis, you will have a picture of keys that occupy a large space and keys that are the most frequently accessed.

**Notes on big key analysis:**

-  All DCS Redis instances support big key analysis.
-  During big key analysis, all keys will be traversed. The larger the number of keys, the longer the analysis takes.
-  Perform big key analysis during off-peak hours and avoid automatic backup periods.
-  For a master/standby or cluster instance, the big key analysis is performed on the standby node, so the impact on the instance is minor. For a single-node instance, the big key analysis is performed on the only node of the instance and will reduce the instance access performance by up to 10%. Therefore, perform big key analysis on single-node instances during off-peak hours.
-  A maximum of 100 big key analysis records (20 for Strings and 80 for Lists/Sets/Zsets/Hashes) are retained for each instance. When this limit is reached, the oldest records will be deleted to make room for new records. You can also manually delete records you no longer need.

**Notes on hot key analysis:**

-  Only DCS Redis 4.0/5.0/6.0 instances support hot key analysis, and the **maxmemory-policy** parameter of the instances must be set to **allkeys-lfu** or **volatile-lfu**.
-  During hot key analysis, all keys will be traversed. The larger the number of keys, the longer the analysis takes.
-  Perform hot key analysis shortly after peak hours to ensure the accuracy of the analysis results.
-  The hot key analysis is performed on the master node of each instance and will reduce the instance access performance by up to 10%.
-  A maximum of 100 hot key analysis records are retained for each instance. When this limit is reached, the oldest records will be deleted to make room for new records. You can also manually delete records you no longer need.

.. note::

   Perform big key and hot key analysis during off-peak hours to avoid 100% CPU usage.

Big Key Analysis Procedure
--------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS Redis instance.

#. Choose **Analysis and Diagnosis** > **Cache Analysis**.

#. On the **Big Key Analysis** tab page, manually perform big key analysis or schedule daily automatic analysis.

#. After an analysis task completes, click **View** to view the analysis results.

   You can view the analysis results of different data types.

   .. note::

      A maximum of 20 big key analysis records are retained for Strings and 80 are retained for Lists, Sets, Zsets, and Hashes.

   .. table:: **Table 1** Results of big key analysis

      +-----------+-------------------------------------------------------------------+
      | Parameter | Description                                                       |
      +===========+===================================================================+
      | Key       | Name of a big key.                                                |
      +-----------+-------------------------------------------------------------------+
      | Type      | Type of a big key, which can be string, list, set, zset, or hash. |
      +-----------+-------------------------------------------------------------------+
      | Size      | Size or number of elements of a big key.                          |
      +-----------+-------------------------------------------------------------------+
      | Shard     | Shard where the big key of the cluster instance is located.       |
      +-----------+-------------------------------------------------------------------+
      | Database  | Database where a big key is located.                              |
      +-----------+-------------------------------------------------------------------+

.. _dcs-ug-190808001__section47852016145218:

Hot Key Analysis Procedure
--------------------------

#. Log in to the DCS console.

#. Click |image2| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS Redis instance.

#. Choose **Analysis and Diagnosis** > **Cache Analysis**.

#. On the **Hot Key Analysis** tab page, manually perform hot key analysis or schedule daily automatic analysis.

   .. note::

      If hot key analysis cannot be performed, set **maxmemory-policy** to **allkeys-lfu** or **volatile-lfu**. If this parameter has already been set to **allkeys-lfu** or **volatile-lfu**, perform hot key analysis right away.

#. After an analysis task completes, click **View** to view the analysis results.

   The hot key analysis results are displayed.

   .. note::

      The console displays a maximum of 100 hot key analysis records for each instance.

   .. table:: **Table 2** Results of hot key analysis

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                          |
      +===================================+======================================================================================================================================================================================================================================================================================================================================+
      | Key                               | Name of a hot key.                                                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Type                              | Type of a hot key, which can be string, hash, list, set, or sorted set.                                                                                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Size                              | Size of the hot key value.                                                                                                                                                                                                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FREQ                              | Reflects the access frequency of a key within a specific period of time.                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                                                      |
      |                                   | **FREQ** is the logarithmic access frequency counter. The maximum value of **FREQ** is 255, which indicates 1 million access requests. After **FREQ** reaches **255**, it will no longer increment even if access requests continue to increase. **FREQ** will decrement by 1 for every minute during which the key is not accessed. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Shard                             | Shard where the hot key of the cluster instance is located.                                                                                                                                                                                                                                                                          |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | DataBase                          | Database where a hot key is located.                                                                                                                                                                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001194403151.png
.. |image2| image:: /_static/images/en-us_image_0000001148603244.png
