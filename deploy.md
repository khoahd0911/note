## DEPLOY

### Main flow
Step1: truffle compile <br>
Step2: truffle migrate (note: network)<br>
Step3: copy CNS address <br>
Step4: copy contract address and its ABI <br>
Step5: update config.js, config.json <br>

NOTE: 





### Deploy to Ethereum network
>Install nodejs
```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs

```

>Install truffle and init
```
npm install -g truffle
cd PROJECT_FOLDER
truffle init
```

> Start Parity ON ANOTHER GIT BASH
```
//kill old process 
pkill -KILL -x parity

//start
parity --no-warp --geth &
```

```js
curl --data '{"method":"parity_addReservedPeer","params":["enode://399f475c03a2f66d7506c6ae96b778ff7763e1ec3d3cbe4b2c7a494e3e7d18f0267e06c03cf127ad95ebf3030724402c6b9c9b9311f7db7f5d98d077b11b7e4e@163.44.171.129:30303"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

curl --data '{"method":"parity_addReservedPeer","params":["enode://64fd3830aa46ff597ecb886bdada7c2ae34c585802f7022ec272e2c65dadb483d356d10c6e9b6411ee69318c75b8e1a1fb6dd277631c759cb2332c12e2dc75f7@150.95.132.79:30303"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

```


>sync time with Japan
```
sudo apt-get install ntpdate
ntpdate -b 0.ubuntu.pool.ntp.org
ntpdate -b 1.ubuntu.pool.ntp.org
ntpdate -b 2.ubuntu.pool.ntp.org
ntpdate -b 3.ubuntu.pool.ntp.org
```

>Deploy contract
```
truffle compile
truffle migrate
```

>truffle.js
```
module.exports = {
  networks: {
      development: {
          host: "localhost",
          port: 8545,
          network_id: "20581"
      },
      production: {
          host: "localhost",
          port: 8545,
          network_id: "9449",
          gasPrice: 10000000000
      }
  }
};
```
### Create account to deploy

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
//PRD
curl --data '{"method":"personal_unlockAccount","params":["0x055229436e8e1b0a2bd4d71d6525c3222ae3ab27","hunter2","0x0"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

//STG
curl --data '{"method":"personal_unlockAccount","params":["0x3e838f01ec28549f5f457000606d787b375c960d","hunter2","0x0"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

```
### 1.6.6. ※kiểm tra Ether đã được gửi hay chưa

```js
sudo apt-get install jq
curl --data '{"method":"eth_getTransactionByHash","params":["0x43616c6c206d6574686f642074657374696e672e000000000000000000000000"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545 | jq
```

### Write one more contract

> pakage.json
```js
{
    "name": "some-contract",
    "version": "1.0.0",
    "description": "",
    "main": "truffle-config.js",
    "directories": {
      "test": "test"
    },
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "dependencies": {
        "zcom-contracts": "git+https://github.com/zcom-cloud-blockchain/solidity.git"

    
    }
  }
```

> npm install

> deploy.js
```js
var SomeContract = artifacts.require("./SomeContract.sol");
ContractNameService = artifacts.require("zcom-contracts/contracts/ContractNameService.sol");

module.exports = function(deployer) {
  deployer.deploy(SomeContract, ContractNameService.address).then(function() {
    return ContractNameService.deployed();
}).then(function(instance) {
    return instance.setContract('SomeContract', 1, SomeContract.address,SomeContract.address);
});
};
```

> 