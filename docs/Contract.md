# Contracts

## Precedence order in Contract inheritance

|Heading|Description|
|-|-|
|**Title**|Precedence order in Contract inheritance|
|**Type**|`fatalTypeError`|
|**Message**|```Definition of base has to precede definition of derived contract```|
|**Solidity version**||
|**Reference**|NameAndTypeResolver.cpp, [Lines 388 - 389](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/NameAndTypeResolver.cpp#L388-L389)|
|**Contributors**|CJ42|


**Description**

The base contract is defined after the derived contract.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Person is Greetings {
    
   // ...
   
}

contract Greetings {
    
    // ...
    
}
```

**Solution**

Define the base contract first, then the derived contract.

```solidity
pragma solidity ^0.5.0;

contract Greetings {
    
    // ...
    
}

contract Person is Greetings {
    
   // ...
   
}
```


---

## Linearization of inheritance impossible

|Heading|Description|
|-|-|
|**Title**|Linearization of inheritance impossible|
|**Type**|`DeclarationError`|
|**Message**|```Linearization of inheritance graph impossible```|
|**Solidity version**||
|**Reference**|[NameAndTypeResolver.cpp, line 395](https://github.com/ethereum/solidity/blob/d5b2f347bf481151ff03fb6dea08e7ce1ce7194c/libsolidity/analysis/NameAndTypeResolver.cpp#L395)|
|**Contributors**||


**Description**

This type of error might occur in two possible situations:
- a contract (A) inherits from two other contracts (B and C), but B already inherited from C.
- there is a problem in the order the inheritances are declared ([see this OpenZeppelin issue](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/1124))

**Example**

```
pragma solidity >=0.4.16 <0.7.0;

contract X {}
contract A is X {}
contract C is A, X {}
```

**Solution**


**References**

- https://github.com/OpenZeppelin/openzeppelin-contracts/issues/1124
- https://github.com/OpenZeppelin/openzeppelin-contracts/issues/1110
- https://ethereum.stackexchange.com/questions/21060/multiple-inheritance-and-linearization


-----

## Contract with payable fallback function but no `receive` ether function

|Heading|Description|
|-|-|
|**Title**|Contract with payable fallback function but no `receive` ether function|
|**Type**||
|**Message**||
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

**Example**

```
pragma solidity >=0.4.16 <0.7.0;

contract Example {
    
    function f() public {
        
    }
    
    fallback() external payable {
        
    }
}
```

**Solution**



-----

# Contract Should be defined as `abstract`

|Heading|Description|
|-|-|
|**Title**|Contract should be defined as `abstract`|
|**Type**|`TypeError`|
|**Message**|```Missing Implementation: Contract [… should be marked as abstract.```|
|**Solidity version**|since 0.6.0|
|**Reference**|[ContractLevelChecker.cpp, lines 28-232]()|
|**Contributors**||


**Description**

**Example**


```
pragma solidity >=0.4.16 <0.7.0;

contract Example {
    
    function f() public virtual pure;
}

```

**Solution**


-----

# Identifier is not a contract


|Heading|Description|
|-|-|
|**Title**|Identifier is not a contract|
|**Type**|`FatalTypeError`|
|**Message**|```Identifier is not a contract```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

**Solution**


```
pragma solidity ^0.5.0;

contract Base {
    
}

contract Example {
    
    struct myStruct {
        address hey;    
    }
    
    function test() public {
        Base _new = new myStruct();
    }
    
}
```

-----

-----

# Trying to create an instance of an abstract contract

|Heading|Description|
|-|-|
|**Title**|Trying to create an instance of an abstract contract|
|**Type**|`TypeError`|
|**Message**|```Trying to create an instance of an abstract contract```|
|**Solidity version**|before 0.6.0|
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract C {
  function a() public;
}

contract D {
  function f() public {
    new C();
  }
}
```

**Solution**

-----

# Trying to create an instance of an abstract contract (2)


|Heading|Description|
|-|-|
|**Title**|Trying to create an instance of an abstract contract (2)|
|**Type**|`TypeError`|
|**Message**|```Cannot instantiate an abstract contract```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

Same as above, but from 0.6.0. The error is different because of the introduction of the `abstract` keyword.

**Example**

```
pragma solidity ^0.6.0;

abstract contract C {
  function a() public;
}

contract D {
  function f() public {
    new C();
  }
}
```

**Solution**
