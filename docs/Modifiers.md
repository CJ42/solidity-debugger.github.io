# Modifiers

## No `_;` specified in Modifier body

|Heading|Description|
|-|-|
|**Title**|No `_;` specified in Modifier body|
|**Type**|`SyntaxError`|
|**Message**|```Modifier body does not contain '_'```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Line 143 - 144](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L143-L144)|
|**Contributors**|CJ42|


**Description**

The modifier does not contain the placeholder `_;`

**Example**

```solidity
pragma solidity ^0.5.9;

contract MyContract {

    modifier Fee {
        require (msg.value != 0);
    }
}

```

**Solution**

Insert the placeholder `_;` inside your modifier body to specify where the function body that the modifier applies to will be placed.


---

## Modifier applied to abstract function

|Heading|Description|
|-|-|
|**Title**|Modifier applied to abstract function|
|**Type**|`SyntaxError`|
|**Message**|```Functions without implementation cannot have modifiers.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...](#)|
|**Contributors**|CJ42|


**Description**

This error defines an attempt to apply a `modifier` to an abstract function (function without a body). This is not possible in Solidity.

**Example**

```solidity
pragma solidity ^0.5.0;

contact Example {

    modifier TxFee(uint _fee) {
        msg.value + _fee;
        _;
    }

    function sendEther() public TxFee;

}
```

**Solution**



---

## Modifier including msg.value applied to non-payable function

|Heading|Description|
|-|-|
|**Title**|Modifier including msg.value applied to non-payable function|
|**Type**|`TypeError`|
|**Message**|```This modifier uses "msg.value" or "callvalue()" and thus the function has to be payable or internal```|
|**Solidity version**||
|**Reference**|[ViewPureChecker.cpp, Line 283 - 288](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ViewPureChecker.cpp#L283-L288)|
|**Contributors**|CJ42|


**Description**

A non-`payable` function applies a `modifier` that handle ethers.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    modifier TxFee(uint _fee) {
        msg.value + _fee;
        _;
    }
    
    function sendEther(address payable _recipient, uint _ether) public TxFee(10) {
        _recipient.transfer(_ether);
    }

    
}
```

**Solution**



---

## Wrong argument count in modifier invocation

|Heading|Description|
|-|-|
|**Title**|Wrong argument count in modifier invocation|
|**Type**|`TypeError`|
|**Message**|```"Wrong argument count for modifier invocation: [nb-of-passed-arguments] arguments given but expected [nb-of-arguments-expected]."```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error describes a modifier attached to a function but that does not specifies the right number of arguments.

**Example**

```
pragma solidity ^0.5.0;

contract Greetings {
    
    address owner;
    
    modifier isOwner(address _caller) {
        require(_caller == owner);
        _;
    }
    
   function sayHello() public view isOwner returns (string memory) {
        return 'Nihao';
    }

}
```

**Solution**

Pass the correct number of arguments in the modifier attached to the function, like below.

```
pragma solidity ^0.5.0;

contract Greetings {
    
    address owner;
    
    modifier isOwner(address _caller) {
        require(_caller == owner);
        _;
    }
    
   function sayHello() public view isOwner(msg.sender) returns (string memory) {
        return 'Nihao';
    }

}
```

---

## Wrong argument type in modifier invocation

|Heading|Description|
|-|-|
|**Title**|Wrong argument type in modifier invocation|
|**Type**|`TypeError`|
|**Message**|```"Invalid type for argument in modifier invocation. Invalid implicit conversion from [type1] to [type2] requested."```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error describes a modifier attached to a function but that contains parameter(s) of the wrong type.

**Example**


```
pragma solidity ^0.5.0;

contract InterestRates {
    
    modifier EnoughMoney(uint _fee) {
        msg.sender.balance > _fee;
        _;
    }
    
    function repayInterest() public EnoughMoney('3') {
        // code here
    }

}
```

**Solution**

Use the correct type for the variable passed to the modifier invocation.

```
pragma solidity ^0.5.0;

contract InterestRates {
    
    modifier EnoughMoney(uint _fee) {
        msg.sender.balance > _fee;
        _;
    }
    
    function repayInterest() public EnoughMoney(3 wei) {
        // code here
    }

}
```

---

## Override changes function to modifier

|Heading|Description|
|-|-|
|**Title**|Override changes function to modifier|
|**Type**|`TypeError`|
|**Message**|```Override changes function to modifier.```|
|**Solidity version**|since 0.4.16|
|**Reference**|[ContractLevelChecker.cpp, line 152](https://github.com/ethereum/solidity/blob/15e39f7d65e4edfec3b643306984477b2f8ef303/libsolidity/analysis/ContractLevelChecker.cpp#L152)|
|**Contributors**||


**Description**

This error describes a contract that inherits functions from another contract and contains a modifier with the same name than a function of the contract it inherited from.

**Example**

```
pragma solidity ^0.5.0;
  
contract A {
    
    function f() public pure {
        
    }
    
}

contract B is A {
    
    modifier f() {
     _;   
    }
}
```

**Solution**


---

## Override changes modifier to function

|Heading|Description|
|-|-|
|**Title**|Override changes modifier to function|
|**Type**|`TypeError`|
|**Message**|```Override changes modifier to function```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, lines ...|
|**Contributors**||


**Description**

This error is the opposite of the previously cited one. It describes a contract B that inherits a modifier from another contract A. However, a function in B has the same name than the modifier defined in A, which lead to a conflict in the override.


**Example**

```
pragma solidity ^0.5.0;

contract A { 
    
    modifier mod(uint a) { 
        _; 
    } 
    
}

contract B is A { 
    
    function mod(uint a) public { 
        // some code here
    } 

}
```

**Solution**



---

## Override changes modifier signature

|Heading|Description|
|-|-|
|**Title**|Override changes modifier signature|
|**Type**|`TypeError`|
|**Message**|```Override changes function to modifier.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, lines ...|
|**Contributors**||


**Description**

This error describes an attempt to override a modifier in an inherited contract, where the modifier parameters or return variable(s) are of different number or types.

**Example**

```
pragma solidity ^0.5.0;

contract A { 

    modifier mod(uint a) { 
        _; 
    } 

}

contract B is A { 

    modifier mod(uint8 a) { 
        _; 
    } 

}

```

**Solution**


---

## Modifier-style base constructor call without arguments.

___Not sure if it shouldn't be in constructor___

|Heading|Description|
|-|-|
|**Title**|Modifier-style base constructor call without arguments.|
|**Type**|`DeclarationError`|
|**Message**|```Modifier-style base constructor call without arguments.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, lines ...|
|**Contributors**||


**Description**

...

**Example**

```
pragma solidity ^0.5.0;
  
contract A { 
    
    constructor() public { 
        
    } 

}
contract B is A { 
    
    constructor() A public {
        
    } 
    
}
```

**Solution**

In this case, add parentheses to `A`
