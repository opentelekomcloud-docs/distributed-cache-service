:original_name: dcs-api-0312021.html

.. _dcs-api-0312021:

Restoring a DCS Instance
========================

Function
--------

This API is used to restore a specified DCS instance.

.. note::

   Only master/standby and cluster DCS instances can be backed up and restored, while single-node instances cannot.

URI
---

POST /v1.0/{project_id}/instances/{instance_id}/restores

:ref:`Table 1 <dcs-api-0312021__table1899262913382>` describes the parameters.

.. _dcs-api-0312021__table1899262913382:

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

:ref:`Table 2 <dcs-api-0312021__table153111335113816>` describes the request parameters.

.. _dcs-api-0312021__table153111335113816:

.. table:: **Table 2** Parameter description

   ========= ====== ========= =======================================
   Parameter Type   Mandatory Description
   ========= ====== ========= =======================================
   remark    String No        Description of DCS instance restoration
   backup_id String Yes       ID of the backup record
   ========= ====== ========= =======================================

**Example request**

.. code-block:: text

   POST https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/restores

.. code-block::

   {
       "remark":"restore instance",
       "backup_id":"8ba256cb-e5ac-44f6-a3da-c03d8f0e5029"
   }

Response
--------

**Response parameters**

:ref:`Table 3 <dcs-api-0312021__table1861319576383>` describes the response parameter.

.. _dcs-api-0312021__table1861319576383:

.. table:: **Table 3** Parameter description

   ========== ====== ============================
   Parameter  Type   Description
   ========== ====== ============================
   restore_id String ID of the restoration record
   ========== ====== ============================

**Example response**

.. code-block::

   {
       "restore_id": "a6155972-800c-4170-a479-3231e907d2f6"
   }

Status Code
-----------

:ref:`Table 4 <dcs-api-0312021__table486141410130>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312021__table486141410130:

.. table:: **Table 4** Status code

   =========== ======================================
   Status Code Description
   =========== ======================================
   200         Restoration task created successfully.
   =========== ======================================
