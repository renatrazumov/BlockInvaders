# BlockInvaders

## DAPPS Network - Hackathon 

### Liquid Apps - Github
- https://github.com/liquidapps-io

### Liquid Apps - Developers 
- https://docs.liquidapps.io/en/v2.0/developers.html
- Kylin Testnet Account
    - https://docs.liquidapps.io/en/v2.0/developers/kylin-account.html

### Liquid Apps - Zeus 
- https://liquidapps.io/zeus
- https://liquidapps.io/liquid-accounts
- https://liquidapps.io/liquid-link
- https://liquidapps.io/liquid-oracles

### Liquid Apps - Repos
- zeus-sdk 
- zeus-ide
- eos-contracts-best-practices
- awesome-eosio-plugins

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

### Create Kylin Testnet Account 
- https://kylin-dapp-faucet.liquidapps.io
