# Type Conversions


## Invalid type for argument in function call

|Heading|Description|
|-|-|
|**Title**|Invalid type for argument in function call|
|**Type**|`TypeError`|
|**Message**|```Invalid type for argument in function call. Invalid implicit conversion from [type1] to [type2] requested.```|
|**Solidity version**||
|**Reference**|[_TypeChecker.cpp_, Line ...](#)|
|**Contributors**|CJ42|


**Description**


**Example**
```solidity
pragma solidity ^0.5.0;

contract Example {
    
    string _age_in_string = "25";
    
    function HappyBirthday(uint8 _age) public pure returns (uint8) {
        return _age + 1;
    }
    
    function NotWorking() public pure {
        HappyBirthday(_age_in_string);
    }
}
```

**Solution**

-----