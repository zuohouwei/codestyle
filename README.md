# E.S.R.Labs C++ Code Style
Code style is a matter of personal taste and discussions about it tend to become emotional. In order to prevent religious wars, we define an E.S.R.Labs set of style rules.

##### Table of Contents  
* [Tabs vs. Spaces](TabsVsSpaces.md)
* [Files](Files.md)
* [Functions](Functions.md)  
* [Classes](Classes.md)  
* [Namespaces](Namespaces.md)  
* [Variables](Variables.md)
* [Constants](Constants.md)
* [Include Guards](#include-guards)


## Global, Local, Parameter Names

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode mode,
    ::lifecycle::Manager* pManager)
{
    ::lifecycle::Manager::TransitionResult result =
        ::lifecycle::Manager::TransitionResult::NONE;
}

</pre></td><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode Md,
    ::lifecycle::Manager* ptr_mgr)
{
    ::lifecycle::Manager::TransitionResult r =
        ::lifecycle::Manager::TransitionResult::NONE;
}
</pre></td></tr>
</table>


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

# Includes
The style used to specify an include shall reflect the locality of the included header file.

1. All includes which are part of the module the including header file is part of shall use quotes *""*
2. All includes which are not part of the module the including header (exterrnal includes) file is part of shall use angle brackets *<>*

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

//File: include/logger/BufferedLoggerOutput.h

#include &lt;estd/forward_list.h&gt;
#include &lt;util/logger/IComponentMapping.h&gt;
#include &lt;util/logger/ILoggerOutput.h&gt;
#include "logger/IEntryOutput.h"
#include "logger/ILoggerListener.h"
#include "logger/ILoggerTime.h"
#include "logger/EntryBuffer.h"
#include "logger/EntrySerializer.h"

</pre></td><td><pre lang="cpp">

//File: include/logger/BufferedLoggerOutput.h

#include "estd/forward_list.h"
#include "util/logger/IComponentMapping.h"
#include "util/logger/ILoggerOutput.h"
#include "logger/IEntryOutput.h"
#include "logger/ILoggerListener.h"
#include "logger/ILoggerTime.h"
#include "logger/EntryBuffer.h"
#include "logger/EntrySerializer.h"

</pre></td></tr>
</table>
**
## Summary
:white_check_mark: for module internal includes use quotes *""*

:white_check_mark: for module external includes use angle brackets *<>*
