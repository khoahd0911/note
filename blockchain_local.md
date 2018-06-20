## BLOCKCHAIN LOCAL
### Step1: vagrant up

```rb
$ansible_install_script = <<SCRIPT
cp /home/vagrant/.ssh/authorized_keys /vagrant/.vagrant/machines/thingchain_1/virtualbox/authorized_keys
sed -i.bak -e "s%http://gb.archive.ubuntu.com/ubuntu/%http://ftp.jaist.ac.jp/pub/Linux/ubuntu/%g" /etc/apt/sources.list
#apt-get install software-properties-common
#apt-add-repository ppa:ansible/ansible
apt-get update
#apt-get install -y ansible
apt-get install -y python-pip libffi-dev libssl-dev
pip install ansible==2.3.1
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.box = "bento/ubuntu-16.04"
  
  config.vm.define :thingchain_1 do |m1|
    m1.vm.network :private_network, ip: "192.168.15.10"
    m1.vm.network :private_network, ip: "192.168.15.11"
    m1.vm.network :private_network, ip: "192.168.15.12"
    m1.vm.network :private_network, ip: "192.168.15.13"
    m1.vm.network :private_network, ip: "192.168.15.14"
    m1.vm.network :private_network, ip: "192.168.15.15"
    m1.vm.network :private_network, ip: "192.168.15.16"
    m1.vm.provider "virtualbox" do |v|
      v.name = "ThingChain 2"
      #v.gui = true
      v.memory = "3000"
      v.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
    end
    m1.vm.provision "shell", inline: $ansible_install_script
  end
  #config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "./ShareFolder/gmo/", "/var/gmo", mount_options: ['dmode=777','fmode=777']

  
end
```

### Step2 clone repo ansible and cd to this folder
2.1: cd gmo
2.2: clone ansible, batch from https://gitlab.thing-chain.site/

### Step3
>3.1 cd ansible
>3.2 run

Database
```js
ansible-playbook -i inventories/local/hosts admin.yml -c local
ansible-playbook -i inventories/local/hosts mysql.yml -c local

ansible-playbook -i inventories/local/hosts batch.yml -c local

ansible-playbook -i inventories/local/hosts batch.yml -c local --tags deploy_batch
ansible-playbook -i inventories/local/hosts api.yml -c local 
ansible-playbook -i inventories/local/hosts web.yml -c local
```
```js
mysql
CREATE USER 'gmo'@'192.168.15.13' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON . TO 'gmo'@'192.168.15.13';
FLUSH PRIVILEGES;
exit
mysql -ugmo -p -h 192.168.15.13
```

```js
mysql
use service_provider
// Then execute this script
// https://gitlab.thing-chain.site/blockchain/design/blob/master/schema/current_schema.sql
ansible-playbook -i inventories/local/hosts mysql.yml -c local --extra-vars="mysql_create_db=true"
```

>3.3 Install miner
```js
apt-get update
apt-get install openssl libssl-dev libudev-dev
curl https://sh.rustup.rs -sSf | sh

wget https://parity-downloads-mirror.parity.io/v1.8.5/x86_64-unknown-linux-gnu/parity_1.8.5_amd64.deb
dpkg -i parity_1.8.5_amd64.deb

parity --no-warp --geth
//systemltc stop parity.service
```

Edit file: https://trello.com/c/6XyaDuke/1376-api-%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89-%E3%81%A9%E3%81%93%E3%81%8B%E3%81%AB%E6%9B%B8%E3%81%8F-21790






### Skype
```js
ansible-playbook -i /vagrant/ansible/inventories/local/hosts admin.yml -c local
ansible-playbook -i /vagrant/ansible/inventories/local/hosts mysql.yml -c local
ansible-playbook -i /vagrant/ansible/inventories/local/hosts mysql.yml -c local --extra-vars="mysql_create_db=true"
ansible-playbook -i /vagrant/ansible/inventories/local/hosts batch.yml -c local
ansible-playbook -i /vagrant/ansible/inventories/local/hosts batch.yml -c local --tags deploy_batch
ansible-playbook -i /vagrant/ansible/inventories/local/hosts api.yml -c local 
ansible-playbook -i /vagrant/ansible/inventories/local/hosts web.yml -c local
ansible-galaxy install --force -r ./requirements.txt --roles-path ./roles
sudo ansible-galaxy install carlosbuenosvinos.ansistrano-deploy carlosbuenosvinos.ansistrano-rollback
https://trello.com/c/6XyaDuke/1376-api-%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89-%E3%81%A9%E3%81%93%E3%81%8B%E3%81%AB%E6%9B%B8%E3%81%8F-21790
curl --data '{"method":"personal_listAccounts","params":[],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
curl --data '{"method":"personal_newAccount","params":["hunter2"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
/home/parity/.parity/chain-spec.json
parity -lrpc=trace --gasprice 10000000000 --force-sealing --geth --config /home/parity/.parity/parity-node.toml


//maybe unused: ansible-playbook -i inventories/local/hosts parity_miner.yml -c local
```


{"jsonrpc":"2.0","result":[
    "0x00458ab1934c6aba4f8e0d1c1112bd8b4b0a91b4","0x00817043ca80ac8ea22797fdcb414c18a7860f7e",
    "0x8922b4b3bd458e64ffba5ab6e1632e853edb4938"
],"id":1}

```js
{
"name": "GMOPrivateChain",
"engine": {
"authorityRound": {
"params": {
"stepDuration": "1",
"validators" : { "list": [
"0x8a6259679397c5573f80c59ef54df292c772be76" ] },
"validateStepTransition": 1,
"immediateTransitions": true
}
}
},
"params": {
"gasLimitBoundDivisor": "0x400",
"maximumExtraDataSize": "0x20",
"minGasLimit": "0x1388",
"networkID" : "20581",
"eip140Transition": 1,
"eip211Transition": 1,
"eip214Transition": 1,
"eip658Transition": 1
},
"genesis": {
"seal": {
"authorityRound": {
"step": "0x0",
"signature": "0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
}
},
"difficulty": "0x20000",
"gasLimit": "0x5B8D80"
},
"accounts": {
"0x0000000000000000000000000000000000000001": { "balance": "1", "builtin": { "name": "ecrecover", "pricing": { "linear": { "base": 3000, "word": 0 } } } },
"0x0000000000000000000000000000000000000002": { "balance": "1", "builtin": { "name": "sha256", "pricing": { "linear": { "base": 60, "word": 12 } } } },
"0x0000000000000000000000000000000000000003": { "balance": "1", "builtin": { "name": "ripemd160", "pricing": { "linear": { "base": 600, "word": 120 } } } },
"0x0000000000000000000000000000000000000004": { "balance": "1", "builtin": { "name": "identity", "pricing": { "linear": { "base": 15, "word": 3 } } } },
"0x8a6259679397c5573f80c59ef54df292c772be76": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0xb91b65f373f94b38dc2f1f8ce2ce6b949d06abb7": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0xfac20328afc04d3e9538497bafa17ab000d669c2": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0xcf7e09a0b20fb7832b9b4cd90bae7958b70890dc": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0x432637221b8ae93ccda5ff2d48084b8f6e4db641": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0xd282bee78af8de182ba21ee745a90b848a218f82": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0x82e30630c4aa85d91945ae6f2f85a270d77d3726": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0x2e3ce7081d83c7cf25691d0d78b7ff18e02872a0": { "balance": "1606938044258990275541962092341162602522202993782792835301376" },
"0xb0a98cc27fcd65b26e771e6e6f64fdea92d1b6d0": { "balance": "1606938044258990275541962092341162602522202993782792835301376" }
}
}
```