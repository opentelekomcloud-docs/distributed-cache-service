:original_name: dcs-api-0312036.html

.. _dcs-api-0312036:

Querying the Quota of a Tenant
==============================

Function
--------

This API is used to query the default instance quota and total memory quota of a tenant and the maximum and minimum quotas a tenant can apply for. Different tenants have different quotas in different regions.

URI
---

GET /v1.0/{project_id}/quota

:ref:`Table 1 <dcs-api-0312036__table13653920143919>` describes the parameter.

.. _dcs-api-0312036__table13653920143919:

.. table:: **Table 1** Parameter description

   ========== ====== ========= ===========
   Parameter  Type   Mandatory Description
   ========== ====== ========= ===========
   project_id String Yes       Project ID.
   ========== ====== ========= ===========

Request
-------

**Request parameters**

None

**Example request**

None

Response
--------

**Response parameters**

:ref:`Table 2 <dcs-api-0312036__table114165246391>` describes the response parameters.

.. _dcs-api-0312036__table114165246391:

.. table:: **Table 2** Parameter description

   +-----------+--------+-----------+-------------------------------------------------------------------------------------------+
   | Parameter | Type   | Mandatory | Description                                                                               |
   +===========+========+===========+===========================================================================================+
   | quotas    | Object | Yes       | Quota information. For details, see :ref:`Table 3 <dcs-api-0312036__table1341618240392>`. |
   +-----------+--------+-----------+-------------------------------------------------------------------------------------------+

.. _dcs-api-0312036__table1341618240392:

.. table:: **Table 3** quotas parameter description

   +---------------+--------+-----------+------------------------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Mandatory | Description                                                                                                |
   +===============+========+===========+============================================================================================================+
   | resources     | Array  | Yes       | List of quotas. For details, see :ref:`Table 4 <dcs-api-0312036__table164180248392>`.                      |
   +---------------+--------+-----------+------------------------------------------------------------------------------------------------------------+
   | resource_user | Object | Yes       | Information about a resource tenant For details, see :ref:`Table 5 <dcs-api-0312036__table1641811248397>`. |
   +---------------+--------+-----------+------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0312036__table164180248392:

.. table:: **Table 4** resources parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                            |
   +=======================+=======================+========================================================================================+
   | quota                 | Integer               | Maximum number of instances that can be created and maximum allowed total memory.      |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | used                  | Integer               | Number of created instances and used memory.                                           |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | type                  | String                | Values:                                                                                |
   |                       |                       |                                                                                        |
   |                       |                       | -  **instances**: indicates the instance quota.                                        |
   |                       |                       | -  **ram**: indicates the memory quota.                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | unit                  | String                | Resource unit.                                                                         |
   |                       |                       |                                                                                        |
   |                       |                       | -  When **type** is set to **instance**, no value is returned.                         |
   |                       |                       | -  When **type** is set to **ram**, **GB** is returned.                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | max                   | Integer               | -  Indicates the maximum limit of instance quota when **type** is set to **instance**. |
   |                       |                       | -  Indicates the maximum limit of memory quota when **type** is set to **ram**.        |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | min                   | Integer               | -  Indicates the minimum limit of instance quota when **type** is set to **instance**. |
   |                       |                       | -  Indicates the minimum limit of memory quota when **type** is set to **ram**.        |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+

.. _dcs-api-0312036__table1641811248397:

.. table:: **Table 5** resource_user parameter description

   =========== ====== ====================
   Parameter   Type   Description
   =========== ====== ====================
   tenant_id   String Resource tenant ID
   tenant_name String Resource tenant name
   =========== ====== ====================

**Example response**

.. code-block::

   {
       "quotas": {
           "resources": [
               {
                   "quota": 10,
                   "used": 3,
                   "type": "instance",
                   "min": 1,
                   "max": 10,
                   "unit": null
               },
               {
                   "quota": 800,
                   "used": 22,
                   "type": "ram",
                   "min": 1,
                   "max": 800,
                   "unit": "GB"
               }
           ],
           "resource_user": {
               "tenant_id": "836152f9838a44089f40f3cf6fd432bf",
               "tenant_name": "op_svc_dcs_003"
           }
       }
   }

Status Code
-----------

:ref:`Table 6 <dcs-api-0312036__table597043515135>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312036__table597043515135:

.. table:: **Table 6** Status code

   =========== ==================================
   Status Code Description
   =========== ==================================
   200         Tenant quota queried successfully.
   =========== ==================================
