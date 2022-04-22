# Define the Device Attributes

Now is the time to describe your device in terms of attributes and values. The Attribute Definition window is where you will do this. Instructions on using this window are presented in the following sections:

- [What Is an Attribute?](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#WhatAttr)
- [Does Your Device Include a Microcontroller (MCU)?](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#UseMCU)
- [Define the GPIO Attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#GPIOAttrs)
- [Define the MCU Attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#MCUAttrs)

Before we start editing, take a minute to think about how your device’s functions map to attributes and values.

## What Is an Attribute?

Think of an attribute as a variable shared between your IoT device and the end-user’s Afero mobile app. Your device sets that variable/attribute in ASR to a value reflecting device state. That value is communicated to the Afero Cloud (for ASR-1 via either a standalone hub or “softhub” built into the Afero mobile app), and from there to the end-user’s mobile app. This causes the app UI to update, reflecting the current value of the attribute. Conversely, the end-user can manipulate the mobile app UI to cause a change in the value of an attribute: the new value is communicated to ASR in your device via the Afero Cloud then hub, and a device action is triggered by that attribute value.

### Examples

A simple control used by many devices is **Power**. The values, or possible settings, are **On** and **Off**. When the device is turned Off, that state is reflected in a dedicated Power attribute. The attribute Off value is sent to the Afero Cloud via a hub, and from there to the Afero mobile app on the end-user’s smartphone. The device representation on the mobile app would most likely include a Power switch control, which would then be switched to Off. If the end-user then set the switch to On, the updated attribute value would be sent back the other way: app → Afero Cloud → hub (for ASR-1) → ASR, and the device would be turned on.

Not all attributes are Boolean; a more sophisticated device might use an attribute to represent Cleaning Mode; the settings (values) could be Spot Clean, Scheduled Clean, and Full Clean. For more about attribute modeling, read [Great Attribute Modeling](https://afero-devdocs.readthedocs.io/en/latest/AttrModel).

### Attribute Sizing

Your module has a defined amount of memory reserved for both system and developer-defined attributes – your Profile cannot exceed this limit. Each module has a different amount of RAM reserved, so as you add attributes to your Profile, select the PROFILE RAM USAGE indicator at the top of the Attributes window to see remaining space:
![Attribute RAM Gauge](img/Attribute-RAM-Gauge.png)

The GREY BAR indicates space used by system attributes. The BLUE BAR indicates space used by developer-defined attributes. Hover over the indicator bar to view actual remaining space, in bytes and percentage. For more details, read [Device Attribute RAM Size](https://afero-devdocs.readthedocs.io/en/latest/AttributeRAM).

### More Attribute Facts

- Attribute history is stored in the Afero Cloud (30 days by default).
- Attribute changes can be tracked and graphed across one-to-n devices.
- Afero Inspector and Afero Console are developer tools available for viewing attribute changes and running analytics.
- Attributes are accessible via a REST API.
- Afero can pull data from your cloud to push to device attributes.
- Afero can push attribute data back to your cloud.

## Does Your Device Include a Microcontroller (MCU)?

There are two types of devices that could use ASR:

- **Devices without an MCU** - A relatively simple device may not have a microcontroller, but still have sensors or controls. For this type of application, ASR exposes four GPIO pins that can be connected to a device that does not need to perform any processing beyond communicating attribute state with Afero. These four attributes are referred to as GPIO ATTRIBUTES.

  GPIO attributes are, of course, tied directly to GPIO pin state, and therefore are defined by characteristics you would expect from pin interfaces: they can be Input or Output, you can activate internal pull-up or pull-down resistors, etc.

- **Devices with an MCU** - A more complicated device might include an MCU, and so might perform logic involving attribute values communicated with Afero. For this purpose, ASR allows you to define 1024 attributes that are not directly tied to the state of a pin on ASR. These are referred to as MCU ATTRIBUTES.

  MCU attributes can be Read-Only or Read/Write, and you can specify the data type for each. (Read [Define MCU Attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#MCUAttrs) for details on data types.)

  Two MCU serial protocols are supported:

  - Serial Peripheral Interface bus (SPI)
  - Universal Asynchronous Receiver/Transmitter (UART)

To learn how to set up communication between ASR and your MCU, please start by reading [MCU to ASR Communication.](https://afero-devdocs.readthedocs.io/en/latest/MCUtoHachi)

You can update the firmware on your MCU by using the Afero OTA Manager in conjunction with the Profile Editor. Read more about this below in [Configure the MCU (Step 4)](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#ConfigMCU) and in the [Afero OTA Manager User Guide](https://afero-devdocs.readthedocs.io/en/latest/OTAMgr).

## Define the GPIO Attributes

We’ll start by defining the GPIO attributes. Note that not all modules have GPIO pins.

1. Click ATTRIBUTES in the Navigation pane to open the Attribute Definition window. (We’ll talk about the MCU PROTOCOL drop-down menu when we [define MCU attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#MCUAttrs), later.) By default the GPIO attributes appear, ready to be defined:

   ![Attribute Definition Window](img/AttributeDefinition.png)

2. Click an attribute’s ON/OFF toggle switch to turn it ON and open the attribute’s definition editor. Depending on the Operation Mode you select for your GPIO pin (INPUT vs. OUTPUT), different options will appear:

   **GPIO Input Options**![Attribute Definition Editor, GPIO Input](img/GPIO-Attributes-Input.png)

   **GPIO Output Options**![Attribute Definition Editor](img/GPIO-Attributes-Output.png)

   If you turn an attribute OFF, you will lose its current definition. To retain your attribute definition but close that attribute’s editor, click the name of the attribute shown in orange at the top-left of the editor. Save your work at any time by clicking the SAVE button in the upper-right of the window.

   

   

3. Complete the fields using the information in the table below:

   | FIELD                                                        | DESCRIPTION                                                  |
   | :----------------------------------------------------------- | :----------------------------------------------------------- |
   | Attribute Name                                               | Type a name that will help you identify this attribute in other contexts. This name will never be visible to the end-user. |
   | Operation Mode                                               | INPUT - Inputs are read-only.PULL UP or PULL DOWN - Select one of these options (they are mutually exclusive) to specify the inclusion of a pull-up or pull-down resistor on the pin, or select neither for NO PULL. Any digital input can be configured as Pull Up, Pull Down, or No Pull.**Note:** On Modulo boards, GPIO 0 is connected to an LED in series with a resistor. When the pin is pulled low the LED turns on; when floating or high the LED turns off. If you enable PULL DOWN on this pin the LED partly turns on and the pin stays between logic levels and does not properly go LOW. This does not cause functionality problems but will show up with a voltmeter. So on this pin only, Pull Down will not work properly unless the LED hardware is manually disconnected, as a voltage divider circuit will be formed.IS TOGGLE - This is a special case for momentary-contact buttons. When IS TOGGLE is selected, a pulse on the input line (i.e., transition from one state to another and then back again) will cause the attribute value to toggle between 0 and 1. This lets you implement a push button.DEBOUNCE TIME - This field allows you to apply a debounce interval (measured in milliseconds) to the associated input. A typical use case would be to ensure that a single press on a noisy pushbutton is interpreted as a single event. Specify 0 to disable the option; the allowed range of debounce intervals is 30-10000 ms.COUNT - The Count option is only available for Input attributes and does not work with the Is Toggle option.When you specify an input as COUNT, the attribute value becomes a counter and increments every time the input pin is pulsed. Unlike other GPIO input attribute values, it is **writeable**, which allows you to reset the value as well as start from a value other than 0. Count attributes should accurately count pulses up to a rate of about 5Hz.LATCH - Latching is currently only available for Input attributes. Latching causes a change in an attribute value to be held until it can be successfully transmitted to the Afero Cloud. This is useful for applications like door or leak sensors where you want to make sure the user is notified of a change even if the state goes back to normal. In these cases the value starts at 0. If an event occurs, the value goes to 1 and that value will be held until a hub can connect. Once the connection is made, the peripheral will send the latched value followed by the current value. If you have a rule to notify the user when an event occurs, that rule will fire when the latched value is received even if the current value is 0. |
   | OUTPUT - Outputs are both read and write.DEFAULT LOGIC LEVEL - Appears if neither PWM nor Pulse is selected. This option represents the binary pin-level state, and should be either 0 or 1. Remember that every time a device loses power and restarts, default values are restored, so think carefully about use cases and how this could affect the end-user.PWM - You can have a maximum of two pins configured as PWMs. Select from any of the GPIOs (0 - 3). For this option, you must specify a few parameters:PWM FREQUENCY - Integer value for frequency in Hz, based on the module you’re using:Modulo-1: 1 to 1,000,000All others: 12 to 100,000DEFAULT DUTY CYCLE - Expressed as a percent, which should be an integer from 0 to 100. Again, every time the device is reset, this default value is restored.PULSE - You can have a maximum of two GPIO pins configured to pulse, and they cannot be bound to other attributes. Note also that if you have an MCU enabled, you will see a variable 30-millisecond delay (jitter) around your pulses. This is because the ASR CPU will be busy with the MCU request while trying to pulse. For details, read [More About Pulsing](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#AboutPulsing).To define the pulse behavior, you must specify a few parameters:PULSE ACTIVE TIME - The pulse width, in milliseconds. Minimum pulse width: 50 ms; maximum: 1000 ms.PULSE INACTIVE TIME - The time, in milliseconds, between the end of one pulse and the start of the next. Minimum time: 50 ms; maximum: 1000 ms.DEFAULT VALUE - For a pulse attribute, the default value field plays a special role: it represents the number of pulses emitted by the pin **at boot**. It is important to recognize that setting a non-zero default value for a pulse is a special case, indeed one that may only rarely be used. If you set the default value to 10, for example, the pin will pulse 10 times when ASR boots, and then halt, and the default value will have no effect on pin behavior until the next boot. For most cases, the **attribute value** of a pulse attribute is more important than the **default value**. Read more directly below.ATTRIBUTE VALUE - The value assigned to this attribute indicates the count of pulses that should be emitted by the pin. When you set the attribute value – either directly, using one of the `af_lib_set_attribute*()` calls, or via a UI interaction – the pin will begin pulsing immediately. The attribute value will count down from the initial setting to zero as the pulsing occurs, and pulsing stops when the attribute value reaches zero. To initiate pulsing again, you may set the attribute to another non-zero value. |                                                              |
   | Active                                                       | By default, an attribute value of 1 sets the I/O voltage to HIGH. To invert that setting so a value of 1 sets the voltage to LOW, select that option. Active Low can be set for all GPIOs that are configured as Input or Output, but are not configured as Toggle (for Input) or PWM (for Output). |
   | Bind to Attributes                                           | Use binding to have changes from one attribute propagate to another attribute locally, without having to go through the Afero Cloud. For details, read [More About Binding](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#AboutBinding).When you bind attributes together, if one of the bound attributes has the STORE IN FLASH option selected, then all the bound attributes must have the STORE IN FLASH option selected. |
   | Store in Flash                                               | This option is available to:**Output** attributes **not** set to Pulse (see note below), and**Input** attributes that **are** set to ISTOGGLE.Selecting this checkbox ensures that an attribute value persists in flash memory if power is interrupted. A good example of this is when a powered-on plug loses, then regains, power. When power is restored, you want the plug to return to the “on” state, the same state it was in prior to losing power.There is a reason STORE IN FLASH is not available to Output attributes set to PULSE. If a pulsing attribute values were stored in flash, the value would be written with every pulse, and that could result in exhausting flash lifetime earlier than expected. |
   | Use ASR Timestamps                                           | This option is available to all attributes, **but only on Modulo-1B, Plumo-2C, and Plumo-2D**.Select this option if you want to report the actual time an attribute was updated, whether the device was offline or online at the time of update.Note that if you want to track the history of updates and not just the last time something happened, you can store the timestamps in a queue using a specified logic that’s used for reporting. You configure the queue by selecting a “queuing policy” in the drop-down menu described below. |
   | Queue Configuration                                          | This option is available to all attributes, **but only on Modulo-1B, Plumo-2C, and Plumo-2D**.If you want to keep track of updates to an attribute, you can configure a queue that stores these updates. If you have selected the USE ASR TIMESTAMPS option, the time of update is also stored.To set up a queue, you must select a Queuing Policy that specifies the **queue order** and **what happens when the queue is full**. After selecting a policy, you will define the Queue Size, which must be an integer between 0 and 65,535. **However**, the size of the queue must fit in your device Profile RAM, so the upper limit will most likely be much lower.Read the details of each queuing policy in [All About Queuing](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#queuepolicy). |

### More About Pulsing

This option gives you a straightforward way to have a GPIO pin send pulses of a defined duration in response to an attribute change. An easy way to visualize this operation is to set up a pulsing GPIO attribute with a slider control. From the mobile app, set the attribute value using the slider… and then watch as the slider moves back down to zero as the pin pulses.

Note that the **number** of pulses is not among the fixed parameters you defined for the attribute. You could define an attribute and always use it as a one-shot pulse (by always setting the attribute value to one), or you could define an attribute that pulses a variable number of times (perhaps blinking an LED for a number of times requested by a UI setting) – the difference would be in the run-time attribute value, not in the attribute definition.

Finally, let’s clarify the behavior of the default value. The default value sets the **initial** attribute value (the pulse count), and pulses are emitted as that value counts down to 0. This happens only once, and won’t be repeated until ASR resets to initial conditions. Given this, it is anticipated that most users will specify a default value of 0, so that no pulsing occurs until the attribute value is explicitly set; but the “pulse at startup” capability is there if you need it.

### More About Binding

We’ll use an example of binding to explain its use further. A good example is an Afero controlled power outlet, in which you would have an attribute that enables or disables power to the socket. On the power outlet itself, you’d also have a switch so the user can manually enable or disable power. What you want to do is “bind” the value of the switch attribute to the value of the power attribute so that if the user operates the switch, the outlet turns on and off. If the user changes the power value from the Afero Cloud, the attribute value for the switch will also update. For example:

| OPERATION                                      | POWER ATTRIBUTE | SWITCH ATTRIBUTE                                          | NOTES                          |
| :--------------------------------------------- | :-------------- | :-------------------------------------------------------- | :----------------------------- |
| All off                                        | 0               | 0                                                         | Start with a steady state.     |
| User presses switch on outlet.                 | 0               | 1                                                         | Switch attribute toggles to 1. |
| 1                                              | 1               | Binding causes power attribute to match switch attribute. |                                |
| User turns off power via the Afero mobile app. | 0               | 1                                                         | Power attribute goes to 0.     |
| 0                                              | 0               | Binding causes switch attribute to match power attribute. |                                |

In the case of binding, there is always a **source attribute** that is the changeable one, and a **destination attribute** that is being updated to match the value of the source attribute. In some cases, the destination attribute will not be writable. In these cases, the update operation will silently fail. Picture a case where you want an I/O input attribute to bind to an I/O output attribute. If the input attribute changes, the output attribute updates to match the new value. But if the output attribute is changed (via the Afero mobile app for example), the input attribute is not updated. This allows binding to work in one direction and not fail in the other.

#### Binding Constraints

Binding causes a change in one IO’s attribute value to update the value of another. As some IO attribute values are controlled by external hardware, binding can only work with certain IO configurations.

| CONFIGURATION | WILL UPDATE? | NOTES                                                        |
| :------------ | :----------- | :----------------------------------------------------------- |
| Input         | No           | Attribute value is controlled by external signal.            |
| Input Toggle  | Yes          | Attribute value is independent of external signal. Pull configuration does not matter. |
| Output        | Yes          |                                                              |
| Output PWM    | Yes          | Since value is 0 to 100 (instead of 0 or 1), a PWM can only be used to bind to another PWM output. |

### All About Queuing

Queued attributes maintain a history of previous updates, as opposed to non-queued attributes, which are overwritten when the device is offline. The policy for what to do when the queue is full and the queue order is configurable.

“Queuing policy” is a combination of queue order and queue-full action, described below.

#### Queue Order

- FIFO (first in, first out)
- LIFO (last in, first out)

#### Queue-Full Action

Queue-full actions determine what to do when the queue is full. They are applied independently, as a function of whether the device is offline or online.

- Replace oldest - Remove the oldest item and add the new item based on queue order.
- Fail - Do not add the new item to the queue. Instead, return an error to the MCU or ASR.
- Flow control - Do not add the new item to the queue. Instead, flow control the MCU or ASR. After space becomes available in the queue, notify the MCU or ASR.

#### Queuing Policy Values

Use the table below to understand the values in the Queuing Policy drop-down menu:

| VALUE     | QUEUE ORDER | QUEUE-FULL WHEN OFFLINE | QUEUE-FULL WHEN ONLINE |
| :-------- | :---------- | :---------------------- | :--------------------- |
| FIFO/R/R  | FIFO        | Replace oldest          | Replace oldest         |
| FIFO/R/FC | FIFO        | Replace oldest          | Flow control           |
| FIFO/F/FC | FIFO        | Fail                    | Flow control           |
| LIFO/R/R  | LIFO        | Replace oldest          | Replace oldest         |
| LIFO/R/FC | LIFO        | Replace oldest          | Flow control           |
| LIFO/F/FC | LIFO        | Fail                    | Flow control           |

## Define the MCU Attributes

Depending on whether your MCU device is a Potenco or another MCU device, the interface for defining the attributes will differ. Go to the section relevant for your MCU device:

- [Define Potenco Attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#HubAttributes)
- [Define (Non-Potenco) MCU Attributes](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#MCUAttributes)

### Define Potenco Attributes

First you will configure your Potenco, then add attributes:

1. Once you’ve clicked ATTRIBUTES in the right-hand navigation bar, you’ll see the DEFINE THE MCU ATTRIBUTES window:![Potenco Configuration](img/APE-PotencoConfig.png)

2. In the Supported Network Interfaces pane, select all the network interfaces that your device supports. Select from WI-FI, ETHERNET, and WAN.

3. In the Device Configuration pane, if you want your MCU to receive the UTC time updates from ASR, select the RECEIVE UTC TIME checkbox. Read more in [Using the Afero Cloud to Keep Time on the MCU](https://afero-devdocs.readthedocs.io/en/latest/SetMCUTime).

4. Now you’re ready to add an attribute. Click the + DEVICE ATTRIBUTE button to open the device attribute editor:![Potenco Attribute Editor](img/APE-PotencoAttrEditor.png)

5. Complete the fields using the information in the table below:

   | FIELD          | DESCRIPTION                                                  |
   | :------------- | :----------------------------------------------------------- |
   | Attribute ID   | Accept the default attribute ID that pre-populates the field, or type another number between 1 and 1023, inclusive. The number must be unique to the Profile. |
   | Attribute Name | Type a name that will help you identify this attribute in other contexts. This name is not visible to the end-user. |
   | Default Value  | Type a value that will be the initial setting for this function. Keep in mind that the Default Value must be compatible with the Data Type; if it’s not, you’ll be warned when you try to save. Also remember that every time a device loses power and restarts, default values are restored. Think about how this could affect the end-user. |
   | Data Type      | ASR uses the data type to allocate the storage size for the attribute. Select from the following:SINT8 - Signed integer (8 bit)SINT16 - Signed integer (16 bit)SINT32 - Signed integer (32 bit)SINT64 - Signed integer (64 bit)Q_15_16 - Signed fixed-point integer (32 bit)BOOLEAN - Logical true/falseUTF8S - String encoded as UTF-8BYTES - Byte array |
   | Max Size       | Maximum size, in bytes, of the attribute data. The max size is pre-defined for all data types, with UTF8S and BYTES the highest at 1536 bytes. Keep in mind that attribute memory is preallocated in ASR, so choose a max that will definitely handle your application needs; if you exceed allocated space at runtime, you will almost certainly overwrite something else. |
   | Read/Write     | MCU attributes are Read-Only by default. If you need to write attributes to your device, then select the WRITE checkbox as well. |

6. Once you’ve defined all your attributes, click SAVE in the upper-right corner of the window.

### Define (Non-Potenco) MCU Attributes

First you will configure your MCU, then add attributes:

1. Click the MCU CONFIGURATION toggle switch to turn it ON and select the protocol your MCU is using, either SPI or UART.

   For the “Plumo-2D” Module Type, only UART protocol is supported.

   

   ![MCU Firmware Updates](img/MCU-Config.png)

2. If you have selected UART, you must select the following transmission options from the drop-down menus:

   | OPTION     | DESCRIPTION                                                  |
   | :--------- | :----------------------------------------------------------- |
   | Baud Rate  | The rate at which incoming bits are read, expressed in bits per second (bps). Select from 4800, 9600, 38400, or 115200. |
   | Parity Bit | For error-checking, a bit added to a string of binary code to make sure the total number of 1-bits in the string is even or odd. Select from NONE, ODD, or EVEN. |
   | Data Width | Number of bits per data frame. Select from 5, 6, 7, 8, or 9. |
   | Stop Bits  | Number of bits used to signal the end of the data transmission. Select from 1, 1.5, or 2. |

3. **The RECEIVE UTC TIME setting applies only to ASR-2 and Modulo-2**: If you want your MCU to receive the UTC time updates from ASR, select the RECEIVE UTC TIME checkbox. Read more in [Using the Afero Cloud to Keep Time on the MCU](https://afero-devdocs.readthedocs.io/en/latest/SetMCUTime).

4. Use the FIRMWARE OTA UPDATES section if you are planning to send firmware image updates to your MCU over-the-air using the OTA Manager. You must select at least one firmware Image Type checkbox to enable OTA firmware updates for your MCU.

   If you don’t see any Image Types, or need an Image Type that isn’t shown, go to the [Afero OTA Manager](https://otamanager.afero.io/) and create a new Image Type. Once you’ve saved this new Image Type, return to the Profile Editor to select the Image Type and complete your Profile.

   For more information on preparing your MCU application code to receive OTA updates, please read [Handling MCU OTA Updates](https://afero-devdocs.readthedocs.io/en/latest/MCU_OTA).

5. Now you’re ready to add an MCU attribute. Click the + MCU ATTRIBUTE button to open the MCU attribute definition editor:![MCU Attribute](img/Define_MCU_Attr.png)

6. Complete the fields using the information in the table below:

   | FIELD               | DESCRIPTION                                                  |
   | :------------------ | :----------------------------------------------------------- |
   | Attribute ID        | Accept the default attribute ID that pre-populates the field, or type another number between 1 and 1023, inclusive. The number must be unique to the Profile. |
   | Attribute Name      | Type a name that will help you identify this attribute in other contexts. This name is not visible to the end-user. |
   | Default Value       | Type a value that will be the initial setting for this function. Keep in mind that the Default Value must be compatible with the Data Type; if it’s not, you’ll be warned when you try to save. Also remember that every time a device loses power and restarts, default values are restored. Think about how this could affect the end-user. |
   | Data Type           | ASR uses the data type to allocate the storage size for the attribute. Select from the following:SINT8 - Signed integer (8 bit)SINT16 - Signed integer (16 bit)SINT32 - Signed integer (32 bit)SINT64 - Signed integer (64 bit)Q_15_16 - Signed fixed-point integer (32 bit)BOOLEAN - Logical true/falseUTF8S - String encoded as UTF-8BYTES - Byte array |
   | Max Size            | Maximum size, in bytes, of the attribute data. The max size is pre-defined for all data types, with UTF8S and BYTES the highest at 255 bytes. Keep in mind that attribute memory is preallocated in ASR, so choose a max that will definitely handle your application needs; if you exceed allocated space at runtime, you will almost certainly overwrite something else. |
   | Read/Write          | MCU attributes are Read-Only by default. If you need to write attributes to your device, then select the WRITE checkbox as well. |
   | Use ASR Timestamps  | Refer to the [Use ASR Timestamps](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#UseTimestamp) section above. |
   | Queue Configuration | Refer to the [Queue Configuration](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#QueueConfig) section above. To understand the queuing policy options, read [All About Queuing](https://afero-devdocs.readthedocs.io/en/latest/AttrDef#queuepolicy). |

7. Once you’ve defined all your attributes, click SAVE in the upper-right corner of the window.

#### MCU Attribute Tips

Here are some helpful tips when editing MCU attribute definitions:

- To define more MCU attributes, click the + MCU ATTRIBUTE button to open the attribute definition editor.
- To delete an attribute, open it for editing then click the trash icon in the upper-right of the window.
- If you’ve added several attributes, scrolling can become annoying; clicking an attribute name at the top-left of the attribute editor will collapse/expand the editor.
- **Important!** Once you’ve enabled MCU attributes and updated the Profile on your ASR, it will expect to have an MCU available on the serial bus, and will attempt to communicate with that device. If there is no device present, communication will fail and recovery may require power-cycling. So it’s important to have your MCU connected to ASR **before** you publish a Profile that includes MCU attribute definitions.

 Next: [Define the Mobile App UI](https://afero-devdocs.readthedocs.io/en/latest/AppUIDef)