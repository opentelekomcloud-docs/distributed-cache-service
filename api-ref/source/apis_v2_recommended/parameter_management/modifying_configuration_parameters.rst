:original_name: UpdateConfigurations.html

.. _UpdateConfigurations:

Modifying Configuration Parameters
==================================

Function
--------

You can modify the configuration parameters of your DCS instance to optimize DCS performance based on your requirements.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/configs

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

.. table:: **Table 2** Request body parameters

   +--------------+-----------+---------------------------------------------------------------------------------+---------------------------------------------------+
   | Parameter    | Mandatory | Type                                                                            | Description                                       |
   +==============+===========+=================================================================================+===================================================+
   | redis_config | No        | Array of :ref:`RedisConfig <updateconfigurations__request_redisconfig>` objects | Array of configuration items of the DCS instance. |
   +--------------+-----------+---------------------------------------------------------------------------------+---------------------------------------------------+

.. _updateconfigurations__request_redisconfig:

.. table:: **Table 3** RedisConfig

   =========== ========= ====== ================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ================================
   param_value Yes       String Value of the configuration item.
   param_name  Yes       String Configuration item name.
   param_id    Yes       String Configuration item ID.
   =========== ========= ====== ================================

Response Parameters
-------------------

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

Modifying the instance configuration parameters. For example, set the **timeout** parameter (maximum amount of idle time after which a client connection is terminated) to 1000 seconds.

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/configs

   {
     "redis_config" : [ {
       "param_id" : "1",
       "param_name" : "timeout",
       "param_value" : "1000"
     } ]
   }

Example Responses
-----------------

None

Status Codes
------------

=========== ==================================================
Status Code Description
=========== ==================================================
204         DCS instance configurations modified successfully.
400         Invalid request.
500         Internal service error.
=========== ==================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
