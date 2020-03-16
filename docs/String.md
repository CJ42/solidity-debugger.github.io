# String


# Index access not possible with `string` type

|Heading|Description|
|-|-|
|**Title**|Index access not possible with `string` type|
|**Type**|`TypeError`|
|**Message**|```Index access for string is not possible.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Exmple {
    
    function createString() public pure returns (string memory) {
        string memory new_string = new string(3);
        new_string[0] = "H";
        new_string[1] = "E";
        new_string[2] = "L";
        new_string[3] = "L";
        new_string[4] = "0";
        return new_string;
    }
    
}
```

**Solution**

You might find the stringUtils library from Nick Johnson useful for this purpose.