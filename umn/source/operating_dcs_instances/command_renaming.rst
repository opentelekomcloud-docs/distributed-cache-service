:original_name: dcs-ug-1009002.html

.. _dcs-ug-1009002:

Command Renaming
================

After creating a DCS Redis 4.0 or later instance, you can rename the following critical commands: Currently, you can only rename the **COMMAND**, **KEYS**, **FLUSHDB**, **FLUSHALL**, **HGETALL**, **SCAN**, **HSCAN**, **SSCAN**, and **ZSCAN** commands.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. In the **Operation** column of an instance, choose **More** > **Command Renaming**.

#. Select a command, enter a new name, and click **OK**.

   In the **Command Renaming** dialog box, click **Add Command** to rename multiple commands at the same time.

   .. note::

      -  Remember the new command names because they will not be displayed on the console for security purposes.
      -  The system will restart the instance after you rename commands. The new commands take effect after the restart.
      -  To use the original name of a command, rename the command again.
      -  The new name can contain 4 to 64 characters including letters, digits, underscores (_), and hyphens (-), and must start with a letter.

.. |image1| image:: /_static/images/en-us_image_0000001148603248.png
