:original_name: dcs-faq-210409001.html

.. _dcs-faq-210409001:

Why Does a Key Disappear in Redis?
==================================

Normally, Redis keys do not disappear. If a key is missing, it may have expired, been evicted, or been deleted.

Perform the following checks one by one:

#. Check whether the key has expired.
#. View the monitoring information and check whether eviction was triggered.
#. Run the **INFO** command on the server side to check whether the key has been deleted.
