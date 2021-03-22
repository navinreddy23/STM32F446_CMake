# STM32F446_CMake with Qt Creator

This repository is created to experiment with CMake and STM32F4 microcontroller. This project describes the steps needed to integrate a microcontroller project with Qt Creator.

If Qt Creator is your favourite IDE for editing the code, why not use it for debugging!

STM32Cube Package is used for generating the HAL and CMSIS libraries: https://www.st.com/en/embedded-software/stm32cube-mcu-mpu-packages.html

## Build instruction - Command line

create a build directory from the root of this repository and execite the build commmands.

### Makefile build - Command line

Generate makefile using: 
`cmake ..`

Compile and generate ELF, HEX, and BIN using:
`make`

### Ninja build - Command line
Generate ninja build using: 
`cmake -GNinja ..`
Compile and generate binaries using: 
`ninja`

## Using Qt Creator to Build and Debug the project. 

### **Step 1**: 
This project uses CMakeLists, therefore the project can be directly imported into Qt Creator using File -> New FIle or Project -> Git Clone.


![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/001_ImportFromGit.png)



### **Step 2:** Clone this repository and select the **QtCompatible** branch.


![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/002_Select_Qt_Branch.png)



### **Step 3**: Select the _OpenOCD_ Run and Debugging Kit and click _Configure Project_.
The configuration for OpenOCD is described in later steps.



![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/003_Select_Debugger_Kit.png)


### **Step 4**: The project automatically loads (if CMake is set to _Run_ automatically on changes). 
There can be **errors** due to the **toolchain path**. 
In that case, set the toolchain path in the top level CMakeLists.txt manually.


![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/004_Project_Loads_into_Qt.png)


### **Step 5**: Press _**Ctrl-B**_ to build the project. 
If the build is successful, the binary size is displayed under _Compile Output_ view.

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/005_Press_CtrlB_to_Build.png)

### **Step 6**: Press **Ctrl-R** to _**flash**_ the binary and _**debug**_ it. 
If no breakpoints are set, you should see the main board LED blinking on the _**NUCLEO-F446RE**_ board. 

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/006_Press_Ctrl%2BR_to_Run.png)


## OpenOCD Kit Configuration

### Step 0: Add Bare-Metal plugin
If the bare-metal plugin was not installed, then it needs to be installed first. 
Go to Help -> About Plugins -> Device Support. Check and install BareMetal plugin. 
Requires restart of Qt Creator to get it working. 

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/014_Add_BareMetal_Plugin.png)

### Step 1: Add OpenOCD config.
Click on Add button and make necessary configurations for your device. In this project ST-LINK V2-1 is used with STM32F4x Microcontroller. 
The OpenOCD configuration is `openocd -f /usr/share/openocd/scripts/interface/stlink-v2-1.cfg -f /usr/share/openocd/scripts/target/stm32f4x.cfg`.

The additional arguments field contains: `-f /usr/share/openocd/scripts/target/stm32f4x.cfg`

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/007_OpenOCD_Config.png)


### Step 2: Add OpenOCD configuration to the BareMetal list.
![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/008_Add_OpenOCD_to_BareMetal_List.png)

### Step 3: Configure the Debugger 

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/009_Debugger_Config.png)

### Configure GDB Extended

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/010_Debugger_Config2.png)

### Step 4: Add ARM GCC and G++ compiler to the manual configurations.

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/011_Add_ARM_GCC_G%2B%2B_compilers.png)

### Step 5: Add ARM-GDB Python compiler to the manual configuration. 

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/012_Add_ARM_GDB_Python_DebugServer.png)

### Step 6: Finally add the OpenOCD Kit and make necessary changes.

![alt text](https://github.com/navinreddy23/STM32F446_CMake/blob/main/Qt_OpenOCD_screenshots/013_OpenOCD_Kit_Config.png)





