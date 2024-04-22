:original_name: ListBackupFileLinks.html

.. _ListBackupFileLinks:

Obtaining the Backup File URL
=============================

Function
--------

This API is used to obtain the download links of backup files.

URI
---

POST /v2/{project_id}/instances/{instance_id}/backups/{backup_id}/links

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | backup_id   | Yes       | String | Backup ID.                                                                    |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +------------+-----------+---------+---------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type    | Description                                                                           |
   +============+===========+=========+=======================================================================================+
   | expiration | Yes       | Integer | Validity period (in seconds) of a URL. The value range is from 5 minutes to 24 hours. |
   +------------+-----------+---------+---------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | Parameter   | Type                                                                        | Description                                                                         |
   +=============+=============================================================================+=====================================================================================+
   | file_path   | String                                                                      | Paths of files in the OBS bucket.                                                   |
   +-------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | bucket_name | String                                                                      | Name of the OBS bucket.                                                             |
   +-------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | links       | Array of :ref:`LinksItem <listbackupfilelinks__response_linksitem>` objects | Collection of URLs for downloading backup files. A maximum of 64 links are allowed. |
   +-------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+

.. _listbackupfilelinks__response_linksitem:

.. table:: **Table 4** LinksItem

   ========= ====== =================================
   Parameter Type   Description
   ========= ====== =================================
   file_name String Backup file name.
   link      String URL for downloading backup files.
   ========= ====== =================================

**Status code: 400**

.. table:: **Table 5** Response body parameters

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

Obtaining the download links of backup files with 1800s validity

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/backups/{backup_id}/links

   {
     "expiration" : 1800
   }

Example Responses
-----------------

**Status code: 200**

Successfully obtained backup file URLs.

.. code-block::

   {
     "file_path" : "42489641-23c4-4855-bc89-befc85e2b7f7/ddfe5f66-a965-43ff-aec7-f3b489dc071b/",
     "bucket_name" : "bucket5da9cf3bfabc4cae9023695b934e5e2b",
     "links" : [ {
       "file_name" : "redis_192.168.63.250_6379_10923-16383_20190820211816.rdb",
       "link" : "https://bucket5da9cf3bfabc4cae9023695b934e5e2b.{obs_endpoint}:443/42489641-23c4-4855-bc89-befc85e2b7f7/ddfe5f66-a965-43ff-aec7-f3b489dc071b/redis_192.168.63.250_6379_10923-16383_20190820211816.rdb?AWSAccessKeyId=VD8CEQNG8VMQODUAAM0D&Expires=1566308915&Signature=s3I%2BrLbo%2BFZw%2BUsjVere%2FOQdKEg%3D"
     } ]
   }

Status Codes
------------

=========== =======================================
Status Code Description
=========== =======================================
200         Successfully obtained backup file URLs.
400         Invalid request.
500         Internal service error.
=========== =======================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
