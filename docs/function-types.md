# Functions types

## Visibility other than `external` or `internal` for function types.

|Heading|Description|
|-|-|
|**Title**|Visibility other than `external` or `internal` for function types.|
|**Type**|`FatalTypeError`|
|**Message**|```Invalid visibility, can only be "external" or "internal".```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 199 - 207](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L199-L207)|
|**Contributors**||


**Description**

The following error message occurs if you define a variable of function type as either private or public.

**Example**

```
pragma solidity ^0.5.0;

library ArrayUtils {
    // internal functions can be used in internal library functions because
    // they will be part of the same code context
    function map(uint[] memory self, function (uint) private returns (uint) f)
        internal
        pure
        returns (uint[] memory r)
    {
        r = new uint[](self.length);
        for (uint i = 0; i < self.length; i++) {
            r[i] = f(self[i]);
        }
    }

}
```

**Solution**

**References**

- https://solidity.readthedocs.io/en/v0.5.11/types.html#function-types


---

## External function type specified as payable

|Heading|Description|
|-|-|
|**Title**|External function type specified as payable|
|**Type**|`FatalTypeError`|
|**Message**|```Only external function types can be payable.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 209 - 213](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L209-L213)|
|**Contributors**||


**Description**

This error in Solidity occurs if you use the specifier `payable` is attached to a function type variable declared as `internal`.

**Example**

```
pragma solidity ^0.5.0;

library ArrayUtils {
    // internal functions can be used in internal library functions because
    // they will be part of the same code context
    function map(uint[] memory self, function (uint) internal payable returns (uint) f)
        internal
        pure
        returns (uint[] memory r)
    {
        r = new uint[](self.length);
        for (uint i = 0; i < self.length; i++) {
            r[i] = f(self[i]);
        }
    }

}
```

**Solution**



**References**

- https://solidity.readthedocs.io/en/v0.5.11/types.html#function-types

---

## Type not set for parameter in function type variable

|Heading|Description|
|-|-|
|**Title**|Type not set for parameter in function type|
|**Type**|`InternalCompilerError`|
|**Message**|```Type not set for parameter```|
|**Solidity version**|since 0.4.20|
|**Reference**|[ReferencesResolver.cpp, line 218](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L218)|
|**Contributors**||


**Description**

This error occurs in Solidity when you specify a variable of function type has not types set for its parameters.

**Example**

```
pragma solidity >=0.4.16 <0.7.0;

contract C {
    function a(function(Nested) external) external pure {}
}
```

**Solution**


---

## Internal type cannot be used for external function type.

|Heading|Description|
|-|-|
|**Title**|Internal type cannot be used for external function type|
|**Type**|`FatalTypeError`|
|**Message**|```Internal type cannot be used for external function type.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 219 - 223](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L219-L223)|
|**Contributors**||


**Description**

A function declared with the `external` visibility cannot accept function-type arguments which have `internal` visibility.

**Example**

```
pragma solidity ^0.5.0;

contract C {
    
    function() external returns (function () internal) x;
    
}
```

**Solution**


---

## Naming function type parameters is deprecated

|Heading|Description|
|-|-|
|**Title**|Naming function type parameters is deprecated|
|**Type**|`warning`|
|**Message**|```Naming function type parameters is deprecated.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, line 315](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/SyntaxChecker.cpp#L315)|
|**Contributors**||


**Description**


**Example**

```
pragma solidity ^0.4.0;

contract Example {
    
    function (uint a, uint b) internal returns (uint) variable_name;
    
}
```

**Solution**


-----

## Return parameters in function types may not be named

|Heading|Description|
|-|-|
|**Title**|Return parameters in function types may not be named|
|**Type**|`SyntaxError`|
|**Message**|```Return parameters in function types may not be named```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, lines...]()|
|**Contributors**||


**Description**

**Example**

```
contract C {
    
    function(uint) returns (bool ret) f;

}
```

**Solution**



-----

## Getter type only supported by ABIEncoderV2

|Heading|Description|
|-|-|
|**Title**|Getter type only supported by ABIEncoderV2|
|**Type**|`TypeError`|
|**Message**|```The following types are only supported for getters in the new experimental ABI encoder: [type used]. Either remove "public" or use "pragma experimental ABIEncoderV2;" to enable the feature."```|
|**Solidity version**|up to current version|
|**Reference**|[TypeChecker.cpp, lines ](#)|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.6.0;

contract C {
    
    struct Y {
        uint b;
    }
    
    struct X {
        Y a;
    }
    
    mapping(uint256 => X) public m;
    
}
```

**Solution**



**References**

- https://github.com/ethereum/solidity/blob/develop/test/libsolidity/syntaxTests/getter/nested_structs.sol

-----