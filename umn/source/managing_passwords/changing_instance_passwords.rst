:original_name: dcs-ug-0312040.html

.. _dcs-ug-0312040:

Changing Instance Passwords
===========================

On the DCS console, you can change the password required for accessing your DCS instance.

.. note::

   -  You cannot change the password of a DCS instance in password-free mode.
   -  The DCS instance for which you want to change the password is in the **Running** state.
   -  The new password takes effect immediately on the server without requiring a restart. The client must reconnect to the server using the new password after a pconnect connection is closed. (The old password can still be used before disconnection.)

Prerequisites
-------------

At least one DCS instance has been created.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. Choose **More** > **Change Password** in the same row as the chosen instance.
#. In the displayed dialog box, set **Old Password**, **New Password**, and **Confirm Password**.

   .. note::

      After 5 consecutive incorrect password attempts, the account for accessing the chosen DCS instance will be locked for 5 minutes. Passwords cannot be changed during the lockout period.

      The password must meet the following requirements:

      -  Cannot be left blank.
      -  The new password cannot be the same as the old password.
      -  Can contain 8 to 32 characters.
      -  Must contain at least three of the following character types:

         -  Lowercase letters
         -  Uppercase letters
         -  Digits
         -  Special characters (:literal:`\`~!@#$^&*()-_=+\\|{},<.>/?`)

#. In the **Change Password** dialog box, click **OK** to confirm the password change.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
