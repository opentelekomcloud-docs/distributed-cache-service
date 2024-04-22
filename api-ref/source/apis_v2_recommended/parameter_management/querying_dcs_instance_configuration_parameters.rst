:original_name: ListConfigurations.html

.. _ListConfigurations:

Querying DCS Instance Configuration Parameters
==============================================

Function
--------

This API is used to query the configuration parameters of a DCS instance.

URI
---

GET /v2/{project_id}/instances/{instance_id}/configs

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                     | Description                                                                    |
   +=======================+==========================================================================================+================================================================================+
   | config_time           | String                                                                                   | Time when the instance was operated on. For example, 2017-03-31T12:24:46.297Z. |
   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | instance_id           | String                                                                                   | Instance ID.                                                                   |
   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | redis_config          | Array of :ref:`QueryRedisConfig <listconfigurations__response_queryredisconfig>` objects | Array of configuration items of the DCS instance.                              |
   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | config_status         | String                                                                                   | DCS instance status that is being modified or has been modified. Options:      |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **UPDATING**                                                                |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **FAILURE**                                                                 |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **SUCCESS**                                                                 |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | Enumeration values:                                                            |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **UPDATING**                                                                |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **FAILURE**                                                                 |
   |                       |                                                                                          |                                                                                |
   |                       |                                                                                          | -  **SUCCESS**                                                                 |
   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | status                | String                                                                                   | Instance status.                                                               |
   +-----------------------+------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+

.. _listconfigurations__response_queryredisconfig:

.. table:: **Table 3** QueryRedisConfig

   ============= ====== =============================================
   Parameter     Type   Description
   ============= ====== =============================================
   param_value   String Configuration parameter value.
   value_type    String Type of the configuration parameter value.
   value_range   String Range of the configuration parameter value.
   description   String Description of the configuration item.
   default_value String Default value of the configuration parameter.
   param_name    String Configuration parameter name.
   param_id      String Configuration parameter ID.
   ============= ====== =============================================

**Status code: 400**

.. table:: **Table 4** Response body parameters

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

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/configs

Example Responses
-----------------

**Status code: 200**

Instance configuration parameters queried successfully.

.. code-block::

   {
     "instance_id" : "50829e5a-a4fc-4c01-8651-80be8a491602",
     "config_status" : "SUCCESS",
     "config_time" : "2020-07-06T07:04:31.464Z",
     "redis_config" : [ {
       "param_id" : "1",
       "param_name" : "timeout",
       "description" : "Close the connection after a client is idle for N seconds (0 to disable)",
       "param_value" : "101",
       "value_range" : "0-7200",
       "value_type" : "Interger",
       "default_value" : "0"
     } ],
     "status" : "RUNNING"
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Instance configuration parameters queried successfully.
400         Invalid request.
500         Internal service error.
=========== =======================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
