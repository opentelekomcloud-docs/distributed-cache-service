:original_name: ListConfigTemplates.html

.. _ListConfigTemplates:

Viewing Parameter Templates
===========================

Function
--------

This API is used to query parameter templates of a tenant, and allows you to specify query criteria.

URI
---

GET /v2/{project_id}/config-templates

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                |
   +=================+=================+=================+============================================================================================================================================================================================+
   | name            | No              | String          | Parameter template name. Fuzzy search is supported.                                                                                                                                        |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type            | Yes             | String          | Template type. Options:                                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                            |
   |                 |                 |                 | -  **sys**: default template                                                                                                                                                               |
   |                 |                 |                 | -  **user**: custom template                                                                                                                                                               |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | engine          | No              | String          | Cache engine: Redis.                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | engine_version  | No              | String          | Cache engine version.                                                                                                                                                                      |
   |                 |                 |                 |                                                                                                                                                                                            |
   |                 |                 |                 | If the cache engine is Redis, the version can be 4.0/5.0/6.0/7.0.                                                                                                                          |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cache_mode      | No              | String          | DCS instance type. The value range is as follows:                                                                                                                                          |
   |                 |                 |                 |                                                                                                                                                                                            |
   |                 |                 |                 | -  **single**: single-node                                                                                                                                                                 |
   |                 |                 |                 | -  **ha**: master/standby                                                                                                                                                                  |
   |                 |                 |                 | -  **cluster**: Redis Cluster                                                                                                                                                              |
   |                 |                 |                 | -  **proxy**: Proxy Cluster                                                                                                                                                                |
   |                 |                 |                 | -  **ha_rw_split**: read/write splitting                                                                                                                                                   |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset          | No              | Integer         | Offset, which is the position where the query starts. The value must be greater than or equal to 0.                                                                                        |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Number of records displayed on each page. The minimum value is **1**. The maximum value is **1000**. If this parameter is not specified, 10 records are displayed on each page by default. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +--------------+---------------------------------------------------------------------------------------------------------+-------------------------+
   | Parameter    | Type                                                                                                    | Description             |
   +==============+=========================================================================================================+=========================+
   | template_num | Integer                                                                                                 | Number of templates.    |
   +--------------+---------------------------------------------------------------------------------------------------------+-------------------------+
   | templates    | Array of :ref:`ConfigTemplatesListInfo <listconfigtemplates__response_configtemplateslistinfo>` objects | Template details array. |
   +--------------+---------------------------------------------------------------------------------------------------------+-------------------------+

.. _listconfigtemplates__response_configtemplateslistinfo:

.. table:: **Table 4** ConfigTemplatesListInfo

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                            |
   +=======================+=======================+========================================================================================================================================+
   | template_id           | String                | Template ID.                                                                                                                           |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | cache_mode            | String                | DCS instance type. The value range is as follows:                                                                                      |
   |                       |                       |                                                                                                                                        |
   |                       |                       | -  **single**: single-node                                                                                                             |
   |                       |                       | -  **ha**: master/standby                                                                                                              |
   |                       |                       | -  **cluster**: Redis Cluster                                                                                                          |
   |                       |                       | -  **proxy**: Proxy Cluster                                                                                                            |
   |                       |                       | -  **ha_rw_split**: read/write splitting                                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                | Template description.                                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | engine                | String                | Cache engine: Redis.                                                                                                                   |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | engine_version        | String                | Cache version.                                                                                                                         |
   |                       |                       |                                                                                                                                        |
   |                       |                       | If the cache engine is Redis, the version can be 3.0/4.0/5.0/6.0/7.0.                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | name                  | String                | Template name.                                                                                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | product_type          | String                | Edition.                                                                                                                               |
   |                       |                       |                                                                                                                                        |
   |                       |                       | Only the basic edition is supported. Value: **generic**.                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | storage_type          | String                | Storage type.                                                                                                                          |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | type                  | String                | Template type. Options:                                                                                                                |
   |                       |                       |                                                                                                                                        |
   |                       |                       | -  **sys**: default template                                                                                                           |
   |                       |                       | -  **user**: custom template                                                                                                           |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Time when the template is created. This parameter is valid only in custom parameter templates. The format is 2023-05-10T11:09:35.802Z. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

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

**Status code: 401**

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

**Status code: 403**

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

**Status code: 404**

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

**Status code: 500**

.. table:: **Table 9** Response body parameters

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

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/config-templates?type=sys&engine=Redis&engine_version=5.0&cache_mode=ha&offset=0&limit=10

Example Responses
-----------------

**Status code: 200**

Parameter templates listed.

.. code-block::

   {
     "template_num" : 1,
     "templates" : [ {
       "template_id" : "6",
       "cache_mode" : "single",
       "description" : null,
       "engine" : "Redis",
       "engine_version" : "4.0",
       "name" : "Default-Redis-4.0-single-generic-DRAM",
       "product_type" : "generic",
       "storage_type" : "DRAM",
       "type" : "sys"
     } ]
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

=========== ==========================================
Status Code Description
=========== ==========================================
200         Parameter templates listed.
400         Invalid request.
401         Invalid authentication information.
403         Request rejected.
404         The requested resource could not be found.
500         Internal service error.
=========== ==========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
