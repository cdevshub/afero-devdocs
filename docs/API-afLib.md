# afLib API

afLib is an MCU library designed to communicate with an Afero Secure Radio module over serial interfaces such as SPI and UART. The library is written in C and provides a simple, lightweight API that provides all the functionality you should need to implement your application. The library is provided for several popular MCU platforms, including Arduino, and is easily ported to your preferred MCU platform, as needed.

The latest library version is **afLib4**; download it from http://github.com/aferodeveloper/afLib.

The library includes the following functions:

- [`arduino_transport_create_<*protocol*>()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLifecycle/#arduino_transport_create_protocol) (supported protocols: SPI and UART)
- [`af_lib_create_with_unified_callback()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLifecycle/#af_lib_create_with_unified_callback)
- [`af_lib_destroy()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLifecycle/#af_lib_destroy)
- [`af_lib_loop()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLoop/#af_lib_loop)
- [`af_lib_is_idle()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLoop/#af_lib_is_idle)
- [`af_lib_sync()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLoop/#af_lib_sync)
- [`af_lib_get_attribute()`](https://afero-devdocs.readthedocs.io/en/latest/afLibAttributes/#af_lib_get_attribute)
- [`af_lib_set_attribute()`](https://afero-devdocs.readthedocs.io/en/latest/afLibAttributes/#af_lib_set_attribute)
- [`af_lib_send_set_response()`](https://afero-devdocs.readthedocs.io/en/latest/afLibCallbacks/#af_lib_send_set_response)
- [`af_lib_asr_has_capability()`](https://afero-devdocs.readthedocs.io/en/latest/afLibCapabilities/#af_lib_asr_has_capability)
- [`af_logger()`](https://afero-devdocs.readthedocs.io/en/latest/afLibLogging)

We also describe the callback function you should write to work with afLib:

- [`attrEventCallback()`](https://afero-devdocs.readthedocs.io/en/latest/afLibCallbacks/#attreventcallback)

If you need to refer to the API documentation for afLib3, [download the archive file (.zip).](https://afero-devdocs.readthedocs.io/en/latest/files/afLib3-DevDocs.zip)