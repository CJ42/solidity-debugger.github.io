# Experimental ABI

This section covers all the errors in Solidity related to the Experimental ABI features (ABIEncoderV2).

---

## Parameter type only available in ABIEncoderV2

|Heading|Description|
|-|-|
|**Title**|Parameter type only available in ABIEncoderV2|
|**Type**|`TypeError`|
|**Message**|```This type is only supported in the new experimental ABI encoder. Use "pragma experimental ABIEncoderV2;" to enable the feature.```|
|**Solidity version**||
|**Reference**||
|**Contributors**||


**Description**

This error describes the use of a parameter type for a function or event that is only available with the Experimental ABI (like a `struct`).

**Example**

```
pragma solidity ^0.5.0;

contract UserDirectory {
    
    struct User {
        string name;
        address addr;
    }

    mapping(address => User) users;
    string[] names;

    event UserAdded(address addr, User user);

    function addUser(User memory _user) public {
        users[_user.addr] = _user;
    }
    
}
```

**Solution**

If you want to be able to pass such parameter in a function or event, add at the beginning of your file the following pragma statement: `pragma experimental ABIEncoderV2`.