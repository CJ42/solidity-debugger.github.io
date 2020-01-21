# Storage & Memory

## Data location specified for wrong type

|Heading|Description|
|-|-|
|**Title**|Data location specified for wrong type|
|**Type**|`typeError`|
|**Message**|```Data location can only be specified for array, struct or mapping types, but "<storage / memory>" was given```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, Lines 381 - 382](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L381-L382)|
|**Contributors**|CJ42|


**Description**

A data location is specified for a wrong variable type.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    function test() public {
        uint memory number = 123;
    }
    
}
```

**Solution**

Remove the data location specifier.
