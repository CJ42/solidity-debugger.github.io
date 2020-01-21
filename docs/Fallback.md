# Fallback function

## Fallback function declared twice

|Heading|Description|
|-|-|
|**Title**|Fallback function declared twice|
|**Type**|`declarationError`|
|**Message**|`Only one fallback function is allowed`|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 74 - 80](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L74-L80)|
|**Contributors**|CJ42|


**Description**

The contract contains two fallback functions.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    function() external {
        
    }
    
    function() external {
        
    }

}
```

**Solution**

Keep only one fallback function.


---

## State mutability specified in Fallback function

|Heading|Description|
|-|-|
|**Title**|State mutability specified in Fallback function|
|**Type**|`typeError`|
|**Message**|```Fallback function must be payable or non-payable, but is < view / pure >```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 388 - 394](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L388-L394)|
|**Contributors**|CJ42|


**Description**

The contract specifies a fallback function with a state mutability of either `view` or `pure`. This is not allowed.

Fallback functions in Solidity can only contain the attribute `payable` (if ether have to be handled).

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    function() external pure {
        
    }
    
}
```

**Solution**

Remove the keyword `view` or `pure` from your fallback function definition.

**References**

- https://github.com/second-state/lity/blob/master/test/libsolidity/syntaxTests/fallback/pure_modifier.sol
- https://github.com/second-state/lity/blob/master/test/libsolidity/syntaxTests/fallback/view_modifier.sol

---

## Parameters specified in the fallback function

|Heading|Description|
|-|-|
|**Title**|Parameters specified in the fallback function|
|**Type**|`typeError`|
|**Message**|```Fallback function cannot take parameters.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 395 - 396](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L395-L396)|
|**Contributors**|CJ42|


**Description**

The fallback function of your contract specifies parameters. This is not allowed.
Fallback functions in Solidity cannot contain parameters.

**Example**

```solidity
pragma solidity ^0.5.10;

contract SweepStake {
    
    function(uint _value) external {
        
    }
    
}
```

**Solution**

Remove any parameter from your fallback function.

---

## Return value specified in Fallback function

|Heading|Description|
|-|-|
|**Title**|Return value specified in Fallback function|
|**Type**|`typeError`|
|**Message**|```Fallback function cannot return values.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 397 - 398](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L397-L398)|
|**Contributors**|CJ42|


**Description**

The fallback functions of your contract specifies a return value. This is not allowed.
In Solidity, fallback functions cannot return value.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    function() external returns (bool) {
        
    }
    
}
```

**Solution**

Remove the `returns` statement from your fallback function definition.

---

## Unvalid Fallback Function visibility

|Heading|Description|
|-|-|
|**Title**|Unvalid Fallback Function visibility|
|**Type**|`typeError`|
|**Message**|```Fallback function must be defined as "external".```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 399 - 400](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L399-L400)|
|**Contributors**|CJ42|


**Description**

The contract contains a fallback function with a visibility other than `external`.
In Solidity, fallback functions cannot be declared as `public`, `private` or `internal`.

As describe in the Solidity documentation, a fallback function :

> ...is executed on a call to the contract if none of the other functions match the given function identifier (or if no data was supplied at all).

**Example**

```
pragma solidity ^0.5.10;

contract Example {
    
    function() public {
        
    }

}
```

**Solution**

Remove the wrong visibility specified and simply declare your fallback function as `external`.

---


