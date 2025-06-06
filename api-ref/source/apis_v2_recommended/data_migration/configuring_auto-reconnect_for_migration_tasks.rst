:original_name: UpdateMigrationTask.html

.. _UpdateMigrationTask:

Configuring Auto-Reconnect for Migration Tasks
==============================================

Function
--------

This API is used to configure auto-reconnect for migration tasks.

URI
---

PUT /v2/{project_id}/migration-task/{task_id}

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | task_id    | Yes       | String | ID of the data migration task.                                                |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================================================================================================================================================================================================+
   | resume_mode     | No              | String          | Reconnection mode of the migration tasks.                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  **auto**: automatically reconnect. In automatic reconnection mode, if the source and target instances are disconnected due to network exceptions, automatic reconnections will be performed indefinitely. Full synchronization will be triggered and requires more bandwidth if incremental synchronization becomes unavailable. Exercise caution when enabling this option. |
   |                 |                 |                 | -  **manual**: manually reconnect.                                                                                                                                                                                                                                                                                                                                              |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 400**

.. table:: **Table 3** Response body parameters

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

**Status code: 403**

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

**Status code: 404**

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

**Status code: 500**

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

Example Requests
----------------

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/{project_id}/migration-task/{task_id}

   {
     "resume_mode" : "auto"
   }

Example Responses
-----------------

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "111400063",
     "error_msg" : "Invalid {0} parameter in the request."
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         Details of the background task queried successfully.
400         Invalid request.
401         Invalid authentication information.
403         Request rejected.
404         The requested resource could not be found.
500         Internal service error.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
