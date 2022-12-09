:original_name: dcs-api-0312020.html

.. _dcs-api-0312020:

Backing Up a DCS Instance
=========================

Function
--------

This API is used to back up a specified DCS instance.

.. note::

   Only master/standby and cluster DCS instances can be backed up and restored, while single-node instances cannot.

URI
---

POST /v1.0/{project_id}/instances/{instance_id}/backups

:ref:`Table 1 <dcs-api-0312020__table1899262913382>` describes the parameters.

.. _dcs-api-0312020__table1899262913382:

.. table:: **Table 1** Parameter description

   =========== ====== ========= ================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ================
   project_id  String Yes       Project ID.
   instance_id String Yes       DCS instance ID.
   =========== ====== ========= ================

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312020__table153111335113816>` describes the request parameters.

.. _dcs-api-0312020__table153111335113816:

.. table:: **Table 2** Parameter description

   ========= ====== ========= ===================================
   Parameter Type   Mandatory Description
   ========= ====== ========= ===================================
   remark    String No        Description of DCS instance backup.
   ========= ====== ========= ===================================

**Example request**

-  Request URL:

   .. code-block:: text

      POST https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/backups

-  Example:

   .. code-block::

      {
          "remark": "Backup instances"
      }

Response
--------

**Response parameters**

:ref:`Table 3 <dcs-api-0312020__table1861319576383>` describes the response parameter.

.. _dcs-api-0312020__table1861319576383:

.. table:: **Table 3** Parameter description

   ========= ====== =======================
   Parameter Type   Description
   ========= ====== =======================
   backup_id String ID of the backup record
   ========= ====== =======================

**Example response**

.. code-block::

   {
       "backup_id": "548ceeff-2cbb-47ab-9a1c-7b085a8c08d7"
   }

Status Code
-----------

:ref:`Table 4 <dcs-api-0312020__table486141410130>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312020__table486141410130:

.. table:: **Table 4** Status code

   =========== =================================
   Status Code Description
   =========== =================================
   200         Backup task created successfully.
   =========== =================================
