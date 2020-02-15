# Mappings

This section covers all the errors in Solidity related to mappings.

---

## Use of mapping type as parameter in a public function

|Heading|Description|
|-|-|
|**Title**|Use of mapping as parameter in a public function|
|**Type**|`TypeError`|
|**Message**|```Mapping types for parameters or return variables can only be used in internal or library functions.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

This error refers to a case where variable of `mapping` type is used as a function parameter in a `public` function. 

**Example**

```solidity
pragma solidity ^0.5.0;

contract MyContract {

    mapping(address => bool) votes;

    function resetVotes(mapping(address => bool) memory _votes_list) public pure {
        // code here
    }
}
```

**Solution**

In Solidity, a function can accept a parameter of `mapping` type only if its visibility is declared as `internal` or `private`.

```solidity
pragma solidity ^0.5.0;

contract MyContract {

    mapping(address => bool) votes;

    function resetVotes(mapping(address => bool) memory _votes_list) internal pure {
        // code here
    }
}
```

---

## Wrong data location for return statement in mapping

|Heading|Description|
|-|-|
|**Title**|Wrong data location for return statement in mapping|
|**Type**|`TypeError`|
|**Message**|```Mapping types can only have a data location of "storage" and thus only be parameters or return variables for internal or library functions.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract MyContract {

    function f() public pure returns(mapping(uint=>uint) memory) {}

}
```

**Solution**


---

## Attempt to create a `mapping` dynamically

|Heading|Description|
|-|-|
|**Title**|Attempt to create a `mapping` dynamically|
|**Type**|`TypeError`|
|**Message**|```Uninitialized mapping. Mappings cannot be created dynamically, you have to assign them from a state variable.```|
|**Solidity version**|Since 0.5.0|
|**Reference**|[TypeChecker.cpp, lines 913 - 917](https://github.com/ethereum/solidity/blob/508cf66da2bdfb7e6677029c9671a0f3ffec68b8/libsolidity/analysis/TypeChecker.cpp#L913-L917)|
|**Contributors**||


**Description**

This error in Solidity refers to a situation when a function attempts to create a `mapping` dynamically.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    function f() public pure { 
        mapping(uint=>uint) storage m; 
    }
    
}
```

**Solution**



-----

## Invalid use of dynamically-sized keys in mapping

|Heading|Description|
|-|-|
|**Title**|Invalid use of dynamically-sized keys in mapping|
|**Type**|`TypeError`|
|**Message**|```Dynamically-sized keys for public mappings are not supported.```|
|**Solidity version**|up to 0.5.4|
|**Reference**|[TypeChecker.cpp, line 520]()|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
	mapping(string => uint) public data;
	
}
```

**Solution**


-----

## Mappings cannot be assigned to

|Heading|Description|
|-|-|
|**Title**|Mappings cannot be assigned to|
|**Type**|`TypeError`|
|**Message**|```Mappings cannot be assigned to```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error in Solidity describes a case when we try to assign a mapping to another.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    mapping(uint=>uint) map;
    
    function error() public {
        
        mapping(uint=>uint) storage a = map;
        map = a;
        (map) = a;
        (map, map) = (a, a);
        
    }
    
}
```

**Solution**
