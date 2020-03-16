# Debug your Solidity contract

Here is a list of all the errors and warnings related to contracts and constructors in Solidity :


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>The constructor of the contract (or its base) uses inline assembly. Because of that, it might be that the deployed bytecode is different from type(...).runtimeCode.</pre>||_StaticAnalyzer.cpp_, [line 213-214](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/StaticAnalyzer.cpp#L213-L214)|


To be solved

