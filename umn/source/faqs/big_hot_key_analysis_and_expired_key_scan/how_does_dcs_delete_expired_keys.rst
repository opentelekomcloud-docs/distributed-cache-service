:original_name: dcs-faq-210531002.html

.. _dcs-faq-210531002:

How Does DCS Delete Expired Keys?
=================================

Question
--------

What are the rules for scheduled deletion of expired keys on a daily basis? Can I customize the rules?

Mechanisms for Deleting Expired Keys
------------------------------------

-  Lazy free deletion: The deletion strategy is controlled in the main I/O event loop. Before a read/write command is executed, a function is called to check whether the key to be accessed has expired. If it has expired, it will be deleted and a response will be returned indicating that the key does not exist. If the key has not expired, the command execution resumes.
-  Scheduled deletion: A time event function is executed at certain intervals. Each time the function is executed, a random collection of keys are checked, and expired keys are deleted.

   .. note::

      To avoid prolonged blocks on the Redis main thread, not all keys are checked in each time event. Instead, a random collection of keys are checked each time. As a result, the memory used by expired keys cannot be released quickly.

Solutions
---------

-  Configure scheduled hot key analysis tasks by referring to :ref:`Hot Key Analysis <dcs-ug-190808001__section47852016145218>`, or use the **SCAN** command to traverse all keys on a scheduled basis and remove expired keys from the memory.
-  Configure a scheduled task to scan all master nodes of the instance. All keys will be scanned, and Redis will determine whether the keys have expired. Expired keys will be released. For details, see :ref:`Scanning Expired Keys <dcs-ug-210330002>`.
