:original_name: dcs-ug-0312034.html

.. _dcs-ug-0312034:

Downloading a Backup File
=========================

Automatically backed up data can be retained for a maximum of 7 days. Manually backed up data is not free of charge and takes space in OBS. Due to these limitations, you are advised to download the RDB and AOF backup files and permanently save them on the local host.

This function is supported only by master/standby and cluster instances, and not by single-node instances. To export the data of a single-node instance to an RDB file, you can use redis-cli. For details, see :ref:`How Do I Export DCS Redis Instance Data? <dcs-faq-0730053>`

Prerequisites
-------------

The instance has been backed up and the backup is still valid.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

   Filter DCS instances to find the desired one.

#. Click the name of the DCS instance to display more details about the DCS instance.

#. On the instance details page, click **Backups & Restorations**.

   A list of historical backup tasks is then displayed.

#. Select the historical backup data to be downloaded, and click **Download**.

#. In the displayed, **Download Backup File** dialog box, select either of the following two download methods.

   Download methods:

   -  By URL

      a. Set the URL validity period and click **Query**.
      b. Download the backup file by using the URL list.

         .. note::

            If you choose to copy URLs, use quotation marks to quote the URLs when running the **wget** command in Linux. For example:

            **wget 'https://obsEndpoint.com:443/redisdemo.rdb?parm01=value01&parm02=value02'**

            This is because the URL contains the special character and (&), which will confuse the **wget** command. Quoting the URL facilitates URL identification.

   -  By OBS

      Perform the procedure as prompted.

.. |image1| image:: /_static/images/en-us_image_0000001194403147.png
