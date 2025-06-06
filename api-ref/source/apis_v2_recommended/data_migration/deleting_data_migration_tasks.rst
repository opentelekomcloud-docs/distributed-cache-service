:original_name: DeleteMigrationTask.html

.. _DeleteMigrationTask:

Deleting Data Migration Tasks
=============================

Function
--------

This API is used to delete data migration tasks.

URI
---

DELETE /v2/{project_id}/migration-tasks/delete

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +--------------+-----------+------------------+---------------------------------------------------+
   | Parameter    | Mandatory | Type             | Description                                       |
   +==============+===========+==================+===================================================+
   | task_id_list | Yes       | Array of strings | List of IDs of the migration tasks to be deleted. |
   +--------------+-----------+------------------+---------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +--------------+------------------+---------------------------------------------------+
   | Parameter    | Type             | Description                                       |
   +==============+==================+===================================================+
   | task_id_list | Array of strings | List of IDs of the migration tasks to be deleted. |
   +--------------+------------------+---------------------------------------------------+

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

Deleting data migration tasks

.. code-block:: text

   DELETE https://{dcs_endpoint}/v2/666486c2d9b948c1bbea57e714d744fa/migration-tasks/delete

   {
     "task_id_list" : [ "2fb6b7e2-5eb8-4380-9d60-ce8d12b19aca" ]
   }

Example Responses
-----------------

**Status code: 200**

Data migration task deleted successfully.

.. code-block::

   {
     "task_id_list" : [ "2fb6b7e2-5eb8-4380-9d60-ce8d12b19aca" ]
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------------------------------+
| Status Code | Description                                                                                 |
+=============+=============================================================================================+
| 200         | Data migration task deleted successfully.                                                   |
+-------------+---------------------------------------------------------------------------------------------+
| 400         | Invalid request.                                                                            |
+-------------+---------------------------------------------------------------------------------------------+
| 401         | Invalid authentication information.                                                         |
+-------------+---------------------------------------------------------------------------------------------+
| 403         | The request is rejected.                                                                    |
+-------------+---------------------------------------------------------------------------------------------+
| 404         | The requested resource does not exist. (No response. For details, see status code **200**.) |
+-------------+---------------------------------------------------------------------------------------------+
| 500         | Internal service error.                                                                     |
+-------------+---------------------------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
