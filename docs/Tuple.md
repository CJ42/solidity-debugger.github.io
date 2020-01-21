# Tuples

## Compound assignment not allowed for tuple type.

|Heading|Description|
|-|-|
|**Title**|Compound assignment not allowed for tuple type.|
|**Type**|`TypeError`|
|**Message**|```Compound assignment is not allowed for tuple types.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 1208](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L1208)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract C {
    function f() public returns (uint a, uint b) {
        (a, b) += (1, 1);
    }
}
```

**Solution**


---

## Tuple Component cannot be empty

|Heading|Description|
|-|-|
|**Title**|Tuple Component cannot be empty|
|**Type**|`FatalTypeError`|
|**Message**|```Tuple component cannot be empty.```|
|**Solidity version**|Since 0.4.3|
|**Reference**|[TypeChecker.cpp, line 1275](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L1275)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.4.3;

contract Test {
    function a() public {
        ( a(), 7);
    }
}
```

**Solution**
