:original_name: dcs-api-0312039.html

.. _dcs-api-0312039:

Querying AZ Information
=======================

Function
--------

This API is used to query the ID of the AZ where a DCS instance resides.

URI
---

GET /v1.0/availableZones

Request
-------

**Request parameters**

None

**Example request**

None

Response
--------

**Response parameters**

:ref:`Table 1 <dcs-api-0312039__table5725353918>` describes the response parameters.

.. _dcs-api-0312039__table5725353918:

.. table:: **Table 1** Parameter description

   +-----------------+--------+---------------------------------------------------------------------------------------+
   | Parameter       | Type   | Description                                                                           |
   +=================+========+=======================================================================================+
   | regionId        | String | Region ID.                                                                            |
   +-----------------+--------+---------------------------------------------------------------------------------------+
   | available_zones | Array  | Array of AZs. For details, see :ref:`Table 2 <dcs-api-0312039__table20901104905614>`. |
   +-----------------+--------+---------------------------------------------------------------------------------------+

.. _dcs-api-0312039__table20901104905614:

.. table:: **Table 2** Parameter description of the available_zones array

   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | Parameter                  | Type                  | Description                                                                        |
   +============================+=======================+====================================================================================+
   | id                         | String                | AZ ID.                                                                             |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | code                       | String                | AZ code.                                                                           |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | name                       | String                | AZ name.                                                                           |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | port                       | String                | Port number of the AZ.                                                             |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | resource_availability      | String                | An indicator of whether there are available Redis 3.0 resources in the AZ.         |
   |                            |                       |                                                                                    |
   |                            |                       | -  **true**: There are available resources in the AZ.                              |
   |                            |                       | -  **false**: There are no available resources in the AZ.                          |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+
   | resource_availability_dcs2 | String                | An indicator of whether there are available Redis 4.0 and 5.0 resources in the AZ. |
   |                            |                       |                                                                                    |
   |                            |                       | -  **true**: There are available resources in the AZ.                              |
   |                            |                       | -  **false**: There are no available resources in the AZ.                          |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "regionId": "XXXXXX",
       "available_zones": [
           {
               "id": "f84448fd537f46078dd8bd776747f573",
               "code": "XXXXXX",
               "name": "XXXXXX",
               "port": "8003",
               "resource_availability": "true"
           },
           {
               "id": "12c47a78666b4e438cd0c692b9860387",
               "code": "XXXXXX",
               "name": "XXXXXX",
               "port": "8002",
               "resource_availability": "true"
           },
           {
               "id": "0725858e0d26434f9aa3dc5fc40d5697",
               "code": "XXXXXX",
               "name": "XXXXXX",
               "port": "8009",
               "resource_availability": "true"
           }
       ]
   }

Status Code
-----------

:ref:`Table 3 <dcs-api-0312039__table201151124142>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312039__table201151124142:

.. table:: **Table 3** Status code

   =========== ====================================
   Status Code Description
   =========== ====================================
   200         AZ information queried successfully.
   =========== ====================================
