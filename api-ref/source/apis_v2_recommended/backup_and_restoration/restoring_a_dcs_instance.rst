:original_name: RestoreInstance.html

.. _RestoreInstance:

Restoring a DCS Instance
========================

Function
--------

This API is used to restore the backup data to a specific DCS instance.

.. note::

   Only master/standby and cluster DCS instances can be backed up and restored, while single-node instances cannot.

URI
---

POST /v2/{project_id}/instances/{instance_id}/restores

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   ========= ========= ====== ========================================
   Parameter Mandatory Type   Description
   ========= ========= ====== ========================================
   backup_id Yes       String Backup ID.
   remark    No        String Description of DCS instance restoration.
   ========= ========= ====== ========================================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========== ====== =============================
   Parameter  Type   Description
   ========== ====== =============================
   restore_id String ID of the restoration record.
   ========== ====== =============================

**Status code: 400**

.. table:: **Table 4** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 5** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

Example Requests
----------------

Restoring the backup files of the DCS instance

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/restores

   {
     "backup_id" : "8ba256cb-e5ac-44f6-a3da-c03d8f0e5029",
     "remark" : "restore instance"
   }

Example Responses
-----------------

**Status code: 200**

Instance restored successfully.

.. code-block::

   {
     "restore_id" : "a6155972-800c-4170-a479-3231e907d2f6"
   }

Status Codes
------------

=========== ===============================
Status Code Description
=========== ===============================
200         Instance restored successfully.
400         Invalid request.
500         Internal service error.
=========== ===============================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
