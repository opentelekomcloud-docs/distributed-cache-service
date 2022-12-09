:original_name: dcs-faq-0730033.html

.. _dcs-faq-0730033:

Why Is Memory of a DCS Redis Instance Used Up by Just a Few Keys?
=================================================================

Possible cause: The output buffer may have occupied an excessive amount of memory.

Solution: After connecting to the instance using redis-cli, run the **redis-cli --bigkeys** command to scan for big keys. Then, run the **info** command to check the output buffer size.
