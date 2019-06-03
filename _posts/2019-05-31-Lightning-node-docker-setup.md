
# Lightning Node - docker setup

### setup docker images
ref: https://hub.docker.com/r/elementsproject/lightningd/







### setup wallet
lightning node:
- create new address
-  wait for the blockchains to sync

```
lightning-cli newaddr
lightning-cli newaddr p2sh-segwit

lightning-cli getinfo
lightning-cli  listfunds
```

```
bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass  getblockcount
bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass sendtoaddress tb1qpprwh7apljv9kgd4hcv2h7d0ah5r4jeqgvrcqz 0.01
 bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass  getwalletinfo

```



links:
https://medium.com/@Jayvdb/setting-up-and-transacting-on-the-bitcoin-lightning-network-a9ada42ec305
https://medium.com/coinmonks/installing-lightning-network-part-2-here-we-go-again-ed5a84f9cade
https://medium.com/coinmonks/raspberry-pi-lightning-network-w-no-external-drive-5-steps-d4fba98ac8cb
https://github.com/ElementsProject/lightning
https://hub.docker.com/r/elementsproject/lightningd/

