:original_name: ListMonitoredObjectsOfInstance.html

.. _ListMonitoredObjectsOfInstance:

Listing Monitored Objects on Secondary Dimensions Under a Primary Dimension
===========================================================================

Function
--------

This API is used to query the monitored objects on secondary dimensions under primary dimension **dcs_instance_id**.

URI
---

GET /v2/{project_id}/dims/monitored-objects/{instance_id}

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+--------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                    |
   +=============+===========+========+================================================================================+
   | project_id  | Yes       | String | Tenant ID.                                                                     |
   +-------------+-----------+--------+--------------------------------------------------------------------------------+
   | instance_id | Yes       | String | ID of the monitored object on the primary dimension, which is the instance ID. |
   +-------------+-----------+--------+--------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------+-----------+--------+----------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                    |
   +===========+===========+========+================================================================+
   | dim_name  | Yes       | String | ID of the primary dimension, which can be **dcs_instance_id**. |
   +-----------+-----------+--------+----------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Type                                                                                                                               | Description                                                                                                                                                                                         |
   +=========================+====================================================================================================================================+=====================================================================================================================================================================================================+
   | router                  | Array of strings                                                                                                                   | Route of the specified dimension. If the dimension is the primary dimension, the array contains the ID of the primary dimension.                                                                    |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | children                | Array of :ref:`DimChild <listmonitoredobjectsofinstance__response_dimchild>` objects                                               | Secondary dimensions under the specified dimension. This parameter is valid only when the dimension is **dcs_instance_id**.                                                                         |
   |                         |                                                                                                                                    |                                                                                                                                                                                                     |
   |                         |                                                                                                                                    | -  The secondary dimension of a Proxy Cluster instance can be **dcs_cluster_redis_node** or **dcs_cluster_proxy_node**.                                                                             |
   |                         |                                                                                                                                    |                                                                                                                                                                                                     |
   |                         |                                                                                                                                    | -  The secondary dimension of a Redis Cluster instance can be **dcs_cluster_proxy_node**.                                                                                                           |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instances               | Array of :ref:`InstancesMonitoredObject <listmonitoredobjectsofinstance__response_instancesmonitoredobject>` objects               | Monitored objects of the specified dimension.                                                                                                                                                       |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dcs_cluster_redis_node  | Array of :ref:`ClusterRedisNodeMonitoredObject <listmonitoredobjectsofinstance__response_clusterredisnodemonitoredobject>` objects | Monitored objects of the Redis Server. This parameter is valid for Proxy Cluster and Redis Cluster instances. The field name is the same as the secondary dimension object name under **children**. |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dcs_cluster_proxy_node  | Array of :ref:`ProxyNodeMonitoredObject <listmonitoredobjectsofinstance__response_proxynodemonitoredobject>` objects               | Monitored objects of proxies. This parameter is valid only for Proxy Cluster DCS Redis 3.0 instances. The field name is the same as the secondary dimension object name under **children**.         |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dcs_cluster_proxy2_node | Array of :ref:`Proxy2NodeMonitoredObject <listmonitoredobjectsofinstance__response_proxy2nodemonitoredobject>` objects             | Monitored objects of the Proxy. This parameter is valid only for Redis 4.0 and 5.0 Proxy Cluster instances. The field name is the same as the secondary dimension object name under **children**.   |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | total                   | Integer                                                                                                                            | Total number of monitored objects on the primary dimension.                                                                                                                                         |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _listmonitoredobjectsofinstance__response_dimchild:

.. table:: **Table 4** DimChild

   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                                         |
   +===========+========+=====================================================================================================================================================================================================+
   | dim_name  | String | Dimension name. The value can be **dcs_instance_id**, **dcs_cluster_redis_node**, or **dcs_cluster_proxy_node**.                                                                                    |
   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dim_route | String | Dimension route. Format: *Dimension name,Sub-dimension name*. For example, if **dim_name** is **dcs_cluster_redis_node**, the value of **dim_route** is **dcs_instance_id,dcs_cluster_redis_node**. |
   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _listmonitoredobjectsofinstance__response_instancesmonitoredobject:

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

.. _listmonitoredobjectsofinstance__response_clusterredisnodemonitoredobject:

.. table:: **Table 6** ClusterRedisNodeMonitoredObject

   +------------------------+--------+-------------------------------------------------------------------------+
   | Parameter              | Type   | Description                                                             |
   +========================+========+=========================================================================+
   | dcs_instance_id        | String | ID of the monitored object, which is the node ID.                       |
   +------------------------+--------+-------------------------------------------------------------------------+
   | name                   | String | Name of the monitored object, which is the node IP address.             |
   +------------------------+--------+-------------------------------------------------------------------------+
   | dcs_cluster_redis_node | String | ID of the monitored object on the **dcs_cluster_redis_node** dimension. |
   +------------------------+--------+-------------------------------------------------------------------------+
   | status                 | String | Status of the monitored object, which is the node status.               |
   +------------------------+--------+-------------------------------------------------------------------------+

.. _listmonitoredobjectsofinstance__response_proxynodemonitoredobject:

.. table:: **Table 7** ProxyNodeMonitoredObject

   +------------------------+--------+-------------------------------------------------------------------------+
   | Parameter              | Type   | Description                                                             |
   +========================+========+=========================================================================+
   | dcs_instance_id        | String | ID of the monitored object, which is the node ID.                       |
   +------------------------+--------+-------------------------------------------------------------------------+
   | name                   | String | Name of the monitored object, which is the node IP address.             |
   +------------------------+--------+-------------------------------------------------------------------------+
   | dcs_cluster_proxy_node | String | ID of the monitored object on the **dcs_cluster_proxy_node** dimension. |
   +------------------------+--------+-------------------------------------------------------------------------+
   | status                 | String | Status of the monitored object, which is the node status.               |
   +------------------------+--------+-------------------------------------------------------------------------+

.. _listmonitoredobjectsofinstance__response_proxy2nodemonitoredobject:

.. table:: **Table 8** Proxy2NodeMonitoredObject

   +-------------------------+--------+--------------------------------------------------------------------------+
   | Parameter               | Type   | Description                                                              |
   +=========================+========+==========================================================================+
   | dcs_instance_id         | String | ID of the monitored object, which is the node ID.                        |
   +-------------------------+--------+--------------------------------------------------------------------------+
   | name                    | String | Name of the monitored object, which is the node IP address.              |
   +-------------------------+--------+--------------------------------------------------------------------------+
   | dcs_cluster_proxy2_node | String | ID of the monitored object on the **dcs_cluster_proxy2_node** dimension. |
   +-------------------------+--------+--------------------------------------------------------------------------+
   | status                  | String | Status of the monitored object, which is the node status.                |
   +-------------------------+--------+--------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 9** Response body parameters

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

   GET https://{dcs_endpoint}/v2/{project_id}/dims/monitored-objects/{instance_id}?dim_name={dim_name}

Example Responses
-----------------

**Status code: 200**

Successfully queried the monitored objects on the primary dimension.

.. code-block::

   {
     "router" : [ "dcs_instance_id" ],
     "total" : 1,
     "children" : [ {
       "dim_name" : "dcs_cluster_redis_node",
       "dim_route" : "dcs_instance_id,dcs_cluster_redis_node"
     } ],
     "instances" : [ {
       "name" : "dcs-test001",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19"
     } ],
     "dcs_cluster_redis_node" : [ {
       "name" : "(master)192.168.2.145",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "b1f4aa9e4dae50888e58c9caecdfc108"
     }, {
       "name" : "(replica)192.168.2.199",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "e0e10e489a73487147928167396474bc"
     }, {
       "name" : "(master)192.168.2.243",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "e797c3ba8bee782e25cdd4a90eb00517"
     }, {
       "name" : "(replica)192.168.2.164",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "d810fb44f9f7a359e000cf277a824c43"
     }, {
       "name" : "(master)192.168.2.95",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "f25c37a4654d50b07e629fc2adfba60f"
     }, {
       "name" : "(replica)192.168.2.51",
       "status" : "RUNNING",
       "dcs_instance_id" : "03ca9da0-1104-40a5-b49d-5ef8e41bfd19",
       "dcs_cluster_redis_node" : "da5149a20dc7caf35587e4d2433fe452"
     } ]
   }

Status Codes
------------

+-------------+----------------------------------------------------------------------+
| Status Code | Description                                                          |
+=============+======================================================================+
| 200         | Successfully queried the monitored objects on the primary dimension. |
+-------------+----------------------------------------------------------------------+
| 500         | Internal service error.                                              |
+-------------+----------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
