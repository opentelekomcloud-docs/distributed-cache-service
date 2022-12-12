:original_name: dcs-api-0312040.html

.. _dcs-api-0312040:

Querying Service Specifications
===============================

Function
--------

This API is used to query the product ID (parameter **product_id**) which indicates the specifications of the DCS service you created.

URI
---

GET /v1.0/products

Request
-------

**Request parameters**

None

**Example request**

None

Response
--------

**Response parameters**

:ref:`Table 1 <dcs-api-0312040__table18437193323916>` describes the response parameters.

.. _dcs-api-0312040__table18437193323916:

.. table:: **Table 1** Parameter description

   +-----------+-------+-----------------------------------------------------------------------+
   | Parameter | Type  | Description                                                           |
   +===========+=======+=======================================================================+
   | products  | Array | List of specifications of the DCS service to which you can subscribe. |
   +-----------+-------+-----------------------------------------------------------------------+

.. table:: **Table 2** products parameter description

   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter                | Type                  | Description                                                                                                                |
   +==========================+=======================+============================================================================================================================+
   | product_id               | String                | Product ID used to differentiate DCS specifications.                                                                       |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | spec_code                | String                | DCS instance specification code. Options:                                                                                  |
   |                          |                       |                                                                                                                            |
   |                          |                       | -  dcs.single_node                                                                                                         |
   |                          |                       | -  dcs.master_standby                                                                                                      |
   |                          |                       | -  dcs.cluster                                                                                                             |
   |                          |                       | -  redis.ha.xu1.tiny.r4.512                                                                                                |
   |                          |                       | -  redis.ha.xu1.tiny.r2.128                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r5.4                                                                                            |
   |                          |                       | -  redis.ha.xu1.tiny.r4.256                                                                                                |
   |                          |                       | -  redis.ha.xu1.tiny.r2.512                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r1.32                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.768                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r3.2                                                                                                 |
   |                          |                       | -  redis.single.xu1.large.64                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r5.8                                                                                            |
   |                          |                       | -  redis.ha.xu1.large.r3.32                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.8                                                                                            |
   |                          |                       | -  redis.ha.xu1.large.r4.1                                                                                                 |
   |                          |                       | -  redis.ha.xu1.tiny.r2.256                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r4.1024                                                                                         |
   |                          |                       | -  redis.ha.xu1.large.r5.16                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r4.32                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r5.24                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r4.64                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.1024                                                                                         |
   |                          |                       | -  redis.ha.xu1.large.r2.48                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r2.24                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r5.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.tiny.r5.512                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r3.8                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r1.768                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r3.24                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r3.512                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r3.1                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r4.4                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r1.24                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r4.2                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r5.192                                                                                          |
   |                          |                       | -  redis.single.xu1.large.16                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r3.1024                                                                                         |
   |                          |                       | -  redis.ha.xu1.large.r4.24                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.48                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r2.1                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.r3.48                                                                                                |
   |                          |                       | -  redis.single.xu1.large.4                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r4.48                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r3.768                                                                                          |
   |                          |                       | -  redis.ha.xu1.tiny.r4.128                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r5.1                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r2.96                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r3.4                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r1.128                                                                                          |
   |                          |                       | -  redis.single.xu1.large.2                                                                                                |
   |                          |                       | -  redis.ha.xu1.tiny.r3.128                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.512                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r3.8                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r4.128                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r3.96                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r4.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.r5.48                                                                                                |
   |                          |                       | -  redis.single.xu1.large.8                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.24                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r1.4                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r5.32                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r1.64                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.96                                                                                           |
   |                          |                       | -  redis.single.xu1.tiny.256                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r5.128                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r2.16                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.8                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r4.512                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r1.384                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r5.768                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r3.256                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r1.256                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r4.64                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r5.256                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r4.384                                                                                          |
   |                          |                       | -  redis.ha.xu1.tiny.r5.128                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r3.24                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.192                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r1.96                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r2.2                                                                                                 |
   |                          |                       | -  redis.single.xu1.large.24                                                                                               |
   |                          |                       | -  redis.ha.xu1.large.r4.4                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r1.1024                                                                                         |
   |                          |                       | -  redis.ha.xu1.large.r2.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r4.16                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r5.96                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r5.384                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r3.16                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r3.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.r4.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.tiny.r5.256                                                                                                |
   |                          |                       | -  redis.single.xu1.large.32                                                                                               |
   |                          |                       | -  redis.ha.xu1.large.r5.2                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r1.16                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r2.384                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r2.192                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r1.48                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r5.8                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r5.16                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r3.128                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r3.4                                                                                                 |
   |                          |                       | -  redis.cluster.xu1.large.r1.192                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r3.384                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r2.4                                                                                            |
   |                          |                       | -  redis.ha.xu1.large.r2.4                                                                                                 |
   |                          |                       | -  redis.single.xu1.tiny.128                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r1.512                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r2.64                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.128                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r2.768                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r5.64                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r3.48                                                                                           |
   |                          |                       | -  redis.single.xu1.tiny.512                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r5.48                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r4.48                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r4.24                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r5.4                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.r2.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.r3.64                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r2.64                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r2.32                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.16                                                                                           |
   |                          |                       | -  redis.cluster.xu1.large.r4.256                                                                                          |
   |                          |                       | -  redis.single.xu1.large.1                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r1.8                                                                                            |
   |                          |                       | -  redis.cluster.xu1.large.r3.32                                                                                           |
   |                          |                       | -  redis.single.xu1.large.48                                                                                               |
   |                          |                       | -  redis.cluster.xu1.large.r5.1024                                                                                         |
   |                          |                       | -  redis.cluster.xu1.large.r3.192                                                                                          |
   |                          |                       | -  redis.cluster.xu1.large.r2.256                                                                                          |
   |                          |                       | -  redis.ha.xu1.tiny.r3.256                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r5.24                                                                                           |
   |                          |                       | -  redis.ha.xu1.tiny.r3.512                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r5.512                                                                                          |
   |                          |                       | -  redis.ha.xu1.large.r5.32                                                                                                |
   |                          |                       | -  redis.cluster.xu1.large.r3.64                                                                                           |
   |                          |                       | -  redis.ha.xu1.large.r2.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p2.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p2.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p2.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p2.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.p3.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p3.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p3.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p3.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.p4.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p4.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p4.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p4.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.p5.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p5.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p5.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p5.8                                                                                                 |
   |                          |                       | -  redis.ha.xu1.large.p6.16                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p6.32                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p6.64                                                                                                |
   |                          |                       | -  redis.ha.xu1.large.p6.8                                                                                                 |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | cache_mode               | String                | DCS instance type. Options:                                                                                                |
   |                          |                       |                                                                                                                            |
   |                          |                       | -  **single**: single-node                                                                                                 |
   |                          |                       | -  **ha**: master/standby                                                                                                  |
   |                          |                       | -  **cluster**: Redis Cluster                                                                                              |
   |                          |                       | -  **proxy**: Proxy Cluster                                                                                                |
   |                          |                       | -  **ha_rw_split**: read/write splitting                                                                                   |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | product_type             | String                | Edition of DCS for Redis.                                                                                                  |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | cpu_type                 | String                | CPU architecture.                                                                                                          |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | storage_type             | String                | Storage type.                                                                                                              |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | details                  | Array of Object       | Details of the specifications. :ref:`Table 3 <dcs-api-0312040__table830249172716>` describes the parameters in this array. |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | engine                   | String                | Cache engine.                                                                                                              |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | engine_versions          | String                | Cache engine version.                                                                                                      |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | spec_details             | String                | DCS specifications. The value subjects to the returned specifications.                                                     |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | spec_details2            | String                | Detailed DCS specifications, including the maximum number of connections and maximum memory size.                          |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | charging_type            | String                | Billing mode. Value: **Hourly**.                                                                                           |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | price                    | Double                | Price of the DCS service to which you can subscribe. (This parameter has been abandoned.)                                  |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | currency                 | String                | Currency.                                                                                                                  |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | prod_type                | String                | Product type.                                                                                                              |
   |                          |                       |                                                                                                                            |
   |                          |                       | Options: **instance** and **obs_space**.                                                                                   |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | cloud_service_type_code  | String                | Cloud service type code.                                                                                                   |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | cloud_resource_type_code | String                | Cloud resource type code.                                                                                                  |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | flavors                  | Array                 | AZs with available resources. :ref:`Table 4 <dcs-api-0312040__table1979512328317>` describes the parameters in this array. |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+
   | billing_factor           | String                | Billing item.                                                                                                              |
   +--------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0312040__table830249172716:

.. table:: **Table 3** details parameter description

   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type   | Description                                                                                                                                                                    |
   +==================+========+================================================================================================================================================================================+
   | capacity         | String | Specification (total memory) of the DCS instance.                                                                                                                              |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_bandwidth    | String | Maximum bandwidth supported by the specification.                                                                                                                              |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_clients      | String | Maximum number of clients supported by the specification, which is usually equal to the maximum number of connections.                                                         |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_connections  | String | Maximum number of connections supported by the specification.                                                                                                                  |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_in_bandwidth | String | Maximum inbound bandwidth supported by the specification, which is usually equal to the maximum bandwidth.                                                                     |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_memory       | String | Maximum available memory.                                                                                                                                                      |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tenant_ip_count  | String | Number of tenant IP addresses corresponding to the specifications.                                                                                                             |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sharding_num     | String | Number of shards supported by the specifications.                                                                                                                              |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | proxy_num        | String | Number of proxies supported by Proxy Cluster instances of the specified specifications. If the instance is not a Proxy Cluster instance, the value of this parameter is **0**. |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_number        | String | Number of DBs of the specifications.                                                                                                                                           |
   +------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0312040__table1979512328317:

.. table:: **Table 4** flavors parameter description

   =============== ====== =================================================
   Parameter       Type   Description
   =============== ====== =================================================
   capacity        String Specification (total memory) of the DCS instance.
   unit            String Memory unit.
   available_zones Array  AZ ID.
   =============== ====== =================================================

**Example response**

.. code-block::

      {
           "product_id": "dcs.master_standby-h",
           "spec_code": "dcs.master_standby",
           "cache_mode": "ha",
           "product_type": "generic",
           "cpu_type": "x86_64",
           "storage_type": "DRAM",
           "details": {
               "capacity": 2,
               "max_memory": 1.5,
               "max_connections": 10000,
               "max_clients": 5000,
               "max_bandwidth": 512,
               "max_in_bandwidth": 42,
               "tenant_ip_count": 3,
               "sharding_num": 1,
               "proxy_num": 0,
               "db_number": 256
           },
           "engine": "redis",
           "engine_versions": "3.0",
           "spec_details": "[{\"mem\":\"2,4,8,16,32,64\"}]",
           "spec_details2": "[{\"capacity\":2,\"max_memory\":1.5,\"max_connections\":10000,\"max_clients\":5000,\"max_bandwidth\":512,\"max_in_bandwidth\":42,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256},{\"capacity\":4,\"max_memory\":3.2,\"max_connections\":10000,\"max_clients\":5000,\"max_bandwidth\":1536,\"max_in_bandwidth\":64,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256},{\"capacity\":8,\"max_memory\":6.4,\"max_connections\":10000,\"max_clients\":5000,\"max_bandwidth\":1536,\"max_in_bandwidth\":64,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256},{\"capacity\":16,\"max_memory\":12.8,\"max_connections\":10000,\"max_clients\":5000,\"max_bandwidth\":3072,\"max_in_bandwidth\":85,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256},{\"capacity\":32,\"max_memory\":25.6,\"max_connections\":10000,\"max_clients\":5000,\"max_bandwidth\":3072,\"max_in_bandwidth\":85,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256},{\"capacity\":64,\"max_memory\":51.2,\"max_connections\":12000,\"max_clients\":5000,\"max_bandwidth\":5120,\"max_in_bandwidth\":128,\"tenant_ip_count\":3,\"sharding_num\":1,\"proxy_num\":0,\"db_number\":256}]",
           "charging_type": "Hourly",
           "price": 0.0,
           "currency": "",
           "prod_type": "instance",
           "cloud_service_type_code": "XXXX",
           "cloud_resource_type_code": "XXXX",
           "flavors": [{
               "capacity": "2",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           },
           {
               "capacity": "4",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           },
           {
               "capacity": "8",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           },
           {
               "capacity": "16",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           },
           {
               "capacity": "32",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           },
           {
               "capacity": "64",
               "unit": "GB",
               "available_zones": ["882f6e449e3245dbb8c1c0fafa494c89",
               "ae04cf9d61544df3806a3feeb401b204",
               "d573142f24894ef3bd3664de068b44b0"]
           }],
           "billing_factor": "Duration"
       }

Status Code
-----------

:ref:`Table 5 <dcs-api-0312040__table11875348101316>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312040__table11875348101316:

.. table:: **Table 5** Status code

   =========== ============================================
   Status Code Description
   =========== ============================================
   200         Service specifications queried successfully.
   =========== ============================================
