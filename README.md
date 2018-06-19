# History of cryptocurrencies

**Cryptocurrency**: a digital asset designed to work 

- as a medium of exchange that uses strong cryptography to secure financial transactions, 
- control the creation of additional units, 
- and verify the transfer of assets. 

Source: [Wikipedia](https://en.wikipedia.org/wiki/Cryptocurrency)

Cryptocurrencies use decentralized control through distributed ledger technology, typically a blockchain, that serves as a public transaction database

**Bitcoin**: considered the first decentralized cryptocurrency.

Since then...

**4,000** altcoin (alternative coins) variants of bitcoin have been created. 

**Formal Definition of cryptocurrency**:

1. The system does not require a central authority, distributed achieve consensus on its state
2. The system keeps an overview of cryptocurrency units and their ownership
3. The system defines whether new cryptocurrency units can be created. If new cryptocurrency units can be created, the system defines the circumstances of their origin and how to determine the ownership of these units
4. Ownership of cryptocurrency units can be proved cryptographically
5. The system allows transactions to be performed in which ownership of the cryptographic units is changed. A transaction statement can only be issued by an entity proving the current ownership of these units
6. If two different instructions for changing the ownership of the same cryptographic units are simultaneously entered, the system performs at most one of them

## A short history of crypto

**1998 - 2009: pre-Bitcoin years**

There have been previous attempts at creating online currencies with ledgers secured by encryption (B-Money and Bit Gold). They were formulated but never fully developed

**2008: Satoshi Nakamoto**

A paper called [Bitcoin - A Peer to Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) was posted to a mailing list discussion on cryptography. It was posted by someone calling themselves Satoshi Nakamoto, who is a mystery to this day

**2009: Bitcoin begins**

The Bitcoin software is made available to the public for the first time and mining - the process through which new Bitcoins are created and transactions are recorded and verified on the blockchain - begins

**2010: Bitcoin is valued for the first time**

As it had never been traded, only mined, it was impossible to assign a monetary value to the units of emerging cryptocurrency. In 2010, someone decided to sells theirs - 10,000 for two pizzas. If the buyer had hung onto those Bitcoins, at today's prices they would be worth more than $100 million

**2011: Rival cryptocurrencies emerge**

altcoins came on the scene to improve the original Bitcoin design by offering grater speed, anonymity, or some other advantage. Among the first were Namecoin and Litecoin. 

**2013 - Bitcoin price crashes**

Shortly after the price of Bitcoin reaches $1000 for the first time, the price quickly declined. Investors suffered losses when it plummeted to $300

**2014 - Scams and theft**

Mt. Gox went offline and lost 850,000 Bitcoins. Investigation are still trying to get to the bottom of exactly wht happened.

**2016 - Ethereum and ICOs**

One cryptocurrency came close to stealing Bitcoin's thunder. This platform is known as Ethereum. Ethereum's arrival was marked by the emergence of the Initial Coin Offerings (ICOs). These are fundraising platforms which offer investors the chance to trade what are often essetnailly stocks or shares in the startup venture. THe chinese government banned them outright. 

**2017 - Bitcoin reaches $10,000**

During this period the market cap of all cryptocoins rose from 11 billion to 300 billion. Blockchain sparked a revolution in fintech industry. 

**Terminology:**

**Blockchain** - A continuously growing list of records. Called blocks, which are linked and secured using cryptography.

Each block typically contains a hash pointer as a link to a previous block, a timestamp and transaction data.

**Peer-to-Peer network** - P2P computing or networking is a distributed application architecture that partitions tasks or workloads between peers.

Peers are equally privileged, equipotent participants in the application. They are said to form a peer-to-peer network of nodes.

**Why secure?**

Security and immutability is important for a couple reasons.

**Immutability** - once data has been written to a blockchain no one, not even a system administrator, can change it.

This provides benefits for audit. As a provider of data you can prove that your data hasn’t been altered, and as a recipient of data you can be sure that the data hasn’t been altered.

Ethereum expands on blockchains by allowing people to create dapps.

**Decentralized apps (dapps)** - decentralized apps are a new type of software program designed to exist on the internet in a way that is not controlled by any single entity.

Where bitcoin is a decentralized value exchange, a decentralized application aims to achieve functionality beyond transactions that exchange value.

**BREAK** (15 mins)

### FUNdamentals

- A Blockchain is immutable, sequential chain of records called Blocks
- Blocks contain transactions, files, or any kind of data
- Blocks are chained together uses hashes

### What are Hash Functions

A function takes an input and from that input derives an output:

**f(x) = y**

**Example:**

```
md5("Hello world") = 5eb63bbbe01eeed093cb22bb8f5acdc3
```

The hash function md5 creates a 32 character hexadecimal output. Hash functions are generally irreversible (one-way), which means you can't figure out the input if you only know the output, unless you brute force attack.

Hash functions are often used for proving that something is the same as something else, without revealing the information beforehand.

Let's try it on this [MD5 generator](http://www.miraclesalad.com/webtools/md5.php)!

Try entering an input, and seeing how it changes.

## Basic blockchain

```
block = {
    'index': 1,
    'timestamp': 1506057125.900785,
    'transactions': [
        {
            'sender': "8527147fe1f5426f9dd545de4b27ee00",
            'recipient': "a77f5cdfa2934df3954a5c7c7da5df1f",
            'amount': 5,
        }
    ],
    'proof': 324984774000,
    'previous_hash': "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
}
```

Each block contains:

- timestamp
- transactions
- proof
- previous_hash
- index

Blocks are immutable. The previous hash gives blockchains immutability. If a hacker corrupts an earlier Block in the chain, all subsequent blocks will contain incorrect hashes.

## Blockchain Demo

Here we will take a look at my blockchain. 

We will start by running my blockchain on port 5000

```
pipenv run python blockchain.py -p 5000
```

I will ramp up and ngrok build:

```
ngrok http 5000
```

We will look at the initial chain at `localhost:5000/chain`:

```
{
    "chain": [
        {
            "index": 1,
            "previous_hash": 1,
            "proof": 100,
            "timestamp": 1529119299.226101,
            "transactions": []
        },
     ],
}
```

We will add a couple transactions at:

**POST localhost:5000/transactions/new**

We will send this POST body:

```
{
 "sender": "d0c03c0ae8574234afd70800ea40045d",
 "recipient": "someone-other-address",
 "amount": 5
}
```

We will mine our first bitcoin:

**GET http://localhost:5000/mine**

We will ramp up a second ngrok on port 5001, then register that node (ie. https://28337cf5.ngrok.io/nodes/register)

Then we will let the second node gain consensus: `http://localhost:5001/nodes/resolve`

We will see that the second chain has adapted to our authoritative blockchain.

## Exercise (20 mins)

Break up into groups and define these terms:

**Proof of work**: [Explain](https://github.com/scy-edu/blockchain/blob/master/blockchain.py#L137-L151)

**Mining**: [Explain](https://github.com/scy-edu/blockchain/blob/master/blockchain.py#L235-L259)

**Consensus**: [Explain](https://github.com/scy-edu/blockchain/blob/master/blockchain.py#L302-L316)

**BREAK** (15 mins)

## Exercise (20 mins)

Try and build your own blockchain. Utilize ngrok to interact between the different blockchains.


## Getting Started with Ethereum

[Notes are here](https://medium.com/mercuryprotocol/how-to-create-your-own-private-ethereum-blockchain-dad6af82fc9f)

Open terminal and install homebrew:

```
ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now install geth:

```
brew tap ethereum/ethereum
brew install ethereum
```

Create Genesis File

The Genesis block is the first block in the chain, the Genesis file is a JSON file that defines the characteristics of that initial block and subsequently the rest of the blockchain

1) Create a directory to hold your network

```
cd ~/Desktop
mkdir ethereum-chain
cd ethereum-chain
```

2) Create your genesis file

```
touch genesis.json
```

Open the genesis file and paste the following:

```
{
   "config": {
      "chainId": 1994,
      "homesteadBlock": 0,
      "eip155Block": 0,
      "eip158Block": 0,
      "byzantiumBlock": 0
   },
   "difficulty": "400",
   "gasLimit": "2000000",
   "alloc": {
      "7b684d27167d208c66584ece7f09d8bc8f86ffff": { 
          "balance": "100000000000000000000000" 
      },
      "ae13d41d66af28380c7af6d825ab557eb271ffff": { 
          "balance": "120000000000000000000000" 
      }
   }
}
```

**config**

- chainId — this is your chain’s identifier, and is used in replay protection.
- homesteadBlock, eip155Block, eip158Block, byzantiumBlock — these relate to chain forking and versioning, so in our case lets leave them 0 since we’re starting a new blockchain.

**difficulty**

This dictates how difficult it is to mine a block. Setting this value low (~10-10000) is helpful in a private blockchain as it lets you mine quickly, which equals fast transactions, and plenty of ETH to test with. For comparison, the Ethereum mainnet Genesis file defines a difficulty of `17,179,869,184`

**gasLimit**

This is the the total amount of gas that can be used in each block. With such a low mining difficulty, blocks will be moving pretty quick, but you should still set this value pretty high to avoid hitting the limit and slowing down your network.

**alloc**

Here you can allocate ETH to specific address. This won't create the account for you, so make sure its an account you already have control of. You will need to add the account to your privte chain in order to use it, and to do that you need access to the keystore/etc file. For example, Geth and MyEtherWallet give you access to this file when you create an account, but Metamask and Coinbase do not. The addresses provided are not realaddresses, they are just examples. 

## Start the Node

1. Instantiate the data directory

```
$ geth --datadir ./myDataDir init ./genesis.json
```

2. Start the Ethereum peer node

```
$ geth --datadir ./myDataDir --networkid 1114 console 2>> myEth.log
```

Output should look like this: 

```
Welcome to the Geth JavaScript console!
instance: Geth/v1.7.3-stable-4bb3c89d/darwin-amd64/go1.8.3
coinbase: 0xae13d41d66af28380c7af6d825ab557eb271ffff
at block: 5 (Thu, 07 Dec 2017 17:08:48 PST)
datadir: /Users/test/my-eth-chain/myDataDir
modules: admin:1.0 clique:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
>
```

3. Display the Ethereum logs

- Open another terminal window
- cd to ethereum-chain
- Type `tail -f myEth.log`

4. Create an account

```
> personal.newAccount("TYPE_A_PW")
```

Do not forget this password! You will be needing it again

5. Set Default Account

- Check your default account, type:

```
> eth.coinbase
```

If this address is the same as the one from step 4, skip step 5

- To set your default account, type:

```
> miner.setEtherbase(web3.eth.accounts[0])
```

6. Start mining

- Check your balance:

```
> eth.getBalance(eth.coinbase)
```

- Run:

```
> miner.start()
```

- End mining, type:

```
> miner.stop()
```

Note:

Vitalik Buterin, released a hybrid system that merges bitcoin-style proof of work with its proof-of stake. 

The plan effectively means ethereum will begin alternating between the two systems, so that 1 / 100 blocks are secured via proof-of-stake and the rest remain on proof of work.

```
Proof of Stake (PoS) concept states that a person can mine or validate block transactions according to how many coins he or she holds. This means that the more Bitcoin or altcoin owned by a miner, the more mining power he or she has.

The proof of stake (PoS) seeks to address this issue by attributing mining power to the proportion of coins held by a miner. This way, instead of utilizing energy to answer PoW puzzles, a PoS miner is limited to mining a percentage of transactions that is reflective of his or her ownership stake. For instance, a miner who owns 3% of the Bitcoin available can theoretically mine only 3% of the blocks.

Bitcoin uses a PoW system and as such is susceptible to a potential Tragedy of Commons. The Tragedy of Commons refers to a future point in time when there will be fewer bitcoin miners available due to little to no block reward from mining. The only fees that will be earned will come from transaction fees which will also diminish over time as users opt to pay lower fees for their transactions. With fewer miners than required mining for coins, the network becomes more vulnerable to a 51% attack. A 51% attack is when a miner or mining pool controls 51% of the computational power of the network and creates fraudulent blocks of transactions for himself, while invalidating the transactions of others in the network.

With a PoS, the attacker would need to obtain 51% of the cryptocurrency to carry out a 51% attack. The proof of stake avoids this ‘tragedy’ by making it disadvantageous for a miner with a 51% stake in a cryptocurrency to attack the network. Although it would be difficult and expensive to accumulate 51% of a reputable digital coin, a miner with 51% stake in the coin would not have it in his best interest to attack a network which he holds a majority share. If the value of the cryptocurrency falls, this means that the value of his holdings would also fall, and so the majority stake owner would be more incentivized to maintain a secure network.
```

[Source](https://www.investopedia.com/terms/p/proof-stake-pos.asp)

## Exercise

Try to add a peer to the your local network.

## Harder Exercise:

[Mine Ethereum on AWS](https://hackernoon.com/how-to-mine-ethereum-in-5-min-3f3bc80d0c4b)

**BREAK** (15 mins)

## Ethereum Blockchain

Ethereum blockchain expands on Bitcoin to do much more than the Bitcoin blockchain. It allows developers to build dapps.

Decentralized apps are a new type of software program designed to exist on the Internet in a way that is not controlled by any single entity.

Where Bitcoin is a decentralized value exchange, a decentralized application aims to achieve functionality beyond transactions that exchange value

## Solidity

Solidity is statically typed, supports inheritance, libraries, and complex user-defined types among other features.

Statically typed means that the type of a variable is known at compile time. The main advantage here is that all kinds of checking can be done by the compiler, and therefore a lot of trivial bugs are caught at a very early stage.


## Smart Contract

A smart contract is a computer protocol intended to facilitate, verify, or enforce the negotation or performance of a contract.

The most prominent smart contract implementation is the ethereum blockchain platform

We are going to develop in a test environment so it wouldn't cost us anything.

## Use cases

- voting
- recording keeping
- digital identities
- iOT
- Real Estate
- Auctions

What other examples can you think of?

## Variables and types

We will open up remix.ethereum.org and use the JavaScript VM (or EVM).

We will create a Course contract:

```
pragma solidity ^0.4.18;

contract Course {

}
```

Define a variable. The type of the variable must be defined

```
pragma solidity ^0.4.18;

contract Course {
	string fName = 'Stanley';
	uint age = 28;
}
```

**Types of variables**

- bool
- uint / int
- address
- Bytes1 through 32
- Bytes
- String
- Mapping
- Struct

**Access modifier**

- public (accessible everywhere)
- private (available to current contract)
- internal (accessed internally to current contract)
- external (called by other contracts, but not internally)

Let's make our variables public: 

```
pragma solidity ^0.4.18;

contract Course {
	string public fName = 'Stanley';
	uint public age = 28;
}
```
You will notice that they have added getters for the public variables, we can now click it to access it.

## Constructor

We can define the variables in the constructor.

```
pragma solidity ^0.4.18;

contract Course {
    
    string public fName;
    uint public age;
    
    constructor() public {
        fName = 'Stanley';
        age = 27;
    }
    
}
```

## Constant variables


```
pragma solidity ^0.4.18;

contract Course {
    
    string public fName;
    string constant lName = 'Yang';
    uint public age;
    
    constructor() public {
        fName = 'Stanley';
        age = 27;
    }
    
}
```

## Setters and Getters

We can use getters and setters to retrieve and set our variables

```
pragma solidity ^0.4.18;

contract Course {
    
    string fName;
    uint age;
    
    function setInstructor(string _fName, uint _age) public {
        fName = _fName;
        age = _age;
    }
    
    function getInstructor() public constant returns (string, uint) {
        return (fName, age);
    }
    
}
```

Now you can `setInstructor` of "Stanley", 28 and retrieve that data from our test blockchain.

## Creating Web UI

We will need to set up Ethereum-Testrpc. This is based on NodeJS

It uses EthereumJS to simulate full client behavior and make developing ethereum applications much faster.

It also includes all popular RPC functions and features (like events) that can be run deterministically to make development a breeze

Check if you have nodeJS and npm installed:

```
node -v
npm -v
```

We will install [ganache-cli](https://github.com/trufflesuite/ganache-cli)

```
$ npm install -g ganache-cli
```

You can now run the command to start it up

```
$ ganache-cli
```

This provides 10 different accounts and 10 private keys, also ramps up a server on 8545

We will now set up our project

```
$ cd ~/Desktop
$ mkdir course-eth
$ cd course-eth
$ npm init -f
```

We will need to install Ethereum web3.js

```
$ npm i -S ethereum/web3.js
```

We can now connect to Web3 Provider on our remix IDE.

We will provide our localhost:8545 to the prompt and connect to it.

![Web3provider](imgs/web3provider.png)

Let's create our `index.html`

```
$ touch index.html main.css
```

In `index.html`:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Course</title>
    
    <link rel="stylesheet" href="main.css">
    <script src="./node_modules/web3/dist/web3.min.js"></script>
</head>
<body>
    <div class="container">
        <h1>Course Instructor</h1>
        <h2 id="instructor"></h2>

        <label for="name" class="col-lg-2 control-label">Instructor Name</label>
        <input id="name" type="text" />

        <label for="name" class="col-lg-2 control-label">Instructor Age</label>
        <input type="text" id="age">
        <button id="button">Update Instructor</button>
    </div>

    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"></script>

    <script>
        // Could be defined already by metamask or mist
        if (typeof web3 !== 'undefined') {
            web3 = new Web3(web3.currentProvider);
        } else {
            // set the provider you want from Web3.providers
            web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
        }

        // specify default ethereum account
        // choose the first account to use
        web3.eth.defaultAccount = web3.eth.accounts[0];

    </script>
    
</body>
</html>
```

In `main.css`:

```
body {
    background-color: #F0F0F0;
    padding: 2em;
    font-family: 'Raleway', 'Source Sans Pro', 'Arial';
}

.container {
    width: 50%;
    margin: 0 auto;
}

label {
    display: block;
    margin-bottom: 10px;
}

input {
    padding: 10px;
    width: 50%;
    margin-bottom: 1em;
}

button {
    margin: 2em 0;
    padding: 1em 4em;
    display: block;
}

#instructor {
    padding: 1em;
    background-color: #fff;
    margin: 1em 0;
}

#loader {
    width: 100px;
    display: none;
}
```

Then we will add the SmartContract to our app:

- Go to Remix
- Click on `Compile`
- Copy the ABI
- Paste it in

```
 var CourseContract = web3.eth.contract([
            {
                "constant": false,
                "inputs": [
                    {
                        "name": "_fName",
                        "type": "string"
                    },
                    {
                        "name": "_age",
                        "type": "uint256"
                    }
                ],
                "name": "setInstructor",
                "outputs": [],
                "payable": false,
                "stateMutability": "nonpayable",
                "type": "function"
            },
            {
                "constant": true,
                "inputs": [],
                "name": "getInstructor",
                "outputs": [
                    {
                        "name": "",
                        "type": "string"
                    },
                    {
                        "name": "",
                        "type": "uint256"
                    }
                ],
                "payable": false,
                "stateMutability": "view",
                "type": "function"
            }
        ]);
```

We will also need to provide where the contract is at:

- To to `Run`
- Copy the address
- Add it into the app

```
var Course = CourseContract.at('0x253adcb228f73b95f69fd5e2de43f7450cc5224b');
```

**Sanity check:**

`console.log` the Course variable

It should looks like that.

We can now use the methods:

```
Course.getInstructor(function(error, result) {
    if (!error) {
        $('#instructor').html(result[0] + " (" + result[1] + ") years old");
    } else {
        console.log(error);
    }
});

$("#button").click(function() {
    Course.setInstructor($("#name").val(), $("#age").val());
});
```

Ropsten vs. testrpc

- testrpc is useful for early stage smart contract development. Contract calls are very quick

- Ropsten is useful for later stage development. It more closely simulates the live Ethereum network

## Events

Events allow the convenient usage of the EVM logging facilities, which in turn can be used to call JavaScript callbacks in the user interface of a dapps, which listen for these events

Add this to our contract:

```
pragma solidity ^0.4.18;

contract Course {
    
    string private fName;
    uint private age;
    
    // Created an event
    event Instructor(
        string name,
        uint age
    );
    
    function setInstructor(string _fName, uint _age) public {
        fName = _fName;
        age = _age;
        
        // invoke Instructor event
        emit Instructor(_fName, _age);
    }
    
    function getInstructor() public constant returns (string, uint) {
        return (fName, age);
    }
    
}
```

We will now get rid of the getInstructor, and add this:

```
instructorEvent.watch(function(error, result) {
    if (!error) {
        $('#loader').hide();
        $("#instructor").html(result.args.name + ' (' + result.args.age + ' years old');
    } else {
        $('#loader').hode();
        console.error(error);
    }
});

$("#button").click(function() {
    $('#loader').show();
    Course.setInstructor($("#name").val(), $("#age").val());
});
```

## Function modifiers

We want to prevent ANYONE from changing the name or age. We want the person who created the account to set the instructor.

function modifiers allow us to check the function to see if the conditions are met.

```
pragma solidity ^0.4.18;

contract Course {
    
    string private fName;
    uint private age;
    address owner;
    
    constructor() public {
        owner = msg.sender;
    }
    
    modifier onlyOwner {
        require(msg.sender == owner);
        _; // this means that if the above statement is true, run the function body
    }
    
    // Created an event
    event Instructor(
        string name,
        uint age
    );
    
    function setInstructor(string _fName, uint _age) onlyOwner public {
        fName = _fName;
        age = _age;
        
        // invoke Instructor event
        emit Instructor(_fName, _age);
    }
    
    // view would not change the state in any way
    function getInstructor() view public returns (string, uint) {
        return (fName, age);
    }
    
}
```

Now we will change the account to a different one:

```
 web3.eth.defaultAccount = web3.eth.accounts[1];
```

And change the JS code here:

```
Course.setInstructor($("#name").val(), $("#age").val(), (err, res) => {
    if (err) {
        $("#loader").hide();
    }
});
```

## Mappings And Structs

Structs provides a way to define new types. It can be used inside mappings and arrays and they an itself contain mappings and arrays.

Let's say we want to add multiple instructors, using mappings and structs give us a way to do this.

In Courses2.sol

```
pragma solidity ^0.4.18;

contract Courses {
    
    struct Instructor {
        uint age;
        string fName;
        string lName;
    }
    
    mapping (address => Instructor) instructors;
    address[] public instructorAccounts;
    
    function setInstructor(address _address, uint _age, string _fName, string _lName) public {
        var instructor = instructors[_address];
        
        instructor.age = _age;
        instructor.fName = _fName;
        instructor.lName = _lName;
        
        instructorAccounts.push(_address) -1;
    }
    
    function getInstructors() view public returns (address[]) {
        return instructorAccounts;
    }
    
    function getInstructor(address _address) view public returns (uint, string, string) {
        return (instructors[_address].age, instructors[_address].fName, instructors[_address].lName);
    }
    
    function countInstructors() view public returns (uint) {
        return instructorAccounts.length;
    }
}
```

## Inheritance & Deployment

We will change the strings to byte16. Strings are really expensive in production:

```
pragma solidity ^0.4.18;

contract Owned {
    address owner;
    
    constructor() public {
        owner = msg.sender;
    }
    
    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }
    
}

contract Courses is Owned {
    
    struct Instructor {
        uint age;
        bytes16 fName; // 16 characters for the first name
        bytes16 lName; // 16 characters for the last name
    }
    
    mapping (address => Instructor) instructors;
    address[] public instructorAccounts;
    
    event instructorInfo(
        bytes16 fName,
        bytes16 lName,
        uint age
    );
    
    function setInstructor(address _address, uint _age, bytes16 _fName, bytes16 _lName) onlyOwner public {
        var instructor = instructors[_address];
        
        instructor.age = _age;
        instructor.fName = _fName;
        instructor.lName = _lName;
        
        instructorAccounts.push(_address) -1;
        
        // emit a signal that the instructor has been set
        emit instructorInfo(_fName, _lName, _age);
    }
    
    function getInstructors() view public returns (address[]) {
        return instructorAccounts;
    }
    
    function getInstructor(address _address) view public returns (uint, bytes16, bytes16) {
        return (instructors[_address].age, instructors[_address].fName, instructors[_address].lName);
    }
    
    function countInstructors() view public returns (uint) {
        return instructorAccounts.length;
    }
}
```

Go ahead and download Metamask to your chrome browser. We will use the Ropsten test net to reflect what happens in the live blockchain in production



## LAB: Create a token

Follow this and build a [token](https://www.ethereum.org/token).