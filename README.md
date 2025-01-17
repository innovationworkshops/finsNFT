This is a working web3 dApp.

What is web3? web3 has become the umbrella term denoting the technologies centered around blockchain and the corresponding ideas such as decentralization, the history of transactions which can not be wiped away (i.e., immutability) and the transparency arising out of the fact that anyone can view the provenance of the tokens (i.e., past history of related transactions) in a public distributed database (i.e., public blockchain).

What is a web3 dApp? Simply stated, a web3 dApp (aka decentralized app) is an app which delivers the end to end user experience in any blockchain based technology (either cryptocurrency or NFTs).

A dApp  uses a distributed database (i.e., blockchain), a distributed file system (e.g., IPFS) and a front end server for UI (e.g., Heroku).

The distributed database contains the tokens (e.g., cryptocurrency or NFTs) and the logic (Smart Contracts). The media file (e.g., image corresponding to a NFT) is stored in a file system which is also decentralized (e.g., Interplanetary File System).  The Smart Contracts are typically written in a language such as Solidity (if using Ethereum) or Cadence (if using another blockchain called Flow).

The user interface through which end users can conveniently access these tokens, files and carry out transactions (e.g., buy or sell tokens, cryptocurrency or NFTs) is written in a front end language such as React. There are JavaScript libraries such as Web3.js which act as a glue between Smart Contracts and front end language.

When a user launches our front-end webapp, it would  prompt the user to authenticate to his/her ethereum account through an ethereum wallet (e.g., MetaMask) which the user would have installed as a browser extension.

Once we have these pieces wired together only monitoring remains to be done. For monitoring transactions in the local blockchain we can install either ganache GUI (never worked for me) or another nifty tool such as explorer (https://github.com/etherparty/explorer). Then when we do our transactions in the ganache block chain it shows up.

In the case of public blockchains there are multiple monitoring options including specialized dApps to let us view NFTs transaction history.


## What this dApp does
There are two main operations that happen in this dApp (decentralized app) powered by two contracts:
* Mint (i.e. generate) an NFT
* Allows us to offer our newly minted NFT
* Allows another user to buy the NFT (this module is under construction) - if deployed publicly, another user would authenticate with his/her wallet (e.g., metamask) and would be able to complete the buy transaction.

The transactions e.g., mint, buy etc., require the use of a cryptocurrency - the cryptocurrency that ethereum natively uses is called ETH - this is what is automatically available through MetaMask. When we purchase some ETH through our ethereum account and then that amount of ETH become available for us to do transactions in through MetaMask wallet. Optionally, a dApp (including this app) could be extended to directly accept other cryptocurrencies like Bitcoin or even fiat currency (i.e., dollars) for transactions. Obviously when using a local development blockchain like ganache, we don't need any real currency (neither crypto not fiat)- ganache itself generates some dummy accounts with some fixed amount of ETH when it starts up. All we need to do is import these accounts in MetaMask.

## How to deploy this dApp

### Prerequisites
* Install node
* Install Ganache cli - local blockchain environment for development (the ganache GUI never worked for me unfortunately so I am resigned to using the CLI)
* Install MetaMask - blockchain wallet which installs as a plugin to firefox, chrome or ios.
* Create an account in MetaMask and note the secret recovery phrase
* Install Truffle - (npm install -g truffle)  - Truffle is a great framework for building dApps including compiling contracts and deploying Contracts.
* Install an IDE - I personally use Atom as it is integrated with GitHub  - the official Ethereum IDE is Remix (a browser based IDE) which has not proved to be a happy tool for me.


### Deploying locally
The project contains untested code only for understanding blockchain and NFT related concepts. It has not been tested as a safe code either for local or for remote deployment.

The steps:

* git  clone - clone this repo locally
* cd to the repo directory and do 'npm install' - this  downloads all the necessary dependencies
* compile the smart contracts by running the following command in our terminal: truffle compile
* run ganache
* Ensure that truffle-config.js has the correct ganache port
* run tests that validate our solution can be executed truffle test
* deploy the contracts on our Ganache local blockchain by running the following command: truffle migrate
* assuming that we have MetaMask installed as  a browser extension, click on metamask icon in the brower toolbar and we will see that it automatically picks up the localhost:8545 wich is the ganache blockchain network. If it doesn't then we need to configure it explicitly in the MetaMask network configuration panel/
* now in the git repo directory open the UI by typing: npm start

It will spin up a browser tab at 127.0.0.1:3000 and bring up the UI for the dApp.

### Deployment on public blockchain
To deploy this dApp on a public blockchain two things  need to be done.
* deploy the UI of the dApp on a host (e.g., Heroku)
* deploy the smart contracts on Ethereum. Here we have several options as follows:
    * deploy on ethereum mainnet - expensive and time consuming
    * deploy on one of the  ethereum testnets such as ropsten
    * deploy on a layer to blockchain network like Polygon which works as a secondary scaling solution on top of ethereum. Additionally Polygon uses a different logic called 'proof of stake' instead of 'proof of work' that would be used if directly deploying on ethereum. Using Proof of stake to resolve transactions requires less compute power and so is said to be climate friendly.
    * deploy on one of the blockchain node providers like Infura, Alchemy or Moralis. This last option is the easiest lowest cost (free) way of getting on etherium network. All these node providers also have libraries to make coding easier - e.g., I found it easier to use Alechemy Web3 library than directly coding web3.js to connect to Solidity (Ethereum language which is used to write smart contracts)

To deploy the contracts on public blockchain network we need to specify the following variables (if hosting locally then we can use .env file; if hosting on a server such as Heroku then the config variables feature should be used to prevent exposing values) .

* PRIVATE_KEYS --> Private Key of the account we are using to deploy (typically the first one in the list of Ganache)
* INFURA_API_KEY  or Alchemy Key --> API key from the node provider (e.g., Infura or Alchemy or Moralis when we register)

After this we need to get some free ether to deploy on testnet. This is needed even if we use alchemy or infura or moralis. We can request free ether by going to a faucet - an Ethereum Faucet is where we are paid a minuscule amount of ETH with basic ad viewing and clicking. This gets deposited in our MetaMask account and then with this account we can connect to an ethereum testnet either directly or via a node provider that we have mentioned above.

Then we need to run the truffle migrate to migrate to the testnet e.g. ropsten: truffle migrate --network ropsten



## Technology stack

- Smart Contract: contains all the logic e.g., to mint NFT, create  offer.
- Solidity: Solidity is an object-oriented, high-level language for implementing smart contracts. Somewhat similar to both JS and Java
- React.js for front end UI
- Truffle: We discussed this above.
- Web3.js: The set of libraries that  are used to interact with a local or remote ethereum node. The glue between front end of the dApp and the Smart Contracts written in Solidity programs
- Ganache
- Node.js
- Metamask
- IPFS: Inter Planetary File System - When we mint or create a NFT, the state and the logic (Smart Contract) gets stored in the blocks - but a distributed filesystem is needed to store the related media and this is what IPFS provides. Pinata is one of the easy frameworks to integrate IPFS in our dApp.

## Reference
Link to reading material and tutorials in my blog post: <a href= "https://www.appcloud101.com/how-dapps-are-revolutionizing-the-user-experience-with-blockchain-technology-a-working-example/"> How dApps are Revolutionizing the User Experience with Blockchain Technology: A Working Example</a>
### Thank you
