:original_name: dcs-migration-0312020.html

.. _dcs-migration-0312020:

What Should I Consider for Online Migration?
============================================

-  Network

   Before online migration, ensure that the network configured for the migration task is connected to source and target Redis instances.

-  Tool

   Use the online migration function provided on the DCS console.

-  Data integrity

   If you suspend your services for data migration, check the data volume and main keys after the migration.

   If you do not suspend your services, migrate data incrementally.

-  Impact of capacity expansion of the source instance

   During online migration, expanding the source instance's capacity may affect the migration or customer data. If the memory of the source instance becomes insufficient during the migration, stop the migration task and then expand the capacity.

-  Timing

   Migration should take place during off-peak hours.

-  Version restrictions

   You can migrate data from an earlier version to a later version, and vice versa, but you need to check whether the target instance supports the commands used in your service systems.
