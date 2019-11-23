# BlockInvaders

## DAPPS Network - Hackathon 

### Liquid Apps - Resources & Documentation
https://docs.liquidapps.io/en/v2.0/

### Liquid Apps - Developers 
- https://docs.liquidapps.io/en/v2.0/developers.html
- Kylin Testnet Account
    - https://docs.liquidapps.io/en/v2.0/developers/kylin-account.html
    
### Liquid Apps - Github
- https://github.com/liquidapps-io
- https://github.com/liquidapps-io/zeus-ide
- https://github.com/liquidapps-io/zeus-sdk

### Gitpod
https://gitpod.io/#https://github.com/liquidapps-io/zeus-ide

### Liquid Apps
- https://liquidapps.io/zeus
- https://liquidapps.io/sdk
- https://liquidapps.io/liquid-accounts
- https://liquidapps.io/liquid-link
- https://liquidapps.io/liquid-oracles

### Zeus IDE

> The Zeus IDE allows new developers to get up and running in mere minutes! It is based on Gitpod, a cloud-based tool for creating IDEs from git repos backed by Docker containers. All a you need to do is log in to Gitpod with your GitHub account and establish a new workspace based on the LiquidApps Zeus IDE GitHub repo.

Behind the scenes, Gitpod executes the following:

- Automatically installs the Docker image, which already contains EOSIO, Zeus and many other tools
- Starts an EOSIO development node
- Generates a basic starting point for a project (using the Zeus SDK)
- Starts a LiquidApps development DSP

### Liquid Apps - vRam
> Alternative & Compatible Storage Solution

1. Integrate the vRAM Library into your dApp Smart Contract, allowing it to interact with the vRAM system.
2. Select the service package/s that satisfy your data storage and access needs.
3. Stake the amount of DAPP Tokens needed for your chosen service package.
4. Support your favorite service provider by staking tokens to them, even if no services are required. 

### Provided by the dApp Service Providers (DSPs)

> DSPs can now provide solutions for dApps' needs, including the most powerful oracle, IBC, storage, and scheduler solutions available, unlocking a wealth of functionality for dApps. As a DSP, you customize your service packages and have full autonomy over staking duration, pricing, and technical specifications.

### Get started as a EOS dApp developer

> CryptoKylin Testnet is for dApp developers who want to test their EOS smart contract before releasing to mainnet.

1. Register an account
Click here to register
- https://www.cryptokylin.io/

2. Get free token from faucet
Use faucet to send free tokens

3. Deploy your smart contract
You know the cleos drill to upload smart contract

4. Test and see it in action
Send API calls to any endpoints here. CryptoKylin also comes with a block explorer that you can view all the activities.

### Create Kylin Testnet Account 
- https://docs.liquidapps.io/en/v2.0/developers/kylin-account.html

```bash
# Create a new available account name (replace 'yourtestaccount' with your account name):
export ACCOUNT=yourtestaccount

# Configure endpoint
export DSP_ENDPOINT=https://kylin-dsp-1.liquidapps.io

# Create wallet
cleos wallet create --file wallet_password.pwd

# Create account and import key
curl http://faucet-kylin.blockzone.net/create/$ACCOUNT > keys.json
export ACTIVE_PRIVATE_KEY=`cat keys.json | jq -e '.keys.active_key.private'`
export ACTIVE_PUBLIC_KEY=`cat keys.json | jq -e '.keys.active_key.public'`
cleos wallet import --private-key $ACTIVE_PRIVATE_KEY
# if this does not work, import key directly

# Get some tokens, stake CPU/NET, buy RAM for contract
curl http://faucet-kylin.blockzone.net/get_token/$ACCOUNT
curl http://faucet-kylin.blockzone.net/get_token/$ACCOUNT
cleos -u $DSP_ENDPOINT system buyram $ACCOUNT $ACCOUNT "100.0000 EOS" -p $ACCOUNT@active
cleos -u $DSP_ENDPOINT system delegatebw $ACCOUNT $ACCOUNT "20.0000 EOS" "80.0000 EOS" -p $ACCOUNT@active
```

### Kylin DAPP Token Faucet
- https://kylin-dapp-faucet.liquidapps.io

### Hackathon Themes
##### Decentralized Finance (DeFi)
For many enthusiasts, DeFi is attractive in that it promises to extend the utility of blockchain to various financial functions, such as derivatives markets, lending platforms, supply chains, and insurance contracts.
Take part in making the financial system more transparent by building any DeFi-related dApp, product or service that harnesses at least two DAPP Network services.

##### Decentralized Gaming
Gaming has transformed from a youth pastime into a thriving industry. Blockchain technology can push the space even further by enabling the ownership of digital goods to flourish and expanding vibrant, interoperable gaming economies.
Use at least two DAPP Network services to build any kind of game or game-related product, and play your part in the blockchain gaming revolution.

##### Extending the DAPP Network’s Functionality
vRAM; LiquidAccounts; LiquidOracles; vCPU; LiquidLink; and much more. So many powerful services are already running on the DAPP Network, and this is only the beginning. 
Build your own service that DSPs can offer on a free-market basis, and help create new opportunities for developers building scalable dApps using the DAPP Network.

### Resources & Articles 
- https://medium.com/the-liquidapps-blog/the-dapp-network-just-added-powerful-new-features-for-eos-dapps-700bfc3e7bd6
- https://medium.com/the-liquidapps-blog/the-dapp-network-is-now-live-on-eos-db467f0dc2f
- https://medium.com/the-liquidapps-blog/all-aboard-the-eos-train-its-free-dbc00d9b21f
- https://medium.com/the-liquidapps-blog/vram-guide-for-experts-f809c8f82a27

