# FIRMWARE REFERENCE

Use the information in this section if you have an MCU in your device that must communicate with ASR. Almost all of the ASR API is common across all supported platforms, but there are a few platform-specific differences in creating the ASR and `af_logger` interfaces. Examples in this documentation will use Arduino APIs but we’ll note where there are differences in other platforms. You can download this library from http://github.com/aferodeveloper/afLib.

- [MCU to ASR Communication](https://developer.afero.io/MCUtoHachi)
- [Device Attribute Message Protocol](https://developer.afero.io/AttrMsgProtocol)
- [Device Attribute Registry](https://developer.afero.io/AttrRegistry)
- [Attribute Value Change Rules](https://developer.afero.io/AttrChangeRules)
- afLib API
  - [afLib Lifecycle](https://developer.afero.io/afLibLifecycle)
  - [Getting/Setting Attributes](https://developer.afero.io/afLibAttributes)
  - [Callbacks and Events](https://developer.afero.io/afLibCallbacks)
  - [The Main Loop](https://developer.afero.io/afLibLoop)
  - [Checking Capabilities](https://developer.afero.io/afLibCapabilities)
- [Attribute Update Reasons and States](https://developer.afero.io/PeripheralUpdates)