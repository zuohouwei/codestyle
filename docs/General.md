[Main Page](README.md)

# Table of contents
* [Functions](#Functions)
* [Constants](#Constants)
* [Variables](#Variables)
* [Includes](#Includes)


# Functions

# Constants
Constants including `enum` values are written all UPPER_CASE with underscore
word separation.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

enum PhyAddress
{
    PHY_0,
    PHY_1    
};

class CanTransceiver
{
public:
    static const
    uint32_t BAUDRATE_HIGH_SPEED = 500000U;    
};

</pre></td><td><pre lang="cpp">

enum PhyAddress
{
    phy0,
    phy1    
};

class CanTransceiver
{
public:
    static const
    uint32_t BaudrateHighSpeed = 500000U;    
};

</pre></td></tr>
</table>

## Summary
:white_check_mark: Constants are all UPPER_CASE

# Variables

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
