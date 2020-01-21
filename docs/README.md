# Solidity Compiler Debug List
A curated list of all the Errors and Warning from the Solidity Compiler.

This repository aims to help Smart Contracts Developers on Ethereum to debug their Solidity files. It offers a list of all the errors and warnings you can possibly encounter when developing with the Remix IDE or during compilation with `solc`.

The list is based on the official C++ source code from the Solidity compiler. The errors and warning messages are all mentioned in the files located in the folder [`libsolidity/analysis`](https://github.com/ethereum/solidity/tree/develop/libsolidity/analysis). 

All the errors and warnings listed below are referenced to the original source file + line number for better analysis. Some explanations and solutions are provided to help debugging.

# What are the errors and warnings in Solidity

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


# Current Status of the Debuger List

The table below list the current state of all the errors reported and described from the Solidity compiler.

- ConstantEvaluator : **2/2** :white_check_mark:
- ContractLevelChecker : **18** / 32
- ContractFlowAnalyzer : **1** / 4
- DeclarationContainer : 0 / 3
- StaticAnalyzer : **8** / 12
- SyntaxChecker : /29
- TypeChecker : /192




- DocStringAnalyser : / 3
- NameAndTypeResolver : / 20
- PostTypeChecker : / 2
- ReferencesResolver : / 20
- ViewPureChecker : / 5

-----


