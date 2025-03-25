:original_name: dcs-faq-210721001.html

.. _dcs-faq-210721001:

How Do I Enable the SYNC and PSYNC Commands?
============================================

-  Migration within DCS:

   -  If the online migration task uses the same account and region as the source instance, select a DCS instance (cloud Redis) as the source. The **SYNC** and **PSYNC** commands will be automatically allowed on the source instance.
   -  If the online migration task uses a different account or in a different region from the source instance, the source instance cannot be a DCS instance (cloud Redis) and the **SYNC** and **PSYNC** commands are disabled on the source instance. In this case, online migration on the console is unavailable. You can migrate data using backup import.
   -  By default, the **SYNC** and **PSYNC** commands can be used when self-hosted Redis is migrated to DCS.

-  Migration from other cloud vendors to DCS:

   -  Generally, cloud vendors disable the **SYNC** and **PSYNC** commands. If you want to use the online migration function on the DCS console, contact the O&M personnel of the source cloud vendor to enable the commands. For offline migration, you can import backup files.
   -  If incremental migration is not required, you can perform full migration by referring to :ref:`Online Full Migration of Redis from Another Cloud with redis-shake <dcs-migrate-0220411>`. This method does not depend on **SYNC** and **PSYNC**.
