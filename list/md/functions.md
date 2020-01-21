# Debug your functions in Solidity

This list references all the errors and warnings related to functions in Solidity


## Functions

|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
|**warning**|<pre>Unused function parameter. Remove or comment out the variable name to silence this warning</pre>||_StaticAnalyser.cpp_, [line 124](https://github.com/ethereum/solidity/blob/efd8d8fe5eced023476af71491e9eae3dbde4d87/libsolidity/analysis/StaticAnalyzer.cpp#L124)|

**Solution :**

```solidity
function sayHello(string memory _name, uint8 _age) public pure returns (string memory) {
    string memory myName = _name;
    return myName;
}
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **findDuplicateDefinitions**|<pre>Function with same name and arguments defined twice.</pre>||_ContractLevelChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
function foo() public pure returns (string memory) {
    return "foo";
}
    
function foo() public pure returns (string memory) {
    return "bar";
}
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Internal functions cannot be payable.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
function store() internal payable {
    // your code here
}
```
-----


## Constructors


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
|**warning**|<pre>"this" used in constructor. Note that external functions of a contract cannot be called while it is being constructed."</pre>||[line 234-240](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/StaticAnalyzer.cpp#L234-L240)|

**Solution :**

```solidity
constructor(uint _ether) public {
    this.sendEther(_ether);
}
    
function sendEther(uint _ether) external {
    address(this).balance + _ether;
    msg.sender.balance - _ether;
}
```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Functions are not allowed to have the same name as the contract. If you intend this to be a constructor, use "constructor(...) { ... }" to define it.</pre>||_SyntaxChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.9;

contract MyContract {
    
    function MyContract() public {
        // do something
    }
    
}
```
-----



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Constructor must be payable or non-payable, but is [state-mutability]</pre>||_ContractLevelChecker.cpp_, [Line ...](#)|

This error is diplayed when the keyword `view` or `pure` is attached to the constructor.

**Error (example) :**

```solidity
constructor(bytes32 _name) public view {}
```
-----



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Constructor must be public or internal</pre>||_ContractLevelChecker.cpp_, [Line ...](#)|


**Error (example) :**

```solidity
constructor(bytes32 _name) private {}
```
-----


**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Constructor must be implemented if declared</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
contract Game {
    
    constructor() public;
}
```
-----


**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Different number of arguments in return statement than in returns declaration.</pre>||_TypeChecker.cpp_, [Line ...](#)|

This error message can occur in 2 cases :

- We have multiple return value declared in the function head. We first look at how many components are mentioned in the tuple in the final return statement. We compare if this number is different than the number of arguments mentioned in the return declaration (function head).

- We have only one return value declared in the function head. We look at how many components are mentioned in the tuple in the final return statement. We check if this number is not equal to one.



**Error (example) :**

```solidity
function makeTransfer(address _recipient) public pure returns(address, address, uint) {
    address _sender = msg.sender;
    uint _value = msg.value;
    return (_sender, _recipient);
}
```