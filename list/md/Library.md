# Debug your Solidity library

Here are a list of all the errors and warnings related to libraries in Solidity :


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
|**typeError**|<pre>The function declaration is here: [function-name]. Libraries cannot call their own functions externally</pre>|since Solidity 0.5.9|_StaticAnalyser.cpp_, [line 312-324](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L312-L324)|

**Solution :**

```solidity
pragma solidity 0.5.9;

library L {
    using L for *;
    
    function f() public pure returns (uint r) { 
        return r.g();
    }
    
    function g(uint) public pure returns (uint) { 
        return 2; 
    }
}
```

**References :**

* https://github.com/ethereum/solidity/issues/6451
* https://github.com/ethereum/solidity/pull/6604/files
-----




|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Libraries cannot be inherited from.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

library MyLibrary {
    // interface code here
}

contract MyContract is MyLibrary {
    
    function encodeString(string memory sentence) public pure returns (bytes memory) {
        return abi.encode(sentence);
    }
    
    function decodeString(bytes memory data) public pure returns (string memory) {
        return abi.decode(data, (string));
    }
    
}
```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Mapping types for parameters or return variables can only be used in internal or library functions.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

contract myContract {
   
    mapping(address => bool) votes;
    
    function resetVotes(mapping(address => bool) memory _voters) public pure {
        
    }
}
```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Internal library function must be implemented if declared.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**
```solidity
library Messenger {
    
    function testConnection() internal pure returns(bool);
    
}
```

**Solution :**
```solidity
library Messenger {
    
    function testConnection() public pure returns(bool);
    
}
```
-----



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Library is not allowed to inherit</pre>||_ContractLevelChecker.cpp_, [Line 476](https://github.com/ethereum/solidity/blob/efd8d8fe5eced023476af71491e9eae3dbde4d87/libsolidity/analysis/ContractLevelChecker.cpp#L476)|


**Error (example) :**

```solidity
library BritishMuseum {
    string constant name = "British Museum"; 
}

library MyLibrary is BritishMuseum {
    
}
```
-----



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Library functions cannot be payable</pre>||_TypeChecker.cpp_, [Line ...](#)|


**Error (example) :**

```solidity
library Vault {
    
    function deposit() public payable;
}
```
-----



**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Constructor cannot be defined in libraries.</pre>||_TypeChecker.cpp_, [Line ...](#)|


**Error (example) :**

```solidity
library Vault {
    
    constructor() public {
        // ...
    }
}
```
-----