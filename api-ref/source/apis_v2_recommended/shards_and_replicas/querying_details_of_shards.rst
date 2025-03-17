:original_name: ListGroupReplicationInfo.html

.. _ListGroupReplicationInfo:

Querying Details of Shards
==========================

Function
--------

This API is used to query information about shards and replicas of Redis 4.0 and later instances (single-node ones not included).

URI
---

GET /v2/{project_id}/instance/{instance_id}/groups

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

   +-------------+----------------------------------------------------------------------------------------------------------+-----------------------------------------+
   | Parameter   | Type                                                                                                     | Description                             |
   +=============+==========================================================================================================+=========================================+
   | group_list  | Array of :ref:`InstanceGroupListInfo <listgroupreplicationinfo__response_instancegrouplistinfo>` objects | List of shards.                         |
   +-------------+----------------------------------------------------------------------------------------------------------+-----------------------------------------+
   | group_count | Integer                                                                                                  | Total number of shards in the instance. |
   +-------------+----------------------------------------------------------------------------------------------------------+-----------------------------------------+

.. _listgroupreplicationinfo__response_instancegrouplistinfo:

.. table:: **Table 3** InstanceGroupListInfo

   +------------------+----------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Parameter        | Type                                                                                                                 | Description                    |
   +==================+======================================================================================================================+================================+
   | group_id         | String                                                                                                               | Shard ID.                      |
   +------------------+----------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | group_name       | String                                                                                                               | Shard name.                    |
   +------------------+----------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | replication_list | Array of :ref:`InstanceReplicationListInfo <listgroupreplicationinfo__response_instancereplicationlistinfo>` objects | List of replicas in the shard. |
   +------------------+----------------------------------------------------------------------------------------------------------------------+--------------------------------+

.. _listgroupreplicationinfo__response_instancereplicationlistinfo:

.. table:: **Table 4** InstanceReplicationListInfo

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                                             | Description                                                                                                                                                                                                                   |
   +=======================+==================================================================================================================================+===============================================================================================================================================================================================================================+
   | replication_role      | String                                                                                                                           | Role of the replica. Options:                                                                                                                                                                                                 |
   |                       |                                                                                                                                  |                                                                                                                                                                                                                               |
   |                       |                                                                                                                                  | -  **master**: master                                                                                                                                                                                                         |
   |                       |                                                                                                                                  |                                                                                                                                                                                                                               |
   |                       |                                                                                                                                  | -  **slave**: replica                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication_ip        | String                                                                                                                           | Replica IP address.                                                                                                                                                                                                           |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_replication        | Boolean                                                                                                                          | Whether the replica is a newly added one.                                                                                                                                                                                     |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication_id        | String                                                                                                                           | Replica ID.                                                                                                                                                                                                                   |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_id               | String                                                                                                                           | Node ID.                                                                                                                                                                                                                      |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                                                                                                                           | Replica status.                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | az_code               | String                                                                                                                           | AZ where the replica is in.                                                                                                                                                                                                   |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dimensions            | Array of :ref:`InstanceReplicationDimensionsInfo <listgroupreplicationinfo__response_instancereplicationdimensionsinfo>` objects | Monitoring metric dimension of the replica used to call the Cloud Eye API for querying monitoring metrics.                                                                                                                    |
   |                       |                                                                                                                                  |                                                                                                                                                                                                                               |
   |                       |                                                                                                                                  | -  Replica monitoring is multi-dimensional. The returned array contains information about two dimensions. When querying monitoring data from Cloud Eye, transfer parameters of multiple dimensions to obtain the metric data. |
   |                       |                                                                                                                                  |                                                                                                                                                                                                                               |
   |                       |                                                                                                                                  | -  The first dimension is the primary dimension of the replica. The dimension name is **dcs_instance_id**, and the dimension value corresponds to the ID of the instance to which the replica belongs.                        |
   |                       |                                                                                                                                  |                                                                                                                                                                                                                               |
   |                       |                                                                                                                                  | -  The name of the second dimension is **dcs_cluster_redis_node**, and the dimension value is the ID of the monitored object of the replica, which is different from the replica ID or node ID.                               |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _listgroupreplicationinfo__response_instancereplicationdimensionsinfo:

.. table:: **Table 5** InstanceReplicationDimensionsInfo

   ========= ====== ==========================
   Parameter Type   Description
   ========= ====== ==========================
   name      String Monitoring dimension name.
   value     String Dimension value.
   ========= ====== ==========================

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

**Status code: 400**

.. table:: **Table 7** Response body parameters

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

   GET https://{dcs_endpoint}/v2/{project_id}/instance/{instance_id}/groups

Example Responses
-----------------

**Status code: 200**

Details of shards and replicas queried successfully.

.. code-block::

   {
     "group_list" : [ {
       "group_id" : "35e1bed6-7de5-4898-9eb2-c362c783df15",
       "group_name" : "group-0",
       "replication_list" : [ {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cda0002d",
         "replication_id" : "dfbd3f84-08bc-42f0-b538-01d03e6dc178",
         "replication_ip" : "192.168.76.25",
         "replication_role" : "master",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6200"
         } ]
       }, {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cdb0002e",
         "replication_id" : "63d4c880-7050-464f-ab19-c8a297474d7d",
         "replication_ip" : "192.168.78.207",
         "replication_role" : "slave",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6201"
         } ]
       } ]
     }, {
       "group_id" : "579a281f-6e63-4822-b0c7-e45c44b7c807",
       "group_name" : "group-1",
       "replication_list" : [ {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cdbd002f",
         "replication_id" : "6284c192-48d1-462b-8fd9-45dad067c1a2",
         "replication_ip" : "192.168.73.164",
         "replication_role" : "master",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6202"
         } ]
       }, {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cdc80030",
         "replication_id" : "b927de3b-42f3-45b5-b0e4-8547f0ef6727",
         "replication_ip" : "192.168.77.172",
         "replication_role" : "slave",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6203"
         } ]
       } ]
     }, {
       "group_id" : "c17305c6-6651-42d9-86bf-5a6087076eb7",
       "group_name" : "group-2",
       "replication_list" : [ {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cdd90031",
         "replication_id" : "caa6636d-a5c1-43b8-990a-3dc134da4522",
         "replication_ip" : "192.168.76.143",
         "replication_role" : "master",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6204"
         } ]
       }, {
         "az_code" : "region01",
         "is_replication" : false,
         "node_id" : "8abfa7aa73291f15017329e1cde50032",
         "replication_id" : "4f46790d-a0b0-4a1b-aa02-1c554fccf62d",
         "replication_ip" : "192.168.72.66",
         "replication_role" : "slave",
         "status" : "Active",
         "dimensions" : [ {
           "name" : "dcs_instance_id",
           "value" : "caf2d19f-7783-44b0-be46-8c9da3ef1e94"
         }, {
           "name" : "dcs_cluster_redis_node",
           "value" : "8263dc69629c5b2d840e9816fa9c6205"
         } ]
       } ]
     } ],
     "group_count" : 3
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         Details of shards and replicas queried successfully.
500         Internal service error.
400         Invalid request.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
