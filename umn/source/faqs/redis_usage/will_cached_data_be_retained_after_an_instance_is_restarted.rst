:original_name: dcs-faq-0220330.html

.. _dcs-faq-0220330:

Will Cached Data Be Retained After an Instance Is Restarted?
============================================================

After a single-node DCS instance is restarted, data in the instance is deleted.

Master/standby and cluster instances (except single-replica clusters) support AOF persistence by default. Data is retained after these instances are restarted.

If AOF persistence is disabled (**appendonly** is set to **no**), data is deleted after the instances are restarted.
