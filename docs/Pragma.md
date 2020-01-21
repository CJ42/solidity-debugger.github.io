# Pragma statements

The section below lists all the errors related to the `pragma solidity` statements, aimed to define the version of the Solidity compiler used.

---

## No compiler version specified

|Heading|Description|
|-|-|
|**Title**|No compiler version specified|
|**Type**|`SyntaxError`|
|**Message**|```Source file does not specify required compiler version! Consider adding “pragma solidity”```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 57 - 72](https://github.com/ethereum/solidity/blob/2ee272acf32fbad4efd1da7919c59792597ce9e6/libsolidity/analysis/SyntaxChecker.cpp#L57-L72)|
|**Contributors**||


**Description**

This error specifies that the `solc` file does not declare a compiler version.

**Example**

```solidity

contract Example {

    // contract code here

}
```

**Solution**

Indicate the version of the compiler used in the first line of your file, using the statement `pragma solidity <version number>`

```solidity
pragma solidity ^0.5.0;

contract Example {

    // contract code here

}
```

---

## Invalid pragma

|Heading|Description|
|-|-|
|**Title**|Invalid Pragma|
|**Type**|`SyntaxError`|
|**Message**|```Invalid Pragma```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, line 81](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/SyntaxChecker.cpp#L81)|
|**Contributors**||


**Description**

This error occurs when you specify an invalid pragma statement.

**Example**

```
pragma 0;
```

**Solution**

---

## Experimental feature name missing

|Heading|Description|
|-|-|
|**Title**|Experimental feature name missing|
|**Type**|`SyntaxError`|
|**Message**|```Experimental feature name is missing```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 86 - 90](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L86-L90)|
|**Contributors**||


**Description**

This error indicates that the experimental feature name of the Solidity compiler is not specified.

**Example**

```solidity
pragma solidity ^0.5.0;
pragma experimental;

contract Example {

    // contract code here

}
```

**Solution**

Indicate the version of the compiler used in the first line of your file, using the statement `pragma solidity <version number>`

```solidity
pragma solidity ^0.5.0;
pragma experimental ABIEncoderV2;

contract Example {

    // contract code here

}
```

---

## Stray arguments in pragma statement

|Heading|Description|
|-|-|
|**Title**|Stray arguments in pragma statement|
|**Type**|`SyntaxError`|
|**Message**|```Stray arguments```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 91 - 95](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L91-L95)|
|**Contributors**||


**Description**

This error indicates that some invalid arguments are specified after the pragma statement.

**Example**

In the example below, both cases raises the error message. Either if another argument is specified (`xyz...`) or parentheses.

```solidity
pragma experimental ABIEncoderV2 xyz...;
pragma experimental (); // this is another error example.

contract Example {

    // contract code here

}
```

**Solution**

Remove any stray arguments from your pragma statements.

```solidity
pragma experimental ABIEncoderV2;
pragma experimental SMTChecker;

contract Example {

    // contract code here

}
```

---

## Empty name for experimental feature

|Heading|Description|
|-|-|
|**Title**|Empty name for experimental feature|
|**Type**|`SyntaxError`|
|**Message**|```Empty experimental feature name is invalid.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 99 - 100](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/SyntaxChecker.cpp#L99-L100)|
|**Contributors**||


**Description**



**Example**

```solidity
pragma solidity ^0.5.0;
pragma experimental "";

contract Example {

    // contract code here

}
```

**Solution**

Use correct name for experimental features

```solidity
pragma solidity ^0.5.0;
pragma experimental ABIEncoderV2;

contract Example {

    // contract code here

}
```

---

## Unsupported experimental feature name

|Heading|Description|
|-|-|
|**Title**|Unsupported experimental feature name|
|**Type**|`SyntaxError`|
|**Message**|```Unsupported experimental feature name.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 101 - 102](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/SyntaxChecker.cpp#L101-L102)|
|**Contributors**||


**Description**

This error describes the use of an unsupported or non-existing experimental feature in Solidity.

**Example**

```solidity
pragma solidity ^0.5.0;
pragma experimental Unexisting_Feature;

contract Example {

    // contract code here

}
```

**Solution**

Use existing experimental features name and make sure their spelling is correct


---

## Duplicate experimental feature name.

|Heading|Description|
|-|-|
|**Title**|Duplicate experimental feature name.|
|**Type**|`SyntaxError`|
|**Message**|```Duplicate experimental feature name.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 103 - 104](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L103-L104)|
|**Contributors**||


**Description**

This error indicates that an experimental feature has been mentioned twice.

**Example**

```solidity
pragma solidity ^0.5.0;
pragma experimental SMTChecker;
pragma experimental SMTChecker;

contract Example {

    // contract code here

}
```

**Solution**

States the experimental feature that you use for the compiler only once.

---

## Unknown pragma.

|Heading|Description|
|-|-|
|**Title**|Unknown pragma.|
|**Type**|`SyntaxError`|
|**Message**|```Unknown pragma "<pragma mentioned>".```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 131](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/SyntaxChecker.cpp#L131)|
|**Contributors**||


**Description**


**Example**

In the example below, the error occurs because `Solidity` is written with an uppercase `S`.

```solidity
pragma Solidity ^0.5.0;

contract Example {

    // contract code here

}
```

**Solution**

Makes sure of the Solidity syntax : `solidity`, all lower case.

---

## Experimental Features turned on

|Heading|Description|
|-|-|
|**Title**|Experimental Features turned on|
|**Type**|`warning`|
|**Message**|```Experimental features are turned on. Do not use experimental features on live deployments```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, lines 109 - 110](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/SyntaxChecker.cpp#L109-L110)|
|**Contributors**||


**Description**

You can write more complex smart contracts in Solidity using additional features from the version 2 of the ABI Encoder. These features are available when you declare the **pragma statement**: `ABIEncoderV2`. However, Solidity warns you that these features are experimental and should not be used in live deployments.

**Example**

```
pragma solidity ^0.5.0;
pragma experimental ABIEncoderV2;

contract MyContract {

    // My contract code here
    
}
```

**Solution**