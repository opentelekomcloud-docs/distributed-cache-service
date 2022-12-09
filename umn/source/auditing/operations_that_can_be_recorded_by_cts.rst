:original_name: dcs-ug-0326018.html

.. _dcs-ug-0326018:

Operations That Can Be Recorded by CTS
======================================

With CTS, you can query, audit, and review operations performed on cloud resources. Traces include the operation requests sent using the management console or open APIs as well as the results of these requests.

The following lists the DCS operations that can be recorded by CTS.

.. table:: **Table 1** DCS operations that can be recorded by CTS

   +--------------------------------------------------------+---------------+--------------------------------------+
   | Operation                                              | Resource Type | Trace Name                           |
   +========================================================+===============+======================================+
   | Creating an instance                                   | DCS           | createDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance creation request                | DCS           | submitCreateDCSInstanceRequest       |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting multiple instances                            | DCS           | batchDeleteDCSInstance               |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting an instance                                   | DCS           | deleteDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance information                         | DCS           | modifyDCSInstanceInfo                |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance configurations                      | DCS           | modifyDCSInstanceConfig              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Changing instance password                             | DCS           | modifyDCSInstancePassword            |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restarting an instance                                 | DCS           | restartDCSInstance                   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance restarting request              | DCS           | submitRestartDCSInstanceRequest      |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Starting an instance                                   | DCS           | startDCSInstance                     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance starting request                | DCS           | submitStartDCSInstanceRequest        |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Clearing instance data                                 | DCS           | flushDCSInstance                     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restarting instances in batches                        | DCS           | batchRestartDCSInstance              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to restart instances in batches   | DCS           | submitBatchRestartDCSInstanceRequest |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Starting multiple instances                            | DCS           | batchStartDCSInstance                |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to start instances in batches     | DCS           | submitBatchStartDCSInstanceRequest   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restoring instance data                                | DCS           | restoreDCSInstance                   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to restore instance data          | DCS           | submitRestoreDCSInstanceRequest      |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Backing up instance data                               | DCS           | backupDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to back up instance data          | DCS           | submitBackupDCSInstanceRequest       |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting instance backup files                         | DCS           | deleteInstanceBackupFile             |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting background tasks                              | DCS           | deleteDCSInstanceJobRecord           |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance specifications                      | DCS           | modifySpecification                  |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to modify instance specifications | DCS           | submitModifySpecificationRequest     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Creating an instance subscription order                | DCS           | createInstanceOrder                  |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Switching between master and standby nodes             | DCS           | masterStandbySwitchover              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Resetting instance password                            | DCS           | resetDCSInstancePassword             |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to clear instance data            | DCS           | submitFlushDCSInstanceRequest        |
   +--------------------------------------------------------+---------------+--------------------------------------+
