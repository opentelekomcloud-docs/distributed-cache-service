:original_name: UpdateBigkeyAutoscanConfig.html

.. _UpdateBigkeyAutoscanConfig:

Configuring Automatic Big Key Analysis
======================================

Function
--------

This API is used to configure automatic big key analysis.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/bigkey/autoscan

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +------------------+-----------------+------------------+-------------------------------------------------------------------------------+
   | Parameter        | Mandatory       | Type             | Description                                                                   |
   +==================+=================+==================+===============================================================================+
   | enable_auto_scan | Yes             | Boolean          | Whether to enable scheduled cache analysis.                                   |
   |                  |                 |                  |                                                                               |
   |                  |                 |                  | -  **true**                                                                   |
   |                  |                 |                  | -  **false**                                                                  |
   +------------------+-----------------+------------------+-------------------------------------------------------------------------------+
   | schedule_at      | Yes             | Array of strings | UTC time of the day that cache analysis is scheduled for. Example: **21:00**. |
   +------------------+-----------------+------------------+-------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +------------------+------------------+------------------------------------------------------------------------------------------+
   | Parameter        | Type             | Description                                                                              |
   +==================+==================+==========================================================================================+
   | instance_id      | String           | Instance ID.                                                                             |
   +------------------+------------------+------------------------------------------------------------------------------------------+
   | enable_auto_scan | Boolean          | Whether to enable scheduled cache analysis.                                              |
   +------------------+------------------+------------------------------------------------------------------------------------------+
   | schedule_at      | Array of strings | UTC time of the day that analysis is scheduled for. Example: **21:00**.                  |
   +------------------+------------------+------------------------------------------------------------------------------------------+
   | updated_at       | String           | Time when the configuration is updated. The time format is **2020-06-15T02:21:18.669Z**. |
   +------------------+------------------+------------------------------------------------------------------------------------------+

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

Scheduling big key analysis tasks to start at 21:00 every day

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/a4d31cb6-3d72-4fdc-8ec9-6e3a41e47f71/instances/5560df16-cebf-4473-95c4-d1b573c16e79/bigkey/autoscan

   {
     "enable_auto_scan" : true,
     "schedule_at" : [ "21:00" ]
   }

Example Responses
-----------------

**Status code: 200**

Big key analysis task configured successfully.

.. code-block::

   {
     "instance_id" : "5f9057b5-c330-4ee2-8138-7e69896eeec3",
     "enable_auto_scan" : true,
     "schedule_at" : [ "21:00" ],
     "updated_at" : "2020-06-17T02:42:40.793Z"
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "DCS.4919",
     "error_msg" : "Does not support bigkey analyze."
   }

Status Codes
------------

=========== ==============================================
Status Code Description
=========== ==============================================
200         Big key analysis task configured successfully.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ==============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
