# Thank you for the help and support from :

<img src="https://i.ibb.co/WkYKKBN/work-on-blockchain-logo.png" height="180px">
<img src="https://i.ibb.co/9H9bbD5/extropy-logo.png" height="180px">
<img src="https://i.ibb.co/r63pHSb/nethermind-logo.png" height="180px">
<img src="https://i.ibb.co/cyc942m/pisa-logo.png" height="180px">


# What is the problem with Solidity?

> Writing smart contracts in Solidity is hard !

<p>If you use Remix, you will quickly get errors displayed in the IDE, which will make you unable to compile and test your contract.</p>

<p>Most errors related to Solidity are not self explanatory. Mostly because they relate directly to the inner working of the EVM, a Virtual Machine quite complex to understand.</p>

<p>To fix your errors, several options:
<ul>
<li>Googling the error message</li>
<li>Posting your code and ask on community forums</li>
<li>Trial and errors</li>
</ul>
</p>

> We need an universal registry to lookup our Solidity errors messages and debug them efficiently.

# What is the Solidity Debugger List?

The Solidity Debugger List is a curated list of all the Errors and Warning messages from the Solidity Compiler, including explanations about each messages.

The errors messages are categorised by core components, or variable types from the Solidity language.

<h3>Click on the left side bar to start exploring them!</h3>
<br>
Each error messages is listed with two code examples::

<ul>
<li>bad code example (to generate the error)</li>
<li>good code example (to solve the error)</li>
</ul>

This aim to help Ethereum smart contract developers to debug their Solidity code, whether they are using the Remix IDE or the `solc` CLI tool. 

The list is based on the official C++ source code from the Solidity compiler. All the errors and warnings listed in this website are referenced to the original source file + line number for better analysis. Such files include those located in the folder [`libsolidity/analysis`](https://github.com/ethereum/solidity/tree/develop/libsolidity/analysis). Some explanations and solutions are provided to help debugging.