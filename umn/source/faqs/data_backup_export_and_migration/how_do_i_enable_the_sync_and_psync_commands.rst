:original_name: dcs-faq-210721001.html

.. _dcs-faq-210721001:

How Do I Enable the SYNC and PSYNC Commands?
============================================

-  Migration within DCS:

   -  By default, the **SYNC** and **PSYNC** commands can be used when self-hosted Redis is migrated to DCS.
   -  During online migration between DCS Redis instances in the same region under the same account, the **SYNC** and **PSYNC** commands are automatically enabled.
   -  During online migration between DCS Redis instances in different regions or under different accounts within a region, the **SYNC** and **PSYNC** commands are not automatically enabled, and online migration cannot be used. You can migrate data using backup files.

-  Migration from other cloud vendors to DCS:

   -  Generally, cloud vendors disable the **SYNC** and **PSYNC** commands. If you want to use the online migration function on the DCS console, contact the O&M personnel of the source cloud vendor to enable the commands. For offline migration, you can import backup files.
   -  If incremental migration is not required, you can perform full migration by referring to :ref:`Online Full Migration of Redis from Another Cloud with redis-shake <dcs-migrate-0220411>`. This method does not depend on **SYNC** and **PSYNC**.
