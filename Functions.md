# Function Names
Function names are written in camelCase starting with a lower case letter.

Try to be precise without repeating yourself. For example if you provide a
function to send a `CanFrame` just call it `send` instead of `sendCanFrame`.
The signature tells the user that this function sends a `CanFrame`.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void shutdownEcu();

class CanTransceiver
{
public:
    ErrorCode send(const CanFrame& frame);

    static bool addGlobalListener(
        ICanFrameListener& listener);
};

</pre></td><td><pre lang="cpp">

void ShutdownEcu();

class CanTransceiver
{
public:
    ErrorCode SendFrame(const CanFrame& frame);

    static bool AddGlobalListener(
        ICanFrameListener& listener);
};

</pre></td></tr>
</table>

## Boolean Functions
If a function returns a boolean value which is not intended to signal success
or failure of the function call, the function should start with _is_ or _has_.
Boolean member functions tend to be `const`.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

bool isEcuInSleepMode();

class CanTransceiver
{
public:
    bool hasWakeupOccurred() const;
};

</pre></td><td><pre lang="cpp">

bool sleepModeActive();

class CanTransceiver
{
public:
    bool wakeupOccurred();
};

</pre></td></tr>
</table>

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
