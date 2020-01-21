# Numbers in Solidity

This list references all the errors and warnings related to numbers in Solidity.



|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Invalid use of underscores in number literal. No trailing underscores allowed.</pre>||_SyntaxChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
uint constant bitcoin_supply = 21_000_000_;
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Invalid use of underscores in number literal. Only one consecutive underscores between digits allowed.</pre>||_SyntaxChecker.cpp_, [Line ...](#)|

**Error (example) :**

```solidity
uint constant bitcoin_supply = 21_000__000;
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **SyntaxError**|<pre>Invalid use of underscores in number literal. No underscores in front of the fraction part allowed.</pre>||_SyntaxChecker.cpp_, [Line 236 - 240](https://github.com/ethereum/solidity/blob/1cc8475309dd1ae36436b0a5cb2285de0e679a35/libsolidity/analysis/SyntaxChecker.cpp#L236-L240)|

**Error (example) :**

```solidity
fixed constant test1 = 10_000_.5;
fixed constant test2 = 10_000_.5;
```
-----
