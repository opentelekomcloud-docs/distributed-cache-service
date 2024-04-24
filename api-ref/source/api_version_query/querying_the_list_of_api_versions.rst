:original_name: en-us_topic_0000001645635650.html

.. _en-us_topic_0000001645635650:

Querying the List of API Versions
=================================

Function
--------

This API is used to query the list of API versions.

URI
---

URI format

GET /

Request
-------

Sample:

.. code-block:: text

   GET https://{dcs_endpoint}/

Response
--------

.. table:: **Table 1** Response parameters

   +-----------+------------------+------------------------------------------------------------------------------------------------------------+
   | Parameter | Type             | Description                                                                                                |
   +===========+==================+============================================================================================================+
   | versions  | Array of objects | List of API versions. For details, see :ref:`Table 2 <en-us_topic_0000001645635650__table49541177222812>`. |
   +-----------+------------------+------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000001645635650__table49541177222812:

.. table:: **Table 2** versions parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                              |
   +=======================+=======================+==========================================================================================================================================+
   | min_version           | String                | The minimum minorversion supported. If the version does not support minorversions, the value is empty.                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | links                 | Array of objects      | API version URI. For details, see :ref:`Table 3 <en-us_topic_0000001645635650__table35183803523>`.                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | String                | ID of the API version.                                                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | updated               | String                | The last time when the API version was updated.                                                                                          |
   |                       |                       |                                                                                                                                          |
   |                       |                       | Time format: UTC YYYY-MM-DDTHH:MM:SS.XXXXXX                                                                                              |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | version               | String                | The maximum minorversion supported. If the version does not support minorversions, the value is empty.                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                | API version status. The value can be as follows:                                                                                         |
   |                       |                       |                                                                                                                                          |
   |                       |                       | -  **CURRENT**: DCS custom APIs provide multiple versions. For APIs offering the same functions, you are recommended to use the v2 APIs. |
   |                       |                       | -  **DEPRECATED**: The version is a deprecated version, which may be deleted later.                                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000001645635650__table35183803523:

.. table:: **Table 3** links parameters

   ========= ====== =============================================
   Parameter Type   Description
   ========= ====== =============================================
   rel       String Identifies the semantics of the relationship.
   href      String Defines the semantics of the relationship.
   ========= ====== =============================================

Sample
------

.. code-block::

   {
       "versions": [{
           "id": "v1.0",
           "links": [{
               "href": "self",
               "rel": "https://{dcs_endpoint}/v1.0/"
           }],
           "min_version": "",
           "status": "DEPRECATED",
           "updated": "2016-12-09T00:00:00Z",
           "version": ""
       },
       {
           "id": "v2",
           "links": [{
               "href": "self",
               "rel": "https://{dcs_endpoint}/v2/"
           }],
           "min_version": "",
           "status": "CURRENT",
           "updated": "2016-12-09T00:00:00Z",
           "version": ""
       }]
   }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
200         Normal
=========== ===========

Error Codes
-----------

For details, see :ref:`Error Codes <errorcode>`.
