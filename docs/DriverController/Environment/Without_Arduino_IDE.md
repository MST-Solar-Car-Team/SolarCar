# Working Language Server with Arduino C++
  
 ## Disclaimer
 I'm sure you've noticed by now that every time you try to run your c++ language sever on the DriverController code, it freaks out. There is little to no documentation on how to work on Arduino code outside its IDE. **However**, the solution has been discovered, and is documented here. Before we begin, the following is assumed about your environment: 
 1. Your IDE is using clangd for your language server 
 2. Clangd is configured to look for config files (this can be done with the `--enable-config` flag) 
 3. You have basic knowledge of your current working environment (I will not be going into details for configuring individual IDEs)
 
 
## Setup

First thing you need to do is `git clone` all the dependencies into some centralised location (I use `/usr/local/lib` for mine). As of now, these are the project dependencies:
- https://github.com/arduino/ArduinoCore-sam.git (Ardunio Sam Boards SDK)
- https://github.com/collin80/due_can.git (Due_CAN for CAN network communication)
- https://github.com/collin80/can_common.git (Dependency of Due_CAN)

Now that you have those installed, you need go into the root of the DriverController project and create a file called `.clangd`. Which will contain the following:

```yaml
CompileFlags: 
  Add:
    - "-D__SAM3X8E__"
    - "-ferror-limit=0"
    # Arduino dependency setup
    - "-I/usr/local/lib/ArduinoCore-sam/cores/arduino/"
    - "-I/usr/local/lib/ArduinoCore-sam/system/libsam/"
    - "-I/usr/local/lib/ArduinoCore-sam/variants/arduino_due_x/"
    - "-I/usr/local/lib/ArduinoCore-sam/system/CMSIS/CMSIS/Include/"
    - "-I/usr/local/lib/ArduinoCore-sam/system/CMSIS/Device/ATMEL/"
    - "-I/usr/local/lib/ArduinoCore-sam/system/CMSIS/Device/ATMEL/sam3xa/include/component"
    # Due can setup
    - "-I/usr/local/lib/due_can/src/"
    - "-I/usr/local/lib/can_common/src/"
```
So what is actually happening in this file? You can see the dependency's you installed are being included into compiler (remember to switch out `/usr/local/lib` with the path of your dependencies). But additionally, two other flags are present. `-ferror-limit=0` will force the compiler to give you all the errors instead of capping it at a certain point. And `-D__SAM3X8E__`tells the Arudino SDK what board you're using. Currently we use an Arduino Due, and you can see its based off of the **Atmel SAM3X8E ARM Cortex-M3 CPU** on the product [page](https://docs.arduino.cc/hardware/due/). So thats why that flag is required.

## Yippe
Your Language Sever hopefully works now. Now you can code and get useful feedback instead of being told all your functions don't exist :)
	

