# Types of Errors and Warnings in Solidity

While you are writing smart contracts in Solidity, you will encounter different type of errors. The table below summarizes the different type of errors.

|Type|Description|
|:--|:---------|
|`warning`|Can compile, but can potentially lead to security issues in your smart contract.|
|`SyntaxError`|Error related to the syntax|
|`TypeError`|Error related to the type|
|`FatalTypeError`|Error related to the type, stop parsing|
|`DeclarationError`|Error related to variable declaration|
|`FatalDeclarationError`|Error related to variable declaration, stop parsing|
|`ParserError`|Internal error related to the Parser|

The difference with the errors declared as `Fatal` is than the parser / compiler will throw and abort [see file ReferenceResolver.cpp for more explanation](https://github.com/ethereum/solidity/blob/develop/libsolidity/analysis/ReferencesResolver.h).