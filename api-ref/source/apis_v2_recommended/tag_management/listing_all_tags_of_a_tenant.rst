:original_name: ListTagsOfTenant.html

.. _ListTagsOfTenant:

Listing All Tags of a Tenant
============================

Function
--------

This API is used to query the tags of all resources owned by a tenant in a specific project.

URI
---

GET /v2/{project_id}/dcs/tags

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

   +-----------+--------------------------------------------------------------+-------------+
   | Parameter | Type                                                         | Description |
   +===========+==============================================================+=============+
   | tags      | Array of :ref:`Tag <listtagsoftenant__response_tag>` objects | Tag list.   |
   +-----------+--------------------------------------------------------------+-------------+

.. _listtagsoftenant__response_tag:

.. table:: **Table 3** Tag

   +-----------+------------------+--------------------------------------------------------+
   | Parameter | Type             | Description                                            |
   +===========+==================+========================================================+
   | key       | String           | Tag key. The key contains a maximum of 128 characters. |
   +-----------+------------------+--------------------------------------------------------+
   | values    | Array of strings | Tag value.                                             |
   +-----------+------------------+--------------------------------------------------------+

**Status code: 400**

.. table:: **Table 4** Response body parameters

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

Example Requests
----------------

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/dcs/tags

Example Responses
-----------------

**Status code: 200**

Successfully queried all tags of the tenant.

.. code-block::

   {
     "tags" : [ {
       "values" : [ "value1", "value2" ],
       "key" : "1"
     }, {
       "values" : [ "value1", "value2" ],
       "key" : "2"
     } ]
   }

Status Codes
------------

=========== ============================================
Status Code Description
=========== ============================================
200         Successfully queried all tags of the tenant.
400         Invalid request.
500         Internal service error.
=========== ============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
