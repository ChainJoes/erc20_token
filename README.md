# ChainJoes ERC20 token

### Total Supply: 100M 
### Symbol: CJ

## Tokenomics
| |Tokens |Percentage|
|----------|-----|--------|
|Private Sale|2.000.000|2%|
|Public Sale|6.000.000|6%|
|Seed|18.000.000|18%|
|Team|16.000.000|16%|
|Liquidity|4.000.000|4%|
|Treasury|17.000.000|17%|
|P2E|35.000.000|35%|
|Airdrop|2.000.000|2%|

## Features? 

- Do we need mint/burn function included? 
- Pausable contract? Or just claim after sale. 
- Voting? 
- Flash Minting?
- Snapshots?
- Proxy to upgrade this contract? 

# How to Deploy

## Config local network
- Install Ganache
- Start Ganache and create new project by point to truffle-config.js file

## Config real network
- Register new account on infura.io
- Create new project
- Get project api and connection link: 
```
ROPSTEN_URL=https://ropsten.infura.io/v3/<your-api-key>
KOVAN_URL=https://kovan.infura.io/v3/<your-api-key>
RINKEBY_URL=https://rinkeby.infura.io/v3/<your-api-key>
MAINNET_URL=https://mainnet.infura.io/v3/<your-api-key>
```
- Goto Truffle project, install node libs
```
npm install truffle-hdwallet-provider --save
npm install bip39 dotenv --save

# where
* bip39 – used to generate wallet mnemonic
* dotenv – simple way to read environment variable files
```
- Generate MNEMONIC words
```
node -e "console.log(require('bip39').generateMnemonic())"
```
- Create `.env` file, put MNEMONIC and <network>_URL to file
```
MNEMONIC=wallet mnemonic 12 words
ROPSTEN_URL=https://ropsten.infura.io/v3/<your-api-key>
KOVAN_URL=https://kovan.infura.io/v3/<your-api-key>
RINKEBY_URL=https://rinkeby.infura.io/v3/<your-api-key>
MAINNET_URL=https://mainnet.infura.io/v3/<your-api-key>
```
- Update truffle-config.js file
```
require('dotenv').config()
const HDWalletProvider = require('truffle-hdwallet-provider')
const MNEMONIC = process.env.MNEMONIC
const ROPSTEN_URL = process.env.ROPSTEN_URL
const KOVAN_URL = process.env.KOVAN_URL
const RINKEBY_URL = process.env.RINKEBY_URL
const MAINNET_URL = process.env.MAINNET_URL

module.exports = {
    // Uncommenting the defaults below
    // provides for an easier quick-start with Ganache.
    // You can also follow this format for other networks;
    // see <http://truffleframework.com/docs/advanced/configuration>
    // for more details on how to specify configuration options!
    contracts_build_directory: "../frontend/src/Contract/abi",
    networks: {
        development: {
            host: "127.0.0.1",
            port: 7545,
            network_id: "*"
        },
        test: {
            host: "127.0.0.1",
            port: 7545,
            network_id: "*"
        },
        ropsten: {
            provider: () => new HDWalletProvider(MNEMONIC, ROPSTEN_URL),
            network_id: 3
        },
        kovan: {
            provider: () => new HDWalletProvider(MNEMONIC, KOVAN_URL),
            network_id: 42
        },
        rinkeby: {
            provider: () => new HDWalletProvider(MNEMONIC, RINKEBY_URL),
            network_id: 4
        },
        // main ethereum network(mainnet)
        mainnet: {
            provider: () => new HDWalletProvider(MNEMONIC, MAINNET_URL),
            network_id: 1
        }
    }

};
```
- To get public wallet address
```
truffle console --network <network>
truffle(ropsten)> web3.eth.getAccounts((err, accounts) => console.log(accounts))
eg:
truffle console --network ropsten
truffle(ropsten)> web3.eth.getAccounts((err, accounts) => console.log(accounts))
[ '0x627306090abab3a6e1400e9345bc60c78a8bef57' ]
``` 
- Prepare some eth from test network faucet
```
https://faucet.metamask.io/
https://faucet.ropsten.be/
https://faucet.metamask.io/
http://faucet.bitfwd.xyz/
https://goerli-faucet.mudit.blog
```

### Deploy a contract to the network

- Remove old build api built files
- Run migrate
```
# For local network
truffle migrate

# Fow specific network
truffle migrate --network <network>
eg: 
truffle migrate --network ropsten
truffle migrate --network mainnet

# Migrate contract only
truffle migrate -f 2 --network ropsten
```
