# The remaining


## _TypeChecker.cpp_


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Wrong argument count for [function-call / constructor-call]. [nb-of-arguments] arguments given but need at least / expected [nb-of-params-expected].</pre>||_TypeChecker.cpp_, [Line ...](#)|


**Error (example) :**
```solidity
function setTwoTx(address payable _address1, address payable _address2) public {
    _address1.transfer(10);
    _address2.transfer(10);
}
    
function sendTx(address _address) public {
    setTwoTx(_address);
}
```
-----





## _ContractLevelChecker.cpp_



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Name has to refer to a struct, enum or contract</pre>||_ReferencesResolver.cpp_, [Line 190 - 194](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L190-L194)|


**Error (example) :**

```solidity
address constant _address1 = msg.sender;
    
function setTwoTx(_address1, address payable _address2) public {
    _address1.transfer(10);
    _address2.transfer(10);
}
    
function sendTx(address _address) public {
    setTwoTx(_address);
}
```
-----
