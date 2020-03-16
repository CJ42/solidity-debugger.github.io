# Array

## Invalid array length

|Heading|Description|
|-|-|
|**Title**|Invalid array length|
|**Type**|`fatalTypeError`|
|**Message**|```Invalid array length, expected integer literal or constant expression.```|
|**Solidity version**||
|**Reference**|ReferencesResolver.cpp, [Lines 256 - 257](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L256-L257)|
|**Contributors**|CJ42|


**Description**

This error occur when you specify the length of a fixed size array with a value that is not constant (Like a variable of `uint` type that can be modified);

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    uint _length = 10;
    
    uint[_length] my_array;
}
```

**Solution**

Specify the length of your array with a literal number (5, 10, 238...) or a constant variable.

---

## Array with negative length specified

|Heading|Description|
|-|-|
|**Title**|Array with negative length specified|
|**Type**|`fatalTypeError`|
|**Message**|```Array with negative length specified.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, Lines 262 - 263](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L262-L263)|
|**Contributors**|CJ42|


**Description**

An variable of type fixed-size array is declared with a length being a negative number.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    uint[-5] my_array;
    
}
```

**Solution**

Use a positive number to specify the length of your fixed-size array.

---

## Array with zero length specified

|Heading|Description|
|-|-|
|**Title**|Array with zero length specified|
|**Type**|`fatalTypeError`|
|**Message**|```Array with zero length specified.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, Lines 258 - 259](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L258-L259)|
|**Contributors**|CJ42|


**Description**

An variable of type fixed-size array is declared with a length being 0.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    uint[0] my_array;
    
}
```

**Solution**

Use a positive number to specify the length of your fixed-size array.

---

## Array to large to be encoded

|Heading|Description|
|-|-|
|**Title**|Array to large to be encoded|
|**Type**|`TypeError`|
|**Message**|```Array is too large to be encoded.```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, Lines...](#)|
|**Contributors**|CJ42|


**Description**

This error occurs when you define a fixed-size array that contains more than 134,217,727 indexes. This appear to be the maximum limit of a working storage. See the links below for related topic

- https://www-01.ibm.com/support/docview.wss?uid=swg21220835
- https://www.ibm.com/support/knowledgecenter/en/SS6SG3_4.2.0/com.ibm.entcobol.doc_4.2/MG/igymapxg001.htm
- http://ibmmainframes.com/about56564.html


**Example**

pragma solidity ^0.5.0;

contract HugeArray {

    function notPossibleToEncode() public pure returns (bytes memory) {
        uint[134_217_728] memory large_array;
        return abi.encode(large_array); 
    }

}


**Solution**

Use a smaller value...


---

## Array with fractional length

|Heading|Description|
|-|-|
|**Title**|Array with Fractional Length|
|**Type**|`TypeError`|
|**Message**|```array with fractional length specified```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 260 - 261](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L260-L261)|
|**Contributors**||


**Description**

In Solidity, it is possible to define a fixed-size array with a fractional length. However, the result of the fraction must be an integer, not a decimal point. So `my_array[10/5]` is allowed, but not `my_array[3/2]`.

**Example**

```
pragma solidity >0.5.0;

contract Example {
    
    uint[3/2] my_array;
    
}
```

**Solution**


---

## Variable cover large part of storage

|Heading|Description|
|-|-|
|**Title**|Variable cover large part of storage|
|**Type**|`warning`|
|**Message**|```Variable covers a large part of storage and thus makes collisions likely. Either use mappings or dynamic arrays and allow their size to be increased only in small quantities per transaction.```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, lines 161 - 163](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/StaticAnalyzer.cpp#L161-L163)|
|**Contributors**||


**Description**



**Example**

```
pragma solidity ^0.5.0;

contract c {
    uint[2**253] data;
}
```

**Solution**


-----

## Empty array component

|Heading|Description|
|-|-|
|**Title**|Empty array component|
|**Type**|`FatalTypeError`|
|**Message**|```Array component cannot be empty```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error occurs when an array is defined but one of its component is empty. The errors is generated for both an inline array (within a function body), or an array that is part of a contract's storage (defined outside a function).

**Example**

```solidity
pragma solidity ^0.5.10;

contract Greetings {
    
    function doNothing() public pure {}
    
    string[3] greetings = ["Hello", "Ola", doNothing()];
     
}

```

**Solution**


-----

## Inline array cannot be declared as lvalue

|Heading|Description|
|-|-|
|**Title**|Inline array cannot be declared as lvalue|
|**Type**|`FatalTypeError`|
|**Message**|```Inline array type cannot be declared as LValue.```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**


```
pragma solidity ^0.5.0;

contract C {
    function f() public {
        [1, 2, 3]++;
        [1, 2, 3] = [4, 5, 6];
    }
}
```

**Solution**


-----

## Out of bounds array access

|Heading|Description|
|-|-|
|**Title**|Out of bounds array access|
|**Type**|`TypeError`|
|**Message**|```Out of bounds array access```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, lines 2230](https://github.com/ethereum/solidity/blob/508cf66da2bdfb7e6677029c9671a0f3ffec68b8/libsolidity/analysis/TypeChecker.cpp#L2230)|
|**Contributors**||


**Description**

This error occurs when you try to access an index that is out of the limit of the array.

**Example**

```
pragma solidity ^0.5.10;

contract Test {
    
    uint8[5] foo = [1,2,3,4,5];
    
    function getElement() public view returns(uint8) {
        return foo[5];
    }
    
}
```

**Solution**
