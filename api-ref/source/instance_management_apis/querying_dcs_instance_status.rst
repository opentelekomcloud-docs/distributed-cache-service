:original_name: dcs-api-0312016.html

.. _dcs-api-0312016:

Querying DCS Instance Status
============================

Function
--------

This API is used to query the number of instances in different states.

URI
---

GET /v1.0/{project_id}/instances/status?includeFailure={includeFailure}

:ref:`Table 1 <dcs-api-0312016__table1624017336377>` describes the parameters.

.. _dcs-api-0312016__table1624017336377:

.. table:: **Table 1** Parameter description

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                                                                                |
   +=================+=================+=================+============================================================================================================================+
   | project_id      | String          | Yes             | Project ID.                                                                                                                |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------+
   | includeFailure  | String          | No              | An indicator of whether the number of DCS instances that failed to be created will be returned to the API caller. Options: |
   |                 |                 |                 |                                                                                                                            |
   |                 |                 |                 | -  **true**: The number of DCS instances that failed to be created will be returned to the API caller.                     |
   |                 |                 |                 | -  **false** or others: The number of DCS instances that failed to be created will not be returned to the API caller.      |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None

**Example request**

.. code-block:: text

   GET https://{dcs_endpoint}/v1.0/{project_id}/instances/status?includeFailure=true

Response
--------

**Response parameters**

:ref:`Table 2 <dcs-api-0312016__table595111370375>` describes the response parameters.

.. _dcs-api-0312016__table595111370375:

.. table:: **Table 2** Parameter description

   +--------------------+---------+----------------------------------------------------------------+
   | Parameter          | Type    | Description                                                    |
   +====================+=========+================================================================+
   | creating_count     | Integer | Number of instances that are being created.                    |
   +--------------------+---------+----------------------------------------------------------------+
   | deleting_count     | Integer | Number of instances that are being deleted.                    |
   +--------------------+---------+----------------------------------------------------------------+
   | running_count      | Integer | Number of running instances.                                   |
   +--------------------+---------+----------------------------------------------------------------+
   | error_count        | Integer | Number of abnormal instances.                                  |
   +--------------------+---------+----------------------------------------------------------------+
   | restarting_count   | Integer | Number of instances that are being restarted.                  |
   +--------------------+---------+----------------------------------------------------------------+
   | createfailed_count | Integer | Number of instances that fail to be created.                   |
   +--------------------+---------+----------------------------------------------------------------+
   | extending_count    | Integer | Number of instances that are being scaled up.                  |
   +--------------------+---------+----------------------------------------------------------------+
   | upgrading_count    | Integer | Number of instances that are being upgraded.                   |
   +--------------------+---------+----------------------------------------------------------------+
   | paying_count       | Integer | Number of instances for which payment is in progress.          |
   +--------------------+---------+----------------------------------------------------------------+
   | migrating_count    | Integer | Number of instances on which data migration is in progress.    |
   +--------------------+---------+----------------------------------------------------------------+
   | flushing_count     | Integer | Number of instances whose data is being cleared.               |
   +--------------------+---------+----------------------------------------------------------------+
   | closed_count       | Integer | Number of instances that have been stopped.                    |
   +--------------------+---------+----------------------------------------------------------------+
   | starting_count     | Integer | Number of instances that are being started.                    |
   +--------------------+---------+----------------------------------------------------------------+
   | closing_count      | Integer | Number of instances that are being stopped.                    |
   +--------------------+---------+----------------------------------------------------------------+
   | restoring_count    | Integer | Number of instances for which data restoration is in progress. |
   +--------------------+---------+----------------------------------------------------------------+

**Example response**

.. code-block::

   {"memcached":{
       "paying_count":0,
       "migrating_count":0,
       "error_count":0,
       "restarting_count":0,
       "createfailed_count":0,
       "flushing_count":0,
       "closed_count":0,
       "extending_count":0,
       "creating_count":0,
       "starting_count":0,
       "closing_count":0,
       "running_count":0,
       "upgrading_count":0,
       "restoring_count":0
      },
   "paying_count":0,
   "migrating_count":0,
   "error_count":0,
   "restarting_count":0,
   "createfailed_count":0,
   "flushing_count":0,
   "redis":{
      "paying_count":0,
      "migrating_count":0,
      "error_count":0,
      "restarting_count":0,
      "createfailed_count":0,
      "flushing_count":0,
      "closed_count":0,
      "extending_count":2,
      "creating_count":0,
      "starting_count":0,
      "closing_count":0,
      "running_count":1,
      "upgrading_count":0,
      "restoring_count":0
      },
   "closed_count":0,
   "extending_count":2,
   "creating_count":0,
   "starting_count":0,
   "closing_count":0,
   "running_count":1,
   "upgrading_count":0,
   "restoring_count":0}
   }

Status Code
-----------

:ref:`Table 3 <dcs-api-0312016__table36591653133>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312016__table36591653133:

.. table:: **Table 3** Status code

   +-------------+-------------------------------------------------------------------------+
   | Status Code | Description                                                             |
   +=============+=========================================================================+
   | 200         | Quantities of DCS instances in different statuses queried successfully. |
   +-------------+-------------------------------------------------------------------------+
