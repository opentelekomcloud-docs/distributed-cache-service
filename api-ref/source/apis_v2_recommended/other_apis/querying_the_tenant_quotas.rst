:original_name: ShowQuotaOfTenant.html

.. _ShowQuotaOfTenant:

Querying the Tenant Quotas
==========================

Function
--------

This API is used to query the default instance quota and total memory quota of a tenant and the maximum and minimum quotas a tenant can apply for. Different tenants have different quotas in different regions.

URI
---

GET /v2/{project_id}/quota

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

   +-----------+-----------------------------------------------------------+--------------------+
   | Parameter | Type                                                      | Description        |
   +===========+===========================================================+====================+
   | quotas    | :ref:`quotas <showquotaoftenant__response_quotas>` object | Quota information. |
   +-----------+-----------------------------------------------------------+--------------------+

.. _showquotaoftenant__response_quotas:

.. table:: **Table 3** quotas

   +-----------+---------------------------------------------------------------------------+----------------+
   | Parameter | Type                                                                      | Description    |
   +===========+===========================================================================+================+
   | resources | Array of :ref:`Resources <showquotaoftenant__response_resources>` objects | List of quotas |
   +-----------+---------------------------------------------------------------------------+----------------+

.. _showquotaoftenant__response_resources:

.. table:: **Table 4** Resources

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                       |
   +=======================+=======================+===================================================================================+
   | unit                  | String                | Resource unit.                                                                    |
   |                       |                       |                                                                                   |
   |                       |                       | -  When **type** is set to **instance**, no value is returned.                    |
   |                       |                       |                                                                                   |
   |                       |                       | -  When **type** is set to **ram**, **GB** is returned.                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | min                   | Integer               | Minimum limit of instance quota when **type** is set to **instance**.             |
   |                       |                       |                                                                                   |
   |                       |                       | -  Minimum limit of memory quota when **type** is set to **ram**.                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | max                   | Integer               | Maximum limit of instance quota when **type** is set to **instance**.             |
   |                       |                       |                                                                                   |
   |                       |                       | -  Maximum limit of memory quota when **type** is set to **ram**.                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | quota                 | Integer               | Maximum number of instances that can be created and maximum allowed total memory. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | used                  | Integer               | Number of created instances and used memory.                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+
   | type                  | String                | The value can be **instance** or **ram**.                                         |
   |                       |                       |                                                                                   |
   |                       |                       | -  **instances**: instance quota                                                  |
   |                       |                       |                                                                                   |
   |                       |                       | -  **ram**: memory quota                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------+

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

**Status code: 500**

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

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/quota

Example Responses
-----------------

**Status code: 200**

Tenant quota queried successfully.

.. code-block::

   {
     "quotas" : {
       "resources" : [ {
         "unit" : { },
         "min" : 1,
         "max" : 10,
         "quota" : 10,
         "used" : 3,
         "type" : "instance"
       }, {
         "unit" : "GB",
         "min" : 1,
         "max" : 800,
         "quota" : 800,
         "used" : 22,
         "type" : "ram"
       } ]
     }
   }

Status Codes
------------

=========== ==================================
Status Code Description
=========== ==================================
200         Tenant quota queried successfully.
400         Invalid request.
500         Internal service error.
=========== ==================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
