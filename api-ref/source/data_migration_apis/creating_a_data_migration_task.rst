:original_name: dcs-api-0514004.html

.. _dcs-api-0514004:

Creating a Data Migration Task
==============================

Function
--------

This API is used to create a data migration task.

Constraints
-----------

None

URI
---

POST /v2/{project_id}/migration-task

.. table:: **Table 1** URI parameter

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                          |
   +=================+=================+=================+======================================================================================================+
   | project_id      | Yes             | String          | Project ID.                                                                                          |
   |                 |                 |                 |                                                                                                      |
   |                 |                 |                 | For details about how to obtain the project ID, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request body parameter description

   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Mandatory       | Type                                                                   | Description                                                                                                                      |
   +==================+=================+========================================================================+==================================================================================================================================+
   | task_name        | Yes             | String                                                                 | Name of the migration task.                                                                                                      |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | description      | No              | String                                                                 | Description of the migration task.                                                                                               |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | migration_type   | Yes             | String                                                                 | Mode of the migration.                                                                                                           |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | Options:                                                                                                                         |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | -  **backupfile_import**: indicates importing backup files.                                                                      |
   |                  |                 |                                                                        | -  **online_migration**: indicates migrating data online.                                                                        |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | migration_method | Yes             | String                                                                 | Type of the migration.                                                                                                           |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | Options:                                                                                                                         |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | -  **full_amount_migration**: indicates a full migration.                                                                        |
   |                  |                 |                                                                        | -  **incremental_migration**: indicates an incremental migration.                                                                |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | backup_files     | No              | :ref:`BackupFilesBody <dcs-api-0514004__table52620454720>` Object      | Backup files to be imported when the migration mode is importing backup files.                                                   |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | network_type     | No              | String                                                                 | Type of the network for communication between the source and destination Redis when the migration mode is online data migration. |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | Options:                                                                                                                         |
   |                  |                 |                                                                        |                                                                                                                                  |
   |                  |                 |                                                                        | -  **vpc**                                                                                                                       |
   |                  |                 |                                                                        | -  **vpn**                                                                                                                       |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | source_instance  | No              | :ref:`SourceInstanceBody <dcs-api-0514004__table1463144520714>` Object | Source Redis information. This parameter is mandatory when the migration mode is online data migration.                          |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | target_instance  | Yes             | :ref:`TargetInstanceBody <dcs-api-0514004__table147217451875>` Object  | Destination Redis instance information.                                                                                          |
   +------------------+-----------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0514004__table52620454720:

.. table:: **Table 3** BackupFilesBody

   +-------------+-----------+------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type                                                             | Description                                                                              |
   +=============+===========+==================================================================+==========================================================================================+
   | file_source | No        | String                                                           | Data source. Currently, only OBS buckets are supported. The value is **self_build_obs**. |
   +-------------+-----------+------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | bucket_name | Yes       | String                                                           | OBS bucket name.                                                                         |
   +-------------+-----------+------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | files       | Yes       | Array of :ref:`Files <dcs-api-0514004__table4440451079>` Objects | List of backup files to be imported.                                                     |
   +-------------+-----------+------------------------------------------------------------------+------------------------------------------------------------------------------------------+

.. _dcs-api-0514004__table4440451079:

.. table:: **Table 4** Files

   +-----------+-----------+--------+-------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                             |
   +===========+===========+========+=========================================================================+
   | file_name | Yes       | String | Name of a backup file.                                                  |
   +-----------+-----------+--------+-------------------------------------------------------------------------+
   | size      | No        | String | File size in bytes.                                                     |
   +-----------+-----------+--------+-------------------------------------------------------------------------+
   | update_at | No        | String | Time when the file is last modified. The format is YYYY-MM-DD HH:MM:SS. |
   +-----------+-----------+--------+-------------------------------------------------------------------------+

.. _dcs-api-0514004__table1463144520714:

.. table:: **Table 5** SourceInstanceBody

   +-----------+-----------+--------+---------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                         |
   +===========+===========+========+=====================================================================+
   | addrs     | Yes       | String | Source Redis name (specified in the **source_instance** parameter). |
   +-----------+-----------+--------+---------------------------------------------------------------------+
   | password  | No        | String | Redis password. If a password is set, this parameter is mandatory.  |
   +-----------+-----------+--------+---------------------------------------------------------------------+

.. _dcs-api-0514004__table147217451875:

.. table:: **Table 6** TargetInstanceBody

   +-----------+-----------+--------+-----------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                       |
   +===========+===========+========+===================================================================================+
   | id        | Yes       | String | Destination Redis instance ID (mandatory in the **target_instance** parameter).   |
   +-----------+-----------+--------+-----------------------------------------------------------------------------------+
   | name      | No        | String | Destination Redis instance name (specified in the **target_instance** parameter). |
   +-----------+-----------+--------+-----------------------------------------------------------------------------------+
   | password  | No        | String | Redis password. If a password is set, this parameter is mandatory.                |
   +-----------+-----------+--------+-----------------------------------------------------------------------------------+

Response
--------

If the status code is 200, the following parameters are returned:

.. table:: **Table 7** Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                             |
   +=======================+=======================+=========================================================================================+
   | id                    | String                | ID of the migration task.                                                               |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------+
   | name                  | String                | Name of the migration task.                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------+
   | status                | String                | Migration task status. The value can be:                                                |
   |                       |                       |                                                                                         |
   |                       |                       | -  **SUCCESS**: Migration succeeded.                                                    |
   |                       |                       | -  **FAILED**: Migration failed.                                                        |
   |                       |                       | -  **MIGRATING**: Migration is in progress.                                             |
   |                       |                       | -  **TERMINATED**: Migration has been stopped.                                          |
   |                       |                       | -  **TERMINATING**: Migration is being stopped.                                         |
   |                       |                       | -  **RUNNING**: The migration task has been created and is waiting to be executed.      |
   |                       |                       | -  **CREATING**: The migration task is being created.                                   |
   |                       |                       | -  **FULLMIGRATING**: Full migration is in progress.                                    |
   |                       |                       | -  **INCRMIGEATING**: Incremental migration is in progress.                             |
   |                       |                       | -  **ERROR**: faulty                                                                    |
   |                       |                       | -  **DELETED**: faulty                                                                  |
   |                       |                       | -  **RELEASED**: automatically released                                                 |
   |                       |                       | -  **MIGRATION_SUCCESS**: The migration is successful, and resources are to be cleared. |
   |                       |                       | -  **MIGRATION_FAILED**: The migration failed, and resources are to be cleared.         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------+

Example Request
---------------

-  Example request URL:

   .. code-block:: text

      POST https://{dcs_endpoint}/v2/{project_id}/migration-task

-  Example request 1 (online migration)

   .. code-block::

      {
        "task_name" : "lmd-test",
        "description" : "Test",
        "migration_type" : "online_migration",
        "migration_method" : "full_amount_migration",
        "network_type" : "vpc",
        "source_instance" : {
          "addrs" : "192.168.1.135:6379",
          "password" : "xxxxxx"
        },
        "target_instance" : {
          "name" : "dcs-test",
          "id" : "4cd5dbb8-aacd-4603-b817-3e97d48c7a20"
        }
      }

-  Example request 2 (importing a backup file)

   .. code-block::

      {
       "backup_files": {
        "bucket_name": "bucket-lmz",
        "file_source": "self_build_obs",
        "files": [
         {
          "file_name": "appendonly03.aof"
         }
        ]
       },
       "migration_method": "full_amount_migration",
       "migration_type": "backupfile_import",
       "target_instance": {
        "id": "318ed365-3c1b-42d7-a5b6-663dded628a0"
       },
       "task_name": "lmd-test"
      }

Example Response
----------------

If the status code is 200, the data migration task is successfully created.

.. code-block::

   {
     "id" : "8aa6999e71cb638b0171f485f5266ef0",
     "name" : "lmd-test",
     "status" : "MIGRATING"
   }

Status Code
-----------

=========== =========================================
Status Code Description
=========== =========================================
200         Data migration task created successfully.
400         Invalid request.
500         Internal service error.
=========== =========================================

Error Codes
-----------

For details, see :ref:`Error Codes <dcs-api-0312044>`.
