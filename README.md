# BlockInvaders Project

## DAPPS Network - Hackathon 

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
- https://kylin.eosx.io/tools/account/create

### Creating Accounts on ZEUS-IDE
```bash
# Create a new available account name (replace 'yourtestaccount' with your account name):
export ACCOUNT=blockinvader

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

### Kylin Block Explorer
- https://kylin.eosx.io/#/tx

### Kylin DAPP Token
- https://kylin.eosx.io/tx/bf815b55b5ea355c1bc0c3f7b31a6f5d51ea53ae88624ad4380851f4975ef542?listView=traces

### Kylin DAPP Token Faucet
- https://kylin-dapp-faucet.liquidapps.io


### Request Testnet Tokens 
- http://faucet.cryptokylin.io/get_token/blockinvader

```BASH
{"success":true,"data":{"account":"blockinvader","tx":"ea1d98e362aaa51d1882ce260b08985b8e5416be432a94aa3a0a9d4f78dfe6ff"}}
```

### View on Block Explorer 
- https://kylin.eosx.io/account/blockinvader

LiquidAccounts are EOS accounts that are stored in vRAM instead of RAM.  This drastically reduces the cost of creating accounts on EOS.  Another great place to understand the service is in the [unit tests](https://github.com/liquidapps-io/zeus-sdk/blob/master/boxes/groups/services/vaccounts-dapp-service/test/vaccountsconsumer.spec.js).

## Prerequisites

* [Zeus](zeus-getting-started.md) - Zeus installs eos and the eosio.cdt if not already installed
* [Kylin Account](kylin-account.md)

## Unbox LiquidAccounts DAPP Service box
This box contains the LiquidAccounts smart contract libraries, DSP node logic, unit tests, and everything else needed to get started integrating / testing the DAPP Network LiquidAccounts in your smart contract.
```bash
# npm install -g @liquidapps/zeus-cmd
zeus unbox vaccounts-dapp-service
cd vaccounts-dapp-service
zeus test
```

## LiquidAccounts

### LiquidAccount Consumer Example Contract used in unit tests
in `contract/eos/vaccountsconsumer/vaccountsconsumer.cpp`
The consumer contract is a great starting point for playing around with the LiquidAccount syntax.
```cpp
/* DELAY REMOVAL OF USER DATA INTO VRAM */
/* ALLOWS FOR QUICKER ACCESS TO USER DATA WITHOUT THE NEED TO WARM DATA UP */
#define VACCOUNTS_DELAYED_CLEANUP 120

/* ADD NECESSARY LIQUIDACCOUNT / VRAM INCLUDES */
#include "../dappservices/vaccounts.hpp"
#include "../dappservices/ipfs.hpp"
#include "../dappservices/multi_index.hpp"

/* ADD LIQUIDACCOUNT / VRAM RELATED ACTIONS */
#define DAPPSERVICES_ACTIONS() \
  XSIGNAL_DAPPSERVICE_ACTION \
  IPFS_DAPPSERVICE_ACTIONS \
  VACCOUNTS_DAPPSERVICE_ACTIONS

#define DAPPSERVICE_ACTIONS_COMMANDS() \
  IPFS_SVC_COMMANDS()VACCOUNTS_SVC_COMMANDS() 
  
#define CONTRACT_NAME() vaccountsconsumer 


CONTRACT_START()
  
  /* THE FOLLOWING STRUCT DEFINES THE PARAMS THAT MUST BE PASSED */
  struct dummy_action_hello {
      name vaccount;
      uint64_t b;
      uint64_t c;
  
      EOSLIB_SERIALIZE( dummy_action_hello, (vaccount)(b)(c) )
  };
  
  /* DATA IS PASSED AS PAYLOADS INSTEAD OF INDIVIDUAL PARAMS */
  [[eosio::action]] void hello(dummy_action_hello payload) {
    /* require_vaccount is the equivalent of require_auth for EOS */
    require_vaccount(payload.vaccount);
    
    print("hello from ");
    print(payload.vaccount);
    print(" ");
    print(payload.b + payload.c);
    print("\n");
  }
  
  [[eosio::action]] void hello2(dummy_action_hello payload) {
    print("hello2(default action) from ");
    print(payload.vaccount);
    print(" ");
    print(payload.b + payload.c);
    print("\n");
  }
  
  [[eosio::action]] void init(dummy_action_hello payload) {
  }
  
  /* EACH ACTION MUST HAVE A STRUCT THAT DEFINES THE PAYLOAD SYNTAX TO BE PASSED */
  VACCOUNTS_APPLY(((dummy_action_hello)(hello))((dummy_action_hello)(hello2)))
  
CONTRACT_END((init)(hello)(hello2)(regaccount)(xdcommit)(xvinit))
```

## Compile

See the unit testing section for details on adding unit tests.

```bash
zeus compile
# compile and test with
zeus test
# test without compiling
zeus test --no-compile-all
```

## Deploy Contract
```bash
export DSP_ENDPOINT=https://kylin-dsp-2.liquidapps.io
export KYLIN_TEST_ACCOUNT=<ACCOUNT_NAME>
export KYLIN_TEST_PUBLIC_KEY=<ACTIVE_PUBLIC_KEY>
# Buy RAM:
cleos -u $DSP_ENDPOINT system buyram $KYLIN_TEST_ACCOUNT $KYLIN_TEST_ACCOUNT "200.0000 EOS" -p $KYLIN_TEST_ACCOUNT@active
# Set contract code and abi
cleos -u $DSP_ENDPOINT set contract $KYLIN_TEST_ACCOUNT vaccountsconsumer -p $KYLIN_TEST_ACCOUNT@active

# Set contract permissions
cleos -u $DSP_ENDPOINT set account permission $KYLIN_TEST_ACCOUNT active "{\"threshold\":1,\"keys\":[{\"weight\":1,\"key\":\"$KYLIN_TEST_PUBLIC_KEY\"}],\"accounts\":[{\"permission\":{\"actor\":\"$KYLIN_TEST_ACCOUNT\",\"permission\":\"eosio.code\"},\"weight\":1}]}" owner -p $KYLIN_TEST_ACCOUNT@active
```

## Select and stake DAPP for DSP package | [DSP Portal Link](https://dsphq.io/packages/heliosselene/accountless1/accountless1?network=kylin)
 * Use [the faucet](https://kylin-dapp-faucet.liquidapps.io/) to get some DAPP tokens on Kylin
 * Information on: [DSP Packages and staking DAPP/DAPPHDL (AirHODL token)](dsp-packages-and-staking.md)
```bash
export PROVIDER=heliosselene
export PACKAGE_ID=accountless1

# select your package: 
export SERVICE=accountless1
cleos -u $DSP_ENDPOINT push action dappservices selectpkg "[\"$KYLIN_TEST_ACCOUNT\",\"$PROVIDER\",\"$SERVICE\",\"$PACKAGE_ID\"]" -p $KYLIN_TEST_ACCOUNT@active

# Stake your DAPP to the DSP that you selected the service package for:
cleos -u $DSP_ENDPOINT push action dappservices stake "[\"$KYLIN_TEST_ACCOUNT\",\"$PROVIDER\",\"$SERVICE\",\"10.0000 DAPP\"]" -p $KYLIN_TEST_ACCOUNT@active
```

## Test
First you'll need to initialize the LiquidAccounts implementation with the `chain_id` of the platform you're operating on.

```bash
# kylin
export CHAIN_ID=5fff1dae8dc8e2fc4d5b23b2c7665c97f9e9d8edf2b6485a86ba311c25639191
cleos -u $DSP_ENDPOINT push action $KYLIN_TEST_ACCOUNT xvinit "[\"$CHAIN_ID\"]" -p $KYLIN_TEST_ACCOUNT
```

Then you can begin registering accounts.  You will need to do this in a nodejs environment using the [`dapp-client-lib`](https://www.npmjs.com/package/@liquidapps/dapp-client).  [Here is an example of using the lib to register an account.](https://github.com/liquidapps-io/zeus-sdk/blob/master/boxes/groups/services/vaccounts-dapp-service/client/examples/push_register_liquid_account.ts).

```bash
npm install -g @liquidapps/dapp-client
```

This example takes:

- the contract name the LiquidAccount project is deployed to
- the active private key of that account
- the `regaccount` as the action name
- the payload with the `vaccount` name

After registering an account, you may also use the library to [push LiquidAccount transactions](https://github.com/liquidapps-io/zeus-sdk/blob/master/boxes/groups/services/vaccounts-dapp-service/client/examples/push_liquid_account_transaction.ts).  In the linked example, you can see that the action name has changed to `hello` and the payload has changed to include the required parameters.


### Resources & Articles 
- https://medium.com/the-liquidapps-blog/the-dapp-network-just-added-powerful-new-features-for-eos-dapps-700bfc3e7bd6
- https://medium.com/the-liquidapps-blog/the-dapp-network-is-now-live-on-eos-db467f0dc2f
- https://medium.com/the-liquidapps-blog/all-aboard-the-eos-train-its-free-dbc00d9b21f
- https://medium.com/the-liquidapps-blog/vram-guide-for-experts-f809c8f82a27
