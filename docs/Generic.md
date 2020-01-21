# Generic errors

## Badly declared keyword

|Heading|Description|
|-|-|
|**Title**|Badly declared identifier|
|**Type**|`declaration error`|
|**Message**|```Undeclared identifier. Did you mean...```|
|**Solidity version**||
|**Reference**|ReferencesResolver.cpp, [Lines 99 - 111](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L99-L111)|
|**Contributors**|CJ42|


**Description**

This error happen when a keyword is badly written.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    address owner;
    
    modifier isOwner {
        requore(owner == msg.sender);
        _;
    }
}
```

**Solution**

Correct the error using the correct keyword suggestion given by the Solidity compiler.

---

## Statement without effect

|Heading|Description|
|-|-|
|**Title**|Statement without effect|
|**Type**|`warning`|
|**Message**|```Statement has no effect```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, Line 185](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/StaticAnalyzer.cpp#L185)|
|**Contributors**|CJ42|


**Description**

This Solidity warning specifies that the indicated statement does not do anything.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    function test2() pure internal {
        5;
    }
    
}
```

**Solution**


---

## Unreachable code

|Heading|Description|
|-|-|
|**Title**|Unreachable code|
|**Type**|`warning`|
|**Message**|```unreachable code```|
|**Solidity version**||
|**Reference**|[ContractFlowAnalyzer.cpp, line 179](https://github.com/ethereum/solidity/blob/d5b2f347bf481151ff03fb6dea08e7ce1ce7194c/libsolidity/analysis/ControlFlowAnalyzer.cpp#L179)|
|**Contributors**||


**Description**

This warning mentions that one (or several) statement(s) in your contract code will never execute. This is because the logic flow in your contract either `return` or stop (`revert` or other case) before this (these) statement(s). See the example below.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    function test(uint _value) public pure returns (bool) {
        
        if ( _value < 10 ) {
            revert();
            _value = 12;
        }
    }
     
}
```

**Solution**

**Reference**

- https://ethereum.stackexchange.com/questions/66001/warning-unreachable-code-in-for-loop-in-solidity-version-0-5-3
- https://github.com/ethereum/solidity/issues/5133
- https://github.com/ethereum/solidity/issues/2340

---

## Use of built-in symbol name for variable or function declaration

|Heading|Description|
|-|-|
|**Title**|Use of built-in symbol name for variable or function declaration|
|**Type**|`warning`|
|**Message**|```This declaration shadows a builtin symbol.```|
|**Solidity version**||
|**Reference**|[NameAndTypeResolver.cpp, lines 524 - 528](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/NameAndTypeResolver.cpp#L524-L528)|
|**Contributors**||


**Description**

This error mentions a variable or function that is declared with the same name as a Solidity's **[special global variable](https://solidity.readthedocs.io/en/v0.5.12/units-and-global-variables.html#special-variables-functions)**. Such variables are also called _built-in symbols_
or _"magic global variables"_ (`msg`, `tx`, `keccak256`...). See the example below.

**Example**

```
pragma solidity ^0.5.0;

contract Example {

    string gasleft;
    uint tx;
    uint selfdestruct;
    
    function keccak256() public pure;

}
```

**Solution**

**References**

- https://github.com/gnosis/MultiSigWallet/issues/29
- https://github.com/ethereum/mist/issues/4046

---

## `return` arguments not allowed

|Heading|Description|
|-|-|
|**Title**|`return` arguments not allowed|
|**Type**|`TypeError`|
|**Message**|```Return arguments not allowed```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error in Solidity refers to a situation where the `return` keyword is mentioned in a place that is not allowed.

**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    modifier Fee(uint _fee) {
        uint total_fee = msg.value + _fee;
        return total_fee;
        _;
        
    }

}
```

**Solution**


---

## Declaration shadows an existing declaration

|Heading|Description|
|-|-|
|**Title**|Declaration shadows an existing declaration|
|**Type**|`warning`|
|**Message**|```This declaration shadows an existing declaration. The shadowed declaration is here```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

**Example**

```
contract Example {
    
    uint a;
    
    function f() public {
        uint a = 32;
    }
    
}
```

**Solution**


---

## Identifier not found or not unique

|Heading|Description|
|-|-|
|**Title**|Identifier not found or not unique|
|**Type**|`fatalDeclarationError`|
|**Message**|```Identifier not found or not unique.```|
|**Solidity version**||
|**Reference**|[ReferencesResolver.cpp, lines 176 - 180](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L176-L180)|
|**Contributors**||


**Description**

Occurs if you do not specify an identifier from the list of the file [/liblangutil/Token.h](https://github.com/ethereum/solidity/blob/develop/liblangutil/Token.h).


**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    intX test2;
    
}
```

**Solution**


---

## Return arguments required

|Heading|Description|
|-|-|
|**Title**|Return argument required|
|**Type**|`TypeError`|
|**Message**|```Return arguments required```|
|**Solidity version**||
|**Reference**|[TypeChecker.cpp, line 783](https://github.com/ethereum/solidity/blob/78be93856b469ca45da87ad372427cf18752b042/libsolidity/analysis/TypeChecker.cpp#L783)|
|**Contributors**||


**Description**

The Solidity compiler raises this error when a function definition contains a `returns` statement, but the final `return` statement is empty and has no arguments.

**Example**

```
pragma solidity ^0.5.0;

  
contract C {
    
    function f() public pure returns (uint) {
        return;
    }

}
```

**Solution**
