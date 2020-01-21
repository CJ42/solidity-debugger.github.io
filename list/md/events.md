# Events debug

The listing below summarize all the errors and warnings related to `event` in Solidity.

|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>More than 3 indexed arguments for event.</pre>||_TypeChecker.cpp_, [Line ...](#)|

Events in Solidity can have up to 3 arguments indexed.

**Error (example) :**

```solidity
event TransferConfirmation(
    address indexed _sender,
    address indexed _recipient,
    uint indexed _amount,
    string indexed _message
);
```

**Solution (example) :**

```solidity
event TransferConfirmation(
    address indexed _sender,
    address indexed _recipient,
    uint indexed _amount,
    string _message
);
```
-----


|**Error Type**|**Message**|**Compiler Version**|**Source**|
| --- | --- | --- | --- |
| **typeError**|<pre>More than 4 indexed arguments for anonymous event.</pre>||_TypeChecker.cpp_, [Line ...](#)|

Events declared as anonymous in Solidity can have up to 4 arguments indexed.

**Error (example) :**

```solidity
event TransferConfirmation(
    address indexed _sender,
    address indexed _recipient,
    uint indexed _amount,
    string indexed _message
    string indexed _received
) anonymous;
```

**Solution (example) :**

```solidity
event TransferConfirmation(
    address indexed _sender,
    address indexed _recipient,
    uint indexed _amount,
    string indexed _message,
    string _received
) anonymous;
```