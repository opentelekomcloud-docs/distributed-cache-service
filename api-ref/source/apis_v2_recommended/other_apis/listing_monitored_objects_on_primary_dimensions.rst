:original_name: ListMonitoredObjects.html

.. _ListMonitoredObjects:

Listing Monitored Objects on Primary Dimensions
===============================================

Function
--------

This API is used to query the monitored objects on the primary dimension **dcs_instance_id**.

URI
---

GET /v2/{project_id}/dims/monitored-objects

.. table:: **Table 1** Path Parameters

   ========== ========= ====== ===========
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===========
   project_id Yes       String Tenant ID.
   ========== ========= ====== ===========

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                         |
   +=================+=================+=================+=====================================================================================================+
   | dim_name        | Yes             | String          | Primary dimension ID, which can be **dcs_instance_id**.                                             |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | offset          | No              | Integer         | Offset, which is the position where the query starts. The value must be greater than or equal to 0. |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Default: **0**                                                                                      |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Number of items displayed per page.                                                                 |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Default: **10**                                                                                     |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                       | Description                                                                                                                      |
   +=======================+============================================================================================================+==================================================================================================================================+
   | router                | Array of strings                                                                                           | Route of the specified dimension. If the dimension is the primary dimension, the array contains the ID of the primary dimension. |
   +-----------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | children              | Array of :ref:`DimChild <listmonitoredobjects__response_dimchild>` objects                                 | Secondary dimensions under the specified dimension. This parameter is valid only when the dimension is **dcs_instance_id**.      |
   |                       |                                                                                                            |                                                                                                                                  |
   |                       |                                                                                                            | -  The secondary dimension of a Proxy Cluster instance can be **dcs_cluster_redis_node** or **dcs_cluster_proxy_node**.          |
   |                       |                                                                                                            |                                                                                                                                  |
   |                       |                                                                                                            | -  The secondary dimension of a Redis Cluster instance can be **dcs_cluster_proxy_node**.                                        |
   +-----------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | instances             | Array of :ref:`InstancesMonitoredObject <listmonitoredobjects__response_instancesmonitoredobject>` objects | Monitored objects of the specified dimension.                                                                                    |
   +-----------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | total                 | Integer                                                                                                    | Total number of monitored objects on the primary dimension.                                                                      |
   +-----------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. _listmonitoredobjects__response_dimchild:

.. table:: **Table 4** DimChild

   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                                         |
   +===========+========+=====================================================================================================================================================================================================+
   | dim_name  | String | Dimension name. The value can be **dcs_instance_id**, **dcs_cluster_redis_node**, or **dcs_cluster_proxy_node**.                                                                                    |
   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dim_route | String | Dimension route. Format: *Dimension name,Sub-dimension name*. For example, if **dim_name** is **dcs_cluster_redis_node**, the value of **dim_route** is **dcs_instance_id,dcs_cluster_redis_node**. |
   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _listmonitoredobjects__response_instancesmonitoredobject:

.. table:: **Table 5** InstancesMonitoredObject

   +-----------------+--------+---------------------------------------------------------------+
   | Parameter       | Type   | Description                                                   |
   +=================+========+===============================================================+
   | dcs_instance_id | String | ID of the monitored object, which is the instance ID.         |
   +-----------------+--------+---------------------------------------------------------------+
   | name            | String | Name of the monitored object, which is the instance name.     |
   +-----------------+--------+---------------------------------------------------------------+
   | status          | String | Status of the monitored object, which is the instance status. |
   +-----------------+--------+---------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 6** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | error_msg             | String                | Error message.                                                                           |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code.                                                                              |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **9**                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_ext_msg         | String                | Extended error information. This parameter is not used currently and is set to **null**. |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}}/v2/{project_id}}/dims/monitored-objects?dim_name={dim_name}

Example Responses
-----------------

**Status code: 200**

Successfully listed the monitored objects on the primary dimension.

.. code-block::

   {
     "router" : [ "dcs_instance_id" ],
     "total" : 3,
     "children" : [ {
       "dim_name" : "dcs_cluster_redis_node",
       "dim_route" : "dcs_instance_id,dcs_cluster_redis_node"
     }, {
       "dim_name" : "dcs_cluster_proxy_node",
       "dim_route" : "dcs_instance_id,dcs_cluster_proxy_node"
     } ],
     "instances" : [ {
       "name" : "dcs-redis-single-node",
       "status" : "RUNNING",
       "dcs_instance_id" : "fe909c47-8990-44a0-9154-d0a1e95e78fe"
     }, {
       "name" : "dcs-redis-master-standby",
       "status" : "RUNNING",
       "dcs_instance_id" : "877e5ae3-482e-4c38-88a0-030a0fa6f399"
     }, {
       "name" : "dcs-proxy-cluster",
       "status" : "RUNNING",
       "dcs_instance_id" : "448ee851-1366-47f2-913a-e21032e690c4"
     } ]
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------+
| Status Code | Description                                                         |
+=============+=====================================================================+
| 200         | Successfully listed the monitored objects on the primary dimension. |
+-------------+---------------------------------------------------------------------+
| 500         | Internal service error.                                             |
+-------------+---------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
