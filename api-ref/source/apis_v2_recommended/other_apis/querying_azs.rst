:original_name: ListAvailableZones.html

.. _ListAvailableZones:

Querying AZs
============

Function
--------

This API is used to query the AZ information of the current region.

URI
---

GET /v2/available-zones

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 1** Response body parameters

   +-----------------+--------------------------------------------------------------------------------------+---------------+
   | Parameter       | Type                                                                                 | Description   |
   +=================+======================================================================================+===============+
   | region_id       | String                                                                               | Region ID.    |
   +-----------------+--------------------------------------------------------------------------------------+---------------+
   | available_zones | Array of :ref:`AvailableZones <listavailablezones__response_availablezones>` objects | Array of AZs. |
   +-----------------+--------------------------------------------------------------------------------------+---------------+

.. _listavailablezones__response_availablezones:

.. table:: **Table 2** AvailableZones

   +-----------------------+-----------------------+-------------------------------------------------------+
   | Parameter             | Type                  | Description                                           |
   +=======================+=======================+=======================================================+
   | code                  | String                | AZ code.                                              |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | port                  | String                | AZ port.                                              |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | name                  | String                | AZ name.                                              |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | id                    | String                | AZ ID.                                                |
   +-----------------------+-----------------------+-------------------------------------------------------+
   | resource_availability | String                | Whether the AZ has available resources.               |
   |                       |                       |                                                       |
   |                       |                       | -  **true**: There are available resources in the AZ. |
   |                       |                       |                                                       |
   |                       |                       | -  **false**: No resource is available                |
   |                       |                       |                                                       |
   |                       |                       | Enumeration values:                                   |
   |                       |                       |                                                       |
   |                       |                       | -  **true**                                           |
   |                       |                       |                                                       |
   |                       |                       | -  **false**                                          |
   +-----------------------+-----------------------+-------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/available-zones

Example Responses
-----------------

**Status code: 200**

The query is successful.

.. code-block::

   {
     "region_id" : "region00",
     "available_zones" : [ {
       "code" : "region01",
       "port" : "8403",
       "name" : "AZ 1.",
       "id" : "effdcbc7d4d64a02aa1fa26b42f56533",
       "resource_availability" : "true"
     }, {
       "code" : "region02",
       "port" : "8404",
       "name" : "AZ 2.",
       "id" : "a0865121f83b41cbafce65930a22a6e8",
       "resource_availability" : "true"
     }, {
       "code" : "region03",
       "port" : "8408",
       "name" : "AZ 3.",
       "id" : "2dcb154ac2724a6d92e9bcc859657c1e",
       "resource_availability" : "true"
     } ]
   }

Status Codes
------------

=========== ========================
Status Code Description
=========== ========================
200         The query is successful.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
