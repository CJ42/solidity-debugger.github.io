# Structs

Here is a list of all the errors and warnings related to `struct` in Solidity.

---

## Empty struct declaration

|Heading|Description|
|-|-|
|**Title**|Empty struct declaration|
|**Type**|`SyntaxError`|
|**Message**|```Defining empty structs is disallowed.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...](#)|
|**Contributors**|CJ42|


**Description**

This error occurs when a `struct` with no member is declared.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {

    struct Unknown {

    }

}
```

**Solution**

You need to declare a `struct` with at least one member.

---

## Recursive struct definition

|Heading|Description|
|-|-|
|**Title**|Recursive struct definition|
|**Type**|`fatalTypeError`|
|**Message**|```Recursive struct definition```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...]()|
|**Contributors**|CJ42|


**Description**

You cannot declare a `struct` which has a member declared with the same type.

**Example**

```solidity
pragma solidity ^0.5.0;

contract FootballTeam {

    struct Player {
        string name;
        uint8 age;
        Player mentor;
    }

}


```

**Solution**
