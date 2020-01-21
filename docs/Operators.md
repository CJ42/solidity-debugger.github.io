# Operators

## Invalid data type comparison 

|Heading|Description|
|-|-|
|**Title**|Invalid Operator Comparison|
|**Type**|fatalTypeError|
|**Message**|```Operator <operator symbol> not compatible with types <type 1> and <type 2>```|
|**Solidity version...**||
|**Reference**|ConstantEvaluator.cpp, [Lines 48-56](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ConstantEvaluator.cpp#L48-L56)|
|**Contributors**|CJ42|


**Description**

This error occur when you compare two strings of invalid type

**Example**

```solidity
pragma solidity ^0.5.0;

contract Greetings {
    
    string nationality = "chineese";
    
    modifier inChinese {
        require(nationality == "chineese");
        _;
    }
    
   function sayHello() public pure inChinese returns (string memory) {
        return 'Nihao';
    }

}
```

**Solution**

For comparing strings, use the built-in function `keccak256()` to compare if both strings are equal.
Note that you might need to convert the `string` into `bytes` first to pass your string as a parameter of `keccak256`. You can do that using the built-in function `abi.encodePacked()`.

```solidity
pragma solidity ^0.5.0;

contract Greetings {
    
    string nationality = "chineese";
    
    modifier inChinese {
        require(keccak256(abi.encodePacked(nationality)) == keccak256("chineese"));
        _;
    }
    
   function sayHello() public view inChinese returns (string memory) {
        return 'Nihao';
    }

}
```

