:original_name: ShowTags.html

.. _ShowTags:

Querying Tags of a DCS Instance
===============================

Function
--------

This API is used to query the tags of an instance by its instance ID.

URI
---

GET /v2/{project_id}/instances/{instance_id}/tags

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+--------------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                           | Description |
   +===========+================================================================================+=============+
   | tags      | Array of :ref:`QueryResourceTag <showtags__response_queryresourcetag>` objects | Tag list.   |
   +-----------+--------------------------------------------------------------------------------+-------------+

.. _showtags__response_queryresourcetag:

.. table:: **Table 3** QueryResourceTag

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   key       String Tag key.
   value     String Tag value.
   ========= ====== ===========

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/tags

Example Responses
-----------------

**Status code: 200**

Instance tags queried successfully.

.. code-block::

   {
     "tags" : [ {
       "value" : "a",
       "key" : "1"
     }, {
       "value" : "b",
       "key" : "2"
     } ]
   }

Status Codes
------------

=========== ===================================
Status Code Description
=========== ===================================
200         Instance tags queried successfully.
=========== ===================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
