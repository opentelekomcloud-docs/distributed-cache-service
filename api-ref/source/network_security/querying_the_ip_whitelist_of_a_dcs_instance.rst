:original_name: ShowIpWhitelist.html

.. _ShowIpWhitelist:

Querying the IP Whitelist of a DCS Instance
===========================================

Function
--------

This API is used to query the IP address whitelist of a specific instance.

URI
---

GET /v2/{project_id}/instance/{instance_id}/whitelist

.. table:: **Table 1** Path parameter

   =========== ========= ====== ============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ============
   project_id  Yes       String Project ID.
   instance_id Yes       String Instance ID.
   =========== ========= ====== ============

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+-------------------------------------------------------------------------+----------------------------------+
   | Parameter             | Type                                                                    | Description                      |
   +=======================+=========================================================================+==================================+
   | enable_whitelist      | Boolean                                                                 | Whether to enable the whitelist. |
   |                       |                                                                         |                                  |
   |                       |                                                                         | Options:                         |
   |                       |                                                                         |                                  |
   |                       |                                                                         | -  **true**                      |
   |                       |                                                                         | -  **false**                     |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------+
   | whitelist             | Array of :ref:`Whitelist <showipwhitelist__response_whitelist>` objects | IP whitelist group.              |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------+

.. _showipwhitelist__response_whitelist:

.. table:: **Table 3** Whitelist

   +------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type             | Description                                                                                                                                                                                                                                                         |
   +============+==================+=====================================================================================================================================================================================================================================================================+
   | group_name | String           | Whitelist group name. A maximum of four groups can be created for each instance.                                                                                                                                                                                    |
   +------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ip_list    | Array of strings | List of IP addresses in the whitelist group. A maximum of 20 IP addresses or IP address ranges can be added to an instance. Separate multiple IP addresses or IP address ranges with commas (,). IP address 0.0.0.0 and IP address range 0.0.0/0 are not supported. |
   +------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instance/{instance_id}/whitelist

Example Response
----------------

**Status code: 200**

Instance whitelist queried successfully.

.. code-block::

   {
     "instance_id" : "5560df16-cebf-4473-95c4-d1b573c16e79",
     "enable_whitelist" : true,
     "whitelist" : {
       "group_name" : "test001",
       "ip_list" : [ "10.10.10.1", "10.10.10.2" ]
     }
   }

Status Codes
------------

=========== ========================================
Status Code Description
=========== ========================================
200         Instance whitelist queried successfully.
=========== ========================================

Error Codes
-----------

See :ref:`Error Codes <dcs-api-0312044>`.
