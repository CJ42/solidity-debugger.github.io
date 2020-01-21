# Constructor

## Constructor defined multiple times

|Heading|Description|
|-|-|
|**Title**|Constructor defined multiple time|
|**Type**|declarationError|
|**Message**|```Another declaration is here: <second contructor location>. More than one constructor defined.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, |
|**Contributors**|CJ42|


**Description**

More than one constructor is defined in the contract.

**Example**

```solidity
pragma solidity ^0.5.0;

contract UserAccounts {
    
    address owner;
    mapping(address => uint) account_balances;
    
    constructor() public {
        owner = msg.sender;
    }
    
    constructor(uint _credit) public {
        account_balances[msg.sender] = _credit;
    }

}
```

**Solution**

Use only one constructor.

```solidity
pragma solidity ^0.5.0;

contract UserAccounts {
    
    address owner;
    mapping(address => uint) account_balances;
    
    constructor() public {
        owner = msg.sender;
        account_balances[msg.sender] = _credit;
    }

}
```


---

## Constructor with empty return

|Heading|Description|
|-|-|
|**Title**|Constructor with empty return|
|**Type**|typeError|
|**Message**|```Non-empty "returns" directive for constructor.```|
|**Solidity version...**|since 0.4.8 (at least)|
|**Reference**|ContractLevelChecker.cpp, |
|**Contributors**|CJ42|


**Description**

The contract `constructor` mentions a return statement in its declaration but does not return anything in the constructor body.

**Example**

```solidity
pragma solidity ^0.5.10;

contract ProofOfBalance {
    
    address public participant;
    
    uint minval;

    constructor(address participant, uint minval) public returns (bool accept) {

        if (participant.balance < minval) {
            accept = false; 
        } else { 
            accept = true;
        }
    }   

}
```

**Solution**

Return the value inside the constructor body.

```solidity
pragma solidity ^0.5.10;

contract ProofOfBalance {
    
    address public participant;
    
    uint minval;

    constructor(address participant, uint minval) public returns (bool accept) {

        if (participant.balance < minval) {
            accept = false; 
        } else { 
            accept = true;
        }

        return accept;
    }   

}
```

---

## Wrong State Mutability in Constructor

|Heading|Description|
|-|-|
|**Title**|Wrong state mutability in Constructor|
|**Type**|typeError|
|**Message**|```Constructor must be payable or non-payable, but is "<state mutability>".```|
|**Solidity version...**||
|**Reference**|ContractLevelChecker, |
|**Contributors**|CJ42|


**Description**

The constructor is declared with the keyword `view` or `pure`, which is not allowed.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    constructor(bytes32 _name) public view {
        // constructor code
    }

}
```

**Solution**

Mentions either the constructor as :

* `payable` : if it will accept ether when deployed.
* nothing.

---

# Wrong Visibility for constructor

|Heading|Description|
|-|-|
|**Title**|Wrong visibility for constructor|
|**Type**|`typeError`|
|**Message**|```Constructor must be public or internal.```|
|**Solidity version...**||
|**Reference**|ContractLevelChecker, |
|**Contributors**|CJ42|


**Description**

The `constructor` is defined with either one of the two following (not-allowed) visibility : `private` or `external`.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    constructor(bytes32 _name) private {
        // constructor code
    }

}
```

**Solution**

Declare your `constructor` as either `public` or `internal`, as described in the error message.


---

## Use of `this` in constructor with `external` function

|Heading|Description|
|-|-|
|**Title**|Use of `this` in constructor with `external` function|
|**Type**|`warning`|
|**Message**|```"this" used in constructor. Note that external functions of a contract. cannot be called while it is being constructed.```|
|**Solidity version**||
|**Reference**|StaticAnalyzer.cpp, |
|**Contributors**|CJ42|


**Description**

The `constructor` calls a function declared as external in your contract.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    constructor(uint _ether) public {
           this.deposit(_ether);
    }
    
    function deposit(uint256 amount) payable public {
        require(msg.value == amount);
    }

}
```

**Solution**

In this case, you could declare the `deposit()` function as `public`.


**References**

- [Programtheblockchain.com - _Writing a contract that can handle Ether._](https://programtheblockchain.com/posts/2017/12/15/writing-a-contract-that-handles-ether/)


---

## Constructor not implemented

|Heading|Description|
|-|-|
|**Title**|Constructor not implemented|
|**Type**|`typeError`|
|**Message**|```Constructor must be implemented if declared.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp, |
|**Contributors**|CJ42|

**Description**

The `constructor` is declared, but does not have a body.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    constructor(uint _ether) public;
    
}
```

**Solution**


---

## Constructor definition in interface not allowed

|Heading|Description|
|-|-|
|**Title**|Constructor definition in interface not allowed|
|**Type**|`TypeError`|
|**Message**|```Constructor cannot be defined in interfaces.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

You cannot define a constructor in an interface in Solidity.

**Example**

```
pragma solidity ^0.5.0;

interface Example {
    
    constructor() external;
    
}
```

**Solution**



---

## Constructor definition in library not allowed

|Heading|Description|
|-|-|
|**Title**|Constructor definition in library not allowed|
|**Type**|`TypeError`|
|**Message**|```Constructor cannot be defined in libraries.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

You cannot define a constructor in a library.

**Example**

```
pragma solidity ^0.5.0;

library Example {
    
    constructor() public {
        
    }
    
}
```

**Solution**


---

## Base constructor arguments given twice.

|Heading|Description|
|-|-|
|**Title**|Base constructor arguments given twice.|
|**Type**||
|**Message**||
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

___Find a way to explain this clearly___

**Example**

```
pragma solidity ^0.5.0;
  
contract C { constructor(uint) public {} }
contract A is C { constructor() C(2) public {} }
contract B is C { constructor() C(2) public {} }
contract D is A, B { }
```

**Solution**

---

## Warning for constructor using inline Assembly

|Heading|Description|
|-|-|
|**Title**|Warning for constructor using inline Assembly|
|**Type**|`warning`|
|**Message**|```The constructor of the contract (or its base) uses inline assembly. Because of that, it might be that the deployed bytecode is different from type(...).runtimeCode.```|
|**Solidity version**|since 0.5.3|
|**Reference**|[StaticAnalyzer.cpp, lines 213 - 214](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/StaticAnalyzer.cpp#L213-L214)|
|**Contributors**||


**Description**

When you try to access the runtimeCode (using the `runtimeCode` built-in method) of a contract that uses inline Assembly in its constructor, Solidity warns you about a possible difference between :

- the bytecode returned by `runtimeCode` and...
- the actual bytecode deployed on the blockchain.

**Example**

```
pragma solidity ^0.5.0;

contract Test {
    
    function getRuntimeCode() public returns (bytes memory) {
        return type(C).runtimeCode;
    }
    
}

contract C {
    
    constructor() public { 
        assembly {
            // assembly statements here
        } 
    }
    
}
```

**Solution**


---

## Wrong argument count for constructor call

|Heading|Description|
|-|-|
|**Title**|Wrong argument count for constructor call|
|**Type**|`TypeError`|
|**Message**|```"Wrong argument count for constructor call: [nb of args given] arguments given but expected [nb of args expected]. Remove parentheses if you do not want to provide arguments here." ```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, lines 259 - 263](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L259-L263)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

interface I {

}

contract C is I(2) {

}
```

**Solution**


---

## Base constructor already provided

# Template for reporting a message

Each message has to be described using the following structure :

|Heading|Description|
|-|-|
|**Title**|Base constructor already provided|
|**Type**|`DeclarationError`|
|**Message**|```Base constructor already provided.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 405](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L405)|
|**Contributors**||


**Description**



**Example**

```
pragma solidity ^0.5.0;
 
contract C { constructor(uint a) public {} }
contract B is C {
    constructor() C(2) C(2) public {}
}
```

**Solution**

