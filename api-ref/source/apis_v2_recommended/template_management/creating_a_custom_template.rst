:original_name: CreateCustomTemplate.html

.. _CreateCustomTemplate:

Creating a Custom Template
==========================

Function
--------

This API is used to create a custom template.

URI
---

POST /v2/{project_id}/config-templates

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type               | Description                                                       |
   +=================+=================+====================+===================================================================+
   | template_id     | Yes             | String             | Default template ID.                                              |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | name            | Yes             | String             | Template name.                                                    |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | type            | Yes             | String             | Template type. Options:                                           |
   |                 |                 |                    |                                                                   |
   |                 |                 |                    | -  **sys**: default template                                      |
   |                 |                 |                    | -  **user**: custom template                                      |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | engine          | No              | String             | Cache engine: Redis.                                              |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | cache_mode      | No              | String             | DCS instance type. The value range is as follows:                 |
   |                 |                 |                    |                                                                   |
   |                 |                 |                    | -  **single**: single-node                                        |
   |                 |                 |                    | -  **ha**: master/standby                                         |
   |                 |                 |                    | -  **cluster**: Redis Cluster                                     |
   |                 |                 |                    | -  **proxy**: Proxy Cluster                                       |
   |                 |                 |                    | -  **ha_rw_split**: read/write splitting                          |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | description     | No              | String             | Template description.                                             |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | engine_version  | No              | String             | Cache version.                                                    |
   |                 |                 |                    |                                                                   |
   |                 |                 |                    | If the cache engine is Redis, the version can be 4.0/5.0/6.0/7.0. |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+
   | params          | Yes             | Map<String,String> | Parameter configuration.                                          |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ============
   Parameter Type   Description
   ========= ====== ============
   id        String Template ID.
   ========= ====== ============

**Status code: 400**

.. table:: **Table 4** Response body parameters

   +---------------+--------+--------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                          |
   +===============+========+======================================================================================+
   | error_msg     | String | Error information.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                          |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to null. |
   +---------------+--------+--------------------------------------------------------------------------------------+

**Status code: 401**

.. table:: **Table 5** Response body parameters

   +---------------+--------+--------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                          |
   +===============+========+======================================================================================+
   | error_msg     | String | Error information.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                          |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to null. |
   +---------------+--------+--------------------------------------------------------------------------------------+

**Status code: 403**

.. table:: **Table 6** Response body parameters

   +---------------+--------+--------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                          |
   +===============+========+======================================================================================+
   | error_msg     | String | Error information.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                          |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to null. |
   +---------------+--------+--------------------------------------------------------------------------------------+

**Status code: 404**

.. table:: **Table 7** Response body parameters

   +---------------+--------+--------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                          |
   +===============+========+======================================================================================+
   | error_msg     | String | Error information.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                          |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to null. |
   +---------------+--------+--------------------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 8** Response body parameters

   +---------------+--------+--------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                          |
   +===============+========+======================================================================================+
   | error_msg     | String | Error information.                                                                   |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                          |
   +---------------+--------+--------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to null. |
   +---------------+--------+--------------------------------------------------------------------------------------+

Example Requests
----------------

Creating a single-node, Redis 5.0 custom template

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/config-templates

   {
     "name" : "Test",
     "cache_mode" : "single",
     "description" : "Test",
     "engine" : "Redis",
     "engine_version" : "5.0",
     "params" : {
       "latency-monitor-threshold" : 15
     },
     "template_id" : "11",
     "type" : "sys"
   }

Example Responses
-----------------

**Status code: 200**

The custom template is created successfully.

.. code-block::

   {
     "id" : "efb1ba06-d3cd-4a77-9173-16f70f2d1343"
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "111400063",
     "error_msg" : "Invalid {0} parameter in the request."
   }

Status Codes
------------

=========== ============================================
Status Code Description
=========== ============================================
200         The custom template is created successfully.
400         Invalid request.
401         Invalid authentication information.
403         Request rejected.
404         The requested resource could not be found.
500         Internal service error.
=========== ============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
