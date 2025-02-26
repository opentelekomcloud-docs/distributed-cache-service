:original_name: dcs-ug-0312042.html

.. _dcs-ug-0312042:

Changing Password Settings for DCS Redis Instances
==================================================

Scenario
--------

DCS Redis instances can be accessed with or without passwords. After an instance is created, you can change its password setting in the following scenarios:

-  To access a DCS Redis instance in password-free mode, you can enable password-free access to clear the existing password of the instance.

.. note::

   -  To change the password setting, the DCS Redis instance must be in the **Running** state.
   -  Password-free access may compromise security. You can set a password by using the password reset function.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. To change the password setting for a DCS Redis instance, choose **Operation** > **More** > **Reset Password** in the same row as the chosen instance.
#. In the **Reset Password** dialogue box, perform either of the following operations as required:

   -  From password-protected to password-free:

      Switch the toggle for **Password-Free Access** and click **OK**.

   -  From password-free to password-protected:

      Enter a password, confirm the password, and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
