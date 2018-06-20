### 1.6.2. ※personal_listAccounts

```js
curl --data '{"method":"personal_listAccounts","params":[],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
```
### 1.6.3. ※personal_newAccount

```js
curl --data '{"method":"personal_newAccount","params":["hunter2"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
```

### 1.6.4. ※personal_sendTransaction

```js
curl --data '{"method":"personal_sendTransaction","params":[{"from":"0x407d73d8a49eeb85d32cf465507dd71d507100c1","to":"0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b","data":"0x41cd5add4fd13aedd64521e363ea279923575ff39718065d38bd46f0e6632e8e","value":"0x186a0"},"hunter2"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
```

### 1.6.5. ※personal_unlockAccount

```js
unlockAccount の最後の引数はunlock している時間なのですが、parity では数値は16進数で表します。また、"0x0" とした場合、無限時間になります。
curl --data '{"method":"personal_unlockAccount","params":["0x055229436e8e1b0a2bd4d71d6525c3222ae3ab27","hunter2","0x0"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545


```
### 1.6.6. ※kiểm tra Ether đã được gửi hay chưa

```js
curl --data '{"method":"eth_getTransactionByHash","params":["0xabf51e7501f462523e70b5cef944d0403bd4c82e247282f4b2c847b16a92cc46"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545 | jq


sudo apt-get update
sudo apt-get install jq
