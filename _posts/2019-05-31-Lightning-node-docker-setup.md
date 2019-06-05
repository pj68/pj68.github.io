
# Lightning Node - docker setup

### setup docker images
ref: https://hub.docker.com/r/elementsproject/lightningd/


```
docker-compose up
sudo docker exec -i -t 1e5379877d76 /bin/bash
```




### setup wallet
lightning node:
- create new address
-  wait for the blockchains to sync

```
lightning-cli newaddr
lightning-cli newaddr p2sh-segwit

lightning-cli getinfo
lightning-cli  listfunds
lightning-cli listconfigs
lightning-cli listpeers

```

```
bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass  getblockcount
bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass sendtoaddress tb1qpprwh7apljv9kgd4hcv2h7d0ah5r4jeqgvrcqz 0.01
 bitcoin-cli  -testnet -rpcuser=rpcuser -rpcpassword=rpcpass  getwalletinfo

```
### send payment
on the lightning node:
 - check for testnet nodes: https://1ml.com/testnet
 - connect to node (note: use telnet ip port to test if public node is up)
 - create channel
 - fund channel


```
lightning-cli connect 03c856d2dbec7454c48f311031f06bb99e3ca1ab15a9b9b35de14e139aa663b463 34.201.74.232 9735


lightning-cli fundchannel 03c856d2dbec7454c48f311031f06bb99e3ca1ab15a9b9b35de14e139aa663b463 1000000

lightning-cli listpeers


```
### docker-compose.yml
```
version: "3"
services:
  bitcoind:
    image: nicolasdorier/docker-bitcoin:0.16.3
    container_name: bitcoind
    environment:
      BITCOIN_EXTRA_ARGS: |
        testnet=1
        whitelist=0.0.0.0/0
        server=1
        rpcuser=rpcuser
        rpcpassword=rpcpass
    expose:
      - "18332"
    ports:
      - "0.0.0.0:18333:18333"
    volumes:
      - "bitcoin_datadir:/data"

  clightning_bitcoin:
    image: elementsproject/lightningd
    container_name: lightningd
    command:
      - --bitcoin-rpcconnect=bitcoind
      - --bitcoin-rpcuser=rpcuser
      - --bitcoin-rpcpassword=rpcpass
      - --plugin-dir=/usr/libexec/c-lightning/plugins
      - --network=testnet
      - --alias=mytestawesomenode
      - --log-level=debug
    environment:
      EXPOSE_TCP: "true"
    expose:
      - "9735"
    ports:
      - "0.0.0.0:9735:9735"
    volumes:
      - "clightning_bitcoin_datadir:/root/.lightning"
      - "bitcoin_datadir:/etc/bitcoin"
    links:
      - bitcoind

volumes:
  bitcoin_datadir:
  clightning_bitcoin_datadir:
```

links:
https://medium.com/@Jayvdb/setting-up-and-transacting-on-the-bitcoin-lightning-network-a9ada42ec305
https://medium.com/coinmonks/installing-lightning-network-part-2-here-we-go-again-ed5a84f9cade
https://medium.com/coinmonks/raspberry-pi-lightning-network-w-no-external-drive-5-steps-d4fba98ac8cb
https://github.com/ElementsProject/lightning
https://hub.docker.com/r/elementsproject/lightningd/

