:original_name: ShowHotkeyTaskDetails.html

.. _ShowHotkeyTaskDetails:

Querying Hot Key Analysis Details
=================================

Function
--------

This API is used to query the hot key analysis details.

URI
---

GET /v2/{project_id}/instances/{instance_id}/hotkey-task/{hotkey_id}

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | hotkey_id   | Yes       | String | ID of the hot key analysis task.                                              |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                              | Description                                                                                                                                                          |
   +=======================+===================================================================================+======================================================================================================================================================================+
   | id                    | String                                                                            | Hot key analysis record ID.                                                                                                                                          |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instance_id           | String                                                                            | Instance ID.                                                                                                                                                         |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                                                                            | Analysis task status. Value range:                                                                                                                                   |
   |                       |                                                                                   |                                                                                                                                                                      |
   |                       |                                                                                   | -  **waiting**                                                                                                                                                       |
   |                       |                                                                                   | -  **running**                                                                                                                                                       |
   |                       |                                                                                   | -  **success**                                                                                                                                                       |
   |                       |                                                                                   | -  **failed**                                                                                                                                                        |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scan_type             | String                                                                            | Analysis method. Value range:                                                                                                                                        |
   |                       |                                                                                   |                                                                                                                                                                      |
   |                       |                                                                                   | -  **manual**                                                                                                                                                        |
   |                       |                                                                                   | -  **auto**                                                                                                                                                          |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | created_at            | String                                                                            | Time when an analysis task is created. The format is **2020-06-15T02:21:18.669Z**.                                                                                   |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | started_at            | String                                                                            | Time when an analysis task started. The format is **2020-06-15T02:21:18.669Z**. (The value is **null** and is not returned when the analysis task is being created.) |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | finished_at           | String                                                                            | Time when an analysis task ended. The format is **2020-06-15T02:21:18.669Z**. (The value is **null** and is not returned when the analysis task is being created.)   |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | num                   | Integer                                                                           | Number of hot keys.                                                                                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | keys                  | Array of :ref:`HotkeysBody <showhotkeytaskdetails__response_hotkeysbody>` objects | Hot key record. (The value is **null** and is not returned when the analysis task is being created.)                                                                 |
   +-----------------------+-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _showhotkeytaskdetails__response_hotkeysbody:

.. table:: **Table 3** HotkeysBody

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                                                  |
   +=======================+=======================+==============================================================================================================================================================================================================================================================================================================================================+
   | name                  | String                | Key name.                                                                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type                  | String                | Key type. Value range:                                                                                                                                                                                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                              |
   |                       |                       | -  **string**                                                                                                                                                                                                                                                                                                                                |
   |                       |                       | -  **list**                                                                                                                                                                                                                                                                                                                                  |
   |                       |                       | -  **set**                                                                                                                                                                                                                                                                                                                                   |
   |                       |                       | -  **zset**                                                                                                                                                                                                                                                                                                                                  |
   |                       |                       | -  **hash**                                                                                                                                                                                                                                                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard                 | String                | Shard where the hot key is located. This parameter is supported only when the instance type is cluster. The format is **ip:port**.                                                                                                                                                                                                           |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db                    | Integer               | Database where a hot key is located.                                                                                                                                                                                                                                                                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | size                  | Long                  | Size of the key value.                                                                                                                                                                                                                                                                                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | unit                  | String                | Key unit. **count**: number of keys; **byte**: key size.                                                                                                                                                                                                                                                                                     |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | freq                  | Integer               | Reflects the access frequency of a key within a specific period of time.                                                                                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                              |
   |                       |                       | The value is the logarithmic access frequency counter. The maximum value is **255**, which indicates 1 million access requests. After the frequency reaches **255**, the value will no longer increase even if access requests continue to increase. The value will decrease by **1** for every minute during which the key is not accessed. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

**Status code: 401**

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

**Status code: 403**

.. table:: **Table 6** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 404**

.. table:: **Table 7** Response body parameters

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

.. table:: **Table 8** Response body parameters

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

   GET https://{dcs_endpoint}/v2/a4d31cb6-3d72-4fdc-8ec9-6e3a41e47f71/instances/5560df16-cebf-4473-95c4-d1b573c16e79/hotkey-task/0ccb25d5-27cf-4188-b5ea-987730a85371

Example Responses
-----------------

**Status code: 200**

Hot key analysis details queried successfully.

.. code-block::

   {
     "id" : "858ee14c-2271-4489-8b82-7bda7459ae3e",
     "instance_id" : "5f9057b5-c330-4ee2-8138-7e69896eeec3",
     "status" : "success",
     "scan_type" : "manual",
     "created_at" : "2020-06-15T02:21:18.669Z",
     "started_at" : "2020-06-15T02:21:23.534Z",
     "finished_at" : "2020-06-15T02:21:25.588Z",
     "keys" : [ {
       "name" : "dcs-hotkey-test",
       "type" : "string",
       "shard" : "192.168.1.134:6379",
       "db" : 0,
       "size" : 3000,
       "unit" : "byte",
       "freq" : 4
     } ]
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "DCS.4922",
     "error_msg" : "Does not support hotkey analyze."
   }

Status Codes
------------

=========== ==============================================
Status Code Description
=========== ==============================================
200         Hot key analysis details queried successfully.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ==============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
