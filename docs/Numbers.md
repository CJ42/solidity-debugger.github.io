# Numbers

This section covers all the errors and warnings related to numbers

## Trailing underscore in number

|Heading|Description|
|-|-|
|**Title**|Trailing underscore in number|
|**Type**|`SyntaxError`|
|**Message**|```Invalid use of underscores in number literal. No trailing underscores allowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...](#)|
|**Contributors**||


**Description**

This error describes the use of an underscore at the end of a number.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply = 21_000_000_;

}
```

**Solution**

Remove the trailing underscore at the end of your number.

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply = 21_000_000;

}
```

---

## Two consecutives underscores between digits

|Heading|Description|
|-|-|
|**Title**|Two consecutives underscores between digits|
|**Type**|`SyntaxError`|
|**Message**|```Invalid use of underscores in number literal. Only one consecutive underscores between digits allowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...]()|
|**Contributors**||


**Description**

This error describes the use of two consecutive underscores between digits.

**Example**

Remove the trailing underscore at the end of your number.

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply = 21_000__000;

}
```

**Solution**

Use only one underscore between numbers for formatting.

Remove the trailing underscore at the end of your number.

```solidity
pragma solidity ^0.5.0;

contract Bitcoin {

    uint constant bitcoin_supply = 21_000_000;

}
```


---

## Underscore in front of decimal point.

|Heading|Description|
|-|-|
|**Title**|Underscore in front of decimal point.|
|**Type**|`SyntaxError`|
|**Message**|```Invalid use of underscores in number literal. No underscores in front of the fraction part allowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines 236 - 240](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L236-L240)|
|**Contributors**||


**Description**

This error describes the use of an underscore in front of a decimal point.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Test {

    fixed constant test1 = 10_000_.5;
    fixed constant test2 = 24_035._5;

}
```

**Solution**

Removes the underscore in front of the decimal point.

```solidity
pragma solidity ^0.5.0;

contract Test {

    fixed constant test1 = 10_000.5;
    fixed constant test2 = 24_035.5;

}
```

---

## Underscore in front of the mantissa

|Heading|Description|
|-|-|
|**Title**|Underscore in front of the mantissa|
|**Type**|`SyntaxError`|
|**Message**|```Invalid use of underscores in number literal. No underscore at the end of the mantissa allowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, line 243](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/SyntaxChecker.cpp#L243)|
|**Contributors**||


**Description**



**Example**

```
pragma solidity ^0.5.0;

contract Example {

    uint D3 = 12_e34;

}
```

**Solution**


---

## Underscore in front of exponent

|Heading|Description|
|-|-|
|**Title**|Underscore in front of exponent|
|**Type**|`SyntaxError`|
|**Message**|```Invalid use of underscores in number literal. No underscore in front of exponent allowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, line 246](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/SyntaxChecker.cpp#L246)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Example {

    uint D4 = 12e_34;

}
```

**Solution**


---

## Use of unary + is disallowed

|Heading|Description|
|-|-|
|**Title**|Use of unary + is disallowed|
|**Type**|`SyntaxError`|
|**Message**|```Use of unary + is disallowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, line 255](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/SyntaxChecker.cpp#L255)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    uint a = 5;
   
    function f() public pure returns (uint) {
        uint b =+ a;
        return b;
    }
}
```

**Solution**
