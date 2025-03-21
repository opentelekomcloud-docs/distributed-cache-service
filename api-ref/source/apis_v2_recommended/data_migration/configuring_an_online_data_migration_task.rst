:original_name: SetOnlineMigrationTask.html

.. _SetOnlineMigrationTask:

Configuring an Online Data Migration Task
=========================================

Function
--------

This API is used to configure an online data migration task.

URI
---

POST /v2/{project_id}/migration/{task_id}/task

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | task_id    | Yes       | String | Online migration task ID.                                                     |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type                                                                                                    | Description                                                                                                                                                                                                                                                                         |
   +====================+=================+=========================================================================================================+=====================================================================================================================================================================================================================================================================================+
   | migration_method   | Yes             | String                                                                                                  | Type of the migration.                                                                                                                                                                                                                                                              |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  Full migration is suitable for scenarios where services can be interrupted. Data is migrated at one time.                                                                                                                                                                        |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         |    Source instance data updated during the migration will not be migrated to the target instance.                                                                                                                                                                                   |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  Incremental migration is suitable for scenarios requiring minimal service downtime.                                                                                                                                                                                              |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         |    The incremental migration parses logs to ensure data consistency between the source and target instances.                                                                                                                                                                        |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         |    After the full migration is complete, incremental migration starts.Options:                                                                                                                                                                                                      |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  **full_amount_migration**: full migration                                                                                                                                                                                                                                        |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  **incremental_migration**: incremental migration                                                                                                                                                                                                                                 |
   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resume_mode        | Yes             | String                                                                                                  | Reconnection mode.                                                                                                                                                                                                                                                                  |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | In automatic reconnection mode, if the source and target instances are disconnected due to network exceptions, automatic reconnections will be performed indefinitely.                                                                                                              |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | Full synchronization will be triggered and requires more bandwidth if incremental synchronization becomes unavailable. Exercise caution when enabling this option.                                                                                                                  |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | Values:                                                                                                                                                                                                                                                                             |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  **auto**: automatically reconnect.                                                                                                                                                                                                                                               |
   |                    |                 |                                                                                                         |                                                                                                                                                                                                                                                                                     |
   |                    |                 |                                                                                                         | -  **manual**: manually reconnect.                                                                                                                                                                                                                                                  |
   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bandwidth_limit_mb | No              | String                                                                                                  | Bandwidth limit. For incremental migration, you can limit the bandwidth to ensure smooth service running. When the data synchronization speed reaches the limit, it can no longer increase. - Unit: MB/s. - Value range: 1-10,240 (an integer greater than 0 and less than 10,241). |
   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | source_instance    | Yes             | :ref:`ConfigMigrationInstanceBody <setonlinemigrationtask__request_configmigrationinstancebody>` object | Source Redis information.                                                                                                                                                                                                                                                           |
   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | target_instance    | Yes             | :ref:`ConfigMigrationInstanceBody <setonlinemigrationtask__request_configmigrationinstancebody>` object | Target Redis information.                                                                                                                                                                                                                                                           |
   +--------------------+-----------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _setonlinemigrationtask__request_configmigrationinstancebody:

.. table:: **Table 3** ConfigMigrationInstanceBody

   +-----------+-----------+--------+-----------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                 |
   +===========+===========+========+=============================================================================+
   | id        | No        | String | Redis instance ID (mandatory if the source Redis address is not specified). |
   +-----------+-----------+--------+-----------------------------------------------------------------------------+
   | addrs     | No        | String | Source Redis address (mandatory if the Redis instance ID is not specified). |
   +-----------+-----------+--------+-----------------------------------------------------------------------------+
   | password  | No        | String | Redis password. If a password is set, this parameter is mandatory.          |
   +-----------+-----------+--------+-----------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------+--------+------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                        |
   +===========+========+====================================================================================+
   | id        | String | Migration task ID.                                                                 |
   +-----------+--------+------------------------------------------------------------------------------------+
   | name      | String | Migration task name.                                                               |
   +-----------+--------+------------------------------------------------------------------------------------+
   | status    | String | Migration status. Options: **SUCCESS**, **FAILED**, **MIGRATING**, **TERMINATED**. |
   +-----------+--------+------------------------------------------------------------------------------------+
   | error     | String | Error message.                                                                     |
   +-----------+--------+------------------------------------------------------------------------------------+

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

Configuring an online migration task with migration type set to incremental, auto-reconnect enabled, and source and target instances configured

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/migration/{task_id}/task

   {
     "migration_method" : "incremental_migration",
     "bandwidth_limit_mb" : 123,
     "resume_mode" : "auto",
     "source_instance" : {
       "id" : null,
       "addrs" : "192.168.1.1:6379,192.168.0.0:6379",
       "password" : "xxxxxx"
     },
     "target_instance" : {
       "id" : "cf4a05df-1c38-47c5-bb5a-0a7b3673b3bd",
       "addrs" : null,
       "password" : null
     }
   }

Example Responses
-----------------

**Status code: 200**

Online data migration task configured.

.. code-block::

   {
     "id" : "90754308-a156-406f-a837-8f852f38a646",
     "name" : "dcs-migration-1db7",
     "status" : "FULLMIGRATING",
     "error" : ""
   }

Status Codes
------------

=========== ======================================
Status Code Description
=========== ======================================
200         Online data migration task configured.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ======================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
