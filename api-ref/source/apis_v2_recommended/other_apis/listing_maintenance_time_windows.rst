:original_name: ListMaintenanceWindows.html

.. _ListMaintenanceWindows:

Listing Maintenance Time Windows
================================

Function
--------

This API is used to query the start time and end time of maintenance windows.

URI
---

GET /v2/instances/maintain-windows

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 1** Response body parameters

   +------------------+--------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Parameter        | Type                                                                                                   | Description                                 |
   +==================+========================================================================================================+=============================================+
   | maintain_windows | Array of :ref:`MaintainWindowsEntity <listmaintenancewindows__response_maintainwindowsentity>` objects | List of supported maintenance time windows. |
   +------------------+--------------------------------------------------------------------------------------------------------+---------------------------------------------+

.. _listmaintenancewindows__response_maintainwindowsentity:

.. table:: **Table 2** MaintainWindowsEntity

   +-----------+---------+---------------------------------------------------------------------------+
   | Parameter | Type    | Description                                                               |
   +===========+=========+===========================================================================+
   | seq       | Integer | Sequence number of the maintenance time window.                           |
   +-----------+---------+---------------------------------------------------------------------------+
   | default   | Boolean | Whether a maintenance time window is set to the default time segment.     |
   +-----------+---------+---------------------------------------------------------------------------+
   | begin     | String  | UTC time when the maintenance time window starts. The format is HH:mm:ss. |
   +-----------+---------+---------------------------------------------------------------------------+
   | end       | String  | UTC time when the maintenance time window ends. The format is HH:mm:ss.   |
   +-----------+---------+---------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 3** Response body parameters

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

   GET https://{dcs_endpoint}/v2/instances/maintain-windows

Example Responses
-----------------

**Status code: 200**

Maintenance time windows queried successfully.

.. code-block::

   {
     "maintain_windows" : [ {
       "default" : true,
       "end" : "19",
       "begin" : "18",
       "seq" : 1
     }, {
       "default" : false,
       "end" : "20",
       "begin" : "19",
       "seq" : 2
     }, {
       "default" : false,
       "end" : "21",
       "begin" : "20",
       "seq" : 3
     }, {
       "default" : false,
       "end" : "22",
       "begin" : "21",
       "seq" : 4
     }, {
       "default" : false,
       "end" : "23",
       "begin" : "22",
       "seq" : 5
     }, {
       "default" : false,
       "end" : "00",
       "begin" : "23",
       "seq" : 6
     }, {
       "default" : false,
       "end" : "01",
       "begin" : "00",
       "seq" : 1
     }, {
       "default" : false,
       "end" : "02",
       "begin" : "01",
       "seq" : 2
     }, {
       "default" : false,
       "end" : "03",
       "begin" : "02",
       "seq" : 3
     }, {
       "default" : false,
       "end" : "04",
       "begin" : "03",
       "seq" : 3
     }, {
       "default" : false,
       "end" : "05",
       "begin" : "04",
       "seq" : 4
     }, {
       "default" : false,
       "end" : "06",
       "begin" : "05",
       "seq" : 5
     }, {
       "default" : false,
       "end" : "07",
       "begin" : "06",
       "seq" : 6
     }, {
       "default" : false,
       "end" : "08",
       "begin" : "07",
       "seq" : 1
     }, {
       "default" : true,
       "end" : "09",
       "begin" : "08",
       "seq" : 2
     }, {
       "default" : false,
       "end" : "10",
       "begin" : "09",
       "seq" : 3
     }, {
       "default" : false,
       "end" : "11",
       "begin" : "10",
       "seq" : 4
     }, {
       "default" : false,
       "end" : "12",
       "begin" : "11",
       "seq" : 5
     }, {
       "default" : false,
       "end" : "13",
       "begin" : "12",
       "seq" : 6
     }, {
       "default" : false,
       "end" : "14",
       "begin" : "13",
       "seq" : 1
     }, {
       "default" : true,
       "end" : "15",
       "begin" : "14",
       "seq" : 2
     }, {
       "default" : false,
       "end" : "16",
       "begin" : "15",
       "seq" : 3
     }, {
       "default" : false,
       "end" : "17",
       "begin" : "16",
       "seq" : 4
     }, {
       "default" : false,
       "end" : "18",
       "begin" : "17",
       "seq" : 5
     } ]
   }

Status Codes
------------

=========== ==============================================
Status Code Description
=========== ==============================================
200         Maintenance time windows queried successfully.
500         Internal service error.
=========== ==============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
