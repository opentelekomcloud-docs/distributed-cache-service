:original_name: dcs-faq-11185.html

.. _dcs-faq-11185:

Will the Same Keys Be Overwritten During Data Migration or Backup Import?
=========================================================================

If the data exists on both the source and target instances, the target data is overwritten by the source data. If the data exists only on the target instance, the data will be retained.

Inconsistency between source and target data after the migration may be due to the target data that existed and was retained before migration.
