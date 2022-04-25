# Add Environment Variable Paths on a PC

Before programming ASR you must install [Python 2.7](https://www.python.org/downloads) and the driver for the [SEGGER J-Link](https://www.segger.com/downloads/jlink/#jlinksoftwareanddocumentationpack). Be sure to install to the default locations on your PC. In addition, before the provisioning script can run successfully you will need to add the paths to these executables to your environment variables. Note that these instructions are for Windows 10, but should be similar for other versions of Windows:

1. Click the Windows menu in the lower-left of your desktop, then click the Settings icon, highlighted in the illustration below:![img](img/AddPath-01.png)

   Windows Settings window opens, where you should start typing “envi”, as shown. Select “Edit the system environment variables” in the drop-down list, as indicated below by the red arrow; this will open the System Properties window.![img](img/AddPath-02.png)

2. On the System Properties window, click the ENVIRONMENTAL VARIABLES button:![img](img/AddPath-03.png)

3. On the Environment Variables window, select PATH to highlight it, then click the EDIT button:![img](img/AddPath-04.png)

4. The Edit Environment Variable window, opens. Click the NEW button on the right, then add the three entries for Python and J-Link, as shown below. Earlier versions of Windows (<10) may require that you add paths by separating them from existing paths with a semicolon (;).

   Be careful you **DO NOT** remove any existing paths when adding your new variable paths.   

5. Click OK on each of the open windows to save the new variable paths.

6. You’re all set!

<table>
<tr>
<th>Argument</th>
<th>Description</th>
</tr>
<tr>
<td>appDir</td>
<td>The top level directory that contains your app. If this option is used then
it assumed your scripts are in</td>
</tr>
<tr>
<td>baseUrl</td>
<td>By default, all modules are located relative to this path. If baseUrl is not
explicitly set, then all modules are loaded relative to the directory that holds
the build file. If appDir is set, then baseUrl should be specified as relative
to the appDir.</td>
</tr>
<tr>
<td>dir</td>
<td>The directory path to save the output. If not specified, then the path will
default to be a directory called "build" as a sibling to the build file. All
relative paths are relative to the build file.</td>
</tr>
<tr>
<td>modules</td>
<td>List the modules that will be optimized. All their immediate and deep
dependencies will be included in the module's file when the build is done. If
that module or any of its dependencies includes i18n bundles, only the root
bundles will be included unless the locale: section is set above.</td>
</tr>
</table>