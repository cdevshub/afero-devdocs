# Define the Device Type

After selecting a project on the Startup window, the Profile Editor opens to the **Device Type definition** window:

![Device Type Definition Window](img/APE-DefineDvcType.png)

## Add Your Information

1. In the DEFINE THE DEVICE TYPE section, complete the fields using the information in the table below:

   | FIELD              | DESCRIPTION                                                  |
   | :----------------- | :----------------------------------------------------------- |
   | Device Type Name   | This name is a string; by default it assumes the name you gave it when creating the project, but you can change it here. Note that if you do change it here, the project name displayed in Profile Editor will also update to reflect the new name. Here are some important things to know about Device Type:In the mobile app, the default name given the device is the Device Type Name. This name will be used only initially as it can be changed to a “friendly name” by the end-user when adding the device to their account, or by editing the device name on the device Settings screen. You, as the developer, can also change this friendly name on the Publish window. So use a descriptive name here that makes sense to you and your end-users. Also, the friendly name is what appears in the Inspector tool to identify your devices.Note that if the end-user does change the friendly name on the mobile app, the Device Type Name itself will not change. The only place you can change the Device Type Name is in this field; and only after the Profile has been published does any change you make reflect on the Publish window and in the Afero system.The Device Type is an important identifier. Once you publish a Profile with a given Device Type, an ID is associated with the Device Type that remains unchanged as long as the Device Type is active. As pointed out above, you can always rename your Device Type using this field, but the `devicetypeID` will not change.Device Type names must be unique across your projects. (Read more in [Before You Proceed](/SelectProject#DOC-158).)The Device Type is used by the OTA Manager to associate an MCU firmware Image Type with devices. |
   | Description        | This description is a string, internal only and not displayed to the end-user. Type a description that is useful to you. |
   | Project Folder     | The directory on your local filesystem where your project is saved. You can’t edit the location; it’s displayed for information purposes only. |
   | Header File Output | If you are using a device that has a separate MCU, a header file containing the device description (attributes) will be generated when you publish your project. By default, the header file will be saved to your project directory, but you can use this setting to save the header file to a different directory. For example, you might wish to save the file directly into the project directory for the associated MCU code (which will rely on the header). |
   | Device Icon        | This icon will be visible to the end-user. Select a meaningful image to represent your device. Click SELECT to see all available icons; highlight the icon you want then click USE THIS ONE! Your selected icon will be displayed in the Preview pane to the right, to give you an idea of how it will look on a smartphone. It will also be displayed to the left of your project name in the Navigation pane. |

2. The POWER OPTIMIZATION section provides controls and information regarding battery power consumption.

   The Power Optimization calculations apply only to projects using either the Modulo-1 or Modulo-1B modules.

   

   - Select an ADVERTISING INTERVAL (in seconds) for Bluetooth. If you’re running on battery power, the shorter the interval, the more battery power is consumed. However, at higher intervals the responsiveness of the device will be negatively affected due to lag time.

   - Once you’ve selected an interval, the DAILY AVERAGE CURRENT field will display the projected average current required by Modulo-1 or Modulo-1B for that interval while idle (the module is said to be idle when performing no function other than advertising).

   - Click the

      

     SHOW ADVANCED POWER CALCULATOR

      

     link at the bottom of the pane to open the

      

     APPROXIMATE BATTERY LIFETIME

      

     estimator. Use this calculator to estimate the runtime of an Modulo-1 or Modulo-1B based on the battery type you’re using. For a more accurate forecast of the battery life, type the number of connections per day and additional power the device may be using. You can also check what the runtimes might be for different battery capacities.

     ![Approximate Battery Life Calculator](img/APE-ApproxBatteryLife.png)

3. Once you’ve defined the Device Type, you’ll want to save the definition.

   - Clicking CANCEL reverts any changes you made on the page.
   - Clicking SAVE initiates validation of the new data and, if validation is successful, the data is saved to your local project directory.

   Every time you save, your data is validated. If validation fails for any reason, an error message will appear then move to the left. Click the error description in the message to highlight the field that needs correcting.

   

 Next: [Define the Device Attributes](/AttrDef)