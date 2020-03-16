# Built-in Solidity Functions

---

# Deprecated functions

## gasleft() instead of msg.gas

|Heading|Description|
|-|-|
|**Title**|gasleft() instead of msg.gas|
|**Type**|`TypeError`|
|**Message**|```"msg.gas" has been deprecated in favor of "gasleft()"```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, Lines 195 - 199](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L195-L199)|
|**Contributors**||


**Description**

**Example**

```solidity
msg.gas
```

**Solution**



---

## blockhash() instead of block.blockhash()

|Heading|Description|
|-|-|
|**Title**|blockhash() instead of block.blockhash()|
|**Type**|`TypeError`|
|**Message**|```"block.blockhash()" has been deprecated in favor of "blockhash()"```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, Lines 200 - 204](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L200-L204)|
|**Contributors**||


**Description**

**Example**

```solidity
block.blockhash()
```

**Solution**



---

## delegatecall() instead of callcode()

|Heading|Description|
|-|-|
|**Title**|delegatecall() instead of callcode()|
|**Type**|`TypeError`|
|**Message**|```"callcode" has been deprecated in favour of "delegatecall".```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, Lines 219 - 225](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L219-L225))|
|**Contributors**||


**Description**

**Example**

```solidity
callcode()
```

**Solution**



---

## "Throw" keyword deprecated

|Heading|Description|
|-|-|
|**Title**|Throw deprecated in favour of revert()|
|**Type**|`SyntaxError`|
|**Message**|```"throw" is deprecated in favour of "revert()", "require()" and "assert()"```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {

    function sendMoney(address payable _recipient) public payable {
        if (msg.sender.balance > msg.value) {
            throw;
        }
        _recipient.transfer(msg.value);
    }

}
```
**Solution**

---

## Failure condition of `send` ignored

|Heading|Description|
|-|-|
|**Title**|Failure condition of `send` ignored|
|**Type**|`warning`|
|**Message**|```Failure condition of 'send' ignored. Consider using 'transfer' instead.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 1000](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L1100)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Escrew {

    function sendMoney(address payable recipient, uint _value) external payable {
        recipient.send(_value);
    }

}
```

**Solution**


-----

## Returned value of low level call not used

|Heading|Description|
|-|-|
|**Title**|Return of low level call not used|
|**Type**|`Warning`|
|**Message**|```Returned value of low level call not used```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.6.0;

contract DeployedContract {
    uint public result = 0;

    function add(uint input) public {
        result = result + input;
    }
}


contract Proxy {    
    
    address deployed_contract = 0x1212121212121212121212121212121212121212;

    function LowLevelCall(uint lucky_number) public { 
        bytes memory _calldata = abi.encode(bytes4(keccak256("add(uint256)")), lucky_number);
        deployed_contract.call(_calldata);
    }


}
```

**Solution**

-----

# StaticCall not supported by EVM version

|Heading|Description|
|-|-|
|**Title**|StaticCall not supported by EVM version|
|**Type**|`TypeError`|
|**Message**|```"staticcall" is not supported by the VM version.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

This error occurs when you specify an evm version prior to byzantium (homestead, tangerineWhistle or SpuriousDragon). Static Call exists since Byzantium only.


**Example**

![StaticCall not supported by EVM version, error in Remix](https://i.ibb.co/L8dqwDP/Screenshot-2020-02-20-at-06-20-17.png)

**Solution**


-----

# Using wrong specifier for empty calldata

|Heading|Description|
|-|-|
|**Title**|Using wrong specifier for empty calldata|
|**Type**|`TypeError`|
|**Message**|```This function requires a single bytes argument. Use "" as argument to provide empty calldata."```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

This error when using a low level funtion like `.call()`, `delegatecall()` or `.staticcall()`. All of these function require a single `bytes` argument as a calldata.

The error appears if you do not include any argument as a mean to provide an empty calldata. 

**Example**

```
pragma solidity ^0.6.0;

contract Example {
    
    function f() public {
        (bool success,) = address(this).call();
        require(success);
    }
    
}
```

**Solution**

As suggested by the error, use "" as argument to provide empty calldata.

```
pragma solidity ^0.6.0;

contract Example {
    
    function f() public {
        (bool success,) = address(this).call("");
        require(success);
    }
    
}
```

---

# Low level call argument not provided correctly

|Heading|Description|
|-|-|
|**Title**|Low level call argument not provided correctly|
|**Type**|`TypeError`|
|**Message**|```This function requires a single bytes argument. If all your arguments are value types, you can use abi.encode(...) to properly generate it.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**


```
pragma solidity ^0.5.0;

contract C {

    function f() public {
        (bool success,) = address(this).call(bytes4(0x12345678));
        require(success);
        (success,) = address(this).call(uint(1));
        require(success);
        (success,) = address(this).call(uint(1), uint(2));
        require(success);
    }

}
```

**Solution**


-----

# Member `.value` only available for `payable` function


|Heading|Description|
|-|-|
|**Title**|Member `.value` only available for `payable` function|
|**Type**|`TypeError`|
|**Message**|```"Member "value" is only available for payable functions."```|
|**Solidity version**|since `0.5.5`|
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity 0.5.5;

contract Apple {
    
    function apple(address payable to, uint256 value, bytes calldata data) external returns (bool success, bytes memory result) {
        return to.call.value(value)(data);
    }
    
    function banana(address payable to, uint256 value, bytes calldata data) external returns (bool success, bytes memory result) {
        return to.delegatecall.value(value)(data); // ERROR
    }
}
```

**Solution**

Add the `payable` keyword to the function declaration.
