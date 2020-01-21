# Control Flow

The errors and warnings below related to loops and conditionals.

## Variable declaration not inside block

|Heading|Description|
|-|-|
|**Title**|Variable declarations can only be used inside blocks.|
|**Type**|`SyntaxError`|
|**Message**|```Variable declarations can only be used inside blocks.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 151 - 152](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L151-L152)|
|**Contributors**|CJ42|


**Description**



**Example**

```
pragma solidity ^0.5.9;

contract MyContract {

    uint a = 3;
    uint b = 2;

    function test() public {

        for (uint x = 1; x <= 10; x++) uint c = a + b + x;

    }

}

```

**Solution**



---

## Invalid use of `continue` keyword

|Heading|Description|
|-|-|
|**Title**|Invalid use of `continue` keyword|
|**Type**|`SyntaxError`|
|**Message**|```"continue" has to be in a "for" or "while" loop.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 189 - 191](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L189-L191)|
|**Contributors**|CJ42|


**Description**


**Example**

```solidity
pragma solidity ^0.5.9;

contract MyContract {

    uint a = 3;
    uint b = 2;

    function test(uint x) public {
        if ( x < a && x > b) {
            bool result = true;
            continue;
        }
    }

}

```

**Solution**



---

## Invalid use of `break` keyword

|Heading|Description|
|-|-|
|**Title**|Invalid use of `break` keyword|
|**Type**|`SyntaxError`|
|**Message**|```"break" has to be in a "for" or "while" loop.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 197 - 199](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L197-L199)|
|**Contributors**|CJ42|


**Description**

**Example**

```solidity
pragma solidity ^0.5.9;

contract MyContract {

    uint a = 3;
    uint b = 2;

    function test(uint x) public {
        if ( x < a && x > b) {
            bool result = true;
            break;
        }
    }

}
```

**Solution**



---


