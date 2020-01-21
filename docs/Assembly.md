# Assembly

## Cannot access local Solidity variable inside inline Assembly

|Heading|Description|
|-|-|
|**Title**|Cannot access local Solidity variable inside inline Assembly|
|**Type**|`declarationError`|
|**Message**|```Cannot access local Solidity variables from inside an inline assembly function.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 312 - 316](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L312-L316)|
|**Contributors**||


**Description**

This error happen when attempting to access a solidity local variable defined outside of an assembly function.

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
    function test() public pure {
        
        uint default_value = 234;
        
        assembly {
            function assembly_test( value ) -> result {
                switch value
                case 0 { result := 0 }
                case 1 { result := 1 }
                default { result := default_value }
            }
        }
        
    }
    
}
```

**Solution**


**References**

- https://solidity.readthedocs.io/en/v0.5.11/assembly.html#functions


-----

## Forbidden use of `_slot` or `_offset` as variable names.

|Heading|Description|
|-|-|
|**Title**|Forbidden use of `_slot` or `_offset` as variable names.|
|**Type**|`DeclarationError`|
|**Message**|```In variable names _slot and _offset can only be used as a suffix.```|
|**Solidity version**|up to 0.5.12|
|**Reference**|[ReferencesResolver.cpp, lines 297 - 301](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L297-L301)|
|**Contributors**||


**Description**


**Example**

```
pragma solidity 0.5.0;

contract C {
    function f() public pure {
        assembly {
            _offset
        }
    }
}
```

**Solution**

**References**

- https://github.com/second-state/lity/blob/master/test/libsolidity/syntaxTests/inlineAssembly/storage_reference_empty_offset.sol
- https://github.com/second-state/lity/blob/master/test/libsolidity/syntaxTests/inlineAssembly/storage_reference_empty_slot.sol


-----

## Multiple Matching identifiers during resolving in Assembly

|Heading|Description|
|-|-|
|**Title**|Multiple Matching identifiers during resolving in Assembly|
|**Type**|`DeclarationError`|
|**Message**|```Multiple matching identifiers. Resolving overloaded identifiers is not supported.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 304 - 308](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L304-L308)|
|**Contributors**||


**Description**

**Example**

```
contract C {
    
    function f() pure public {}
    function f(address) pure public {}
    function g() pure public {
        assembly {
            let x := f
        }
    }
}
```

**Solution**


-----

## Constant variables not supported by inline Assembly

|Heading|Description|
|-|-|
|**Title**|Constant variables not supported by inline Assembly|
|**Type**|`TypeError`|
|**Message**|```Constant variables not supported by inline assembly.```|
|**Solidity version**|From 0.5.0 to 0.5.10|
|**Reference**|[TypeChecker.cpp, line 634]()|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract BitcoinToken {
    
    uint constant bitcoin_supply = 21_000_000;
    
    function calculateMarketCap(uint bitcoin_price) public pure {
        
        assembly {
            let market_cap := mul(bitcoin_price, bitcoin_supply)    
        }
        
    }
}
```

**Solution**


-----

## Storage variables cannot be assigned to

|Heading|Description|
|-|-|
|**Title**|Storage variables cannot be assigned to.|
|**Type**|`TypeError`|
|**Message**|```Storage variables cannot be assigned to.```|
|**Solidity version**|Up to 0.5.16|
|**Reference**|[TypeChecker.cpp, line ...]()|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
    uint[] x;
    
    function() external {
        uint[] storage y = x;
        assembly {
            y_slot := 1
            y_offset := 2
        }
    }
    
}
```

**Solution**