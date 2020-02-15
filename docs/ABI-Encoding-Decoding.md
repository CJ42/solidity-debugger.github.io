# ABI Encoding & Decoding

The errors below relate to the `abi` methods.

## More / Less than two arguments for `abi.decode()`

|Heading|Description|
|-|-|
|**Title**|More / Less than two arguments for `abi.decode()`|
|**Type**|`TypeError`|
|**Message**|```This function takes two arguments, but " + toString(arguments.size()) + " were provided.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, lines 133 - 135 ](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L133-L135)|
|**Contributors**||


**Description**

Solidity gives you an error message when you provide more (or less) than two arguments to the `abi.decode()` built-in function.

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
  function f() public pure {
    abi.decode();
    abi.decode(msg.data);
    abi.decode(msg.data, uint, uint);
  }
  
}
```

**Solution**

The [Solidity documentation](https://solidity.readthedocs.io/en/v0.5.12/units-and-global-variables.html#abi-encoding-and-decoding-functions) explains how the `abi.decode()` function must be used. You must pass a value of `bytes` type as a first parameter, and then provide the types between parentheses as second argument.

```
abi.decode(bytes memory encodedData, (...)) returns (...)
```

Example: 

```
(uint a, uint[2] memory b, bytes memory c) = abi.decode(data, (uint, uint[2], bytes));
```

---

## Second argument to `abi.decode()` has to be a tuple of types

|Heading|Description|
|-|-|
|**Title**|Second argument to `abi.decode()` has to be a tuple of types|
|**Type**|`TypeError`|
|**Message**|```"The second argument to "abi.decode" has to be a tuple of types."```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 163](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L163)|
|**Contributors**||


**Description**

This error in Solidity occurs when you do not specify the second parameter of `abi.decode` between parentheses.

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
  function decodeNumber(bytes memory data) public pure returns (uint8) {
        uint8 nb = abi.decode(data, uint8);
        return nb;
    }
  
}
```

**Solution**

Write the second parameter of `abi.decode()` between parentheses, even if you need to return only one type.

```
pragma solidity ^0.5.0;

contract C {
    
  function decodeNumber(bytes memory data) public pure returns (uint8) {
        uint8 nb = abi.decode(data, (uint8));
        return nb;
    }
  
}
```

---

## Decoding type not supported

|Heading|Description|
|-|-|
|**Title**|Decoding type not supported|
|**Type**|`TypeError`|
|**Message**|```Decoding type [...] not supported```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line]()|
|**Contributors**||


**Description**

The `abi.decode()` built-in method in Solidity does not support `struct` as a decoding type.

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
    struct T {
        uint a;
        uint b;
    }
    
  function f() public pure returns (uint) {
    return abi.decode("abc", (T));
  }
  
}
```

**Solution**


---

## Argument has to be a type name

|Heading|Description|
|-|-|
|**Title**|Argument has to be a type name|
|**Type**|`TypeError`|
|**Message**|```Argument has to be a type name```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 197](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L197)|
|**Contributors**||


**Description**

Solidity gives you an error when you provides an other value than a type name to `abi.decode`

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
    function decodeNb(bytes memory data) public pure returns (uint8) {
        return abi.decode(data, (data));
    }
  
}
```

**Solution**


-----

## Fractional numbers cannot yet be encoded


|Heading|Description|
|-|-|
|**Title**|Fractional numbers cannot yet be encoded|
|**Type**|`TypeError`|
|**Message**|```Fractional numbers cannot yet be encoded.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.12;

contract Example {
    
    function test() public pure returns (bytes memory) {
        return abi.encode(32/7);
    }
    
}
```

**Solution**