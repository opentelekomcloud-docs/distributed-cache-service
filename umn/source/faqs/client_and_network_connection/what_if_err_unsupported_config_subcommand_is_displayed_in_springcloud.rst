:original_name: dcs-faq-0730009.html

.. _dcs-faq-0730009:

What If "ERR Unsupported CONFIG subcommand" is Displayed in SpringCloud?
========================================================================

By using DCS Redis instances, Spring Session can implement session sharing. When interconnecting with Spring Cloud, the following error information is displayed:


.. figure:: /_static/images/en-us_image_0266315619.png
   :alt: **Figure 1** Spring Cloud error information

   **Figure 1** Spring Cloud error information

For security purposes, DCS does not support the **CONFIG** command initiated by a client. You need to perform the following steps:

#. On the DCS console, set the value of the **notify-keyspace-event** parameter to **Egx** for a DCS Redis instance.

#. Add the following content to the XML configuration file of the Spring framework:

   <util:constant

   static-field="org.springframework.session.data.redis.config.ConfigureRedisAction.NO_OP"/>

#. Modify the related Spring code. Enable the **ConfigureRedisAction.NO_OP** bean component to forbid a client to invoke the **CONFIG** command.

   @Bean

   public static ConfigureRedisAction configureRedisAction() {

   return ConfigureRedisAction.NO_OP;

   }

For more information, see the `Spring Session Documentation <https://docs.spring.io/spring-session/docs/current/api/>`__.

.. important::

   Session sharing is supported only by **single-node** and **master/standby** DCS Redis instances, but not by cluster DCS Redis instances.
