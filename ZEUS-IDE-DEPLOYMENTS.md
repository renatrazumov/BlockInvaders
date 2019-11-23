#gitpod account creation 

```bash
gitpod /workspace/zeus-ide $ {
> cd dapp; zeus start-localenv
> }; HISTFILE=/workspace/.gitpod/cmd-1 history -r
⚓ Setup environment 02-eos-local-nodeos.js
Initing dappservices plugins
Adding 1.8.0 Parameters
⚓ Setup environment 05-eos-local-bios.js
(node:708) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.
⚓ Setup environment 15-eos-demux.js
☁️ Running service: demux port: 3195
⚓ Setup environment 15-ipfs-dameon.js
☁️ Running service: ipfs-daemon port: 3199
⚓ Setup environment 20-eos-local-dapp-services.js
☁️ Running service: dapp-services-node port: 13015
☁️ Running service: dapp-services-node port: 26030
⚓ Setup environment 21-eos-local-services-all-dapp-services.js
☁️ Running service: auth-dapp-service-node port: 13127
☁️ Running service: auth-dapp-service-node port: 26254
☁️ Running service: cron-dapp-service-node port: 13131
☁️ Running service: cron-dapp-service-node port: 26262
☁️ Running service: dns-dapp-service-node port: 13284
☁️ Running service: dns-dapp-service-node port: 26568
☁️ Running service: history-dapp-service-node port: 13143
☁️ Running service: history-dapp-service-node port: 26286
☁️ Running service: ipfs-dapp-service-node port: 13115
☁️ Running service: ipfs-dapp-service-node port: 26230
☁️ Running service: log-dapp-service-node port: 13110
☁️ Running service: log-dapp-service-node port: 26220
☁️ Running service: oracle-dapp-service-node port: 13112
☁️ Running service: oracle-dapp-service-node port: 26224
☁️ Running service: readfn-dapp-service-node port: 13141
☁️ Running service: readfn-dapp-service-node port: 26282
☁️ Running service: storage-dapp-service-node port: 13142
☁️ Running service: storage-dapp-service-node port: 26284
☁️ Running service: vaccounts-dapp-service-node port: 13129
☁️ Running service: vaccounts-dapp-service-node port: 26258
☁️ Running service: vcpu-dapp-service-node port: 13386
☁️ Running service: vcpu-dapp-service-node port: 26772
```

```bash
gitpod /workspace/zeus-ide/dapp $ cleos wallet create -n blockinvader --file wallet_password.pwd
Creating wallet: blockinvader
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
saving password to wallet_password.pwd
```
```bash
gitpod /workspace/zeus-ide/dapp $ curl http://faucet-kylin.blockzone.net/create/$ACCOUNT > keys.json
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   422  100   422    0     0    395      0  0:00:01  0:00:01 --:--:--   395
```
```bash
gitpod /workspace/zeus-ide/dapp $ export ACTIVE_PRIVATE_KEY=`cat keys.json | jq -e '.keys.active_key.private'`
gitpod /workspace/zeus-ide/dapp $ export ACTIVE_PUBLIC_KEY=`cat keys.json | jq -e '.keys.active_key.public'`
```
```bash
gitpod /workspace/zeus-ide/dapp $ cleos wallet import --private-key 5JebAwDdk9EhWbWJiLGuvnxzwjVmWaX7Ba65RLDfkFyQLwoUocQimported private key for: EOS8ZxHTfcT5BfMuyvJDhV6SyDAktQ3kmGSoPo2drdweAHJ88mogC
```
```bash
gitpod /workspace/zeus-ide/dapp $ curl http://faucet-kylin.blockzone.net/get_token/$ACCOUNT                                      {"success":true,"data":{"account":"blockinvader","tx":"c83cc047dc52b1b92b4e8d388f1543ebf05d21f283bf6dd781a59991c69493f4"}}gitpod /workspace/zeus-ide/dapp $ curl http://faucet-kylin.blockzone.net/get_token/$ACCOUNT
{"success":true,"data":{"account":"blockinvader","tx":"843c8a9bef62cccdd8d3448c1c5ace6cb2e23a2dba534110e1c48ced911f60e5"}}gitpod /workspace/zeus-ide/dapp $ cleos -u $DSP_ENDPOINT system buyram $ACCOUNT $ACCOUNT "100.0000 EOS" -p $ACCOUNT@active
executed transaction: 4373dad32672915cc9972154ca4b8900b852c02cf9e8c749d793f358a845be39  128 bytes  762 us
#         eosio <= eosio::buyram                {"payer":"blockinvader","receiver":"blockinvader","quant":"100.0000 EOS"}
#   eosio.token <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ram","quantity":"99.5000 EOS","memo":"buy ram"}
#  blockinvader <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ram","quantity":"99.5000 EOS","memo":"buy ram"}
#     eosio.ram <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ram","quantity":"99.5000 EOS","memo":"buy ram"}
#   eosio.token <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ramfee","quantity":"0.5000 EOS","memo":"ram fee"}
#  blockinvader <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ramfee","quantity":"0.5000 EOS","memo":"ram fee"}
#  eosio.ramfee <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.ramfee","quantity":"0.5000 EOS","memo":"ram fee"}
#   eosio.token <= eosio.token::transfer        {"from":"eosio.ramfee","to":"eosio.rex","quantity":"0.5000 EOS","memo":"transfer from eosio.ramfee t...
#  eosio.ramfee <= eosio.token::transfer        {"from":"eosio.ramfee","to":"eosio.rex","quantity":"0.5000 EOS","memo":"transfer from eosio.ramfee t...
#     eosio.rex <= eosio.token::transfer        {"from":"eosio.ramfee","to":"eosio.rex","quantity":"0.5000 EOS","memo":"transfer from eosio.ramfee t...
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```
```bash
gitpod /workspace/zeus-ide/dapp $ cleos -u $DSP_ENDPOINT system delegatebw $ACCOUNT $ACCOUNT "20.0000 EOS" "80.0000 EOS" -p $ACCOUNT@active
executed transaction: c4176ecc749dc1a5989371d4be1111d3adb4d31df15d14cb732ff858ae91334a  144 bytes  587 us
#         eosio <= eosio::delegatebw            {"from":"blockinvader","receiver":"blockinvader","stake_net_quantity":"20.0000 EOS","stake_cpu_quant...
#   eosio.token <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.stake","quantity":"100.0000 EOS","memo":"stake bandwidth"}
#  blockinvader <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.stake","quantity":"100.0000 EOS","memo":"stake bandwidth"}
#   eosio.stake <= eosio.token::transfer        {"from":"blockinvader","to":"eosio.stake","quantity":"100.0000 EOS","memo":"stake bandwidth"}
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```
