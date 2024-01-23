:original_name: dcs-migration-1117001.html

.. _dcs-migration-1117001:

Backup Migration from Another Cloud
===================================

Application Scenarios
---------------------

Use the DCS console to migrate Redis data from Redis of another cloud or self-hosted Redis to DCS for Redis.

Simply download the source Redis data and then upload the data to an OBS bucket in the same region as the target DCS Redis instance. After you have created a migration task on the DCS console, DCS will read data from the OBS bucket and data will be migrated to the target instance.

.aof, .rdb, .zip, and .tar.gz files can be uploaded to OBS buckets. You can directly upload .aof and .rdb files or compress them into .zip or .tar.gz files before uploading.

Prerequisites
-------------

-  The OBS bucket must be in the same region as the target DCS Redis instance.
-  The data files to be uploaded must be in the .aof, .rdb, .zip, or .tar.gz format.
-  To migrate data from a single-node or master/standby Redis instance of another cloud, create a backup task and download the backup file.
-  To migrate data from a cluster Redis instance of another cloud, download all backup files, upload all of them to the OBS bucket, and select all of them for the migration. Each backup file contains data for a shard of the instance.

.. _dcs-migration-1117001__dcs-migration-190703002_section1128152020384:

Step 1: Prepare the Target DCS Redis Instance
---------------------------------------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.
-  If you already have a DCS Redis instance, you do not need to create one again, but you need to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`.

Step 2: Create an OBS Bucket and Upload Backup Files
----------------------------------------------------

#. Create an OBS bucket.

   a. Log in to the OBS Console and click **Create Bucket**.

   b. Select a region.

      The OBS bucket must be in the same region as the target DCS Redis instance.

   c. Specify **Bucket Name**.

      The bucket name must meet the naming rules specified on the console.

   d. Set **Storage Class** to **Standard**, **Warm** or **Cold**.

   e. Set **Bucket Policy** to **Private**, **Public Read**, or **Public Read and Write**.

   f. Configure default encryption.

   g. Click **Create Now**.

#. Upload the backup data files to the OBS bucket by using OBS Browser+.

   If the backup file to be uploaded does not exceed 5 GB, upload the file using the OBS console by referring to step :ref:`3 <dcs-migration-1117001__dcs-migration-190703002_dcs-ug-0312037_li8307135965315>`.

   If the backup file to be uploaded is larger than 5 GB, perform the following steps to upload the file using OBS Browser+.

   a. Download OBS Browser+.

      For details, see section "Downloading OBS Browser+" in *Object Storage Service (OBS) Tools Guide (OBS Browser+)*.

   b. Install OBS Browser+.

      For details, see section "Installing OBS Browser+" in *Object Storage Service (OBS) Tools Guide (OBS Browser+)*.

   c. Log in to OBS Browser+.

      For details, see section "Logging In to OBS Browser+" in *Object Storage Service (OBS) Tools Guide (OBS Browser+)*.

   d. Create a bucket.

   e. Upload backup data.

#. .. _dcs-migration-1117001__dcs-migration-190703002_dcs-ug-0312037_li8307135965315:

   On the OBS console, upload the backup data files to the OBS bucket.

   Perform the following steps if the backup file size does not exceed 5 GB:

   a. In the bucket list, click the name of the created bucket.

   b. In the navigation pane, choose **Objects**.

   c. On the **Objects** tab page, click **Upload Object**.

   d. Upload the objects.

      To upload objects, drag files or folders to the **Upload Object** area or click **add file**. A maximum of 100 files can be uploaded at a time. The total size cannot exceed 5 GB.


      .. figure:: /_static/images/en-us_image_0000001634759086.png
         :alt: **Figure 1** Uploading an object

         **Figure 1** Uploading an object

   e. (Optional) Select **KMS encryption** to encrypt the file you want to upload.

   f. Click **Upload**.

Step 3: Create a Migration Task
-------------------------------

#. Log in to the DCS console.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Backup Import Task**.

#. Enter the task name and description.

#. In the **Source Redis** area, select **OBS Bucket** for **Data Source** and then select the OBS bucket to which you have uploaded backup files.

#. Click **Add Backup** and select the backup files to be migrated.

#. In the **Target Redis** area, select the **Target Redis Instance** prepared in :ref:`Step 1: Prepare the Target DCS Redis Instance <dcs-migration-1117001__dcs-migration-190703002_section1128152020384>`.

#. If the target Redis instance has a password, enter the password and click **Test Connection** to check whether the password is correct. If the instance is not password-protected, click **Test Connection** directly.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.
