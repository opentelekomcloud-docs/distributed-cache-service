:original_name: dcs-api-0312024.html

.. _dcs-api-0312024:

Deleting Backup Files
=====================

Function
--------

This API is used to delete the files backed up by a DCS instance.

URI
---

DELETE /v1.0/{project_id}/instances/{instance_id}/backups/{backup_id}

:ref:`Table 1 <dcs-api-0312024__table4154121820350>` describes the parameters.

.. _dcs-api-0312024__table4154121820350:

.. table:: **Table 1** Parameter description

   =========== ====== ========= =======================
   Parameter   Type   Mandatory Description
   =========== ====== ========= =======================
   project_id  String Yes       Project ID.
   instance_id String Yes       DCS instance ID
   backup_id   String Yes       ID of the backup record
   =========== ====== ========= =======================

Request
-------

**Request parameters**

None

**Example request**

.. code-block:: text

   DELETE https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/backups/{backup_id}

Response
--------

**Response parameters**

:ref:`Table 2 <dcs-api-0312024__table5929344419>` describes the response parameters.

.. _dcs-api-0312024__table5929344419:

.. table:: **Table 2** Parameter description

   ========= ====== ==================================
   Parameter Type   Description
   ========= ====== ==================================
   message   String Result of deleting the backup file
   ========= ====== ==================================

**Example response**

.. code-block::

   {
       "message": ""
   }

Status Code
-----------

:ref:`Table 3 <dcs-api-0312024__table8301101911215>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312024__table8301101911215:

.. table:: **Table 3** Status code

   =========== =================================
   Status Code Description
   =========== =================================
   200         Backup file deleted successfully.
   =========== =================================
