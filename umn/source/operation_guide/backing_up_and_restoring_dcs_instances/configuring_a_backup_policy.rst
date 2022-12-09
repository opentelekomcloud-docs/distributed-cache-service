:original_name: dcs-ug-0312031.html

.. _dcs-ug-0312031:

Configuring a Backup Policy
===========================

On the DCS console, you can configure an automatic backup policy. The system then backs up data in your instances according to the backup policy.

If automatic backup is not required, disable the automatic backup function in the backup policy.

Prerequisites
-------------

At least one master/standby DCS instance has been created.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. Click the name of the DCS instance to display more details about the DCS instance.
#. On the instance details page, click **Backups & Restorations**.
#. Slide |image2| to the right to enable automatic backup. Backup policies will be displayed.

   .. table:: **Table 1** Parameters in a backup policy

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================+
      | Backup Schedule                   | Day of a week on which data in the chosen DCS instance is automatically backed up.                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | You can select one or multiple days of a week.                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Retention Period (days)           | The number of days that automatically backed up data is retained.                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | Backup data will be permanently deleted at the end of retention period and cannot be restored. Value range: 1-7.                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Start Time                        | Time at which automatic backup starts. Value: the full hour between 00:00 to 23:00                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | The DCS checks backup policies once every hour. If the backup start time in a backup policy has arrived, data in the corresponding instance is backed up.                                                                                  |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   |    Instance backup takes 5 to 30 minutes. The data added or modified during the backup process will not be backed up. To reduce the impact of backup on services, it is recommended that data should be backed up during off-peak periods. |
      |                                   |                                                                                                                                                                                                                                            |
      |                                   |    Only instances in the **Running** state can be backed up.                                                                                                                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001194403149.png
.. |image2| image:: /_static/images/en-us_image_0000001256735725.png
