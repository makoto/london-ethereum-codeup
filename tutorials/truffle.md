## Prerequisite

- node.js, npm

## Installing truffle and testrpc

```
npm install -g truffle
npm install -g ethereumjs-testrpc
```

make sure that both truffle and testrpc are on version higher than v3

## Starting testrpc (in a seperate window)

testrpc is a in memory blockchain.
Starting testrpc will create 10 sample accounts.

```
minoue@macminoue:~/work/chopin/log (ts_test_branded_payment_methods)*$ testrpc -v
EthereumJS TestRPC v3.0.3

Available Accounts
==================
(0) 0xc3e1f9d8ff7a64926a45dc9d0390b614477ebdb8
(1) 0xbcdd61a66a7a28616600503c4d9ad0bf9a73a769
(2) 0x2e83d861a4ce9580600b0e65860b78d97e72bece
(3) 0xe330b37ec5131e868177870d38d92ea34155f552
(4) 0x53453084d024b59da1785530b7dead0d490c1f5e
(5) 0x604e953063d9970230a9ba843b56125795b50fb7
(6) 0x8bb5c454eea4f7cf7d9ebab957d073d2b0cfff34
(7) 0xcb15d4292fab38d2778840266ff72c63a25148e9
(8) 0x52b32748e5734862ec60a1e632d4ec3e9c9dcc33
(9) 0x49cdfff79a252bc3d6d443b76b357478cf883877

Private Keys
==================
(0) a9d10df1a88f98af544ef77e871e98493a86343e07c94aef0742abdbd3c1fe52
(1) fe74cbc2dcceae06ce7ba2b1e3e6a6454f57255eb0c9fb0eadd554bdea27f7e8
(2) 6b5619ddcc0d69ee604da4b4c78235859d73e458ee3dab236733ecc17634708f
(3) 8a2ef71700be423e951ce1baaa8cc756e2e6d4876eec2867b8be9e906910de56
(4) 2224b4e91238b9af25ab79ee79813a0c2d8f29557aa74c56a7fbf39286dde79a
(5) 824334d93f3777911b1d908f2e64a1c3cf9615a1a20659a8d627586bdc7c76c6
(6) 4d4cad5e443be4281471ebde8dde68af6d70f5d20b73b40945b535da562e43b2
(7) 8b30a2e0344c67c980cb000f6e522f32a898d1af247e77b85323b636521ca8ec
(8) 2d38e0f67bff9244c6a4f325b47cd32bdc3f28b1f6239a42a2d3bcd32cdab463
(9) 86f233c38767cf2392752b26635f774c2922372818cd54b74d3cb85ace6e345d

HD Wallet
==================
Mnemonic:      paddle pigeon worry system follow unveil skull bean today title flip festival
Base HD Path:  m/44'/60'/0'/0/{account_index}

Listening on localhost:8545
```

### Creating sample project

```
mkdir truffletest1
cd truffletest1
minoue@macminoue:~/work/truffletest1 $ truffle init
Downloading project...
Project initialized.

  Documentation: http://truffleframework.com/docs

Commands:

  Compile: truffle compile
  Migrate: truffle migrate
  Test:    truffle test
```

### Running Test

```
minoue@macminoue:~/work/truffletest1 $ truffle test
Compiling ./contracts/ConvertLib.sol...
Compiling ./contracts/MetaCoin.sol...
Compiling ./contracts/Migrations.sol...
Compiling ./test/TestMetacoin.sol...
Compiling truffle/Assert.sol...
Compiling truffle/DeployedAddresses.sol...


  TestMetacoin
    ✓ testInitialBalanceUsingDeployedContract (56ms)
    ✓ testInitialBalanceWithNewMetaCoin

  Contract: MetaCoin
    ✓ should put 10000 MetaCoin in the first account
    ✓ should call a function that depends on a linked library (53ms)
    ✓ should send coin correctly (117ms)


  5 passing (529ms)
```

### Running Migrations

```
minoue@macminoue:~/work/truffletest1 $ truffle migrate
Compiling ./contracts/ConvertLib.sol...
Compiling ./contracts/MetaCoin.sol...
Compiling ./contracts/Migrations.sol...
Writing artifacts to ./build/contracts

Using network 'development'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  Migrations: 0x71096105a6ba3c764959a1c7abd71b7c5f9016aa
Saving successful migration to network...
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying ConvertLib...
  ConvertLib: 0xa07005ec2aa6cc13f99e425b00a01054620e96ae
  Linking ConvertLib to MetaCoin
  Deploying MetaCoin...
  MetaCoin: 0x1d5046f058d20de21538309c71a8883f4ade6072
Saving successful migration to network...
Saving artifacts...
```

### Interacting with smart contract via console

#### Starting up console

```
truffle console
```

#### Show existing accounts

```
truffle(development)> web3.eth.accounts
[ '0xc3e1f9d8ff7a64926a45dc9d0390b614477ebdb8',
  '0xbcdd61a66a7a28616600503c4d9ad0bf9a73a769',
  '0x2e83d861a4ce9580600b0e65860b78d97e72bece',
  '0xe330b37ec5131e868177870d38d92ea34155f552',
  '0x53453084d024b59da1785530b7dead0d490c1f5e',
  '0x604e953063d9970230a9ba843b56125795b50fb7',
  '0x8bb5c454eea4f7cf7d9ebab957d073d2b0cfff34',
  '0xcb15d4292fab38d2778840266ff72c63a25148e9',
  '0x52b32748e5734862ec60a1e632d4ec3e9c9dcc33',
  '0x49cdfff79a252bc3d6d443b76b357478cf883877' ]
```

#### Displaying a balance of an account;

Ethereum provides a standard javascript library to interact with smart contract via JSON RPC called [web3](https://github.com/ethereum/wiki/wiki/JavaScript-API)

```
var accounts = web3.eth.accounts;
// synchronous mode
web3.eth.getBalance(accounts[0]).toNumber()
// 99883546600000000000
// asynchronous mode
web3.eth.getBalance(accounts[0], function(error, result){ console.log(result.toNumber())})
// 99883546600000000000
```

The balance is usually output in the smallest unit called wei (1/10**17). Convert into Ether.

```
web3.fromWei(web3.eth.getBalance(accounts[0]).toNumber(),'Ether')
// '99.8835466'
```

#### Calling a function through Truffle js wrapper

Truffle framework provider another JS library called [truffle-artifactor](https://github.com/trufflesuite/truffle-artifactor), which wraps the deployed smart contract so you can interact with the smart contract automatically without specifying contract address, etc.

```
var instance;
MetaCoin.deployed().then(function(i){instance = i});
instance.getBalance.call(accounts[0]).then(function(o){console.log(o.toNumber())})
// 10000
instance.getBalance.call(accounts[1]).then(function(o){console.log(o.toNumber())})
// 0
```

`MetaCoin.deployed()` will return the smart contract as a js object.
`contract_instance.functionName.call()` is the standard way to call read only smart contract. When you read data from smart contract, you do not have to pay gas.

#### Sending a transaction through Truffle js wrapper

Any state changing operation can be achieved by sending a transaction. Sending transaction always requires a gas.

```
instance.sendCoin(accounts[1], 10, {from: accounts[0]});
instance.getBalance.call(accounts[0]).then(function(o){console.log(o.toNumber())})
// 9990
instance.getBalance.call(accounts[1]).then(function(o){console.log(o.toNumber())})
// 10
```

#### Quitting console

```
truffle(development)> .exit
```

### Creating web interface

At truffle 3.0, front end build process became configurable so you could use your favorite prefred choice such as webpack, grunt, etc.

For this tutorial, it will use webpack scaffold

```
minoue@macminoue:~/work/truffletest1 $ npm init
# follow the instruction
minoue@macminoue:~/work/truffletest1 (master)*$ truffle init webpack
Downloading project...
Installing dependencies...
Project initialized.

  Documentation: https://github.com/trufflesuite/truffle-init-webpack

Commands:

  Compile:        truffle compile
  Migrate:        truffle migrate
  Test:           truffle test
  Build Frontend: npm run build
  Run Linter:     npm run lint
  Run Dev Server: npm run dev
```

#### Startup dev Server

```
minoue@macminoue:~/work/truffletest1 (master)*$ npm run dev

> truffle-init-webpack@0.0.1 dev /Users/minoue/work/truffletest1
> webpack-dev-server

Project is running at http://localhost:8080/
webpack output is served from /
Hash: df047bd484da81e18ff7
Version: webpack 2.2.1
Time: 1778ms
     Asset       Size  Chunks                    Chunk Names
    app.js    1.35 MB       0  [emitted]  [big]  main
index.html  925 bytes          [emitted]         
chunk    {0} app.js (main) 1.32 MB [entry] [rendered]
   [82] ./~/web3/index.js 193 bytes {0} [built]
   [86] ./app/javascripts/app.js 3.64 kB {0} [built]
   [87] (webpack)-dev-server/client?http://localhost:8080 5.28 kB {0} [built]
   [88] ./build/contracts/MetaCoin.json 3.27 kB {0} [built]
   [90] ./~/ansi-regex/index.js 135 bytes {0} [built]
  [129] ./~/punycode/punycode.js 14.7 kB {0} [built]
  [132] ./~/querystring-es3/index.js 127 bytes {0} [built]
  [161] ./~/strip-ansi/index.js 161 bytes {0} [built]
  [164] ./app/stylesheets/app.css 905 bytes {0} [built]
  [171] ./~/truffle-contract/index.js 2.64 kB {0} [built]
  [206] ./~/url/url.js 23.3 kB {0} [built]
  [241] (webpack)-dev-server/client/overlay.js 3.6 kB {0} [built]
  [242] (webpack)-dev-server/client/socket.js 856 bytes {0} [built]
  [244] (webpack)/hot/emitter.js 77 bytes {0} [built]
  [246] multi (webpack)-dev-server/client?http://localhost:8080 ./app/javascripts/app.js 40 bytes {0} [built]
     + 232 hidden modules
webpack: Compiled successfully.
```

You should see the following like pages

![](https://camo.githubusercontent.com/04b08e699097d088bc3080440c66327615e1d776/687474703a2f2f692e696d6775722e636f6d2f556f75357261592e706e67)

Try to send coin to another address, then confirm from your truffle console that coin is transferred from one account to another.
