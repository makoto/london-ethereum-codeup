# CodeUp #13

## Participants

- 9 registered, 6 attended

## [Ethereum Jurgon Busters](https://docs.google.com/presentation/d/16KBFTskiBovLY2NL_JCPNEWObQ8iPxbB181mc0_WaKU/edit)

This is the slide I prepared for anyone new to Ethereum terminologies.

## [Building Private chain with Docker](https://github.com/mattbradburyuk/ethereumplay)

[Matt](https://github.com/mattbradburyuk) walked through his Doker project that setup private chain environment which will

- create docker images that installs necessary tools(mosthly geth)
- launch 2 docker instances with the image
- setup private blockchain connecting to the two nodes
- create accounts, start mining, and filling in ether to the accounts.
- also sends some ether to metamask account (address hard-coded)

## [Ethereum Naming System](https://github.com/arachnid/ens/)

[Nick](https://github.com/arachnid) walked through his Ethereum Naming Services.

This is complete rewrite from the one he presented at [London Ethereum Meetup in June](http://www.meetup.com/ethereum/events/231452190/)

My takeaways are

- This is a lot simplified version than the previous one.
- ENS is just another Solidity contract so great study material if you want to learn Solidity
- Tests are written with [dapple](https://github.com/nexusdev/dapple) framework. Dapple is a great tool that lets you write tests in Solidity, though Nick is planning to rewrite in normal javascript because (a) nice to write tests in different language than to the implementation, and (b) testrpc gives you a option to traverse to certain block which will be essential to write date dependent contract.

## Others

Some random links shared during the study group

- [Vitalik's view on ethereum for financial services](https://r3cev.com/blog/2016/6/2/ethereum-platform-review)
- [Hive - Ethereum end-to-end test harness](https://github.com/karalabe/hive)
- [TestRPC DAO Hack Demo](https://github.com/tcoulter/dao-truffle), [video demo](https://www.youtube.com/watch?v=MLtsmnhiXCE)
