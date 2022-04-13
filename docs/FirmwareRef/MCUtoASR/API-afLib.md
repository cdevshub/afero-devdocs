# afLib API

afLib is an MCU library designed to communicate with an Afero Secure Radio module over serial interfaces such as SPI and UART. The library is written in C and provides a simple, lightweight API that provides all the functionality you should need to implement your application. The library is provided for several popular MCU platforms, including Arduino, and is easily ported to your preferred MCU platform, as needed.

The latest library version is **afLib4**; download it from http://github.com/aferodeveloper/afLib.

The library includes the following functions:

- [`arduino_transport_create_<*protocol*>()`](https://developer.afero.io/afLibLifecycle#Func-transport-create) (supported protocols: SPI and UART)
- [`af_lib_create_with_unified_callback()`](https://developer.afero.io/afLibLifecycle#Func-afLib-unified)
- [`af_lib_destroy()`](https://developer.afero.io/afLibLifecycle#Func-af_destroy)
- [`af_lib_loop()`](https://developer.afero.io/afLibLoop#Func-af_loop)
- [`af_lib_is_idle()`](https://developer.afero.io/afLibLoop#Func-af_is_idle)
- [`af_lib_sync()`](https://developer.afero.io/afLibLoop#Func-af_sync)
- [`af_lib_get_attribute()`](https://developer.afero.io/afLibAttributes#Func-getAttribute)
- [`af_lib_set_attribute()`](https://developer.afero.io/afLibAttributes#Func-setAttribute)
- [`af_lib_send_set_response()`](https://developer.afero.io/afLibCallbacks#Func-sendSetResponse)
- [`af_lib_asr_has_capability()`](https://developer.afero.io/afLibCapabilities#Func-af_has_capability)
- [`af_logger()`](https://developer.afero.io/afLibLogging)

We also describe the callback function you should write to work with afLib:

- [`attrEventCallback()`](https://developer.afero.io/afLibCallbacks#Func-attrEventCallback)

If you need to refer to the API documentation for afLib3, [download the archive file (.zip).](https://developer.afero.io/static/custom/files/afLib3-DevDocs.zip)