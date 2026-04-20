:original_name: dcs_03_0016.html

.. _dcs_03_0016:

Upgrading the Minor or Proxy Version of a DCS Instance
======================================================

DCS optimizes functions and fixes vulnerabilities in minor and proxy upgrades. This section describes how to upgrade the minor or proxy version of an instance.

Upgrading the minor or proxy version does not affect the instance connection addresses, password, whitelist, or monitoring and alarms.

Notes and Constraints
---------------------

-  Available for DCS Redis 4.0 and later instances.
-  Only Proxy Cluster and read/write splitting instances involve proxy versions.
-  An instance can be upgraded to the latest minor or proxy version which cannot be specified.
-  To upgrade the minor version of a Redis Cluster instance, ensure that the client can properly process the **MOVED** and **ASK** commands. Otherwise, requests will fail.
-  Rollback is unavailable.

Impacts
-------

-  Perform instance upgrades during off-peak hours. Otherwise, upgrades may fail when the instance memory or CPU usage exceeds 90% or write traffic bursts. In such cases, try again during off-peak hours.
-  The instance's minor version is upgraded by migrating nodes. During the migration, latency will increase. A migrating shard will become read-only for 1 minute and intermittently disconnected. Ensure that the client can reconnect and handle exceptions.
-  The upgrading instance will be intermittently disconnected. Ensure that the client can reconnect and handle exceptions. Perform the upgrade during off-peak hours.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click a DCS instance.

#. On the **Basic Information** page, you can view or upgrade the minor or proxy versions of the instance.


   .. figure:: /_static/images/en-us_image_0000002477620454.png
      :alt: **Figure 1** Upgrading an instance's minor or proxy version

      **Figure 1** Upgrading an instance's minor or proxy version

   When the upgrade button is gray and cannot be clicked, the instance's minor or proxy version is already the latest.

   -  Upgrading a minor version

      a. Click **Upgrade** next to **Minor Version**.

         Also, to upgrade the proxy version, enable **Upgrade Proxy Version** in the displayed window.

      b. Click **OK**. The upgrade is complete when the upgrade task is in the **Successful** state.

   -  Upgrading a proxy version

      a. Click **Upgrade** next to **Proxy Version**.

         Also, to upgrade the minor version, enable **Upgrade Minor Version** in the displayed window.

      b. Click **OK**. The upgrade is complete when the upgrade task is in the **Successful** state.

.. |image1| image:: /_static/images/en-us_image_0000002248341190.png
