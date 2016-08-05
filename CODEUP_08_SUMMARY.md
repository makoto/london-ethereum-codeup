# CodeUp #8 summary 

## Post DAO

For DAO holders who wish to have their Ether back, you can do so via [new Mist browser](https://slacknation.github.io/medium/12/12.html
), or through [online wallet](https://www.myetherwallet.com/#the-dao). Please bear in mind that you have to provide private key (which may not be secure) if you use the latter approach.

We went through a code called [AmIOnTheFork](https://etherscan.io/address/0x2bd2326c993dfaef84f696526064ff22eba5b362#code) which checks if the DAO balance went down (hence forked).
While discussing the code, we also discussed about better exception handling when sender accidentally sends ethers.
The current best practice is rather than `throw` which burns all the gases, return the ethers to the sender so that any unused gas will also be returned.

## Ethereum Studio and Oraclize

[@bertani](https://github.com/bertani) gave us hands on workshop about using [Ethereum Studio](https://live.ether.camp/) as well as integration with Oraclize. The more detail is at [Ethereum Studio integrates Oraclize](http://blog.ether.camp/post/145202667083/ethereum-studio-integrates-oraclize).
[@bertani](https://github.com/bertani) also gave us very in depth explanation about how Oraclize work.

My personal opinion is that Ethereum Studio is great for training purpose because you don't have to setup and sync blockchain node locally.
The downside is that their compilation errors are not as informative as that of [Browser Solidity](https://ethereum.github.io/browser-solidity/#version=soljson-latest.js)

## Mist Dapp support

If you want your Dapp to support Mist browser, add `mist` variable to your frontend code. Here is the [example](https://github.com/oraclize/dapp-proof-of-identity/blob/master/web-ui/index.html#L196). 

## Public Ethereum node

While explaining how Ethereum Studio work, we also talked about how to get read only access for users who haven't setup geth with RPC enabled.
A couple of Dapp providers actually provides [read only node](https://eth2.augur.net) so you can instantiate `Web3` with these endpoint if there are no local geth.

## Others

- [Ether Unit Converter](http://ether.fund/tool/converter) is a handy utility to convert ether to various units (eg: wei)
- [Zerocoin](http://zerocoin.org/) is another upcoming cryptocurrency project
 
