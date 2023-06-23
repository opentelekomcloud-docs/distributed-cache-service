:original_name: dcs-faq-0730023.html

.. _dcs-faq-0730023:

What Should I Do If an Error Occurs in Redis Exporter?
======================================================

Start the Redis exporter using the CLI. Based on the output, check for errors and troubleshoot accordingly.

.. code-block:: console

   [root@ecs-swk /]./redis_exporter -redis.addr 192.168.0.23:6379
   INFO[0000] Redis Metrics Exporter V0.15.0   build date:2018-01-19-04:08:01 sha1: a0d9ec4704b4d35cd08544d395038f417716a03a
     Go:go1.9.2
   INFO[0000] Providing metrics at :9121/metrics
   INFO[0000] Connecting to redis hosts: []string{192.168.0.23:6379}
   INFO[0000] Using alias:[]string{""}
