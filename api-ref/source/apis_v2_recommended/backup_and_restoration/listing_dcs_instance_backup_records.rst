:original_name: ListBackupRecords.html

.. _ListBackupRecords:

Listing DCS Instance Backup Records
===================================

Function
--------

This API is used to query the backup records of a specific DCS instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/backups

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
   | begin_time | No        | String  | Query start time (UTC). Format: yyyyMMddHHmmss, for example, 20170718235959.                        |
   +------------+-----------+---------+-----------------------------------------------------------------------------------------------------+
   | end_time   | No        | String  | Query end time (UTC). Format: yyyyMMddHHmmss, for example, 20170718235959.                          |
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

   +------------------------+-------------------------------------------------------------------------------------------------+------------------------------+
   | Parameter              | Type                                                                                            | Description                  |
   +========================+=================================================================================================+==============================+
   | total_num              | Integer                                                                                         | Number of returned records.  |
   +------------------------+-------------------------------------------------------------------------------------------------+------------------------------+
   | backup_record_response | Array of :ref:`BackupRecordResponse <listbackuprecords__response_backuprecordresponse>` objects | Array of the backup details. |
   +------------------------+-------------------------------------------------------------------------------------------------+------------------------------+

.. _listbackuprecords__response_backuprecordresponse:

.. table:: **Table 4** BackupRecordResponse

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | backup_id             | String                | Backup ID.                                                                                        |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | period                | String                | Backup execution time.                                                                            |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | backup_name           | String                | Backup record name.                                                                               |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | instance_id           | String                | Instance ID.                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | size                  | Long                  | Size of the backup file (byte).                                                                   |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | backup_type           | String                | Backup type.                                                                                      |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **manual**: manual backup                                                                      |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **auto**: automatic backup                                                                     |
   |                       |                       |                                                                                                   |
   |                       |                       | Enumeration values:                                                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **manual**                                                                                     |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **auto**                                                                                       |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | created_at            | String                | Time when the backup task is created.                                                             |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Time at which DCS instance backup is completed.                                                   |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | progress              | String                | Backup progress.                                                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code displayed for a backup failure.                                                        |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0001* - Failed to start the backup and restoration tool.                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0002* - Execution timed out.                                                           |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0003* - Failed to delete the bucket.                                                   |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0004* - Failed to obtain the AK/SK.                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0005* - Failed to create the bucket.                                                   |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0006* - Failed to query the backup data size.                                          |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0007* - Failed to synchronize data during restoration.                                 |
   |                       |                       |                                                                                                   |
   |                       |                       | -  *dcs.08.0008* - The scheduled backup task is not running. The instance is running other tasks. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | remark                | String                | Description of DCS instance backup.                                                               |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Backup status. The options are as follows:                                                        |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **waiting**: The task is waiting to begin.                                                     |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **backuping**: DCS instance backup is in progress.                                             |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **succeed**: DCS instance backup succeeded.                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **failed**: DCS instance backup failed.                                                        |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **expired**: The backup file has expired.                                                      |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **deleted**: The backup file has been deleted manually.                                        |
   |                       |                       |                                                                                                   |
   |                       |                       | Enumeration values:                                                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **waiting**                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **backuping**                                                                                  |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **succeed**                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **failed**                                                                                     |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **expired**                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **deleted**                                                                                    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | is_support_restore    | String                | Whether restoration is supported. Options: **TRUE** and **FALSE**.                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | execution_at          | String                | Execution time.                                                                                   |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | backup_format         | String                | Backup format.                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | Enumeration values:                                                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **aof**                                                                                        |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **rdb**                                                                                        |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

**Status code: 400**

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

**Status code: 500**

.. table:: **Table 6** Response body parameters

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

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/backups?offset={offset}&limit={limit}&beginTime={begin_Time}&end_time={end_Time}

Example Responses
-----------------

**Status code: 200**

DCS instance backup records queried successfully.

.. code-block::

   {
     "total_num" : 1,
     "backup_record_response" : [ {
       "period" : { },
       "backup_type" : "manual",
       "created_at" : "2019-05-10T08:31:16.166Z",
       "remark" : "001",
       "is_support_restore" : "TRUE",
       "backup_id" : "4631832a-14c6-45b0-a0b3-3abd8f591ad1",
       "backup_name" : "backup_20190510163116",
       "instance_id" : "5560df16-cebf-4473-95c4-d1b573c16e79",
       "size" : 880232,
       "updated_at" : "2019-05-10T08:32:30.546Z",
       "progress" : "100.00",
       "error_code" : { },
       "status" : "succeed",
       "execution_at" : "2019-05-11T08:31:16.166Z",
       "backup_format" : "aof"
     } ]
   }

Status Codes
------------

=========== =================================================
Status Code Description
=========== =================================================
200         DCS instance backup records queried successfully.
204         No DCS instance backup record is found.
400         Invalid request.
500         Internal service error.
=========== =================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
