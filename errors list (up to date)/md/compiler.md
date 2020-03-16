# Compiler debug

The listing below summarize all the errors and warnings related to the `pragma` statements of the Solidity compiler.


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Source file requires different compiler version (current compiler is [compiler version in Remix]. - note that nightly builds are considered to be stricly less than the released version.</pre>||_SyntaxChecker.cpp_, [Line ...](#)|

-----

|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Source file does not specify required compiler version! Consider adding “pragma solidity”</pre>||_SyntaxChecker.cpp_, [Line 57 - 72](https://github.com/ethereum/solidity/blob/2ee272acf32fbad4efd1da7919c59792597ce9e6/libsolidity/analysis/SyntaxChecker.cpp#L57-L72)|

**Error :**

```solidity
> error occurs here
contract NewHello{
    // contract code here
}
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Experimental feature name is missing</pre>||_SyntaxChecker.cpp_, [Line 86 - 90](https://github.com/ethereum/solidity/blob/2ee272acf32fbad4efd1da7919c59792597ce9e6/libsolidity/analysis/SyntaxChecker.cpp#L86-L90)|

**Error (example):**

```solidity
pragma experimental;

contract MyContract {
    // Write your code here
}

```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Stray arguments</pre>||_SyntaxChecker.cpp_, [Line 91 - 95](https://github.com/ethereum/solidity/blob/2ee272acf32fbad4efd1da7919c59792597ce9e6/libsolidity/analysis/SyntaxChecker.cpp#L91-L95)|

**Error (example) :**

```solidity
pragma experimental ABIEncoderV2 nextGen;

contract MyContract {
    // Write your code here
}
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Duplicate experimental feature name</pre>||_SyntaxChecker.cpp_, [Line 103 - 104](https://github.com/ethereum/solidity/blob/2ee272acf32fbad4efd1da7919c59792597ce9e6/libsolidity/analysis/SyntaxChecker.cpp#L103-L104)|

**Error (example) :**

```solidity
pragma experimental SMTChecker;
pragma experimental SMTChecker;

contract MyContract {
    // Write your code here
}

```
-----



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>This type is only supported in the new experimental ABI encoder. Use \
"pragma experimental ABIEncoderV2;" to enable the feature.</pre>||_TypeChecker.cpp_, [Line ...](#)|

This error refers to the use of a feature that is only available with Version 2 of the ABIEncoder. To silent this error message, add the `pragma experimental ABIEncoderV2;` at the top of your file. 

**Error (example) :**

```solidity
pragma solidity ^0.5.0;

contract UserDirectory {
    
    struct Contact {
        string email;
        string phone;
    }
    
    struct User {
        string name;
        address addr;
        Contact contact;
    }
    
    event UserAdded(address indexed addr, User user);
}
```


**Solution (example) :**

```solidity
pragma solidity ^0.5.0;
pragma experimental ABIEncoderV2;

contract UserDirectory {
    
    struct Contact {
        string email;
        string phone;
    }
    
    struct User {
        string name;
        address addr;
        Contact contact;
    }
    
    event UserAdded(address indexed addr, User user);
}
```
-----