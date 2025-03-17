:original_name: BatchStopMigrationTasks.html

.. _BatchStopMigrationTasks:

Stopping Data Migration Tasks
=============================

Function
--------

This API is used to stop data migration tasks in batches. If a success response is returned, the request is successfully delivered. The migration tasks are stopped only when their status is **TERMINATED**.

URI
---

POST /v2/{project_id}/migration-task/batch-stop

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   =============== ========= ================ =========================
   Parameter       Mandatory Type             Description
   =============== ========= ================ =========================
   migration_tasks Yes       Array of strings Data migration task list.
   =============== ========= ================ =========================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------+-------------------------------------------------------------------------------------------------------------+---------------------------+
   | Parameter       | Type                                                                                                        | Description               |
   +=================+=============================================================================================================+===========================+
   | migration_tasks | Array of :ref:`StopMigrationTaskResult <batchstopmigrationtasks__response_stopmigrationtaskresult>` objects | Data migration task list. |
   +-----------------+-------------------------------------------------------------------------------------------------------------+---------------------------+

.. _batchstopmigrationtasks__response_stopmigrationtaskresult:

.. table:: **Table 4** StopMigrationTaskResult

   +-----------+--------+----------------------------------------------------------------+
   | Parameter | Type   | Description                                                    |
   +===========+========+================================================================+
   | result    | String | Result of delivering the request for stopping migration tasks. |
   +-----------+--------+----------------------------------------------------------------+
   | task_id   | String | ID of the data migration task.                                 |
   +-----------+--------+----------------------------------------------------------------+

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

**Status code: 401**

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

**Status code: 403**

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

**Status code: 404**

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

**Status code: 500**

.. table:: **Table 9** Response body parameters

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

Stopping data migration tasks in batches

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/migration-task/batch-stop

   {
     "migration_tasks" : [ "b21989ec-2889-4b8e-99db-19c073425ec2", "5130d57f-640a-435b-bc3a-0fb1860a5340" ]
   }

Example Responses
-----------------

**Status code: 200**

"Migration tasks are being stopped.

.. note::

   The migration tasks are stopped when their status is **TERMINATED**.

.. code-block::

   {
     "migration_tasks" : [ {
       "result" : "success",
       "task_id" : "b21989ec-2889-4b8e-99db-19c073425ec2"
     }, {
       "result" : "failed",
       "task_id" : "5130d57f-640a-435b-bc3a-0fb1860a5340"
     } ]
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_msg" : "invalid migration task id in the request.",
     "error_code" : "DCS.4855"
   }

Status Codes
------------

+-----------------------------------+-------------------------------------------------------------------------+
| Status Code                       | Description                                                             |
+===================================+=========================================================================+
| 200                               | "Migration tasks are being stopped.                                     |
|                                   |                                                                         |
|                                   | .. note::                                                               |
|                                   |                                                                         |
|                                   |    The migration tasks are stopped when their status is **TERMINATED**. |
+-----------------------------------+-------------------------------------------------------------------------+
| 400                               | Invalid request.                                                        |
+-----------------------------------+-------------------------------------------------------------------------+
| 401                               | Invalid authentication information.                                     |
+-----------------------------------+-------------------------------------------------------------------------+
| 403                               | The request is rejected.                                                |
+-----------------------------------+-------------------------------------------------------------------------+
| 404                               | The requested resource is not found.                                    |
+-----------------------------------+-------------------------------------------------------------------------+
| 500                               | Internal service error.                                                 |
+-----------------------------------+-------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
