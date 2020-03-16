# Errors related to Built-in functions

Here are a list of all the errors and warnings related to Solidity built-in functions :

|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>"msg.gas" has been deprecated in favor of "gasleft()"</pre>||_StaticAnalyzer.cpp_, [line 195-199](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L195-L199)|

Simply replace `msg.gas` by `gasleft()`.


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>"block.blockhash()" has been deprecated in favor of "blockhash()"</pre>||_StaticAnalyzer.cpp_, [line 200-204](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L200-L204)|

Simply replace `block.blockhash()` by `blockhash()`.


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>"callcode" has been deprecated in favour of "delegatecall".</pre>||_StaticAnalyzer.cpp_, [line 219-225](https://github.com/ethereum/solidity/blob/f05805c955f73fd2ea1d14dc9edf14b472631b17/libsolidity/analysis/StaticAnalyzer.cpp#L219-L225)|

Simply replace `callcode` by `delegatecall`.



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>"throw" is deprecated in favour of "revert()", "require()" and "assert()"</pre>||_SyntaxChecker.cpp_, [line ...](#)|

Simply replace `throw` by one of the following error handling function : `require()`, `revert()` or `assert()`.



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>The use of the "var" keyword is disallowed. The declaration part of the statement can be removed, since it is empty.</pre>||_SyntaxChecker.cpp_, [line ...](#)|


