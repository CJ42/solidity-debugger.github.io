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

## Named arguments in type conversion not allowed

|Heading|Description|
|-|-|
|**Title**|Named arguments in type conversion not allowed|
|**Type**|`TypeError`|
|**Message**|```Type conversion cannot allow named arguments.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, lines...]()|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.6.0;

contract BadExample {
    
    function f() public {
        
        uint({arg:1});
    
        
    }
    
}
```

**Solution**



-----

## Exactly one argument expected for explicit type conversion.

|Heading|Description|
|-|-|
|**Title**|Exactly one argument expected for explicit type conversion.|
|**Type**|`TypeError`|
|**Message**|```Exactly one argument expected for explicit type conversion.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
uint256 _a = uint();
```

**Solution**

