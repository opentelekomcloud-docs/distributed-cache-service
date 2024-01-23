:original_name: dcs-ug-210330002.html

.. _dcs-ug-210330002:

Scanning Expired Keys
=====================

Background
----------

There are two ways to delete a key in Redis.

-  Use the **DEL** command to directly delete a key.
-  Use commands such as **EXPIRE** to set a timeout on a key. After the timeout elapses, the key becomes inaccessible but is not deleted immediately because Redis is mostly single-threaded. Redis uses the following strategies to release the memory used by expired keys:

   -  Lazy free deletion: The deletion strategy is controlled in the main I/O event loop. Before a read/write command is executed, a function is called to check whether the key to be accessed has expired. If it has expired, it will be deleted and a response will be returned indicating that the key does not exist. If the key has not expired, the command execution resumes.

   -  Scheduled deletion: A time event function is executed at certain intervals. Each time the function is executed, a random collection of keys are checked, and expired keys are deleted. (By default, 10 checks are executed every second. Each check randomly scans 20 keys which are set to expire.)

      .. note::

         To avoid prolonged blocks on the Redis main thread, not all keys are checked in each time event. Instead, a random collection of keys are checked each time. As a result, the memory used by expired keys cannot be released quickly.

Expired Key Scan
----------------

DCS integrates these strategies and allows you to periodically release the memory used by expired keys. You can configure scheduled scans on the master nodes of your instances. The entire keyspace is traversed during the scans, triggering Redis to check whether the keys have expired and to remove expired keys if any.

.. note::

   This function is supported only by DCS Redis 4.0, 5.0, and 6.0 instances.

   Perform expired key scans during off-peak hours to avoid 100% CPU usage.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner of the management console and select the region where your instance is located.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS Redis instance.

#. Choose **Analysis and Diagnosis** > **Cache Analysis**.

#. On the **Expired Key Scan** tab page, scan for expired keys and release them.

   -  Click **Start Scanning** to scan for expired keys immediately.
   -  Enable **Scheduled** to schedule automatic scans at a specified time. For details about how to configure automatic scans, see :ref:`Scheduling Automatic Scans <dcs-ug-210330002__en-us_topic_0000001094742130_section169111727182515>`.

#. After the expired key scan task is submitted, view it in the task list.


   .. figure:: /_static/images/en-us_image_0000001730390749.png
      :alt: **Figure 1** Expired key scan tasks

      **Figure 1** Expired key scan tasks

.. note::

   The scan fails in the following scenarios:

   -  An exception occurred.
   -  There are too many keys, resulting in a timeout. Some keys have already been deleted before the timeout.

.. _dcs-ug-210330002__en-us_topic_0000001094742130_section169111727182515:

Scheduling Automatic Scans
--------------------------

To schedule automatic scans, click |image2| next to **Scheduled**. Set the parameters as required, and click **OK**.

:ref:`Table 1 <dcs-ug-210330002__en-us_topic_0000001094742130_table74477042711>` describes the parameters for scheduling automatic scans.

.. _dcs-ug-210330002__en-us_topic_0000001094742130_table74477042711:

.. table:: **Table 1** Parameters for scheduling automatic scans

   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                                                                                                                                                                                                                                                                                                                                                             | Value Range                 | Default Value | Remarks                                                                                                                                                                                                                               |
   +=================+=========================================================================================================================================================================================================================================================================================================================================================================================================================================+=============================+===============+=======================================================================================================================================================================================================================================+
   | Start At        | The first scan can only start after the current time.                                                                                                                                                                                                                                                                                                                                                                                   | Format: YYYY-MM-DD hh:mm:ss | ``-``         | ``-``                                                                                                                                                                                                                                 |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Interval        | Interval between scans.                                                                                                                                                                                                                                                                                                                                                                                                                 | 0 to 43,200 (unit: minute)  | 1440          | -  If the previous scan is not complete when the start time arrives, the upcoming scan will be skipped.                                                                                                                               |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               | -  If the previous scan is complete within five minutes after the start time, the upcoming scan will not be skipped.                                                                                                                  |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               |                                                                                                                                                                                                                                       |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               |    .. note::                                                                                                                                                                                                                          |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               |                                                                                                                                                                                                                                       |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               |       Continuous scans may cause high CPU usage. Set this parameter based on the total number of keys in the instance and the increase of keys. For details, see the following performance description and configuration suggestions. |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Timeout         | This parameter is used to prevent scanning timeout due to unknown reasons. If scanning times out due to unknown reasons, subsequent scheduled tasks cannot be executed. After the specified timeout elapses, a failure message is returned and the next scan will be performed.                                                                                                                                                         | 1 to 86,400 (unit: minute)  | 2880          | -  Set the timeout to at least twice the interval.                                                                                                                                                                                    |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                         |                             |               | -  You can set a value based on the time taken in previous scans and the maximum timeout that can be tolerated in the application scenario.                                                                                           |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Keys to Iterate | The **SCAN** command is used to iterate the keys in the current database. The **COUNT** option is used to let the user tell the iteration command how many elements should be returned from the dataset in each iteration. For details, see the `description of the SCAN command <https://redis.io/commands/scan/>`__. Iterative scanning can reduce the risks of slowing down Redis when a large number of keys are scanned at a time. | 10 to 1000                  | 10            | For example, if there are 10 million keys in Redis and the number of keys to iterate is set to 1000, a full scan will be complete after 10,000 iterations.                                                                            |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Performance**

-  The **SCAN** command is executed at the data plane every 5 ms, that is, 200 times per second. If **Keys to Iterate** is set to **10**, **100**, or **1000**, 2000, 20,000, or 200,000 keys are scanned per second.
-  The larger the number of keys scanned per second, the higher the CPU usage.

**Reference test**

A master/standby instance is scanned. There are 10 million keys that will not expire and 5 million keys that will expire. The expiration time is 1 to 10 seconds.

-  Natural deletion: 10,000 records are deleted per second. It takes 8 minutes to delete 5 million expired keys. The CPU usage is about 5%.
-  **Keys to Iterate** set to **10**: The scanning takes 125 minutes (15 million/2000/60 seconds) and the CPU usage is about 8%.
-  **Keys to Iterate** set to **50**: The scanning takes 25 minutes (15 million/10,000/60 seconds) and the CPU usage is about 10%.
-  **Keys to Iterate** set to **100**: The scanning takes 12.5 minutes (15 million/20,000/60 seconds) and the CPU usage is about 20%.
-  **Keys to Iterate** set to **1000**: The scanning takes 1.25 minutes (15 million/200,000/60 seconds) and the CPU usage is about 25%.

**Configuration suggestions**

-  You can configure the number of keys to be scanned and the scanning interval based on the total number of keys and the increase in the number of keys in the instance.
-  In the reference test with 15 million keys and **Keys to Iterate** set to **10**, the scanning takes about 125 minutes. In this case, set the interval to more than 4 hours.
-  If you want to accelerate the scanning, set **Keys to Iterate** to **100**. It takes about 12.5 minutes to complete the scanning. Therefore, set the interval to more than 30 minutes.
-  The larger the number of keys to iterate, the faster the scanning, and the higher the CPU usage. There is a trade-off between time and CPU usage.
-  If the number of expired keys does not increase rapidly, you can scan expired keys once a day.

   .. note::

      Start scanning during off-peak hours. Set the interval to one day and the timeout to two days.

.. |image1| image:: /_static/images/en-us_image_0000001681179997.png
.. |image2| image:: /_static/images/en-us_image_0000001153500240.png
