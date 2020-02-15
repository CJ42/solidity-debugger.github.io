# Variables

This section covers most of the errors and warnings related to variables in Solidity. You will find a lot of examples of errors messages especially related to variables declared as `constant`.

## Unused local variable

|Heading|Description|
|-|-|
|**Title**|Unused local variable|
|**Type**|`warning`|
|**Message**|```Unused local variable```|
|**Solidity version**||
|**Reference**|[StaticAnalyser.cpp, Line 127](https://github.com/ethereum/solidity/blob/efd8d8fe5eced023476af71491e9eae3dbde4d87/libsolidity/analysis/StaticAnalyzer.cpp#L127)|
|**Contributors**|CJ42|


**Description**

**Example**

```solidity
function birthday(uint8 _age) public pure returns (uint8) {
    uint8 new_age = _age++;
    return _age++;
}

```

**Solution**



---

## Uninitialized constant variable

|Heading|Description|
|-|-|
|**Title**|Uninitialized constant variable|
|**Type**|`typeError`|
|**Message**|```Uninitialized constant variable```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**|CJ42|


**Description**

A variable is declared with the keyword `constant` inside your contract but does not have any value assigned to it.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply;

}
```

**Solution**

Assign a value to your variable declared as `constant`

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply = 21_000_000;

}
```

---

## Constant variable declared with a non compiled-time value.

|Heading|Description|
|-|-|
|**Title**|Constant variable declared with a non compiled-time value.|
|**Type**|`typeError`|
|**Message**|```Initial value for constant variable has to be compile-time constant.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**|CJ42|


**Description**

A variable is declared as `constant` inside your contract but the value assigned to it is invalid (dynamic, not compiled-time).

In Solidity, a constant variable is hardcoded inside the bytecode (not allocated to storage).

**Example**

In this example, the `msg.sender` value is invalid.

```solidity
pragma solidity ^0.5.0;

contract Example {

    address constant _address1 = msg.sender;

}
```

**Solution**

Assign a literal value to your `constant` variable. To use our previous example (so in the case of an `address constant`), write directly the address in hexadecimal inside your contract.

```solidity
pragma solidity ^0.5.0;

contract Example {

    address constant _address1 = 0xc0ffee254729296a45a3885639AC7E10F9d54979;

}
```

---

## Variable of non-value type declared as constant

|Heading|Description|
|-|-|
|**Title**|Variable of non-value type declared as constant|
|**Type**|`TypeError`|
|**Message**|```Constants of non-value type not yet implemented.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Line 461](https://github.com/ethereum/solidity/blob/508cf66da2bdfb7e6677029c9671a0f3ffec68b8/libsolidity/analysis/TypeChecker.cpp#L461)|
|**Contributors**|CJ42|


**Description**



**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {

    uint8[5] constant _array = [1, 2, 3, 4, 5];
    
}
```

**Solution**

---


## Constant keyword defined inside function

|Heading|Description|
|-|-|
|**Title**|Constant keyword defined inside function|
|**Type**|`declarationError`|
|**Message**|```The "constant" keyword can only be used for state variables.```|
|**Solidity version**||
|**Reference**|ReferencesResolver.cpp, [Lines 339 - 350](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L349-L350)|
|**Contributors**|CJ42|


**Description**

A variable with the `constant` keyword is defined inside a function.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    function test() public {
        uint8[3] memory constant _array = [1, 2, 3];
    }
    
}
```

**Solution**

---


## Cyclic constant definition

|Heading|Description|
|-|-|
|**Title**|Cyclic constant definition|
|**Type**|`FatalTypeError`|
|**Message**|```Cyclic constant definition (or maximum recursion depth exhausted).```|
|**Solidity version**|since 0.4.19|
|**Reference**|[ConstantEvaluator.cpp, lines 84-85](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ConstantEvaluator.cpp#L84-L85)|
|**Contributors**||


**Description**

Solidity version 0.4.19 introduces a new mechanism that detects large cyclic dependencies in variables and structs. Cyclic dependencies are limited to 256 bits since this version.

**Example**

```
pragma solidity >=0.4.16 <0.7.0;

contract C {
    uint constant L2 = LEN - 10;
    uint constant L1 = L2 / 10;
    uint constant LEN = 10 + L1 * 5;
    function f() public {
        uint[LEN] a;
    }
}
```

Here is an other example where the error gets generated

```
pragma solidity >=0.4.16 <0.7.0;

contract C {
    uint constant LEN = LEN;
    function f() public {
        uint[LEN] a;
    }
}
```



**Solution**


**References**

- https://github.com/trufflesuite/truffle/issues/135

-----

## Variable type cannot be `library`

|Heading|Description|
|-|-|
|**Title**|Variable type cannot be `library`|
|**Type**|`TypeError`|
|**Message**|```The type of a variable cannot be a library.```|
|**Solidity version**|since 0.5.13|
|**Reference**|TypeChecker.cpp, line 473|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

library A {
 
}


contract B {
    
    A my_contract;
    
}
```

**Solution**

