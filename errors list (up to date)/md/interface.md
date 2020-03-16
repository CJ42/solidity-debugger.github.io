# Debug your Solidity interface

Here are a list of all the errors and warnings related to `interface` in Solidity :


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Interfaces cannot inherit.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

contract MyContract {
    
    function encodeString(string memory sentence) public pure returns (bytes memory) {
        return abi.encode(sentence);
    }
    
    function decodeString(bytes memory data) public pure returns (string memory) {
        return abi.decode(data, (string));
    }
    
}

interface MyInterface is MyContract {
    // interface code here
}
```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Variables cannot be declared in interfaces</pre>||_TypeChecker.cpp_, [Line ...](#)|

The quickfix for this error is to encapsulate the variables inside a struct. However, this might take up more space in storage.

**Error (example) :**
```solidity
pragma solidity ^0.5.0;

interface LegalContract {
    
    address party1;
    address party2;
    
}
```

**Solution :**
```solidity
pragma solidity ^0.5.0;

interface LegalContract {
     
     struct Parties {
         address party1;
         address party2;
     } 
     
}
```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError / overrideError**|<pre>Overriding function return types differ..</pre>||_ContractLevelChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.9;

interface Greetings {
    function hello() external pure returns (string memory);
    function goodbye() external pure returns (string memory);
}

contract FrenchContract is Greetings {
    
    function hello() external pure returns (string memory) {
        return "Bonjour";
   }

}


contract RobotContract is Greetings {
    
    function hello() external pure returns (uint) {
        return 1;
    }
    
}
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Functions in interfaces cannot have an implementation</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

interface Game {
    
    function play() public {
        // some code here
    }
}
```


**Solution (example) :**

```solidity
pragma solidity ^0.5.0;

interface Game {
    
    function play() public;
}
```


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Functions in interfaces must be declared external.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

interface Game {
    
    function play() public;
}
```


**Solution (example) :**

```solidity
pragma solidity ^0.5.0;

interface Game {
    
    function play() external;
}
```



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>Constructor cannot be defined in interfaces.</pre>||_TypeChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

interface Game {
    
    constructor() public;
}
```