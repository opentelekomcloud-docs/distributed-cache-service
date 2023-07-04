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
   | Creating an instance                                   | Redis         | createDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance creation request                | Redis         | submitCreateDCSInstanceRequest       |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting multiple instances                            | Redis         | batchDeleteDCSInstance               |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting an instance                                   | Redis         | deleteDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance information                         | Redis         | modifyDCSInstanceInfo                |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance configurations                      | Redis         | modifyDCSInstanceConfig              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Changing instance password                             | Redis         | modifyDCSInstancePassword            |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restarting an instance                                 | Redis         | restartDCSInstance                   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance restarting request              | Redis         | submitRestartDCSInstanceRequest      |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Starting an instance                                   | Redis         | startDCSInstance                     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting an instance starting request                | Redis         | submitStartDCSInstanceRequest        |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Clearing instance data                                 | Redis         | flushDCSInstance                     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restarting instances in batches                        | Redis         | batchRestartDCSInstance              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to restart instances in batches   | Redis         | submitBatchRestartDCSInstanceRequest |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Starting multiple instances                            | Redis         | batchStartDCSInstance                |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to start instances in batches     | Redis         | submitBatchStartDCSInstanceRequest   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Restoring instance data                                | Redis         | restoreDCSInstance                   |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to restore instance data          | Redis         | submitRestoreDCSInstanceRequest      |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Backing up instance data                               | Redis         | backupDCSInstance                    |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to back up instance data          | Redis         | submitBackupDCSInstanceRequest       |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting instance backup files                         | Redis         | deleteInstanceBackupFile             |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Deleting background tasks                              | Redis         | deleteDCSInstanceJobRecord           |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Modifying instance specifications                      | Redis         | modifySpecification                  |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to modify instance specifications | Redis         | submitModifySpecificationRequest     |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Creating an instance subscription order                | Redis         | createInstanceOrder                  |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Switching between master and standby nodes             | Redis         | masterStandbySwitchover              |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Resetting instance password                            | Redis         | resetDCSInstancePassword             |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Submitting a request to clear instance data            | Redis         | submitFlushDCSInstanceRequest        |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Accessing Web CLI                                      | Redis         | webCliLogin                          |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Running commands in Web CLI                            | Redis         | webCliCommand                        |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Exiting Web CLI                                        | Redis         | webCliLogout                         |
   +--------------------------------------------------------+---------------+--------------------------------------+
   | Migrating offline data                                 | Redis         | offlineMigrate                       |
   +--------------------------------------------------------+---------------+--------------------------------------+
