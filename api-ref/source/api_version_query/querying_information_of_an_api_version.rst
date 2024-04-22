:original_name: en-us_topic_0000001693796125.html

.. _en-us_topic_0000001693796125:

Querying Information of an API Version
======================================

Function
--------

Querying Information of an API Version.

URI
---

URI format

GET /{api_version}

.. table:: **Table 1** Parameters

   +-----------------------+-----------------------+--------------------------------------+
   | Parameter             | Type                  | Description                          |
   +=======================+=======================+======================================+
   | api_version           | String                | Target API version.                  |
   |                       |                       |                                      |
   |                       |                       | The value can be **v1.0** or **v2**. |
   +-----------------------+-----------------------+--------------------------------------+

Request
-------

Sample:

.. code-block:: text

   GET https://{dcs_endpoint}/v2

Response
--------

.. table:: **Table 2** Response parameters

   +-----------+--------+------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                |
   +===========+========+============================================================================================================+
   | version   | Object | List of API versions. For details, see :ref:`Table 3 <en-us_topic_0000001693796125__table49541177222812>`. |
   +-----------+--------+------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000001693796125__table49541177222812:

.. table:: **Table 3** versions parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                              |
   +=======================+=======================+==========================================================================================================================================+
   | min_version           | String                | The minimum minorversion supported. If the version does not support minorversions, the value is empty.                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | links                 | Array of objects      | API version URI. For details, see :ref:`Table 4 <en-us_topic_0000001693796125__table35183803523>`.                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | String                | ID of the API version.                                                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | updated               | String                | The last time when the API version was updated.                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | version               | String                | The maximum minorversion supported. If the version does not support minorversions, the value is empty.                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                | API version status. The value can be as follows:                                                                                         |
   |                       |                       |                                                                                                                                          |
   |                       |                       | -  **CURRENT**: DCS custom APIs provide multiple versions. For APIs offering the same functions, you are recommended to use the v2 APIs. |
   |                       |                       | -  **DEPRECATED**: The version is a deprecated version, which may be deleted later.                                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000001693796125__table35183803523:

.. table:: **Table 4** links parameters

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
       "version": {
           "id": "v2",
           "links": [{
               "href": "self",
               "rel": "https://{dcs_endpoint}/v2/"
           }],
           "min_version": "",
           "status": "CURRENT",
           "updated": "2016-12-09T00:00:00Z",
           "version": ""
       }
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
