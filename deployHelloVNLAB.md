
Step1: delete files in build folder <br>
Step2: truffle compile <br>
Step3: truffle migrate <br>
Step4: Regist CNS, abi( abi of my contract) <br>
Step5: Change cnsAddress in config.js <br>
(Step6): Change CNS address and abi in html file
```html
<html>

<body>
    <script src="node_modules/eth-client/dist/eth-client.min.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
    <script type="text/javascript">
    const cnsAddress = '0x6c107d669eeb74f823c66d8688dafab91ec9c984';
    const baseUrl = 'http://beta.blockchain.z.com';
    const abi = [{"constant":true,"inputs":[],"name":"provider","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"isVersionContract","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"isVersionLogic","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"contractName","outputs":[{"name":"","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"isVersionContractOrLogic","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"sayHello","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"cns","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"getContractName","outputs":[{"name":"","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"getCns","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[{"name":"_cns","type":"address"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"}];
    var account;
    var contract;
	register();
    function register() {
        ethClient.Account.create(baseUrl, '', function(err, _account) {
            if (err) {
                console.log(err);
            } else {
                account = _account;
                contract = new ethClient.AltExecCnsContract(account, cnsAddress);
				contract.call('', 'Hello', 'sayHello', [], abi, function(err, res) {
					if (err) console.error(err);
					else console.log(res.join(','));
				});
                console.log(account.getAddress());
            }
        });
    };
    
    </script>
   
</body>

</html>
```


### Error when run: npm install eth-client --no-bin-links

```js
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:276:23)
gyp ERR! stack     at emitTwo (events.js:106:13)
gyp ERR! stack     at ChildProcess.emit (events.js:191:7)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:219:12)
```
>fix:

```js
sudo apt-get install build-essential g++
``` 
