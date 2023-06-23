:original_name: dcs-ug-0312008.html

.. _dcs-ug-0312008:

Accessing a DCS Redis 4.0/5.0/6.0 Instance on the Console
=========================================================

Access a DCS Redis instance through Web CLI. This function is supported only by DCS Redis 4.0 and later instances, and not by DCS Redis 3.0 instances.

.. note::

   -  Do not enter sensitive information in Web CLI to avoid disclosure.
   -  Keys and values cannot contain spaces.
   -  If the value is empty, **nil** is returned after the **GET** command is executed.

Prerequisites
-------------

The instance is in the **Running** state.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. In the row containing the desired instance, choose **More** > **Connect to Redis** to go to the Web CLI login page.
#. Enter the password of the DCS instance. On Web CLI, select the current Redis database, enter a Redis command in the command box, and press **Enter**.

   .. note::

      If no operation is performed for more than 5 minutes, the connection times out. You must enter the access password to connect to the instance again.

.. |image1| image:: /_static/images/en-us_image_0000001194522775.png
