:original_name: RestartOrFlushInstances.html

.. _RestartOrFlushInstances:

Restarting DCS Instances or Clearing DCS Instance Data
======================================================

Function
--------

This API is used to restart a running DCS instance.

Data clearance operations cannot be undone on DCS Redis 4.0, 5.0, and 6.0 instances.

URI
---

PUT /v2/{project_id}/instances/status

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+------------------+---------------------------------------------------------------+
   | Parameter       | Mandatory       | Type             | Description                                                   |
   +=================+=================+==================+===============================================================+
   | instances       | No              | Array of strings | List of instance IDs.                                         |
   +-----------------+-----------------+------------------+---------------------------------------------------------------+
   | action          | No              | String           | Operation on the instance:                                    |
   |                 |                 |                  |                                                               |
   |                 |                 |                  | **restart**: force restart                                    |
   |                 |                 |                  |                                                               |
   |                 |                 |                  | **soft_restart**: restart only the instance process           |
   |                 |                 |                  |                                                               |
   |                 |                 |                  | **flush**: clear data                                         |
   |                 |                 |                  |                                                               |
   |                 |                 |                  | .. note::                                                     |
   |                 |                 |                  |                                                               |
   |                 |                 |                  |    Only DCS Redis 4.0, 5.0, and 6.0 instances can be flushed. |
   +-----------------+-----------------+------------------+---------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------+
   | Parameter | Type                                                                                      | Description                                                      |
   +===========+===========================================================================================+==================================================================+
   | results   | Array of :ref:`BatchOpsResult <restartorflushinstances__response_batchopsresult>` objects | Result of deleting, restarting, or clearing data of an instance. |
   +-----------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------+

.. _restartorflushinstances__response_batchopsresult:

.. table:: **Table 4** BatchOpsResult

   +-----------+--------+----------------------------------------------------------------+
   | Parameter | Type   | Description                                                    |
   +===========+========+================================================================+
   | result    | String | Instance deletion result. Options: **success** and **failed**. |
   +-----------+--------+----------------------------------------------------------------+
   | instance  | String | DCS instance ID.                                               |
   +-----------+--------+----------------------------------------------------------------+

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

Force restarting a DCS instance

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/{project_id}/instances/status

   {
     "instances" : [ "2e803f66-fbb0-47ad-b6cb-fb87f5bed4ef" ],
     "action" : "restart"
   }

Example Responses
-----------------

**Status code: 200**

DCS instances restarted successfully or the instance data cleared successfully.

.. code-block::

   {
     "results" : [ {
       "instance" : "e3a7019c-8824-4c1a-8289-5300f19b9f64",
       "result" : "success"
     } ]
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------------------+
| Status Code | Description                                                                     |
+=============+=================================================================================+
| 200         | DCS instances restarted successfully or the instance data cleared successfully. |
+-------------+---------------------------------------------------------------------------------+
| 400         | Invalid request.                                                                |
+-------------+---------------------------------------------------------------------------------+
| 500         | Internal service error.                                                         |
+-------------+---------------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
