:original_name: dcs-migration-0312017.html

.. _dcs-migration-0312017:

Can I Migrate Data from a Multi-DB Source Redis Instance to a Cluster DCS Redis Instance?
=========================================================================================

A total of 256 DBs (DB 0 to DB 255) can be configured for a single-node, read/write splitting, or master/standby DCS instance.

-  If the target is a cluster instance (a cluster instance has only one DB):

   Solutions:

   #. Combine different DBs in the source Redis instance into one DB.
   #. Apply for multiple DCS instances.

   After the migration, the instance connection address and DB IDs change. In this case, modify the configurations for your services.
