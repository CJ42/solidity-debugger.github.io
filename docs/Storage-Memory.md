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

-----

## Uninitialized storage pointer

|Heading|Description|
|-|-|
|**Title**||
|**Type**|`DeclarationError` (since 0.5.12)|
|**Message**|```Uninitialized storage pointer.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

This type of error occurs with variables of type `mapping`, `struct` or `array`.

When such variable is 1) a local variable (defined within a function), and 2) a reference pointer to a state variable (storage variable, defined with the keyword `storage` for data location).

The error occurs because the state variable is uninitialized.

The example below, taken from b9lab blog is self explanatory.

**Example**

```
pragma solidity ^0.4.0;

contract FirstSurprise {
 
 struct Camper {
   bool isHappy;
 }
 
 mapping(uint => Camper) public campers;
 
 function setHappy(uint index) public {
   campers[index].isHappy = true;
 }
 
 function surpriseOne(uint index) public {
   Camper storage c;
   c.isHappy = false;
 }
}
```

**Solution**

Initialized the variable within the constructor, or before the `storage` reference occurs.

**Reference**

- https://blog.b9lab.com/storage-pointers-in-solidity-7dcfaa536089

- https://github.com/ethereum/solidity/blob/develop/test/libsolidity/syntaxTests/nameAndTypeResolution/211_uninitialized_mapping_array_variable.sol