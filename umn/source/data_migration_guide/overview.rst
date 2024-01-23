:original_name: dcs-migration-0713001.html

.. _dcs-migration-0713001:

Overview
========

Due to variations of Redis application environments and scenarios, migration solutions must be detailed to address actual requirements. The time required for data migration is related to the data volume, the location of source Redis data, and the network bandwidth. Record and evaluate the duration during the rehearsal phase.

When migrating data, analyze the cache commands (reference: :ref:`Command Compatibility <dcs-pd-200312003>`) used by your service systems and verify the commands one by one during the rehearsal phase. If necessary, contact technical support.

.. important::

   -  Data migration is an important and stringent task requiring high accuracy and timeliness. It varies depending on specific services and operation environments.
   -  Cases provided in this document are for reference only. Consider your service scenarios and requirements during actual migration.
   -  Some commands in this document contain instance passwords, which will be recorded in the operating system (OS). Ensure that the passwords are not disclosed and clear operation records in a timely manner.
