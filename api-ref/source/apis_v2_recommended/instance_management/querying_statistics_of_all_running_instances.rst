:original_name: ListStatisticsOfRunningInstances.html

.. _ListStatisticsOfRunningInstances:

Querying Statistics of All Running Instances
============================================

Function
--------

This API is used to query the statistics of all DCS instances that are in the **Running** state.

URI
---

GET /v2/{project_id}/instances/statistic

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +------------+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Parameter  | Type                                                                                                     | Description                                           |
   +============+==========================================================================================================+=======================================================+
   | statistics | Array of :ref:`InstanceStatistic <liststatisticsofrunninginstances__response_instancestatistic>` objects | Statistics of all instances in the **Running** state. |
   +------------+----------------------------------------------------------------------------------------------------------+-------------------------------------------------------+

.. _liststatisticsofrunninginstances__response_instancestatistic:

.. table:: **Table 3** InstanceStatistic

   +---------------+--------+--------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                                |
   +===============+========+============================================================================================+
   | input_kbps    | String | Incoming traffic (kbit/s) of the DCS instance.                                             |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | output_kbps   | String | Outgoing traffic (kbit/s) of the DCS instance.                                             |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | instance_id   | String | Instance ID.                                                                               |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | keys          | Long   | Number of cached data records                                                              |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | used_memory   | Long   | Used memory size in MB.                                                                    |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | max_memory    | Long   | Total memory size in MB.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | cmd_get_count | Long   | Number of times the GET command is run.                                                    |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | cmd_set_count | Long   | Number of times the SET command is run.                                                    |
   +---------------+--------+--------------------------------------------------------------------------------------------+
   | used_cpu      | String | Accumulated CPU time consumed by the cache in the user state and kernel state, in seconds. |
   +---------------+--------+--------------------------------------------------------------------------------------------+

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

   GET https://{dcs_endpoint}/v2/{project_id}/instances/statistic

Example Responses
-----------------

**Status code: 200**

Instance statistics queried successfully.

.. code-block::

   {
     "statistics" : [ {
       "output_kbps" : "0.0",
       "instance_id" : "e008652d-18e0-43ff-924e-072261e0372a",
       "keys" : 0,
       "used_memory" : 0,
       "cmd_get_count" : 0,
       "used_cpu" : "0.0",
       "cmd_set_count" : 0,
       "input_kbps" : "0.0",
       "max_memory" : 460
     }, {
       "output_kbps" : "0.0",
       "instance_id" : "c577a1eb-33b7-42c7-8231-ad32358599ac",
       "keys" : 0,
       "used_memory" : 0,
       "cmd_get_count" : 0,
       "used_cpu" : "0.0",
       "cmd_set_count" : 0,
       "input_kbps" : "0.0",
       "max_memory" : 460
     }, {
       "output_kbps" : "1.19",
       "instance_id" : "e8b98471-55d5-4695-b0bb-8f336a98e207",
       "keys" : 0,
       "used_memory" : 0,
       "cmd_get_count" : 0,
       "used_cpu" : "0.0",
       "cmd_set_count" : 0,
       "input_kbps" : "0.03",
       "max_memory" : 460
     }, {
       "output_kbps" : "0.0",
       "instance_id" : "bc61c690-4b34-4cbe-9ce3-11246aea7aba",
       "keys" : 0,
       "used_memory" : 0,
       "cmd_get_count" : 0,
       "used_cpu" : "0.0",
       "cmd_set_count" : 0,
       "input_kbps" : "0.0",
       "max_memory" : 6963
     } ]
   }

Status Codes
------------

=========== =========================================
Status Code Description
=========== =========================================
200         Instance statistics queried successfully.
400         Invalid request.
500         Internal service error.
=========== =========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
