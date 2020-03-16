# Interfaces

This section covers all the errors in Solidity related to interfaces

---

## Interface inheritance not allowed

|Heading|Description|
|-|-|
|**Title**|Interface inheritance not allowed|
|**Type**|`TypeError`|
|**Message**|```Interfaces cannot inherit.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

This error statement describes the case where an `interface` contract attempts to inherit from another contract.

**Example**

```solidity
pragma solidity ^0.5.0;

contract MyContract {

    // contract code here

}

interface MyInterface is MyContract {

    // interface code here

}
```

**Solution**

Only a contract can inherit from `interface`, not the other way around. See below :

```solidity
pragma solidity ^0.5.0;

interface MyInterface {

    // interface code here

}

contract MyContract is MyInterface {

    // contract code here

}
```

---

## Function implemented inside an interface

|Heading|Description|
|-|-|
|**Title**|Function implemented inside an interface|
|**Type**|`TypeError`|
|**Message**|```Functions in interfaces cannot have an implementation.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

This error describes a function that is implemented (contains a body) inside an `interface` contract.

**Example**

```solidity
pragma solidity ^0.5.0;

interface MyInterface {

    function myFunction(uint _a) external {
        // some code here
    }
}
```

**Solution**

Functions declared inside `interfaces` cannot have an implementation. You must then remove the curly braces `{}` and end your function statement with a semicolon `;`.

```solidity
pragma solidity ^0.5.0;

interface MyInterface {

    function myFunction(uint _a) external;

}
```

## Function visibility other than `external` inside an interface

|Heading|Description|
|-|-|
|**Title**|Function visibility other than `external` inside an interface|
|**Type**|`TypeError`|
|**Message**|```Functions in interfaces must be declared external.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

This error in Solidity specifies that a function inside an `interface` has a visibility other than `external`

**Example**

The example and solution below is directly taken from the [Solidity Documentation](https://solidity.readthedocs.io/en/v0.5.11/contracts.html#interfaces).

```solidity
pragma solidity >=0.5.0 <0.7.0;

interface Token {
    enum TokenType { Fungible, NonFungible }
    struct Coin { string obverse; string reverse; }
    function transfer(address recipient, uint amount) public;
}
```

**Solution**

In Solidity, all functions inside an `interface` contract must be declared `external`. Note that this restriction only applies to `interface`.

```solidity
pragma solidity >=0.5.0 <0.7.0;

interface Token {
    enum TokenType { Fungible, NonFungible }
    struct Coin { string obverse; string reverse; }
    function transfer(address recipient, uint amount) external;
}
```

If you would like to create a non-implemented function with a visibility other than `external`, then your only option is to define you contract as an **abstract contract**. Contracts are considered as **abstract** when at least one of their function lacks an implementation. Their benefit is that their functions (including the non-implemented ones) are not restricted to the `external` visibility (compare to `interface`).

Simply replace the keyword `interface` by `contract` (see example below).

```solidity
pragma solidity >=0.5.0 <0.7.0;

contract Token {
    enum TokenType { Fungible, NonFungible }
    struct Coin { string obverse; string reverse; }
    function transfer(address recipient, uint amount) public;
}
```

---

## State variables not allowed in interfaces

|Heading|Description|
|-|-|
|**Title**|State variables not allowed in interfaces|
|**Type**|`TypeError`|
|**Message**|```Variables cannot be declared in interfaces.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error describes an interface contract that contain variables declarations statements. In Solidity, `interface` contracts cannot contain state variables.

**Example**

```
pragma solidity ^0.5.0;

interface LegalContract {
    
   address party1;
   address party2;
    
}
```

**Solution**

A potential solution would be to wrap the state variables inside a `struct`, as shown below:

```
pragma solidity ^0.5.0;

interface LegalContract {
    
    struct Parties {
        address party1;
        address party2; 
    }
    
}
```

----

## Interface defined as `abstract`

|Heading|Description|
|-|-|
|**Title**|Interface defined as `abstract`|
|**Type**|`TypeError`|
|**Message**|```Interfaces do not need the "abstract" keyword, they are abstract implicitly.```|
|**Solidity version**|since 0.6.1|
|**Reference**|ContractLevelChecker.cpp|
|**Contributors**||


**Description**

An `interface` is defined as `abstract`.

**Example**

```
pragma solidity >=0.4.16 <0.7.0;

abstract interface Example {
    
}

```

**Solution**

Remove the `abstract` keyword. Interface are abstract contracts, since they contain only functions without implementations.

-----

## Interface function declared as `virtual`

|Heading|Description|
|-|-|
|**Title**|Interface function declared as `virtual`|
|**Type**|`warning`|
|**Message**|```Interface functions are implicitly "virtual"```|
|**Solidity version**|since 0.6.1|
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

This warning message reminds you that it is not necessary to use the `virtual` keyword when defining a function within an `interface`, since interface's functions never are implemented. Therefore, they are `virtual` by default.

**Example**

```
pragma solidity ^0.6.0;

interface Example {
    
    function f() external virtual;
    
}
```

**Solution**


```
pragma solidity ^0.6.0;

interface Example {
    
    function f() external virtual;
    
}
```

-----

# Cannot instantiate an interface


|Heading|Description|
|-|-|
|**Title**|Cannot instantiate an interface|
|**Type**|`TypeError`|
|**Message**|```Cannot instantiate an interface```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.6.0;

  
interface I {}

contract C {
    
    function f() public {
        new I();
    }
    
}
```

**Solution**
