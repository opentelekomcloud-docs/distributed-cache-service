:original_name: dcs-faq-210812001.html

.. _dcs-faq-210812001:

How Long Are Keys Stored? How Do I Set Key Expiration?
======================================================

-  Key storage duration

   -  Keys that do not have an expiration are stored permanently.
   -  Keys that have an expiration are deleted after they expire. For details, see :ref:`Scanning Expired Keys <dcs-ug-210330002>`.
   -  To remove the expiration set for a key, run the **PERSIST** command.

-  Setting key expiration

   You can run the **EXPIRE** or **PEXPIRE** command to set the key expiration time. For example, if you run **expire key1 100**, key1 will expire in 100 seconds. If you run **pexpire key2 1800**, key2 will expire in 1800 milliseconds.

   **EXPIRE** sets key expiration in seconds, and **PEXPIRE** sets key expiration in milliseconds.
