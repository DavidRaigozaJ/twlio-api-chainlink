## MasterClass assignments completed

StableCoin contract deployed to 0x58c4B4460b110753D9a904cC1b1112FC841136BC on mumbai

RecordLabel contract deployed to 0x81b7fE7D1432683d19f10E8a1aa7C26363d7eFA1 on mumbai

Approving RecordLabel to spend the balance of the SimpleStableCoin deployer ("0xe821c6eEe1d0149E46E947Fe802cf79D31698691") as payments to artists...


Adding following artist data to RecordLabel:  ca22091a-3c00-11e9-974f-549f35141000 Tones&I 14000000 frustramatic@gmail.com

# Repo for the Chainlink Functions Deep Dive Masterclass

This repo houses code prepared to demonstrate the power of Chainlink Functions. Chainlink Functions is a powerhouse technology that helps blockchain engineers connect their Decentralized Applications to **any** data source or API on Earth. While keeping API keys and secrets secure (through encryption), and having the data returned from decentralized computation run through Chainlink's consensus protocol, to ensure that the data returned to your smart contract is
- trust minimized
- verifiably cryptographically truthful

The Masterclass will be held on 2 May 2023, at 5pm EST.  Details can be found [here](https://go.chain.link/masterclass/functions-module-1)


Creating Functions billing subscription
Waiting 1 blocks for transaction 0x88f7d4f9cc66adfe181acd8e3d088786fddf1601902e4bd3dbb1908533f2d8f5 to be confirmed...
Subscription created with ID: 779
Duplicate definition of Transfer (Transfer(address,address,uint256,bytes), Transfer(address,address,uint256))
Funding with 2.5 LINK
Waiting 1 blocks for transaction 0xc9a074ee4e871050450c350c7c15e843799fa300f6d9634275b4859dba922b4f to be confirmed...
Subscription 779 funded with 2.5 LINK
Adding consumer contract address 0x81b7fE7D1432683d19f10E8a1aa7C26363d7eFA1 to subscription 779
Waiting 2 blocks for transaction 0xe41e544d9d4f2ef7d5d6a38045c40c781f83713c6019b222360b2912daad65a0 to be confirmed...
Authorized consumer contract: 0x81b7fE7D1432683d19f10E8a1aa7C26363d7eFA1

Created subscription with ID: 779
Owner: 0xe821c6eEe1d0149E46E947Fe802cf79D31698691
Balance: 2.5 LINK
1 authorized consumer contract:
[ '0x81b7fE7D1432683d19f10E8a1aa7C26363d7eFA1' ]

Seeded initial Artist Data for Tones&I and assigned them wallet address 0x4E7a7c8779DF158dF75638d1b4FF97C0Dd463b55.





> **⚠️⚠️⚠️ Important ⚠️⚠️⚠️**
> registration is compulsory!

Chainlink Functions is currently in a closed beta. Request access to use Chainlink Functions at https://functions.chain.link.


## What we are building

This use case showcases how Chainlink Functions can be used to facilitate a digital agreement between a record label and a music artist, with Chainlink Functions being used to obtain the artists streaming numbers from a Spotify wrapper.  You are also provided high level guidance on implementing a system to notify artists of payouts,  using the [Twilio SendGrid Email API](https://www.twilio.com/en-us/sendgrid/email-api)

The `RecordLabel` contract represents an on-chain payment contract between a music artist and the record label. Chainlink Functions is used to poll the latest monthly streaming numbers for the artist, using Soundcharts' Spotify API. The artist is paid in a (demo) Stablecoin called STC.

If the artist has acquired new streams since last measured, the Chainlink Functions code will use the Twilio-Sendgrid email API to send the artist an email informing them that some STC payments are coming their way. The Functions code will also send the latest stream count back to the smart contract so it can be recorded immutably on the blockchain. The returned value is passed through [Chainlink's Off-Chain Reporting consensus mechanism](https://docs.chain.link/architecture-overview/off-chain-reporting/) - which the nodes in the [Decentralized Oracle Network](https://chain.link/whitepaper) that are returning this stream's data achieve a cryptographically verifiable consensus on that returned data!

The smart contract calculates how much STC is payable to the recording artist (in real life, the payment could be in the form of a stablecoin such as USDC). The record label and the artist have an agreed payment rate: for example, the artist gets 1 STC for every 10000 additional streams. This rate is part of the smart contract's code and represents a trust-minimized, verifiable, on-chain record of the agreement.

<img width="540" alt="Messenger" src="https://user-images.githubusercontent.com/8016129/224178418-27f62a67-d44a-4fb4-8e74-c4c967f312dd.png"> <span /><span />

## Instruction Manual
A step by step written manual for the workshop is available [here](https://docs.google.com/document/d/e/2PACX-1vQh2ZN_K6QpIK1ebt8BjSAwdMZCBgZXSxPYTTaI7dufvM8k2odO9bHpbYlgT6GIobGCfDbIv9c_4czs/pub).

The basic workflow is as follows.  There are only three pieces that we need to prepare: 
- the Custom Code we want executed using Chainlink's decentralized oracle network
- the request configuration and 
- the Consumer/Client smart contract that receives this configuration in its `executeRequest()` method.

![Workflow components In Functions](https://user-images.githubusercontent.com/8016129/235579898-fe5441a0-ea1f-4f88-bb2b-153f35062d25.png)

After that, the rest of the heavy lifting is done by the Chainlink Decentralized Oracle Network, **including the fully decentralized execution of the custom code you provide,and the application of Chainlink's Off Chain Reporting consensus protocal to the results of the computation done in your custom code!**.  

The repo provides a bunch of Hardhat Tasks that give you CLI-based tooling to deploy contracts, trigger Chainlink Functions, encrypt secrets that are available off-chain etc.# twlio-api-chainlink
