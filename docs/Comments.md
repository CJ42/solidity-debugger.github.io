# Comments

Most of the errors in this section are related with the use Natspec comments and doxygen tags.

## Documented parameter not found

|Heading|Description|
|-|-|
|**Title**|Documented parameter not found |
|**Type**|`DocstringParsingError`|
|**Message**|```Documented parameter [parameter name] not found in the parameter list of the function.```|
|**Solidity version**||
|**Reference**|[DocStringAnalyser.cpp, lines 87 - 92](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/DocStringAnalyser.cpp#L87-L92)|
|**Contributors**||


**Description**

This error occurs with Natspec comments, when a function parameter documented with the `@param` tag is not listed in the function.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    /**
     * @param a value to pass
     * @param b true or false
     * @param c a parameter that does not exist
     */
    function test(uint a, bool b) public pure returns (uint) {
        
    }

}
```

**Solution**


---

## Doc Tag name invalid

|Heading|Description|
|-|-|
|**Title**|Doc Tag name invalid|
|**Type**|`DocstringParsingError`|
|**Message**|```Doc tag @<tag> not valid for <node-name>```|
|**Solidity version**||
|**Reference**|DocStringAnalyse.cpp, [Line 134](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/DocStringAnalyser.cpp#L134)|
|**Contributors**|CJ42|


**Description**

This error message describe the use of a doxygen tag not allowed for a specific element in your Solidity contract.

**Example**

The example below will output the following error message : `Doc tag @title not valid for functions.`

```solidity
pragma solidity ^0.5.0;

contract Math {
    
    /// @notice Math function to calculate square root
    /// @dev Not working with decimal numbers
    /// @param x The number to calculate the square root of
    /// @return y The square root of x
    /// @title sqrt()
    function sqrt(uint x) internal pure returns (uint y) {
        uint z = (x + 1) / 2;
        y = x;
        while (z < y) {
            x = z;
            z = (x / z + z) / 2;
        }
    }
}
```

**Solution**

Please refer to the [Solidity documentation](https://solidity.readthedocs.io/en/v0.5.10/natspec-format.html?highlight=natspec#tags) to understand how to format **doxygen tags**.


---

## End of tag name not found

|Heading|Description|
|-|-|
|**Title**|Doc Tag name invalid|
|**Type**|`DocstringParsingError`|
|**Message**|```End of <tag-name> not found```|
|**Solidity version**||
|**Reference**||
|**Contributors**|CJ42|


**Description**

This error message describe the use of a doxygen tag with no termination

**Example**

The example below will output the following error message : `Doc tag @title not valid for functions.`

```solidity
pragma solidity ^0.5.0;

contract Math {
    
    /// @notice Math function to calculate square root
    /// @dev Not working with decimal numbers
    /// @param
    function sqrt(uint x) internal pure returns (uint y) {
        uint z = (x + 1) / 2;
        y = x;
        while (z < y) {
            x = z;
            z = (x / z + z) / 2;
        }
    }
}
```

**Solution**

Please refer to the [Solidity documentation](https://solidity.readthedocs.io/en/v0.5.10/natspec-format.html?highlight=natspec#tags) to understand how to format **doxygen tags**.

