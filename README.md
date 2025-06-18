# `regen-temp-testnet` chain details

This is a temporary chain which has been setup for testing out the upcoming `v6` upgrade on Regen Network. This chain will act as a testing bed for node operators to ensure readiness for mainnet upgrade.

 - **Chain-id**: `regen-temp`
 - **denom**: `uregen`
 - **Current `regen` version**: `v5.1.4`
 - **Genesis file**: https://github.com/vitwit/regen-temp-testnet/blob/main/genesis.json

### Endpoints
 - **RPC**: https://rpc.regen-temp.vitwit.com
 - **API**: https://api.regen-temp.vitwit.com
 - **Explorer**: https://explorer.regen-temp.vitwit.com
 - **Faucet**: https://faucet.regen-temp.vitwit.com
 - **Peer**: 4b4524bf20524da17e17da08f5466c24e1dbc619@155.138.209.88:26656

### How to join
Theser is a bash script provided in the repo `join.sh`. It will manually build and install `regen` and `cosmovisor` binaries in your system along with downloading the genesis file and starting the systemd service. After executing the script wait till your node is caught up with the network. You can check the sync status of your node using the following command:
```
curl localhost:26657/status | jq .result.sync_info.catching_up
```
If this command returns `false` then your node has caught up with the network. If it returns `true` then wait for some time and execute the command again till it catches up.

#### Starting validator 

Create keys on your node using:
```
regen keys add <val-name>
```

Head over to the faucet link mentioned above and request tokens for your address.

Note: Please make sure you submit the `create-validator` tx only after your node is fully synced.

Create your validator using the following command:
```
regen tx staking create-validator --amount 4900000000uregen \
--commission-max-change-rate 0.01 \
--commission-max-rate 0.2 \
--commission-rate 0.1 \
--moniker <your-moniker> \
--min-self-delegation 1 \
--pubkey $(regen tendermint show-validator) \
--chain-id regen-temp \
--fees 1000uregen \
--from <val-name> 
```
