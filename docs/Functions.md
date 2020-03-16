# Functions

You will find below all the errors and warnings related to functions in Solidity.

---

## Unused function parameter

|Heading|Description|
|-|-|
|**Title**|Unused function parameter|
|**Type**|`warning`|
|**Message**|```Unused function parameter. Remove or comment out the variable name to silence this warning.```|
|**Solidity version**||
|**Reference**|[StaticAnalyzer.cpp, Line 124](https://github.com/ethereum/solidity/blob/efd8d8fe5eced023476af71491e9eae3dbde4d87/libsolidity/analysis/StaticAnalyzer.cpp#L124)|
|**Contributors**||


**Description**



**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {

    function sayHello(string memory _name, uint8 _age) public pure returns (string memory) {
        string memory myName = _name;
        return myName;
    }
}
```

**Solution**

---

## No visibility specified in function declaration


|Heading|Description|
|-|-|
|**Title**|No visibility specified in function declaration|
|**Type**|`SyntaxError`|
|**Message**|```No visibility specified. Did you intend to add "public"```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Line...](#)|
|**Contributors**|CJ42|


**Description**

The function does not specify a visibility.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Test {

    function run() {
        // do something
    }

}
```

**Solution**

Declare your function with one of the following visibility : `public`, `private`, `internal` or `external`.

---

## Function with same name and argument defined twice

|Heading|Description|
|-|-|
|**Title**|Function with same name + argument defined twice|
|**Type**|`declarationError`|
|**Message**|```Function with same name and arguments defined twice.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, |
|**Contributors**|CJ42|


**Description**

Two functions with the same names and arguments are defined in your smart contract.

**Example**

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    function foo() public pure returns(string memory) {
        return "foo";
    }
    
    function foo() public pure returns(string memory) {
        return "foo";
    }
    
}
```

**Solution**

You can declare several function with the same name (_eg:_ `foo()`) but each function should have different set of arguments.

```solidity
pragma solidity ^0.5.10;

contract Example {
    
    function foo() public pure returns(string memory) {
        return "foo";
    }
    
    function foo(string memory _string) public pure returns(string memory) {
        return _string;
    }
    
}
```

---

## Different return type when overriding function

|Heading|Description|
|-|-|
|**Title**|Different return type when overriding function|
|**Type**|`typeError / overrideError`|
|**Message**|```Overriding function return types differ.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, |
|**Contributors**|CJ42|


**Description**

The contract overrides a function from an inherited contract but specifies a different type for the return value.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Greetings {

    function hello() external pure returns (string memory);

    function goodbye() external pure returns (string memory);

}

contract French is Greetings {
    
    function hello() external pure returns (string memory) {
        return "Bonjour";
    }

}

contract Robot is Greetings {

    function hello() external pure returns (uint) {
        return 1;
    }
}
```

**Solution**



---

## Different visibility when overriding function

|Heading|Description|
|-|-|
|**Title**|Different visibility when overriding function|
|**Type**|`typeError / overrideError`|
|**Message**|```Overriding function visibility differs.```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 190 - 194](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L190-L194)|
|**Contributors**|CJ42|


**Description**

The contract overrides a function from an inherited contract but specifies a wrong visibility type. You can only overrides a function in Solidity with the same visibility scope :

- `public`  <---> `external`
- `private` <---> `internal`


**Example**

```solidity
pragma solidity ^0.5.0;

contract Token {
    
   function transfer(address _to, uint256 _value) external returns (bool success) {
       // your code here
   }

}

contract StandardToken is Token {
    
    function transfer(address _to, uint256 _value) internal returns (bool success) {
        // your code here
    }
    
}
```

**Solution**

The following overriding options are available :

- from `external` to `public`
- from `public` to `external`
- from `internal` to `private`
- from `private` to `internal`

---

## Different State Mutability when overriding function

|Heading|Description|
|-|-|
|**Title**|Different State Mutability when overriding function|
|**Type**|`typeError / overrideError`|
|**Message**|```"Overriding function changes state mutability from < State Mutability 1 > to < State Mutability 2 >."```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 196 - 205](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L196-L205)|
|**Contributors**|CJ42|


**Description**

The contract overrides a function from an inherited contract but implements a different state mutability (`view`, `pure` or nothing).

**Example**

```solidity
pragma solidity ^0.5.0;

contract Token {
    
   function transfer(address _to, uint256 _value) external pure returns (bool success) {
       // your code here
   }

}

contract StandardToken is Token {
    
    function transfer(address _to, uint256 _value) external view returns (bool success) {
        // your code here
    }
    
}
```


**Solution**

Make sure that the overriden function implements the same state mutability than the initial function.

---

## Implemented function redeclared as abstract

|Heading|Description|
|-|-|
|**Title**|Implemented function redeclared as abstract|
|**Type**|`typeError`|
|**Message**|```Redeclaring an already implemented function as abstract```|
|**Solidity version**||
|**Reference**|ContractLevelChecker.cpp, [Lines 235 - 236](https://github.com/ethereum/solidity/blob/4f7fec6911482c9c3f8fbf2e3fa5874597648fc6/libsolidity/analysis/ContractLevelChecker.cpp#L235-L236)|
|**Contributors**|CJ42|


**Description**

A contract re-implements a function inherited from an other contract but declares it as abstract.

**Example**

```solidity
pragma solidity ^0.5.0;

contract Greetings {
    
   function sayHello() public pure returns (string memory) {
        return 'hello';
    }

}

contract Person is Greetings {
    
    function sayHello() public pure returns (string memory);
    
}
```

**Solution**


---

## Function not visible by other function call

|Heading|Description|
|-|-|
|**Title**|Function not visible by other function call|
|**Type**|`declarationError`|
|**Message**|```Undeclared identifier. <function1> is not (or not yet) visible at this point.```|
|**Solidity version**||
|**Reference**|ReferencesResolver.cpp, [Lines 99 - 111](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/ReferencesResolver.cpp#L99-L111)|
|**Contributors**|CJ42|


**Description**

**Example**

In the following example, our function `testTwo()` cannot execute because it is calling a function `testOne()` declared as `external`, therefore, not callable inside the contract.

```solidity
pragma solidity ^0.5.0;

contract Test {
    
    function testOne() external {
        // do something
    }
    
    function testTwo() public {
        testOne();
    }
}
```

**Solution**

---

## Function have the same name of the contract

|Heading|Description|
|-|-|
|**Title**|Function have the same name of the contract|
|**Type**|`SyntaxError`|
|**Message**|```Functions are not allowed to have the same name as the contract. If you intend this to be a constructor, use "constructor(...) { ... }" to define it.```|
|**Solidity version**|since 0.5|
|**Reference**|[SyntaxChecker.cpp, Lines...(#)|
|**Contributors**||


**Description**

This error describes a `function` that uses the same name than the contract name. This is not allowed in solidity

**Example**

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    function Example() public {
        // do something
    }

}
```

**Solution**

Use the `constructor() public` syntax. This function will run only once your contract is deployed.

```solidity
pragma solidity ^0.5.0;

contract Example {
    
    constructor() public {
        // do something
    }

}
```

---

## Naming function type parameters is deprecated.

|Heading|Description|
|-|-|
|**Title**|Naming function type parameters is deprecated.|
|**Type**|`warning`|
|**Message**|```Naming function type parameters is deprecated.```|
|**Solidity version**||
|**Reference**|[SyntaxChecker.cpp, Lines...]())|
|**Contributors**||


**Description**

This example describes that types are mentioned for parameters 

**Example**

**Solution**




---

## Function Signature Hash Collision

|Heading|Description|
|-|-|
|**Title**|Function Signature Hash Collision|
|**Type**|`TypeError`|
|**Message**|```Function signature hash collision for [function_name]```|
|**Solidity version**||
|**Reference**|[ContractLevelChecker.cpp, lines 445-449](https://github.com/ethereum/solidity/blob/d5b2f347bf481151ff03fb6dea08e7ce1ce7194c/libsolidity/analysis/ContractLevelChecker.cpp#L445-L449)|
|**Contributors**||


**Description**

This error occurs in Solidity when two functions generates exactly the same signature. This is a really case scenario.

**Example**

This is an example where two Solidity functions generate the same signature.

```
pragma solidity ^0.5.0;

contract a {
    
    function withdraw(uint256) public {
        
    }
    
    
    function OwnerTransferV7b711143(uint256) public {
        
    }
    
}

```

Another example of hash collision occurs below, but with variable name.

```
pragma solidity ^0.5.0;

// example 1
contract a {
    int public gsf;
    int public tgeo;
}

```

**Solution**

Define a different function name for one of the two functions for which the signature collides.

**References**

- https://ethereum.stackexchange.com/questions/23743/what-if-two-ether-functions-have-the-same-signature

- https://www.bitdegree.org/learn/solidity-functions#function-overloading

- https://www.reddit.com/r/ethdev/comments/6n6t9w/function_hash_collision_potential_misuse/
- https://www.4byte.directory/


---

## Function Overload clash

|Heading|Description|
|-|-|
|**Title**|Function overload clash|
|**Type**|`TypeError`|
|**Message**|```Function overload clash during conversion to external types for arguments.```|
|**Solidity version**||
|**Reference**|[ContractLevelChecker.cpp, lines 432 - 436](https://github.com/ethereum/solidity/blob/d5b2f347bf481151ff03fb6dea08e7ce1ce7194c/libsolidity/analysis/ContractLevelChecker.cpp#L432-L436)|
|**Contributors**||


**Description**



**Example**

```
pragma solidity >=0.4.16 <0.7.0;

contract A {
    function f(B _in) public pure returns (B out) {
        out = _in;
    }

    function f(address _in) public pure returns (address out) {
        out = _in;
    }
}

contract B {
}
```

**Solution**

**References**

- https://github.com/ethereum/solidity/issues/4832

- https://github.com/ethereum/solidity/issues/3755


---

## Return Statement ___different than___ Return Declaration

|Heading|Description|
|-|-|
|**Title**|Return Statement ___different than___ Return Declaration|
|**Type**|`TypeError`|
|**Message**|```Different number of arguments in return statement than in returns declaration.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error in Solidity describe that the number of arguments specified in the `return` statement (within the function) is different than the number of arguments specified in the `returns` declaration. 


**Example**

```
pragma solidity ^0.5.0;

contract Example {
    
    function test() public pure returns (uint, uint) {
        return (1, 2, 3);
    }

}
```

**Solution**

The number of arguments specified in `returns` and `return` must be the same.

---

## Implicit conversion error in `return` statement

|Heading|Description|
|-|-|
|**Title**|Implicit conversion error in `return` statement|
|**Type**|`TypeError`|
|**Message**|```"Return argument type [type1] is not implicitly convertible to expected type [type2]."```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract Test {
    
    enum NUMBERS { ZERO, ONE, TWO }
    
    uint nb1;
    string nb2;
    
    function getNumbers() public view returns(uint, uint) {
        return (nb1, NUMBERS.ONE);
    }

}
```

**Solution**



---



# `virtual` and `private` cannot be used together

|Heading|Description|
|-|-|
|**Title**||
|**Type**||
|**Message**||
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

In Solidity, functions defined as `private` are visible only in the contract they are defined in, not the inheritting contracts.

A function defined with the `virtual` keyword can be **overriden** in inheritting contracts.

Therefore, these two keywords conflict and cannot be used together.

**Example**

```
pragma solidity ^0.6.0;

contract A {

    function test() private virtual {
        // some logic here
    }
    
}
```

**Solution**

If you want your future contracts to be able to override this function, then the best case would be to define it as `internal`.

-----

## Functions without implementation must be declared `virtual`

|Heading|Description|
|-|-|
|**Title**|Functions without implementation must be declared `virtual`|
|**Type**|`TypeError`|
|**Message**|```Functions without implementation must be marked virtual.```|
|**Solidity version**|since 0.6.0|
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.6.0;

contract Example {

    function g() public {
        // some code here
    }
    
    function f() public;
    
}
```

**Solution**


-----

# Duplicate named arguments

|Heading|Description|
|-|-|
|**Title**|Duplicate named arguments|
|**Type**|`TypeError`|
|**Message**|```Duplicate named argument <arg>```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**

```
pragma solidity ^0.5.0;

contract test {
    
    function a(uint a, uint b) public returns (uint r) {
        r = a + b;
    }
    
    function b() public returns (uint r) {
        r = a({a: 1, a: 2});
    }
    
}
```

**Solution**


-----

# Named argument does not match function declaration

|Heading|Description|
|-|-|
|**Title**|Named argument does not match function declaration|
|**Type**|`TypeError`|
|**Message**|```Named argument does not match function declaration```|
|**Solidity version**||
|**Reference**|TypeChecker.cpp|
|**Contributors**||


**Description**

**Example**


```
pragma solidity ^0.5.0;

contract test {
    
    function a(uint a, uint b) public returns (uint r) {
        r = a + b;
    }
    
    function b() public returns (uint r) {
        r = a({a: 1, c: 2});
    }

    
}
```



**Solution**