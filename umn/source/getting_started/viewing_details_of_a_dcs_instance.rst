:original_name: dcs-ug-0312016.html

.. _dcs-ug-0312016:

Viewing Details of a DCS Instance
=================================

On the DCS console, you can view DCS instance details.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Search for DCS instances using any of the following methods:

   -  Search by keyword.

      Enter a keyword to search.

   -  Select attributes and enter their keywords to search.

      Currently, you can search by name, ID, connection address (IP address:port number), AZ, status, instance type, and cache engine.

   For more information on how to search, click the question mark to the right of the search box.

#. On the DCS instance list, click the name of a DCS instance to display more details about it. :ref:`Table 1 <dcs-ug-0312016__table63471440101219>` describes the parameters.

   .. _dcs-ug-0312016__table63471440101219:

   .. table:: **Table 1** Parameters on the Basic Information page of a DCS instance

      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Section               | Parameter                  | Description                                                                                                                                            |
      +=======================+============================+========================================================================================================================================================+
      | Instance Details      | Name                       | Name of the chosen instance. To modify the instance name, click the |image2| icon.                                                                     |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Status                     | State of the chosen instance.                                                                                                                          |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | ID                         | ID of the chosen instance.                                                                                                                             |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Cache Engine               | Cache engine and cache engine version used by the DCS instance. For example, Redis 3.0.                                                                |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Instance Type              | Type of the selected instance. Currently, supported types include single-node, master/standby, Proxy Cluster, and Redis Cluster.                       |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Cache Size                 | Specification of the chosen instance.                                                                                                                  |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Used/Available Memory (MB) | The used memory space and maximum available memory space of the chosen instance.                                                                       |
      |                       |                            |                                                                                                                                                        |
      |                       |                            | The used memory space includes:                                                                                                                        |
      |                       |                            |                                                                                                                                                        |
      |                       |                            | -  Size of data stored on the DCS instance                                                                                                             |
      |                       |                            | -  Size of Redis-server buffers (including client buffer and repl-backlog) and internal data structures                                                |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | CPU                        | CPU of the DCS instance.                                                                                                                               |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Created                    | Time at which the chosen instance started to be created.                                                                                               |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Run                        | Time at which the instance was created.                                                                                                                |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Maintenance                | Time range for any scheduled maintenance activities on cache nodes of this DCS instance. To modify the time window, click the |image3| icon.           |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Description                | Description of the chosen DCS instance. To modify the description, click the |image4| icon.                                                            |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Connection            | Password Protected         | Currently, password-protected access and password-free access are supported.                                                                           |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | IP Address                 | IP address and port number of the chosen instance.                                                                                                     |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network               | AZ                         | Availability zone in which the cache node running the selected DCS instance resides.                                                                   |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | VPC                        | VPC in which the chosen instance resides.                                                                                                              |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Subnet                     | Subnet in which the chosen instance resides.                                                                                                           |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Security Group             | Security group that controls access to the chosen instance. To modify the security group, click the |image5| icon.                                     |
      |                       |                            |                                                                                                                                                        |
      |                       |                            | This parameter is displayed only for DCS Redis 3.0 instances. DCS for Redis 4.0 and 5.0 are based on VPC endpoints and do not support security groups. |
      +-----------------------+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001194522893.png
.. |image2| image:: /_static/images/en-us_image_0266235362.png
.. |image3| image:: /_static/images/en-us_image_0266235362.png
.. |image4| image:: /_static/images/en-us_image_0266235362.png
.. |image5| image:: /_static/images/en-us_image_0266235362.png
