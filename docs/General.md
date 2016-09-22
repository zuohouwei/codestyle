[Main Page](README.md)

# Table of contents
* [Const Corectness](#Const Corectness)
* [Constants](#Constants)
* [Variables](#Variables)
* [Includes](#Includes)
* [Functions](#Functions)
* [Comments](#Comments)


## Const Corectness
Const should be used wherever possible. It makes an interfaces easier to use and offers potential for optimization to the compiler.

## Constants
Constants including `enum` values are written all UPPER_CASE with underscore
word separation.

### Example
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

### Summary
:white_check_mark: Constants are all UPPER_CASE

## Variables

## Includes

The style used to specify an include shall reflect the locality of the included header file.

1. All includes which are part of the module the including header file is part of shall use quotes *""*
2. All includes which are not part of the module the including header (exterrnal includes) file is part of shall use angle brackets *<>*

### Example
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
### Summary
:white_check_mark: for module internal includes use quotes *""*

:white_check_mark: for module external includes use angle brackets *<>*

## Functions

## Comments
Comments

Generally speaking, there shouldn't be many comments in source files. If you have to write comments for a piece of code, consider rewriting it so that it is easier to understand. Extracting inlined functions with speaking names might be one possible approach.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class Timeout 
{
    public:

    static const uint8_t MAX_TIMEOUT_IN_MS = 128U; 
    
    ...
}

</pre></td><td><pre lang="cpp">

class Timeout 
{
    public:

    static const uint8_t MAX_TIMEOUT = 128U; // unit is miliseconds
    
    ...
}

</pre></td></tr>
</table>
**
### Summary
:white_check_mark: try to encode all important information in the source code itself.

