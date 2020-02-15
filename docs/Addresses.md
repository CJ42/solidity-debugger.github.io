# Addresses

## Wrong address specifier

|Heading|Description|
|-|-|
|**Title**|Wrong address specifier|
|**Type**|`typeError`|
|**Message**|```Address types can only be payable or non-payable.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, Lines 138 - 141](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L138-L141)|
|**Contributors**|CJ42|


**Description**

Happen when you specify the keyword `view` or `pure` in front of an `address`.
In Solidity, a variable of `address` type can only be specified as `payable` or not.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    address pure owner;
}
```

**Solution**

Remove the keyword `view` or `pure` in your variable declaration.

-----

## Explicit conversion from non-payable address to contract with payable fallback function

|Heading|Description|
|-|-|
|**Title**|Explicit conversion from non-payable address to contract with payable fallback function|
|**Type**|`TypeError`|
|**Message**|```Explicit type conversion not allowed from non-payable "address" to [Contract type variable], which has a payable fallback function.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, lines...]()|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.10;

contract BadExample {
    
  function f() public pure returns (C c) {
    address a = address(2);
    c = C(a);
  }
  
  function() external payable {
    // some code here
  }
  
}

```

**Solution**