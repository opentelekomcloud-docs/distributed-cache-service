:original_name: dcs-faq-0730034.html

.. _dcs-faq-0730034:

Can I Recover Data from Deleted DCS Instances?
==============================================

If a DCS instance is automatically deleted or manually deleted through the Redis client, its data cannot be retrieved. If you have backed up the instance, you can restore its data from the backup. However, the restoration will overwrite the data written in during the period from the backup and the restoration.

You can restore backup data to an instance other than a single-node one through **Backups & Restorations** on the DCS console. For details, see :ref:`Restoring a DCS Instance <dcs-ug-0312033>`.

If a DCS instance is deleted, the instance data and its backup will also be deleted. Before deleting an instance, you can download the backup files of the instance for permanent local storage and can also migrate them to a new instance if you need to restore the data. For details about how to download the backup data, see :ref:`Downloading a Backup File <dcs-ug-0312034>`
