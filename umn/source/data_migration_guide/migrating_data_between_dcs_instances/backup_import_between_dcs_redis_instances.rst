:original_name: dcs-migration-0312004.html

.. _dcs-migration-0312004:

Backup Import Between DCS Redis Instances
=========================================

You can migrate data between DCS instances by importing backup files.

-  If the source Redis and target Redis are in the same region under the same DCS account, and the source Redis is not a single-node instance, see :ref:`Importing Backup Data from a Redis Instance <dcs-migration-0312004__en-us_topic_0000001893744560_section168361859027>`.
-  If the source Redis and target Redis are in different regions or under different DCS accounts, or the source Redis is a single-node instance, see :ref:`Importing Backup Data from an OBS Bucket <dcs-migration-0312004__en-us_topic_0000001893744560_section12790115912358>`.

Notes and Constraints
---------------------

To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

.. _dcs-migration-0312004__en-us_topic_0000001893744560_section7611653155815:

Prerequisites
-------------

-  You have successfully backed up the source Redis instance.

   -  For :ref:`Importing Backup Data from a Redis Instance <dcs-migration-0312004__en-us_topic_0000001893744560_section168361859027>`, you do not need to download the backup file to the local PC. For details about how to back up data, see :ref:`Manually Backing Up a DCS Instance <dcs-ug-0312032>`.
   -  For :ref:`Importing Backup Data from an OBS Bucket <dcs-migration-0312004__en-us_topic_0000001893744560_section12790115912358>`, download the backup file to the local PC by referring to :ref:`Downloading a Backup File <dcs-ug-0312034>`.

-  You have prepared the target Redis instance. If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.

   Redis is backward compatible. The target instance version must be the same as or later than the source instance version.

-  Ensure that the target Redis instance has sufficient storage space. You can clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

.. _dcs-migration-0312004__en-us_topic_0000001893744560_section168361859027:

Importing Backup Data from a Redis Instance
-------------------------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner of the console and select the region where your source and target instances are located.

#. In the navigation pane, choose **Data Migration**. The migration task list is displayed.

#. Click **Create Backup Import Task**.

#. Enter the task name and description.

   The task name must start with a letter, contain 4 to 64 characters, and contain only letters, digits, hyphens (-), and underscores (_).

#. For source Redis, set **Data Source** to **Redis**.


   .. figure:: /_static/images/en-us_image_0000001955154978.png
      :alt: **Figure 1** Selecting a data source (Redis)

      **Figure 1** Selecting a data source (Redis)

#. For **Source Redis Instance**, select the source instance to be migrated.

#. Select the backup task whose data is to be migrated.

#. For **Target Redis Instance**, select the DCS Redis instance prepared in :ref:`Prerequisites <dcs-migration-0312004__en-us_topic_0000001893744560_section7611653155815>`.

#. If the target Redis instance has a password, enter the password and click **Test Connection** to check whether the password is correct. If the instance is not password-protected, click **Test Connection** directly.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

.. _dcs-migration-0312004__en-us_topic_0000001893744560_section12790115912358:

Importing Backup Data from an OBS Bucket
----------------------------------------

Simply download the source Redis data and then upload the data to an OBS bucket in the same account and region as the target DCS Redis instance. After you have created a backup import task, data in the OBS bucket will be read and migrated to the target Redis.

.. note::

   -  .aof, .rdb, .zip, and .tar.gz files can be uploaded to OBS buckets. You can directly upload .aof and .rdb files or compress them into .zip or .tar.gz files before uploading.
   -  To migrate data from a cluster Redis instance, download all backup files and upload all of them to the OBS bucket. Each backup file contains data for a shard of the instance. During the migration, you need to select backup files of all shards.

#. **Create an OBS bucket in the account and region where the target Redis instance is located.** If a qualified OBS bucket is available, you do not need to create one.

   When creating an OBS bucket, pay attention to the configuration of the following parameters. For details on how to set other parameters, see "Creating a Bucket" in *Object Storage Service User Guide*.

   -  **Region**:

      The OBS bucket must be in the same region as the target DCS Redis instance.

   -  **Default Storage Class**: Select **Standard** or **Infrequent Access**.

      Do not select **Archive**. Otherwise, the migration will fail.

#. Upload the backup file to the OBS bucket.

   a. In the bucket list, click the name of the created bucket.

   b. In the navigation pane, choose **Objects**.

   c. On the **Objects** tab page, click **Upload Object**.

   d. Specify **Storage Class**.

      Do not select **Archive**. Otherwise, the migration will fail.

   e. Upload the objects.

      Drag files or folders to the **Upload Object** area or click **add file**.

      A maximum of 100 files can be uploaded at a time. The total size cannot exceed 5 GB. If the total size of files to be uploaded exceeds 5 GB, click "How to Upload a File Larger than 5 GB" in the upper part of the **Upload Object** dialog box and perform operations as instructed.

   f. Click **Upload**.

#. Click |image2| in the upper left corner and choose **Distributed Cache Service for Redis** under **Databases** to open the DCS console.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Backup Import Task**.

#. Enter the task name and description.

   The task name must start with a letter, contain 4 to 64 characters, and contain only letters, digits, hyphens (-), and underscores (_).

#. In the **Source Redis** area, select **OBS Bucket** for **Data Source** and then select the OBS bucket to which you have uploaded backup files.

#. Click **Add Backup** and select the backup files to be migrated.

#. In the **Target Redis** area, select the **Target Redis Instance** prepared in :ref:`Prerequisites <dcs-migration-0312004__en-us_topic_0000001893744560_section7611653155815>`.

#. If the target Redis instance has a password, enter the password and click **Test Connection** to check whether the password is correct. If the instance is not password-protected, click **Test Connection** directly.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

.. |image1| image:: /_static/images/en-us_image_0000001999635737.png
.. |image2| image:: /_static/images/en-us_image_0000001963155450.png
