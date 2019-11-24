# BlockInvaders Project

## DAPPS Network Hackathon 

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

# LiquidAccounts

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

# vRAM

vRAM is a caching solution that enables DAPP Service providers (specialized EOS nodes) to load data to and from RAM <> vRAM on demand.  Data is evicted from RAM and stored in vRAM after the transaction has been run.  This works similar to the way data is passed to and from regular computer RAM and a hard drive.  As with EOS, RAM is used in a computer sometimes because it is a faster storage mechanism, but it is scarce in supply as well.  For more information on the technical details of the transaction lifecycle, please read the [vRAM Guide For Experts](https://medium.com/the-liquidapps-blog/vram-guide-for-experts-f809c8f82a27) article and/or the [whitepaper](https://liquidapps.io/DAPP%20Network%20and%20DAPP%20Token%20Whitepaper%20v2.0.pdf).

vRAM requires a certain amount of data to be stored in RAM permanently in order for the vRAM system to be trustless.  This data is represented as rows in the `ipfsentry` table of any `dapp::multi_index` enabled smart contract.  It is used to create the merkle root that is used by the smart contract to verify the data's integrity before being used.  Each row in the `ipfsentry` table is structured with an IPFS universal resource identifier (`vector<char>`) and a shard id (`uint64_t`).  The default maximum amount of shards (thus relating to the maximum amount of RAM required) is 1024.  Said differently, the total amount of RAM that a `dapp::multi_index` will need to use is `1024 * (vector<char> data + uint64_t id)`.

The DAPP Services Provider is responsible for removing this data after the transaction's lifecycle.  If the DSP does not perform this action, the `ipfsentry` table will continue to grow until the account's RAM supply has been exhausted or the DSP resumes its services.

## Prerequisites

* [Zeus](zeus-getting-started.md) - Zeus installs eos and the eosio.cdt if not already installed
* [Kylin Account](kylin-account.md)

## Unbox sample template
This box supports all DAPP Services and unit tests and is built to integrate your own vRAM logic.
```bash
mkdir mydapp; cd mydapp
zeus unbox dapp --no-create-dir
zeus create contract mycontract
```

## Or use one of our template contracts
```bash
# unbox coldtoken contract and all dependencies
zeus unbox coldtoken
cd coldtoken
# unit test coldtoken contract locally
zeus test
```

## Add your contract logic
in contract/eos/mycontract/mycontract.cpp
```cpp
#pragma once

#include "../dappservices/log.hpp"
#include "../dappservices/plist.hpp"
#include "../dappservices/plisttree.hpp"
#include "../dappservices/multi_index.hpp"

#define DAPPSERVICES_ACTIONS() \
  XSIGNAL_DAPPSERVICE_ACTION \
  LOG_DAPPSERVICE_ACTIONS \
  IPFS_DAPPSERVICE_ACTIONS

/*** IPFS: (xcommit)(xcleanup)(xwarmup) | LOG: (xlogevent)(xlogclear) ***/
#define DAPPSERVICE_ACTIONS_COMMANDS() \
  IPFS_SVC_COMMANDS()LOG_SVC_COMMANDS() 

/*** UPDATE CONTRACT NAME ***/
#define CONTRACT_NAME() mycontract

using std::string;

CONTRACT_START()
  public:

  /*** YOUR LOGIC ***/

  private:
    struct [[eosio::table]] vramaccounts {
      asset    balance;
      uint64_t primary_key()const { return balance.symbol.code().raw(); }
    };

    /*** VRAM MULTI_INDEX TABLE ***/
    typedef dapp::multi_index<"vaccounts"_n, vramaccounts> cold_accounts_t;

    /*** FOR CLIENT SIDE QUERY SUPPORT ***/
    typedef eosio::multi_index<".vaccounts"_n, vramaccounts> cold_accounts_t_v_abi;
    TABLE shardbucket {
      std::vector<char> shard_uri;
      uint64_t shard;
      uint64_t primary_key() const { return shard; }
    };
    typedef eosio::multi_index<"vaccounts"_n, shardbucket> cold_accounts_t_abi;

/*** ADD ACTIONS ***/
CONTRACT_END((your)(actions)(here))
```

## Compile

See the unit testing section for details on adding unit tests.

```bash
zeus compile
# compile and test with
zeus test
```

## Deploy Contract
```bash
export DSP_ENDPOINT=https://kylin-dsp-1.liquidapps.io
export KYLIN_TEST_ACCOUNT=<ACCOUNT_NAME>
export KYLIN_TEST_PUBLIC_KEY=<ACTIVE_PUBLIC_KEY>
# Buy RAM:
cleos -u $DSP_ENDPOINT system buyram $KYLIN_TEST_ACCOUNT $KYLIN_TEST_ACCOUNT "200.0000 EOS" -p $KYLIN_TEST_ACCOUNT@active
# Set contract code and abi
cleos -u $DSP_ENDPOINT set contract $KYLIN_TEST_ACCOUNT ../contract -p $KYLIN_TEST_ACCOUNT@active

# Set contract permissions
cleos -u $DSP_ENDPOINT set account permission $KYLIN_TEST_ACCOUNT active "{\"threshold\":1,\"keys\":[{\"weight\":1,\"key\":\"$KYLIN_TEST_PUBLIC_KEY\"}],\"accounts\":[{\"permission\":{\"actor\":\"$KYLIN_TEST_ACCOUNT\",\"permission\":\"eosio.code\"},\"weight\":1}]}" owner -p $KYLIN_TEST_ACCOUNT@active
```

## Select and stake DAPP for DSP package
 * Use [the faucet](https://kylin-dapp-faucet.liquidapps.io/) to get some DAPP tokens on Kylin
 * Information on: [DSP Packages and staking DAPP/DAPPHDL (AirHODL token)](dsp-packages-and-staking.md)
```bash
export PROVIDER=uuddlrlrbass
export PACKAGE_ID=package1

# select your package: 
export SERVICE=ipfsservice1
cleos -u $DSP_ENDPOINT push action dappservices selectpkg "[\"$KYLIN_TEST_ACCOUNT\",\"$PROVIDER\",\"$SERVICE\",\"$PACKAGE_ID\"]" -p $KYLIN_TEST_ACCOUNT@active

# Stake your DAPP to the DSP that you selected the service package for:
cleos -u $DSP_ENDPOINT push action dappservices stake "[\"$KYLIN_TEST_ACCOUNT\",\"$PROVIDER\",\"$SERVICE\",\"10.0000 DAPP\"]" -p $KYLIN_TEST_ACCOUNT@active
```

## Test
Finally you can now test your vRAM implementation by sending an action through your DSP's API endpoint

```bash
cleos -u $DSP_ENDPOINT push action $KYLIN_TEST_ACCOUNT youraction1 "[\"param1\",\"param2\"]" -p $KYLIN_TEST_ACCOUNT@active

# coldtoken (issue / transfer use vRAM):
cleos -u $DSP_ENDPOINT push action $KYLIN_TEST_ACCOUNT create "[\"$KYLIN_TEST_ACCOUNT\",\"1000000000 TEST\"]" -p $KYLIN_TEST_ACCOUNT
cleos -u $DSP_ENDPOINT push action $KYLIN_TEST_ACCOUNT issue "[\"$KYLIN_TEST_ACCOUNT\",\"1000 TEST\",\"yay vRAM\"]" -p $KYLIN_TEST_ACCOUNT
cleos -u $DSP_ENDPOINT push action $KYLIN_TEST_ACCOUNT transfer "[\"$KYLIN_TEST_ACCOUNT\",\"natdeveloper\",\"1000 TEST\",\"yay vRAM\"]" -p $KYLIN_TEST_ACCOUNT
```

The result should look like:
```
executed transaction: 865a3779b3623eab94aa2e2672b36dfec9627c2983c379717f5225e43ac2b74a  104 bytes  67049 us
#  yourcontract <= yourcontract::youraction1         {"param1":"param1","param2":"param2"}
>> {"version":"1.0","etype":"service_request","payer":"yourcontract","service":"ipfsservice1","action":"commit","provider":"","data":"DH......"}
```

## Get table row
```bash
# zeus:
zeus get-table-row "CONTRACT_ACCOUNT" "TABLE_NAME" "SCOPE" "TABLE_PRIMARY_KEY" --endpoint $DSP_ENDPOINT | python -m json.tool
# curl: 
curl http://$DSP_ENDPOINT/v1/dsp/ipfsservice1/get_table_row -d '{"contract":"CONTRACT_ACCOUNT","scope":"SCOPE","table":"TABLE_NAME","key":"TABLE_PRIMARY_KEY"}' | python -m json.tool

# coldtoken:
zeus get-table-row $KYLIN_TEST_ACCOUNT "accounts" $KYLIN_TEST_ACCOUNT "TEST" --endpoint $DSP_ENDPOINT | python -m json.tool
curl http://$DSP_ENDPOINT/v1/dsp/ipfsservice1/get_table_row -d '{"contract":"CONTRACT_ACCOUNT","scope":"CONTRACT_ACCOUNT","table":"accounts","key":"TEST"}' | python -m json.tool
```



### Resources & Articles 
- https://medium.com/the-liquidapps-blog/the-dapp-network-just-added-powerful-new-features-for-eos-dapps-700bfc3e7bd6
- https://medium.com/the-liquidapps-blog/the-dapp-network-is-now-live-on-eos-db467f0dc2f
- https://medium.com/the-liquidapps-blog/all-aboard-the-eos-train-its-free-dbc00d9b21f
- https://medium.com/the-liquidapps-blog/vram-guide-for-experts-f809c8f82a27
