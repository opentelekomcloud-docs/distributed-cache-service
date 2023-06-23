:original_name: dcs-faq-0521006.html

.. _dcs-faq-0521006:

How Do I Analyze the Hot Keys of a DCS Redis 3.0 Instance?
==========================================================

DCS for Redis 3.0 does not support hot key analysis on the console. Alternatively, you can use the following methods to analyze hot keys:

-  Method 1: Analyze the service structure and service implementation to discover possible hot keys.

   For example, hot keys can be easily found in the service code during flash sales or user logins.

   Advantage: Simple and easy to implement.

   Disadvantage: Requires familiarity with the service code. In addition, the analysis become more difficult as the service scenarios become more complex.

-  Method 2: Collect key access statistics in the client code to discover hot keys.

   Disadvantage: Requires intrusive code modification.

-  Method 3: Capture and analyze packets.

   Advantage: Simple and easy to implement.
