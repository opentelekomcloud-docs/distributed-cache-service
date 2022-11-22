:original_name: dcs-ug-210226001.html

.. _dcs-ug-210226001:

Importing Backup Files from Redis
=================================

Scenario
--------

Use the DCS console to migrate Redis data from self-hosted Redis to DCS for Redis.

Simply back up your Redis data, create a migration task on the DCS console, and then import the backup to a DCS Redis instance.

Prerequisites
-------------

A master/standby or cluster DCS Redis instance has been created as the target for the migration. The source instance has data and has been backed up.

.. _dcs-ug-210226001__section15805239143710:

Step 1: Obtain the Source Instance Name and Password
----------------------------------------------------

Obtain the name of the source Redis instance.

.. _dcs-ug-210226001__en-us_topic_0179456697_en-us_topic_0177563520_section1128152020384:

Step 2: Prepare the Target DCS Redis Instance
---------------------------------------------

-  If a DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0326008>`.
-  If a DCS Redis instance is available, you do not need to create a new one. However, you must clear the instance data before the migration.

   -  If the target instance is Redis 4.0 or 5.0, clear the data by referring to :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`.
   -  If the target instance is a DCS Redis 3.0 instance, run the **FLUSHALL** command to clear data.

You can use a DCS Redis 3.0, 4.0, or 5.0 instance as the target instance.

Step 3: Create a Migration Task
-------------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Data Migration**.

#. Click **Create Backup Import Task**.

#. Enter the task name and description.

#. Set **Data Source** to **Redis**.

#. For source Redis, select the instance prepared in :ref:`Step 1: Obtain the Source Instance Name and Password <dcs-ug-210226001__section15805239143710>`.

#. Select the backup task whose data is to be migrated.

#. Select the target instance created in :ref:`Step 2: Prepare the Target DCS Redis Instance <dcs-ug-210226001__en-us_topic_0179456697_en-us_topic_0177563520_section1128152020384>`.

#. Enter the password of the target instance. Click **Test Connection** to verify the password.

#. Click **Next**.

#. Confirm the migration task details and click **Submit**.

   Go back to the data migration task list. After the migration is successful, the task status changes to **Successful**.

.. |image1| image:: /_static/images/en-us_image_0000001148443514.png
