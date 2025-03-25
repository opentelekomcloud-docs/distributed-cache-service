:original_name: en-us_topic_0079835992.html

.. _en-us_topic_0079835992:

Overview
========

On the DCS console, you can back up and restore DCS instances.

Importance of DCS Instance Backup
---------------------------------

There is a small chance that inconsistent data could exist in a DCS instance owing to service system exceptions or problems in loading data from persistence files. In addition, some systems demand not only high reliability but also data security, data restoration, and even permanent data storage.

Currently, data in DCS instances can be backed up to OBS. If a DCS instance becomes faulty, data in the instance can be restored from backup so that service continuity is not affected.

Backup Modes
------------

DCS instances support the following backup modes:

-  Automated backup

   You can create a scheduled backup policy on the DCS console. Then, data in the chosen DCS instances will be automatically backed up at the scheduled time.

   You can choose the days of the week on which scheduled backup will run. Backup data will be retained for a maximum of seven days. Backup data older than seven days will be automatically deleted.

   The primary purpose of scheduled backups is to create complete data replicas of DCS instances so that the instance can be quickly restored if necessary.

-  Manual backup

   Backup requests can be issued manually. Data in the chosen DCS instances will be backed up to OBS.

   Before performing high-risk operations, such as system maintenance or upgrade, back up DCS instance data.

   When a DCS instance is in use, its backup data will not be automatically deleted. You can manually delete backup data as required. When you delete the instance, its backup data is deleted along with the instance. If you need the backup data, download and save it in advance.

Impact on DCS Instances During Backup
-------------------------------------

**Backup tasks are run on standby cache nodes, without incurring any downtime.**

In the event of full synchronization of master and standby nodes or heavy instance load, it takes a few minutes to complete data synchronization. If instance backup starts before data synchronization is complete, the backup data will be slightly behind the data in the master cache node.

New data changes on the master node during an ongoing backup are not included in the backup.

Additional Information About Data Backup
----------------------------------------

-  Instance type

   Redis: Only master/standby, Proxy Cluster, and Redis Cluster instances can be backed up and restored, while single-node instances cannot. However, you can export data of a single-node instance to an RDB file using redis-cli. For details, see :ref:`Can I Export Backup Data of DCS Redis Instances to RDB Files Using the Console? <dcs-faq-0730054>`

-  Backup mechanisms

   DCS for Redis 3.0 persists data with Redis AOF. DCS for Redis 4.0 and later persist data to RDB or AOF files in manual backup mode, and to RDB files in automatic backup mode.

   Backup tasks run on standby cache nodes. DCS instance data is backed up by compressing and storing the data persistence files from the standby cache node to OBS.

   DCS checks instance backup policies once an hour. If a backup policy is matched, DCS runs a backup task for the corresponding DCS instance.

-  Impact on DCS instances during backup

   Backup tasks run on standby cache nodes, without incurring any downtime.

   In the event of full-data synchronization or heavy instance load, it takes a few minutes to complete data synchronization. If instance backup starts before data synchronization is complete, the backup data will be slightly behind the data in the master cache node.

   During instance backup, the standby cache node stops persisting the latest changes to disk files. If new data is written to the master cache node during backup, the backup file will not contain the new data.

-  Backup time

   It is advisable to back up instance data during off-peak periods.

-  Storage of backup files

   Backup files are stored to OBS.

-  Handling exceptions in scheduled backup

   If a scheduled backup task is triggered while the DCS instance is restarting or being scaled up, the scheduled backup task will be run in the next cycle.

   If backing up a DCS instance fails or the backup is postponed because another task is in progress, DCS will try to back up the instance in the next cycle. A maximum of three retries are allowed within a single day.

-  Retention period of backup data

   Scheduled backup: Files can be retained for up to seven days. Overdue backup files that are created earlier will be automatically deleted, but at least one backup file will be retained.

   Manual backup: The latest backup files (up to 24) are always stored unless they are manually deleted.

   .. note::

      -  A total of 24 latest backups (automatic and manual) can be stored. To store the 25th backup, the earliest one will be automatically deleted.
      -  When you delete the instance, its backup data is deleted along with the instance. If you need the backup data, download and save it in advance.

Data Restoration
----------------

-  Data restoration process

   #. You can initiate a data restoration request using the DCS console.
   #. DCS obtains the backup file from OBS.
   #. Read/write to the DCS instance is suspended.
   #. The original data persistence file of the master cache node is replaced by the backup file.
   #. The new data persistence file (that is, the backup file) is reloaded.
   #. Data is restored, and the DCS instance starts to provide read/write service again.

-  Impact on service systems

   Restoration tasks run on master cache nodes. During restoration, data cannot be written into or read from instances.

-  Handling data restoration exceptions

   If a backup file is corrupted, DCS will try to fix the backup file while restoring instance data. If the backup file is successfully fixed, the restoration proceeds. If the backup file cannot be fixed, the master/standby DCS instance will be changed back to the state in which it was before data restoration.
