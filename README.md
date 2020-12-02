What is in this repository
===
This repository contains Verilog files that have been modified to enable Watchdog LED Feedback Interface on the da Vinci Research Kit. This feature will show up in the upcoming firmware release [Rev 7.0](https://github.com/jhu-cisst/mechatronics-firmware/wiki/FPGA-Firmware-Release-Notes). 

**Implementation:**
One green LED and one red LED is used for this interface. Seven LED flashing modes are implemented according to the user-defined watchdog period: 

-   ``2Hz red``: watchdog is disabled, equivalent to setting a period of 0ms.
-   ``constant green``: watchdog period between 0ms to 50ms.
-   ``2Hz green``: watchdog period between 50ms to 100ms.
-   ``1Hz green``: watchdog period between 100ms to 150ms.
-   ``0.5Hz green``: watchdog period between 150ms to 200ms.
-   ``green off``: watchdog period larger than 200ms, unsafe watchdog period.
-   ``constant red``: watchdog timeout, communication between PC and FPGA board is unhealthy.
-   ``red off``: watchdog period defined within the safe range and no timeout exists.

Variable ``wdog_timeout_led`` in the ``BoardReg.v`` file signals ``CtrlLED.v`` of a detected timeout case. Variable ``wdog_period_status`` in the ``BoardReg.v`` file carries current watchdog period, which determines which flashing frequency should be used for the green LED or red LED.

**Files:**
- ``CtrlLED.v``: Main file that controls LED flashing mode. 
- ``BoardReg.v``: File contains the watchdog module and sends watchdog feedback to ``CtrlLED.v``.
- ``Constants.v``: File contains constants for different watchdog period.
- ``FPGA1394-QLA.v``: Top-level module controls the Firewire-1394 QLA board. 
- ``FPGA1394Eth-QLA.v``: Top-level module controls the Firewire-1394 QLA board with Ethernet port feature enabled.  

Please refer to this official repository of [dVRK mechatronics firmware](https://github.com/jhu-cisst/mechatronics-firmware) for more information about the da Vinci Research Kit.
