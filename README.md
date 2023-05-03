# PSoC&trade; 4: MSCLP CAPSENSE&trade; low-power proximity tuning

This code example demonstrates an implementation of a low-power proximity sensing application for maximum proximity sensing at the largest distance to detect a target (a hand). It includes recommended power states and transitions, adjustments for tuning parameters, and the method of tuning. This example uses a proximity widget in multi-sense CAPSENSE&trade; low-power (MSCLP - 5th-generation low-power CAPSENSE&trade;) to demonstrate different considerations to implement a low-power design.

This document also explains how to manually tune the low-power widget for optimum performance and largest distance w.r.t parameters such as power consumption and response time using the CSD-RM sensing technique and CAPSENSE&trade; Tuner.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-msclp-capsense-lp-proximity)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzYwMzMiLCJTcGVjIE51bWJlciI6IjAwMi0zNjAzMyIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IE1TQ0xQIENBUFNFTlNFJnRyYWRlOyBsb3ctcG93ZXIgcHJveGltaXR5IHR1bmluZyIsInJpZCI6IndhaW5nYW5rYXIiLCJEb2MgdmVyc2lvbiI6IjEuMi4wIiwiRG9jIExhbmd1YWdlIjoiRW5nbGlzaCIsIkRvYyBEaXZpc2lvbiI6Ik1DRCIsIkRvYyBCVSI6IklDVyIsIkRvYyBGYW1pbHkiOiJQU09DIn0=)


## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/cms/en/design-support/tools/sdk/modustoolbox-software/) v3.0 or later

   **Note:** This code example version requires ModusToolbox&trade; software version 3.0 or later and is not backward compatible with v2.4 or older versions.

- Board support package (BSP) minimum required version: 0.6.0
- Programming language: C
- Associated parts: PSoC&trade; 4000T datasheet

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.16 (`ARM`)
- IAR C/C++ compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- PSoC&trade; 4000T CAPSENSE&trade; evaluation kit (`CY8CKIT-040T`) - Default value of `TARGET`

## Hardware setup

This example uses the board's default configuration. See the Kit user guide to ensure that the board is configured correctly.

## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/dgdl/Infineon-ModusToolbox_Library_Manager_2.0_User_Guide-UserManual-v01_00-EN.pdf?fileId=8ac78c8c8386267f0183a960c5945992) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The "project-creator-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional
<br>

The following example clones the "[PSoC&trade; 4: MSCLP CAPSENSE&trade; low-power proximity tuning](https://github.com/Infineon/mtb-example-psoc4-msclp-capsense-lp-proximity)" application with the desired name "CAPSENSE_Low_Power_Proximity_Tuning" configured for the *CY8CKIT-040T* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-040T --app-id mtb-example-psoc4-msclp-capsense-lp-proximity --user-app-name CAPSENSE_Low_Power_Proximity_Tuning --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can invoke the Library Manager GUI tool from the terminal using `make library-manager` command or use the Library Manager CLI tool "library-manager-cli" to change the BSP.

The "library-manager-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--add-bsp-name` | Name of the BSP that should be added to the application | Required
`--set-active-bsp` | Name of the BSP that should be as active BSP for the application | Required
`--add-bsp-version`| Specify the version of the BSP that should be added to the application if you do not wish to use the latest from manifest | Optional
`--add-bsp-location`| Specify the location of the BSP (local/shared) if you prefer to add the BSP in a shared path | Optional

<br />

Following example adds the CY8CKIT-040T BSP to the already created application and makes it the active BSP for the app:

   ```
   library-manager-cli --project "C:/mtb_projects/CAPSENSE_Low_Power_Proximity_Tuning" --add-bsp-name CY8CKIT-040T --add-bsp-version "latest-v4.X" --add-bsp-location "local"

   library-manager-cli --project "C:/mtb_projects/CAPSENSE_Low_Power_Proximity_Tuning" --set-active-bsp APP_CY8CKIT-040T
   ```

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows Start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.

   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.

   3. In the **Select Application** screen, select the appropriate IDE from the **Target IDE** drop-down menu.

   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

<br>

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and then import the libraries using the `make getlibs` command.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

The project already has the necessary settings by default, so you can go to [Operation](#operation) to test the example. If you want to understand the tuning process and follow the stages for this kit or your own board, go to [Tuning procedure](#tuning-procedure) and then test it using [Operation](#operation).

## Operation

1. Connect the board to your PC using the provided micro USB cable through the KitProg3 USB connector as follows:

   **Figure 1. Connecting the CY8CKIT-040T kit to a computer**

   <img src="images/psoc4000t_kit_connected.png" alt="Figure 1" width="350"/>

2. The SWD, I2C and user LED modes are multiplexed to the same pins (GPIO Pins P3[2] and P3[3]) in CY8CKIT-040T. The interface can be switched between these using the FW-loader commands. Download and unzip the *Batch_files_for_mux_selection* zipped file from the Beta package to the *bin* folder inside the *fw-loader* folder in the ModusToolbox&trade; installation directory. 
    
   Default location: */ModusToolbox/tools_3.0/fw-loader/bin*
   
   Select the SWD mode by running the `Select_SWD` batch file to program the CY8CKIT-040T kit. For detailed information, see **Section 2.3.1** in CY8CKIT-040T kit user guide.

3. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade; software</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The target and the toolchain is specified manually:
      ```
      make program TARGET=<BSP> TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TARGET=CY8CKIT-040T TOOLCHAIN=GCC_ARM
      ```
   </details>

4. After programming, the application starts automatically.

5. To test the application, bring your hand near the the CAPSENSE&trade; proximity sensor and notice that LED3 turns ON with RED color, and turns OFF when the hand is moved away. In this case the maximum distance the proximity sensor can sense substantially is 45mm. It can also detect a touch. When you touch the sensor (outer loop), the LED1 turns on with color BLUE and turns off when you remove the touch.


   **Table 1. LED1 and LED3 state for Proximity and Touch**

    Hand position  | LED1  | LED3  |
   :------------------| :-----| :-----|
    Proximity  | OFF |RED  |
    Touch  | BLUE | RED |

   <br>

   **Figure 2. LED3 turns on upon bringing the hand nearby**

   <img src="images/proximity.png" alt="Figure 2" width="400"/>


### Monitor data using CAPSENSE&trade; Tuner

1. Select I2C mode by running the *Select_I2C* batch file to enable I2C communication between onboard KitProg and CAPSENSE&trade; Tuner.

2. Open CAPSENSE&trade; Tuner from the 'Tools' section in the IDE Quick Panel.

   You can also run the CAPSENSE&trade; Tuner application standalone from *{ModusToolbox&trade; install directory}/ModusToolbox&trade;/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS/* folder.

   See the [ModusToolbox&trade; user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*)for options to open the CAPSENSE&trade; tuner application using the CLI.

3. Ensure that the kit is in CMSIS-DAP Bulk mode (KitProg3 Status LED is ON and not blinking). See [Firmware-loader](https://github.com/Infineon/Firmware-loader) to learn on how to update the firmware and switch modes in KitProg3.

4. In the tuner application, click on the **Tuner communication setup** icon or select **Tools** > **Tuner communication setup**. In the window that appears, select the I2C checkbox under KitProg3 and configure as follows:

   - **I2C address:** 8
   - **Sub-address:** 2 bytes
   - **Speed (kHz):** 400

   These are the same values set in the EZI2C resource.

   **Figure 3. Tuner communication setup parameters**

   <img src="images/tuner-comm-setup.png" alt="Figure 3" width="550"/>

5. Click **Connect** or select **Communication** > **Connect** to establish a connection.

   **Figure 4. Establish connection**

   <img src="images/tuner-connect.png" alt="Figure 4" width="300" />

6. Click **Start** or select **Communication** > **Start** to start data streaming from the device.

   **Figure 5. Start tuner communication**

   <img src="images/tuner-start.png" alt="Figure 5" width="300" />

   The *Widget/Sensor Parameters* tab is updated with the parameters configured in the CAPSENSE&trade; Configurator window. The tuner displays the data from the sensor in the *Widget View* and *Graph View* tabs.

7. Set the **Read mode** to Synchronized mode. Navigate to the **Widget view** tab and notice that the **Proximity0** widget is highlighted in blue when you touch it.

   **Figure 6. Widget view of the CAPSENSE&trade; Tuner**

   <img src="images/tuner-widget-view.png" alt="Figure 6" width="750"/>

8. Go to the **Graph View** tab to view the raw count, baseline, difference count, and status for each sensor. Observe that the low-power widget sensor (**LowPower0_Sns0**) raw count is plotted once the device completes a full-frame scan (or detects a touch) in **WOT** mode and moved to **Active/ALR** mode.

   **Figure 7. Graph view of the CAPSENSE&trade; Tuner**

   <img src="images/tuner-graph-view-intro.png" alt="Figure 7" width="750"/>

9. Observe the **Widget/Sensor parameters** section in the CAPSENSE&trade; Tuner window as shown in Figure 7.

10. Switch to the **SNR Measurement** tab for measuring the SNR and verify that the SNR is above 5:1 and Signal count is above 50; select **Proximity0** and **Proximity0_Sns0** sensor, and then click **Acquire noise** as follows:

    **Figure 8. CAPSENSE&trade; Tuner - SNR measurement: Acquire noise**

    <img src="images/tuner-acquire-noise.png" alt="Figure 8" width="750"/>

      **Note:** Because the scan refresh rate is lower in **ALR** mode, it will take more time to acquire noise. Touch the CAPSENSE&trade; proximity loop before clicking **Acquire noise** to transition the device to **ACTIVE** mode to get signal faster.

11. Once noise is acquired, bring your hand near the proximity loop at a distance around **45 mm** above it and then click **Acquire signal**. Ensure that the hand remains above the proximity loop as long as the signal acquisition is in progress. Observe that the SNR is above 5:1 and Signal count is above 50. If not, repeat signal acquisition by lowering the hand, and thus getting a higher signal.

    The maximum distance the proximity loop can sense is where the SNR is greater than 5:1 for a particular set of hardware parameters. **Later in this example, you will learn how changing the hardware parameters affect the distance and SNR** in section [Set initial hardware parameters](#stage-1-set-initial-hardware-parameters).

    The calculated SNR on this proximity widget is displayed, as Figure 9 shows.

    **Figure 9. CAPSENSE&trade; Tuner - SNR measurement: acquire signal**

    <img src="images/tuner-acquire-signal.png" alt="Figure 9" width="750"/>

12. To measure the SNR of the low-power sensor (**LowPower0_Sns0**), set the **Finger threshold** to max (65535) in **Widget/Sensor Parameters** for the **LowPower0** widget as shown in Figure 10. A set the **Proximity threshold** and **Touch Threshold** to max (65535) value in the **Widget/Sensor Parameters** of the **Proximity_Sns0** widget as shown in Figure 11.

    This is required because the application will stop scanning the low-power sensor when there is a proximity or touch detected and will transition to active mode.

      **Figure 10. CAPSENSE&trade; update finger threshold**

      <img src="images/tuner-threshold-update.png" alt="Figure 10" width="750"/>

      **Figure 11. CAPSENSE&trade; update proximity and touch threshold**

      <img src="images/tuner-threshold-update-proximity.png" alt="Figure 11" width="750"/>

13. Repeat steps 10 and 11 to observe the SNR and signal as Figure 12 shows.

       **Figure 12. CAPSENSE&trade; Tuner - SNR measurement: low-power widget**

       <img src="images/tuner-lowpower-snr.png" alt="Figure 12" width="750"/>


### Current consumption

Follow the instructions in the **Measure current at different power modes** section of the code example [PSoC™ 4: MSCLP CAPSENSE™ low power](https://github.com/Infineon/mtb-example-psoc4-msclp-capsense-low-power) to measure the current consumption.


## Tuning procedure


<details><summary><b> Create custom BSP for your board </b></summary>

1. Create a custom BSP for your board having any device, by following the steps given in [ModusToolbox™ BSP Assistant user guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_BSP_Assistant_1.0_User_Guide-UserManual-v02_00-EN.pdf?fileId=8ac78c8c8386267f0183a972f45c59af). This code example was created for the device "CY8C4046LQI-T452".

2. Open the *design.modus* file from the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder obtained in the previous step and enable CAPSENSE&trade; to get the *design.cycapsense* file. CAPSENSE&trade; configuration can then be started from scratch as explained below.


</details>

The following steps explain the tuning procedure for the proximity loop and the low-power widget.

**Note:** See the section "Selecting CAPSENSE&trade; hardware parameters" in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) to learn about the considerations for selecting each parameter values. In addition, see the "Low-power widget parameters" section in the [Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/002-34231) to learn about the considerations for parameter values specific to low-power widgets.

The tuning flow of the proximity widget is shown in **Figure 13**.

**Figure 13. Proximity widget Tuning flow**

   <img src="images/flowchart_for_tuning.png" alt="Figure 13"/>

To tune the low-power widget, see the **Tuning flow** section of the code example [PSoC™ 4: MSCLP CAPSENSE™ low power](https://github.com/Infineon/mtb-example-psoc4-msclp-capsense-low-power).

Do the following to tune the proximity widget:

- [Stage 1: Set initial hardware parameters](#stage-1-set-initial-hardware-parameters)

- [Stage 2: Calculate and set sense clock frequency](#stage-2-calculate-and-set-sense-clock-frequency)

- [Stage 3: Fine-tune for required SNR, power, and refresh rate](#stage-3-fine-tune-for-required-snr-power-and-refresh-rate)

- [Stage 4: CDAC dither parameters](#stage-4-cdac-dither-parameters)

- [Stage 5: Tune threshold parameters](#stage-5-tune-threshold-parameters)

### Stage 1: Set initial hardware parameters
-------------------------

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. Launch the Device Configurator tool.

   You can launch the Device Configurator in Eclipse IDE for ModusToolbox&trade; from the **Tools** section in the IDE Quick Panel or in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox&trade;/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS* folder.

3. Enable CAPSENSE&trade; channel in Device Configurator as follows:

   **Figure 14. Enable CAPSENSE&trade; in Device Configurator**

   <img src="images/device-configurator.png" alt="Figure 14"/>

   Save the changes and close the window.

4. Launch the CAPSENSE&trade; Configurator tool.

   You can launch the CAPSENSE&trade; Configurator tool in Eclipse IDE for ModusToolbox&trade; from the "CAPSENSE&trade;" peripheral setting in the Device Configurator or directly from the Tools section in the IDE Quick Panel.

   You can also launch it in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox&trade;/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS* folder.

   See the [ModusToolbox&trade; CAPSENSE&trade; Configurator tool guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in ModusToolbox&trade;.

5. In the **Basic** tab, add a proximity widget 'Proximity0' and a low-power widget 'LowPower0'. Set their sensing mode as CSD RM (self-cap) and set the CSD tuning mode as *Manual tuning*.

   **Figure 15. CAPSENSE&trade; Configurator - Basic tab**

   <img src="images/basic-csd-settings.png" alt="Figure 15"/>

6. Do the following in the **General** tab under the **Advanced** tab:

   1. Select **CAPSENSE&trade; IMO Clock frequency** as **46 MHz**.

   2. Set the **Modulator clock divider** to **1** to obtain the maximum available modulator clock frequency as recommended in the [CAPSENSE&trade; design guide](https://www.infineon.com/AN85951).

   3. Set the **Number of init sub-conversions** based on the hint shown when you hover over the edit box. Retain the default value (will be set in [Stage 2: Calculate and set sense clock frequency](#stage-2-calculate-and-set-sense-clock-frequency))

   4. Use **Wake-on-Touch settings** to set the refresh rate and frame timeout while in lowest power mode (Wake-on-Touch mode).

   5. Set **Wake-on-Touch scan interval (ms)** based on the required low-power state scan refresh rate. For example, to get a 16-Hz refresh rate, set the value to **63**.

   6. Set the **Number of frames in Wake-on-Touch** as the maximum number of frames to be scanned in WoT mode if there is no touch detected. This determines the maximum time the device will be kept in the lowest-power mode if there is no user activity. The maximum time can be calculated by multiplying this parameter with the **Wake-on-Touch scan interval (ms)** value.

      For example, to get 10 seconds as the maximum time in WoT mode, set **Number of frames in Wake-on-Touch** to **160** for the scan interval set as 63 ms.

      **Note:** For tuning low-power widgets, **Number of frames in Wake-on-Touch** must be less than the  **Maximum number of raw counts in SRAM** based on the number of sensors in WoT mode as follows:

      **Table 2. Maximum number of raw counts in SRAM**

       Number of low <br> power widgets  | Maximum number of <br> raw counts in SRAM  |
      :---------------------| :-----|
       1  | 245 |
       2  | 117 |
       3  | 74 |
       4  | 53 |
       5  | 40 |
       6  | 31 |
       7  | 25 |
       8  | 21 |

   7. Retain the default settings for all regular and low-power widget filters. You can enable or update the filters later depending on the signal-to-noise ratio (SNR) requirements in [Stage 3: Fine-tune for required SNR, power, and refresh rate](#stage-3-fine-tune-for-required-snr-power-and-refresh-rate).

      Filters are used to reduce the peak-to-peak noise; however, using filters will result in a higher scan time.

      **Figure 16. CAPSENSE&trade; Configurator - General settings**

      <img src="images/advanced-general-settings.png" alt="Figure 16"/>

      **Note:** Each tab has a **Restore Defaults** button to restore the parameters of that tab to their default values.

7. Go to the **CSD settings** tab and make the following changes:

   1. Set **Inactive sensor connection** as **Shield**.

   2. Set **Shield mode** as **Active**.

   3. Set **Total shield count** as **12** (Enabling all the inactive sensors as shield).

   4. Select **Enable CDAC auto-calibration** and **Enable compensation CDAC**.

      This helps in achieving the required CDAC calibration levels (85% of maximum count) for all sensors in the widget while maintaining the same sensitivity across the sensor elements.

   5. Select **Enable CDAC dither**.

      This helps in removing flat spots by adding white noise that moves the conversion point around the flat-spots region.

      **Figure 17. CAPSENSE&trade; Configurator - Advanced CSD settings**

      <img src="images/advanced-csd-settings.png" alt="Figure 17"/>

8. Go to the **Widget details** tab.


   Select **Proximity0** from the left pane, and then set the following:

   - **Sense clock divider:** Retain the default value (will be set in [Stage 2: Calculate and set sense clock frequency](#stage-2-calculate-and-set-sense-clock-frequency))

   - **Clock source:** Direct

      **Note:** Spread spectrum clock (SSC) or PRS clock can be used as a clock source to deal with EMI/EMC issues.

   - **Number of sub-conversions: 60**

     60 is a good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in [Stage 3: Fine-tune for required SNR, power, and refresh rate](#stage-3-fine-tune-for-required-snr-power-and-refresh-rate).

   - **Proximity threshold:** 65535

      Proximity threshold is set to the maximum to avoid the waking up of the device from WoT mode due to touch detection; this is required to find the signal and SNR. Change the 
      
   - **Touch threshold:** 65535

      Touch threshold is also set to the maximum to avoid the waking up of the device from WoT.

   - **Noise threshold:** 40

   - **Negative noise threshold:** 40

   - **Low baseline reset:** 30

   - **Hysteresis:** 10

   - **ON debounce:** 3

      **Figure 18. CAPSENSE&trade; Configurator - Proximity Widget details tab under the Advanced tab**

      <img src="images/advanced-widget-settings_proximity.png" alt="Figure 18" />

   Now, select **LowPower0** from the left pane, and then set the following:

   - **Sense clock divider:** Retain the default value (will be set in [Stage 2: Calculate and set sense clock frequency](#stage-2-calculate-and-set-sense-clock-frequency))

   - **Clock source:** Direct

      **Note:** Spread spectrum clock (SSC) or PRS clock can be used as the clock source to deal with EMI/EMC issues.

   - **Number of sub-conversions: 60**

     60 is a good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in [Stage 3: Fine-tune for required SNR, power, and refresh rate](#stage-3-fine-tune-for-required-snr-power-and-refresh-rate).

   - **Finger threshold:** 65535

      Finger threshold is set to the maximum to avoid the waking up of the device from WoT mode due to touch detection so that you can acquire signal for SNR measurement.

   - **Noise threshold:** 10

   - **Negative noise threshold:** 10

   - **Low baseline reset:** 10

   - **ON debounce:** 1

      **Figure 19. CAPSENSE&trade; Configurator - Low-Power Widget details tab under the Advanced tab**

     <img src="images/advanced-widget-settings.png" alt="Figure 19" />

   **Note:** These values reduce the influence of the baseline on the sensor signal, which helps to get the true difference count. Retain the default values for all other threshold parameters; these parameters are set in [Stage 5: Tune threshold parameters](#stage-5-tune-threshold-parameters).

9. Go to the **Scan Configuration** tab to select the pins and scan slots. Do the following:

   1. Configure the pins for electrodes using the drop-down menu.

   2. Configure the scan slots using the **Auto-assign slots** option. The other option is to allot each sensor a scan slot based on the entered slot number.

   3. Select Proximity0_Sns0 as **Ganged** under the **LowPower0** widget as shown in **Figure 20**.

   4. Check the notice list for warning or errors.

      **Figure 20. Scan Configuration tab**

      <img src="images/scan-configuration.png" alt="Figure 20"/>

10. Click **Save** to apply the settings.

<br>

### Stage 2: Calculate and set sense clock frequency
-------------------------

The maximum frequency set should charge and discharge the sensor completely, which is verified using an oscilloscope and an active probe. To view the charging and discharging waveforms of the sensor, probe at the sensors (or as close as possible to the sensors), and not at the pins or resistor. See **Figure 21** and **Figure 22** for more deatils. You can also use a passive probe which will add an additional parasitic capacitance of around 15 pF; therefore, the tuning may be not optimal. These figures show the signals observed on shield.

**Figure 21**  shows proper charging when sense clock frequency is correctly tuned i.e., the voltage is settling to the required voltage at the end of each phase. **Figure 22** shows incomplete settling (charging/discharing) and hence the sense clock divider is set to 28 as shown in **Figure 21**.

 **Notes:** 
   - If you are explicitly using the PRS or SSCx clock source to lower electromagnetic interference, ensure that you select the sense clock frequency that meets the conditions mentioned in the [ModusToolbox&trade; CAPSENSE&trade; configurator guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_CapSense_Configurator_Guide_(Version_2.0)-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed9999c3b364d&utm_source=cypress&utm_medium=referral&utm_campaign=202110_globe_en_all_integration-files) in addition to the above conditions. PRS and SSCx techniques spread the frequency across a range.

   - Actual sense clock frequency value is chosen such that the divider is divisible by 4 to have all four scan phases for equal durations. 

The project uses max sense clock frequency by default. If an incomplete charging/discharging is observed (as in **Figure 22**), the sense clock divider is increased until the sensor and shield is fully charged/discharged.
For tuning your board, ensure to charge/dischage by probing at both the sensor and shield.

**Figure 21. Proper charge cycle of a sensor**

   <img src="images/csdrm-waveform.png" alt="" width="400"/>

   **Figure 22. Improper charge cycle of a sensor**

   <img src="images/csdrm-waveform_improper.png" alt="" width="400"/>
   
Observe Point A and B marked in **Figure 21**, it is charging/discharging properly to VDD/2 whereas in **Figure 22**, it is not reaching to VDD/2.

   Set the final value in the CAPSENSE&trade; configurator using the steps given in **Step 8** of **Stage 1**, which ensures the maximum possible sense clock frequency (for good gain) while allowing the sensor capacitance to fully charge and discharge in each phase of the MSCLP CSD sensing method.

   The actual sense clock frequency value is chosen such that the divider is divisible by 4 in order to have all the four scan phases for equal duration.

   **Table 3. Sense clock frequency settings for CY8CKIT-040T kit**

   Development kit | Sense clock divider | 
   :-------- |:-----------|
   CY8CKIT-040T (Pin P2.5) | 28 |
<br>

### Stage 3: Fine-tune for required SNR, power, and refresh rate
-------------------------

1. Measure the SNR for the maximum proximity height as mentioned in the [Operation](#operation) section (45mm in this case) by placing your hand above the proximity loop, and perform sensor tuning until the minimum SNR of 5:1 and a signal count of at least 50 are achieved.

2. Update the number of sub-conversions.

   Do the following to update the number of sub-conversions:

   1. Update the number of sub-conversions (N<sub>sub</sub>) directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; Tuner. Increasing the N<sub>sub</sub> will increase the sensitivity.

      CY8CKIT-040T has a built-in CIC2 filter which increases the resolution for the same scan time. See [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/AN234231) for detailed information on the CIC2 filter.

   2. Current consumption is directly proportional to the number of sub-conversions; therefore, decrease the number of sub-conversions to achieve a lower current consumption.

      **Note:** Number of sub-conversions should be greater than or equal to 4.

   3. Calculate the decimation rate using **Equation 1**. The resolution increases with an increase in the decimation rate; therefore, set the maximum decimation rate achieved.

      **Equation 1. Decimation rate**

      ![](images/decimation-equation.png)

      **Note:** You cannot set the value of the decimation rate greater than 255. If the value of decimation rate from **Equation 2** is greater than 255, truncate it to 255.

   4. Load the parameters to the device and measure SNR as mentioned in steps 10 and 11 in the [Operation](#operation) section. Perform tuning until the minimum SNR of 5:1 and a signal count at least greater than 50 are achieved.

   5. Skip this step if the following conditions are met:

      - Measured SNR from the previous stage is greater than 5:1.

      - Signal count is greater than 50.

   If your system is very noisy (counts >20), do the following to enable filters:

   1. Open **CAPSENSE&trade; Configurator** from ModusToolbox&trade; Quick Panel and select the appropriate filter:

      **Figure 23. Filter settings in CAPSENSE&trade; Configurator**

      <img src="images/advanced-filter-settings.png" alt="Figure 23"/>

      **Notes:**
      - Add the filter based on the type of noise in your measurements. See [ModusToolbox&trade; CAPSENSE&trade; configurator guide](https://www.infineon.com/file/492896/download) for details.
      - The current example has an built-in CIC2 filter; therefore, it is recommended to enable the IIR filter.

   2. Reprogram the device to update the filter settings.

<br>

### Stage 4: CDAC dither parameters
-------------------------

MSCLP uses CDAC dithering to reduce flat spots. The optimal polynomial and other parameters depend on the number of sub-conversions (N<sub>sub</sub>).

The following macros show the recommended dither parameters in **main.c**:
```
#define	CDAC_DITHER_SCALE          0u

#define	CDAC_DITHER_SEED           255u

#define	CDAC_DITHER_POLY           142u
```

Table 4 shows the general recommended values of dither parameters based on N<sub>sub</sub> selection.

**Table 4.  General recommendations for dither parameters**

N<sub>sub</sub> Range | CDAC_Dither_poly| CDAC_Dither_Seed |  CDAC_Dither_scale
:--- | :--- | :--- | :---
8 to 12 | 9 | 15 | 1
13 to 15 | 9 | 15 | 0
16 to 23 | 18 | 31 | 1
24 to 31 | 18 | 31 | 0
32 to 41 | 33 | 63 | 1
42 to 63 | 33 | 63 | 0
64 to 84 | 65 | 127 | 1
85 to 127 | 65 | 127 | 0
128 to 174 | 142 | 255 | 1
175 to 255 | 142 | 255 | 0
\>255 | 142 | 255 | 0

<br>

### Stage 5: Tune threshold parameters
-------------------------


The software threshold is set for each widget based on the diff counts. Do the following in CAPSENSE&trade; Tuner to set up the threshold for a widget:

1. Switch to the **SNR Measurement** tab and select **Proximity0**.

2. Use the signal measured after getting the 5:1 SNR from Step 11 in the [Monitor data using CAPSENSE&trade; Tuner](#monitor-data-using-capsensetrade-tuner) section.

3. Set the thresholds according to the following recommendations:

   - Proximity threshold = 80 percent of the signal

   - Touch threshold = 80 percent of the touch signal

      **Note:** Here, the touch threshold denotes the threshold for the proximity sensor to detect a touch when it is touched by a finger. When the proximity sensor is touched, the sensor yields a higher signal compared the proximity signal; therefore, it is the **touch signal**. You can figure out the touch signal by repeating the Step 11 in the [Monitor data using CAPSENSE&trade; Tuner](#monitor-data-using-capsensetrade-tuner) section, by touching the sensor and measuring the signal.

   - Noise threshold = 40 percent of the signal

   - Negative noise threshold = 40 percent of the signal

   - Low baseline reset = 30

   - Hysteresis = 10 percent of the signal

   - ON debounce = 3

4. For the LowPower0_Sns0 sensor, switch to the **SNR Measurement** tab and follow steps 10 and 11 in the [Monitor data using CAPSENSE&trade; Tuner](#monitor-data-using-capsensetrade-tuner) section.

   After measuring the signal by placing the hand at the max distance, set the thresholds according to the following recommendations:

   - Finger threshold = 80 percent of the signal

   - Noise threshold = 40 percent of the signal

   - Negative noise threshold = 40 percent of the signal

   - Low baseline reset = 30

   - ON debounce = 1

   **Note:** It is recommended to have ON debounce as '1'. Because we are reading the status signal of the proximity widget instead of the low-power widget to turn ON and OFF the status LEDs. Therofore, we don't require the debounce feature for the low-power widget. However, this is application-specific, and users can update it according to their needs.

5. Set the threshold parameters in the **Widget/Sensor parameters** section of the CAPSENSE&trade; Tuner:

   **Figure 24. Widget threshold parameters**

   <img src="images/tuner-threshold-settings.png" alt="Figure 24"/>

6. Apply the settings to the device and to the project by clicking **To device** and then **To Project** as Figure 24 shows, and close the tuner. The change is updated in the *design.cycapsense* file and reflected in the CAPSENSE&trade; Configurator.

   **Figure 25. Apply to project setting**

   <img src="images/tuner-apply-settings.png" alt="Figure 25"/>

   If your sensor is tuned correctly, you will observe that the proximity status goes from 0 to 1 in the **Status** sub-window of the **Graph View** window as Figure 26 shows. The successful tuning of the proximity sensor is also indicated by LED3 in the kit; it turns ON when the hand comes closer than the maximum distance and turns OFF when the hand is moved away from the proximity sensor.

   **Figure 26. Sensor status in CAPSENSE&trade; Tuner showing proximity status**

   <img src="images/tuner-status.png" alt="Figure 26"/>

   Upon touching the proximity loop, a further change in status from 1 to 3 can be observed, which indicates a touch. Along with this, LED1 will turn ON in blue color.

   **Figure 27. Sensor status in CAPSENSE&trade; Tuner showing touch status**

   <img src="images/tuner-status-touch.png" alt="Figure 27"/>

8. Close the CAPSENSE&trade; Tuner and launch CAPSENSE&trade; Configurator. You should now see all the changes that you made in the CAPSENSE&trade; Tuner reflected in the CAPSENSE&trade; Configurator.

   **Table 5. Software tuning parameters obtained based on sense for CY8CKIT-040T**

   Parameter | Proximity0 | LowPower0|
   :-------- |:-----------|:---------
   Proximity signal | 481 |41 |
   Touch signal | 8960 | NA |
   Proximity threshold | 391 |33|
   Touch threshold | 7168 |NA |
   Noise threshold |196|16|
   Negative noise threshold |196 |16 |
   Low baseline reset | 30 |30 |
   Hysteresis | 49 |NA |
   ON debounce | 3|1|

   **Note:** For the low-power widget the touch threshold is the finger threshold.

   </details>

<br>


## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

**Note:** The debug port is disabled by default for CY8CKIT-040T, because it uses the pins P3[2] (SWDIO) and P3[3] (SWDCK) for User LED. If debug is required, enable the **Debug** setting under the **Systems** tab in the Device Configurator and change the **Debug Mode** setting to **SWD**. Because User LED mode is multiplexed on the same pins, the user LED will not blink when debug is enabled.

## Design and implementation

The project contains one proximity sensor configured as a regular widget and a low-power widget in CSD-RM sensing mode. See the [Tuning procedure](#tuning-procedure) section for step-by-step instructions to configure other settings of the **CAPSENSE&trade; Configurator**.

Upon successful tuning of the system, it will be able to detect your hand when your hand is in proximity detection range, and indicate the detection using LEDs.

There are two LEDs used in this project:

- *LED1*: Touch status. Turns ON in blue color when your finger touches the proximity sensor and turns OFF when you remove your finger.

- *LED3*: Proximity status. Turns ON in red color when your hand comes in the proximity detection range and turns OFF when the hand is moved away.

The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; user guide for more details on selecting a middleware). See [AN85951 - PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details on CAPSENSE&trade; features and usage.

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.

The MOSI pin of the SPI slave peripheral is used to transfer data to the three serially connected LEDs for controlling color, brightness, and ON or OFF operation. The three LEDs form a daisy-chain connection; the communication happens over the serial interface to create an RGB configuration. The LED accepts an 8-bit input code, with three bytes for red, green, and blue color, five bits for global brightness, and three blank '1' bits. See the [LED datasheet](https://media.digikey.com/pdf/Data%20Sheets/Everlight%20PDFs/12-23C_RSGHBHW-5V01_2C_Rev4_12-17-18.pdf) for more details.


### Set up the VDDA supply voltage and debug mode in Device Configurator

1. Open Device Configurator from the Quick Panel.

2. Go to the **System** tab. Select the **Power** resource, and set the VDDA value under **Operating conditions** as follows:

   **Figure 28. Setting the VDDA supply in the System tab of Device Configurator**

   <img src="images/vdda-settings.png" alt="Figure 28"/>

3. By default, SWD pins are active in all device power modes. Disable debug mode to disable SWD pins and thereby reduce the power consumption as follows:

   **Figure 29. Disable Debug mode in the System tab of Device Configurator**

   <img src="images/disable-swd.png" alt="Figure 29"/>


### Resources and settings

**Figure 30. EZI2C settings**

<img src="images/ezi2c-config.png" alt="Figure 30" width="800"/>

**Figure 31. SPI settings**

<img src="images/spi-config.png" alt="Figure 31" width="800"/>

**Table 6. Application resources**

 Resource  |  Alias/Object     |    Purpose     |
 :------- | :------------    | :------------ |
 SCB (I2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; Tuner |
 SCB (SPI) (PDL) | CYBSP_MASTER_SPI          | SPI master driver to control serial LEDs |
 CAPSENSE&trade; | CYBSP_MSC | CAPSENSE&trade; driver to interact with the MSC hardware and interface the CAPSENSE&trade; sensors |
 Digital pin | CYBSP_SERIAL_LED | To show the proximity operation and power mode states|

</details>

<br>

### Firmware flow

**Figure 32. Firmware flowchart**

<img src="images/firmware-flowchart.png" alt="Figure 32" width="800"/>

<br>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/dgdl/Infineon-AN79953_Getting_Started_with_PSoC_4-ApplicationNotes-v21_00-EN.pdf?fileId=8ac78c8c7cdc391c017d07271fd64bc1) – Getting started with PSoC&trade; 4
Code examples  | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub
Device documentation | [PSoC&trade; 4 datasheets](https://www.infineon.com/cms/en/search.html#!view=downloads&term=psoc4&doc_group=Data%20Sheet) <br />[PSoC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!view=downloads&term=psoc4&doc_group=Additional%20Technical%20Information)
Development kits | Select your kits from the [evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) page.
Libraries on GitHub  | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSoC&trade; 4 peripheral driver library (PDL) <br>  [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Middleware on GitHub  | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents <br> [psoc4-middleware](https://github.com/Infineon/psoc4-middleware) – Links to all PSoC&trade; 4 middleware
Tools | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices.

<br>

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE236033* – *PSoC&trade; 4: MSCLP CAPSENSE&trade; low-power proximity tuning*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example
 1.1.0   | Minor folder structure changes that doesn't break backward compatibility
 1.2.0   | Minor README and configuration update

 <br>

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2023. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br />
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br />
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit www.infineon.com. Other names and brands may be claimed as property of their respective owners.
