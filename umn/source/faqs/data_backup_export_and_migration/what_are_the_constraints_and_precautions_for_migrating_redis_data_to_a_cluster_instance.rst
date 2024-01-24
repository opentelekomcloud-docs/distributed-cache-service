:original_name: dcs-migration-0312019.html

.. _dcs-migration-0312019:

What Are the Constraints and Precautions for Migrating Redis Data to a Cluster Instance?
========================================================================================

-  Proxy Cluster instances

   Proxy Cluster instances are used in the same way that you use single-node or master/standby instances. However, only one DB is configured for a Proxy Cluster instance by default, and the **SELECT** command is not supported. When data files are imported in batches, an error message will be displayed and ignored if the **SELECT** command exists. Then, the remaining data will continue to be imported.

   Example:

   DB 0 and DB 2 in the source Redis instance contain data, and the generated AOF or RDB file contains these two DBs.

   When the source Redis data is imported into a Proxy Cluster DCS instance, the **SELECT 2** command will be ignored, and then data in DB 2 in the source Redis instance will be imported.

   Note that:

   -  If different DBs in the source Redis instance contain the same keys, values of keys in the DB with the largest ID will overwrite those in the other DBs.
   -  If the source Redis instance contains multiple DBs, data is stored in the same DB after being migrated to a cluster DCS instance, and the **SELECT** command is not supported. In this case, modify the configurations for your services.

-  Redis Cluster instances

   Only one DB is configured for a Redis Cluster instance. Data is migrated to a Redis Cluster instance in a different way from other types of instances. Nodes in the shards of a Redis Cluster must be connected separately through clients. Data is imported to the nodes separately. Run the following command to query the IP addresses of the cluster nodes:

   **redis-cli -h {Redis Cluster IP} -p 6379 -a {password} cluster nodes**

   In the returned list of IP addresses, record the ones marked by "master".
