
# Type Type

## Wrong number of arguments provided to `type()`

|Heading|Description|
|-|-|
|**Title**|Wrong number of arguments provided to `type()`|
|**Type**|`TypeError`|
|**Message**|```"This function takes one argument, but <number of arguments> were provided."```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 209](https://github.com/ethereum/solidity/blob/efd8d8fe5eced023476af71491e9eae3dbde4d87/libsolidity/analysis/TypeChecker.cpp#L209)|
|**Contributors**||


**Description**

**Example**

**Solution**


```
pragma solidity ^0.6.0;

contract D {
    
}

contract C {
  
  function g() public pure returns (string memory) {
      string memory contract_name = type(D, 3);
      return contract_name;
  }
  
}
```

-----

## `contract` type expected for `type()`

|Heading|Description|
|-|-|
|**Title**|`contract` type expected for `type()`|
|**Type**|`TypeError`|
|**Message**|```"Invalid type for argument in function call. Contract type required, but <...> provided."```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract A {
    
}

contract B {
    
    function test() public returns (bytes memory) {
        return type(uint).creationCode;
    }
}
```

**Solution**

