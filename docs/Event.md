# Events

## Event declared twice

|Heading|Description|
|-|-|
|**Title**|Event declared twice|
|**Type**|`declarationError`|
|**Message**|```Event with same name and arguments defined twice.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, |
|**Contributors**|CJ42|


**Description**

The contrat declares an `event` with the same name and argument twice.

In Solidity, **event overloading** is allowed.
Two events can share the same name as long as their topics are differents (the same way that duplicate function names are allowed as long as their argument types differ). 

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    event Deposit(address _address, uint _deposit);
    event Deposit(address _address, uint _deposit);
    
}
```

**Solution**

Change the name of your event, or specifies different topics.

---

## More than 3 `indexed` arguments for event.

|Heading|Description|
|-|-|
|**Title**|More than 3 `indexed` arguments for event.|
|**Type**|`TypeError`|
|**Message**|```More than 3 indexed arguments for event.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error in Solidity specifies an event declared with more than 3 `indexed` arguments.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    modifier EnoughMoney(uint _fee) {
        msg.sender.balance > _fee;
        _;
    }
    
    event Receipt(
        address indexed sender,
        address indexed recipient,
        uint indexed amount,
        uint indexed timestamp
    );
    
    
    function repayInterest() public EnoughMoney(3 wei) {
        // code here
    }

}
```

**Solution**


---

## More than 4 `indexed` arguments for anonymous event

|Heading|Description|
|-|-|
|**Title**|More than 4 `indexed` arguments for anonymous event|
|**Type**|`TypeError`|
|**Message**|```More than 4 indexed arguments for anonymous event.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error in Solidity specifies an `anonymous` event declared with more than 4 `indexed` arguments.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    modifier EnoughMoney(uint _fee) {
        msg.sender.balance > _fee;
        _;
    }
    
    event Receipt(
        address indexed sender,
        address indexed recipient,
        uint indexed amount,
        uint indexed timestamp,
        string indexed message
    ) anonymous;
    
    
    function repayInterest() public EnoughMoney(3 wei) {
        // code here
    }

}
```

**Solution**

If you want to keep your event `anonymous`, you will have to select the arguments that you will not be indexed, and keep the number of indexed arguments to no more than 4.

---

## Internal or recursive type not allowed as event parameter type.

|Heading|Description|
|-|-|
|**Title**|Internal or recursive type not allowed as event parameter type.|
|**Type**|`TypeError`|
|**Message**|```Internal or recursive type not allowed as event parameter type.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 595](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L595)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    event Deposit(
        uint a,
        uint b,
        function (uint, uint) internal returns (uint) f
    );
}
```

**Solution**



---

## Expression has to be an event invocation

|Heading|Description|
|-|-|
|**Title**|Expression has to be an event invocation|
|**Type**|`TypeError`|
|**Message**|```Expression has to be an event invocation.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 837](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L837)|
|**Contributors**||


**Description**

Occurs when you specify a variable name other than an event in an `emit`.

**Example**

```
pragma solidity ^0.5.0;

contract C {
  uint256 Test;

  function f() public {
    emit Test();
  }
}
```

**Solution**


---

## Event invocation have to be prefixed by "emit"

|Heading|Description|
|-|-|
|**Title**|Event invocation have to be prefixed by "emit"|
|**Type**|`TypeError`|
|**Message**|```Event invocations have to be prefixed by "emit".```|
|**Solidity version**|Since 0.5.0|
|**Reference**|[TypeChecker.cpp, line 1540](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L1540)|
|**Contributors**||


**Description**

Prior to version 0.5 of Solidity, the `emit` keyword was not needed to invoke `event`s. Since Solidity 0.5.x, this keyword is mandatory.
A good example is the MultiSigWallet contract from Gnosis. Since the contract was created using the compiler version 0.4.15, events were declared without the `emit` keyword.


**Example**

```
pragma solidity ^0.5.0;

contract SimpleVault {
    
    event Deposit(address _from, uint value);
    
    function makeDeposit(uint _value) public payable {
        // some code here
        address _from = msg.sender;
        Deposit(_from, _value);
    }
}
```

**Solution**
