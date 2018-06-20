


## Error: File busy
Solution: 
Step1: install in NEWFOLDER
Step2: edit file package-lock.json
Step3: copy 2 files pakage, folder node_modules
Step4: back to project folder: npm install

```js
cd ..
mkdir khoa
npm install ????
```
> "bitcore-lib": "0.15.0" => 14 AND delete bitcore-lib in dependencies
```json
"bitcore-mnemonic": {
      "version": "1.5.0",
      "resolved": "https://registry.npmjs.org/bitcore-mnemonic/-/bitcore-mnemonic-1.5.0.tgz",
      "integrity": "sha512-sbeP4xwkindLMfIQhVxj6rZSDMwtiKmfc1DqvwpR6Yg+Qo4I4WHO5pvzb12Y04uDh1N3zgD45esHhfH0HHmE4g==",
      "requires": {
        "bitcore-lib": "^0.15.0",
        "unorm": "^1.3.3"
      },
      "dependencies": {
        "inherits": {
          "version": "2.0.1",
          "resolved": "https://registry.npmjs.org/inherits/-/inherits-2.0.1.tgz",
          "integrity": "sha1-sX0I0ya0Qj5Wjv9xn5GwscvfafE="
        },
```

```js
cp /khoa/package-lock.json /vagrant_data/
cp /khoa/package.json /vagrant_data
cp -Lr /khoa/node_modules/ /vagrant_data/
cd /vagrant_data
npm install
```

## Send data
>Step1: code

Remember import lib.
production CNS: 0x9148550103573a730535f95a01323a9fc3dc6aa0  
staging CNS:    0x164aedb1e7ae7e3d85c090aea6e70746f43b11bc

>Step2: deploy

```js
truffle compile

curl --data '{"method":"parity_addReservedPeer","params":["enode://399f475c03a2f66d7506c6ae96b778ff7763e1ec3d3cbe4b2c7a494e3e7d18f0267e06c03cf127ad95ebf3030724402c6b9c9b9311f7db7f5d98d077b11b7e4e@163.44.171.129:30303"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

curl --data '{"method":"parity_addReservedPeer","params":["enode://64fd3830aa46ff597ecb886bdada7c2ae34c585802f7022ec272e2c65dadb483d356d10c6e9b6411ee69318c75b8e1a1fb6dd277631c759cb2332c12e2dc75f7@150.95.132.79:30303"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545

truffle migrate (REMEMBER Sync)

```


## Something else
sudo npm install npm@latest -g


>※First, Uninstall completely nodejs and npm.

js
$ sudo apt remove nodejs npm

>※Then, reinstall it over the link below:
js
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install npm@latest -g



## Error: listen EADDRINUSE
```js
ps aux | grep node
```
vagrant  14761  0.0  2.0 704016 38520 pts/0    Sl+  01:22   0:01 node app.js
vagrant  15069  0.0  0.0 107456   908 pts/2    S+   01:59   0:00 grep --color=auto node
```js
$ sudo kill -9 14761
$ node app.js
```

## Delete => error: There have been validation errors => object type: string type => fixed.





jp1	stg-ci-jp1-1	150.95.36.132	   192.168.70.14
ssh root@150.95.36.132

jp1	stg-api-jp1-1	150.95.36.144	192.168.70.3

ssh root@150.95.36.144
chohth.ah4IL7ie










## RUN ON SERVERS
150.95.36.67
150.95.32.181
150.95.32.188
rootパスワードはdj-u7Thie7eso7eiです



※First, Uninstall completely nodejs and npm.

js
$ sudo apt remove nodejs npm

>※Then, reinstall it over the link below:
```js
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs     (v8.11.3)
sudo npm install npm@latest -g    (npm install npm@5.6.0 -g)
sudo apt-get install g++
sudo apt-get install libtool pkg-config build-essential autoconf automake


FROM WINDOWS
scp -r root@150.95.36.67:/var/www/test_performance/performance-test/test/asset/output_result D:/workspace/TASK/TEST/OUTPUT/67


0x4d411206f429f598ea2c31d77d2f844e3bde2c02