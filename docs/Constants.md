[Main Page](../README.md)

# Table of contents
* [Constants](Constants.md#constants)

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


