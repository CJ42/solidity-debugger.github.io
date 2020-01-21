# Math operations

## Division by zero

|Heading|Description|
|-|-|
|**Title**|Division by zero|
|**Type**|`typeError`|
|**Message**|```Division by zero```|
|**Solidity version**||
|**Reference**|[StaticAnalyser.cpp, Line 284-288](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/StaticAnalyzer.cpp#L284-L288)|
|**Contributors**|CJ42|


**Description**

**Example**

```solidity
function divide(uint _number) public pure {
    uint result = _number / 0;
}
```

**Solution**
