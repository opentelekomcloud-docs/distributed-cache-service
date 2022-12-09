:original_name: dcs-ug-1009002.html

.. _dcs-ug-1009002:

Command Renaming
================

After creating a DCS Redis 4.0 or 5.0 instance, you can rename the following critical commands: **COMMAND**, **KEYS**, **FLUSHDB**, **FLUSHALL**, and **HGETALL**.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. In the **Operation** column of an instance, choose **More** > **Command Renaming**.
#. Select a command, enter a new name, and click **OK**.

   .. note::

      -  You can rename multiple commands at a time.
      -  The new command names will take effect only after you restart the instance. Remember the new command names because they will not be displayed on the console for security purposes.
      -  To use the original name of a command, rename the command again.
      -  The new name must contain at least four characters.

.. |image1| image:: /_static/images/en-us_image_0000001148603248.png
