:original_name: cache-instance-password.html

.. _cache-instance-password:

DCS Instance Passwords
======================

Passwords can be configured to control access to your DCS instances, ensuring the security of your data.

.. note::

   After 5 consecutive incorrect password attempts, the account for accessing the chosen DCS instance will be locked for 5 minutes. Passwords cannot be changed during the lockout period.

   The password must meet the following requirements:

   -  Cannot be left blank.
   -  Cannot be the same as the old password.
   -  Can contain 8 to 32 characters.
   -  Must contain at least three of the following character types:

      -  Lowercase letters
      -  Uppercase letters
      -  Digits
      -  Special characters (:literal:`\`~!@#$^&*()-_=+\\|{},<.>/?`)

Using Passwords Securely
------------------------

#. Hide the password when using redis-cli.

   If the **-a <password>** option is used in redis-cli in Linux, the password is prone to leakage because it is logged and kept in the history. You are advised not to use **-a <password>** when running commands in redis-cli. After connecting to Redis, run the **auth** command to complete authentication as shown in the following example:

   .. code-block::

      $ redis-cli -h 192.168.0.148 -p 6379
      redis 192.168.0.148:6379>auth {yourPassword}
      OK
      redis 192.168.0.148:6379>

#. Use interactive password authentication or switch between users with different permissions.

   If the script involves DCS instance access, use interactive password authentication. To enable automatic script execution, manage the script as another user and authorize execution using sudo.

#. Use an encryption module in your application to encrypt the password.
