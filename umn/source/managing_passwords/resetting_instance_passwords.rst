:original_name: dcs-ug-0312041.html

.. _dcs-ug-0312041:

Resetting Instance Passwords
============================

On the DCS console, you can configure a new password if you forget your instance password.

.. note::

   -  For a DCS Redis instance, you can change it from password mode to password-free mode or from password-free mode to password mode by resetting its password. For details, see :ref:`Changing Password Settings for DCS Redis Instances <dcs-ug-0312042>`.
   -  The DCS instance for which you want to reset the password is in the **Running** state.
   -  The new password takes effect immediately on the server without requiring a restart. The client must reconnect to the server using the new password after a pconnect connection is closed. (The old password can still be used before disconnection.)

Prerequisites
-------------

At least one DCS instance has been created.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. Choose **More** > **Reset Password** in the row containing the chosen instance.
#. In the **Reset Password** dialog box, enter a new password and confirm the password.

   .. note::

      The password must meet the following requirements:

      -  Cannot be left blank.
      -  Can contain 8 to 32 characters.
      -  Contain at least three of the following character types:

         -  Lowercase letters
         -  Uppercase letters
         -  Digits
         -  Special characters (:literal:`\`~!@#$^&*()-_=+\\|{},<.>/?`)

#. Click **OK**.

   .. note::

      The system will display a success message only after the password is successfully reset on all nodes. If the reset fails, the instance will restart and the password of the cache instance will be restored.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
