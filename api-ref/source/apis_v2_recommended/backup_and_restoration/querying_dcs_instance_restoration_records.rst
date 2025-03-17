:original_name: ListRestoreRecords.html

.. _ListRestoreRecords:

Querying DCS Instance Restoration Records
=========================================

Function
--------

This API is used to query the restoration records of a specific DCS instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/restores

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type    | Description                                                                                         |
   +============+===========+=========+=====================================================================================================+
   | begin_time | No        | String  | Start time of the period to be queried. Format: yyyyMMddHHmmss, for example, 20170718235959.        |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | end_time   | No        | String  | End time of the period to be queried. Format: yyyyMMddHHmmss, for example, 20170718235959.          |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | limit      | No        | Integer | Number of items displayed on each page.                                                             |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | offset     | No        | Integer | Offset, which is the position where the query starts. The value must be greater than or equal to 0. |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-------------------------+------------------------------------------------------------------------------------------------+-----------------------------------+
   | Parameter               | Type                                                                                           | Description                       |
   +=========================+================================================================================================+===================================+
   | restore_record_response | Array of :ref:`InstanceRestoreInfo <listrestorerecords__response_instancerestoreinfo>` objects | Array of the restoration records. |
   +-------------------------+------------------------------------------------------------------------------------------------+-----------------------------------+
   | total_num               | Integer                                                                                        | Total number.                     |
   +-------------------------+------------------------------------------------------------------------------------------------+-----------------------------------+

.. _listrestorerecords__response_instancerestoreinfo:

.. table:: **Table 4** InstanceRestoreInfo

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                         |
   +=======================+=======================+=====================================================================================================+
   | backup_id             | String                | Backup ID.                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | restore_id            | String                | ID of the restoration record.                                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | backup_name           | String                | Backup record name.                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Time when the restoration completed.                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | restore_remark        | String                | Description of the restoration.                                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | created_at            | String                | Time when the restoration task was created.                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | progress              | String                | Restoration progress.                                                                               |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code displayed for a restoration failure.                                                     |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0001** - Failed to start the backup and restoration tool.                               |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0002** - Execution timed out.                                                           |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0003** - Failed to delete the bucket.                                                   |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0004** - Failed to obtain the AK/SK.                                                    |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0005** - Failed to create a bucket.                                                     |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0006** - Failed to query the backup data size.                                          |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0007** - Failed to synchronize data during restoration.                                 |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **dcs.08.0008** - The scheduled backup task is not running. The instance is running other tasks. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | restore_name          | String                | Name of a restoration record.                                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | backup_remark         | String                | Description of the backup.                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+
   | status                | String                | Restoration status.                                                                                 |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **waiting**: The task is waiting to begin.                                                       |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **restoring**: The restoration is in progress.                                                   |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **succeed**: The restoration is successful.                                                      |
   |                       |                       |                                                                                                     |
   |                       |                       | -  **failed**: The restoration failed.                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------+

**Status code: 400**

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

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/restores?offset={offset}&limit={limit}&begin_Time={begin_Time}&end_Time={end_Time}

Example Responses
-----------------

**Status code: 200**

DCS instance restoration records queried successfully.

.. code-block::

   {
     "restore_record_response" : [ {
       "backup_id" : "f4823e9e-fe9b-4ffd-be79-4e5d6de272bb",
       "restore_id" : "a6155972-800c-4170-a479-3231e907d2f6",
       "backup_name" : "backup_20170718000002",
       "updated_at" : "2017-07-18T21:41:35.182Z",
       "restore_remark" : "doctest",
       "created_at" : "2017-07-18T21:41:20.721Z",
       "progress" : "100.00",
       "error_code" : { },
       "restore_name" : "restore_20170718214120",
       "backup_remark" : { },
       "status" : "succeed"
     } ],
     "total_num" : 1
   }

Status Codes
------------

=========== ======================================================
Status Code Description
=========== ======================================================
200         DCS instance restoration records queried successfully.
204         No instance restoration record found.
400         Invalid request.
=========== ======================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
