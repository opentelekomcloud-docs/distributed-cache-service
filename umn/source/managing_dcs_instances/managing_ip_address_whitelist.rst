:original_name: dcs-ug-190812001.html

.. _dcs-ug-190812001:

Managing IP Address Whitelist
=============================

DCS helps you control access to your DCS instances in the following ways, depending on the deployment mode:

-  To control access to DCS Redis 3.0 instances, you can use security groups. Whitelists are not supported. For details about how to configure a security group, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.
-  To control access to DCS Redis 4.0/5.0/6.0 instances, you can use whitelists. Security groups are not supported.

The following describes how to manage whitelists of a Redis 4.0/5.0/6.0 instance to allow access only from whitelisted IP addresses. If no whitelists are added for the instance or the whitelist function is disabled, all IP addresses that can communicate with the VPC can access the instance.

Creating a Whitelist Group
--------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS instance.

#. Choose **Instance Configuration** > **Whitelist** and then click **Create Whitelist Group**.

#. In the **Create Whitelist Group** dialogue box, specify **Group Name** and **IP Address/Range**.

   .. table:: **Table 1** Whitelist parameters

      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------+
      | Parameter             | Description                                                                                                                                     | Example                |
      +=======================+=================================================================================================================================================+========================+
      | Group Name            | Whitelist group name of the instance.                                                                                                           | DCS-test               |
      |                       |                                                                                                                                                 |                        |
      |                       | A maximum of four whitelist groups can be created for each instance.                                                                            |                        |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------+
      | IP Address/Range      | A maximum of 20 IP addresses or IP address ranges can be added to an instance. Separate multiple IP addresses or IP address ranges with commas. | 10.10.10.1,10.10.10.10 |
      |                       |                                                                                                                                                 |                        |
      |                       | Unsupported IP address and IP address range: 0.0.0.0 and 0.0.0.0/0.                                                                             |                        |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------+

#. Click **OK**.

   A whitelist group is automatically enabled for the instance once created. Only whitelisted IP addresses can access the instance.

   .. note::

      -  In the whitelist group list, click **Modify** to modify the IP addresses or IP address ranges in a group, and click **Delete** to delete a whitelist group.
      -  After whitelist has been enabled, you can click **Disable Whitelist** above the whitelist group list to allow all IP addresses connected to the VPC to access the instance.

.. |image1| image:: /_static/images/en-us_image_0000001681129365.png
