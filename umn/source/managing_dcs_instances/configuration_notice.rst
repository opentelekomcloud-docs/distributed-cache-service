:original_name: dcs-ug-0312023.html

.. _dcs-ug-0312023:

Configuration Notice
====================

-  In most cases, different DCS instance management operations cannot proceed concurrently. If you initiate a new management operation while the current operation is in progress, the DCS console prompts you to initiate the new operation again after the current operation is complete. DCS instance management operations include:

   -  Creating a DCS instance
   -  Configuring parameters
   -  Restarting a DCS instance
   -  Changing the instance password
   -  Resetting the instance password
   -  Scaling, backing up, or restoring an instance

-  You can restart a DCS instance while it is being backed up, but the backup task will be forcibly interrupted and is likely to result in a backup failure.

.. important::

   In the event that a cache node of a DCS instance is faulty:

   -  The instance remains in the **Running** state and you can continue to read from and write to the instance. This is achieved thanks to the high availability of DCS.
   -  Cache nodes can recover from internal faults automatically. Manual fault recovery is also supported.
   -  Certain operations (such as parameter configuration, password change or resetting, backup, restoration, and specification modification) in the management zone are not supported during fault recovery. You can contact technical support or perform these operations after the cache nodes recover from faults.
