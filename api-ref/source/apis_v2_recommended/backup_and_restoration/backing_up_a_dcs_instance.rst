:original_name: CopyInstance.html

.. _CopyInstance:

Backing Up a DCS Instance
=========================

Function
--------

This API is used to back up a specific DCS instance.

.. note::

   Only master/standby and cluster DCS instances can be backed up and restored, while single-node instances cannot.

URI
---

POST /v2/{project_id}/instances/{instance_id}/backups

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

   +-----------------+-----------------+-----------------+-------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                         |
   +=================+=================+=================+=====================================+
   | remark          | No              | String          | Description of DCS instance backup. |
   +-----------------+-----------------+-----------------+-------------------------------------+
   | backup_format   | No              | String          | Format of the DCS instance backup.  |
   |                 |                 |                 |                                     |
   |                 |                 |                 | Enumeration values:                 |
   |                 |                 |                 |                                     |
   |                 |                 |                 | -  **aof**                          |
   |                 |                 |                 |                                     |
   |                 |                 |                 | -  **rdb**                          |
   +-----------------+-----------------+-----------------+-------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   backup_id String Backup ID.
   ========= ====== ===========

**Status code: 400**

.. table:: **Table 4** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | error_msg             | String                | Error message.                                                                           |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code.                                                                              |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **9**                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_ext_msg         | String                | Extended error information. This parameter is not used currently and is set to **null**. |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 5** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | error_msg             | String                | Error message.                                                                           |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code.                                                                              |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **9**                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_ext_msg         | String                | Extended error information. This parameter is not used currently and is set to **null**. |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

Example Requests
----------------

Backing up a specified DCS instance to an AOF file

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/backups

   {
     "remark" : "Backup instances",
     "backup_format" : "aof"
   }

Example Responses
-----------------

**Status code: 200**

The specified DCS instance is backed up successfully.

.. code-block::

   {
     "backup_id" : "548ceeff-2cbb-47ab-9a1c-7b085a8c08d7"
   }

Status Codes
------------

=========== =====================================================
Status Code Description
=========== =====================================================
200         The specified DCS instance is backed up successfully.
400         Invalid request.
500         Internal service error.
=========== =====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
