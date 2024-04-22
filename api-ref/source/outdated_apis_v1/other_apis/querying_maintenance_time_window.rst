:original_name: dcs-api-0312041.html

.. _dcs-api-0312041:

Querying Maintenance Time Window
================================

Function
--------

The API is used to query the start time and end time of the maintenance time window.

URI
---

GET /v1.0/instances/maintain-windows

Request
-------

**Request parameters**

None

**Example request**

None

Response
--------

**Response parameters**

:ref:`Table 1 <dcs-api-0312041__en-us_topic_0166889588_table615617458391>` describes the response parameters.

.. _dcs-api-0312041__en-us_topic_0166889588_table615617458391:

.. table:: **Table 1** Parameter description

   ================ ===== ===========================================
   Parameter        Type  Description
   ================ ===== ===========================================
   maintain_windows Array List of supported maintenance time windows.
   ================ ===== ===========================================

.. table:: **Table 2** maintain_windows parameter description

   +-----------+---------+-----------------------------------------------------------------------------------------+
   | Parameter | Type    | Description                                                                             |
   +===========+=========+=========================================================================================+
   | seq       | Integer | Sequence number of the maintenance time window.                                         |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | begin     | String  | Start time of the maintenance time window.                                              |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | end       | String  | End time of the maintenance time window.                                                |
   +-----------+---------+-----------------------------------------------------------------------------------------+
   | default   | Boolean | An indicator of whether the maintenance time window is set to the default time segment. |
   +-----------+---------+-----------------------------------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "maintain_windows": [
           {
               "seq": 1,
               "begin": "22",
               "end": "02",
               "default": false
           },
           {
               "seq": 2,
               "begin": "02",
               "end": "06",
               "default": true
           },
           {
               "seq": 3,
               "begin": "06",
               "end": "10",
               "default": false
           },
           {
               "seq": 4,
               "begin": "10",
               "end": "14",
               "default": false
           },
           {
               "seq": 5,
               "begin": "14",
               "end": "18",
               "default": false
           },
           {
               "seq": 6,
               "begin": "18",
               "end": "22",
               "default": false
           }
       ]
   }

Status Code
-----------

:ref:`Table 3 <dcs-api-0312041__en-us_topic_0166889588_table611872191420>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312041__en-us_topic_0166889588_table611872191420:

.. table:: **Table 3** Status code

   =========== =================================================
   Status Code Description
   =========== =================================================
   200         Successfully queried the maintenance time window.
   =========== =================================================
