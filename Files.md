# File Names
Files that contain classes should contain only one class. The header and
source file are named like the class **MyClass.h** and **MyClass,cpp**.
The extension for C++ source files is *.cpp*, the extension for C source files
is *.c*, the extension for assembly files is *.s*. Header files have the
extension *.h* no matter which content. Sometimes you might find *.hpp* files
that contain implementation source code of class templates.

# Include Guards
Include guards shall prevent code from being processed multiple times which
would cause compilation errors. There are two forms of allowed include guards:
1. All capital letter path beginning after the *include* folder separated by  
   underscore and terminated by *_H_*.
2. A unique identifier like *HE793FCD8_FC04_45D3_A438_533341BBA7B1*

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">
//File: include/can/CanTransceiver.h

#ifndef CAN_CANTRANSCEIVER_H_
#define CAN_CANTRANSCEIVER_H_

#endif /* CAN_CANTRANSCEIVER_H_ */

//File: include/bsp/ethernet/Bcm89811.h

#ifndef HE793FCD8_FC04_45D3_A438_533341BBA7B1
#define HE793FCD8_FC04_45D3_A438_533341BBA7B1

#endif /* HE793FCD8_FC04_45D3_A438_533341BBA7B1 */
</pre></td><td><pre lang="cpp">
//File: include/can/CanTransceiver.h

#ifndef CANTRANSCEIVER_H_
#define CANTRANSCEIVER_H_

#endif /* CANTRANSCEIVER_H_ */

//File: include/bsp/ethernet/Bcm89811.h

#ifndef HE793FCD8_FC04_45D3_A438_533341BBA7B1
#define HE793FCD8_FC04_45D3_A438_533341BBA7B1

#endif
</pre></td></tr>
</table>
**
## Summary
:white_check_mark: Include guard is all UPPER_CASE file name + path

:white_check_mark: Include guard is unique identifier
