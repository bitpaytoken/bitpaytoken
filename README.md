# BitPayToken

BitPayToken is an initiative for start accepting digital assets as payment method. It's built upon ethereum platfom and performs transaction within seconds. Smart contract strictly following ERC20 standard for wallet integration and community. 

## Getting Started

### Prerequisites

1. Geth
2. Solidity compiler

### Installing

Install all Prerequisites with these commands (Tested on ubuntu 16.04LTS linux system)

```
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install -y ethereum
sudo apt-get install -y solc
```

Now, To compile this contract we will put it in a json format and assign a JavaScript variable, then we send it to an output file.

```
echo "var storageOutput=`solc --optimize --combined-json abi,bin,interface bitpaytoken.sol`" > bitpaytoken.js
```

Now, start geth with following

```
geth console
```

you will be get a javascript console

```
>
```

Now, in geth console

```
>loadScript('bitpaytoken.js')
true
>storageOutput
/*Will return json object*/
```

The object keys identify the contract name, the abi in json, the bin code and lastly the solidity compile version.

Now, lets assing some variable 

```
>var storageContractAbi = storageOutput.contracts['Storage.sol:Storage'].abi
/*Will return json object array*/

>var storageContract = eth.contract(JSON.parse(storageContractAbi))
undefined

>var storageBinCode = "0x" + storageOutput.contracts['Storage.sol:Storage'].bin
/*Will return hexa string*/
```

Now, unlock a personal account whatever you want to deploy with

```
>personal.unlockAccount(eth.accounts[0])
```

Now, create transaction object

```
>var deployTransationObject = { from: eth.accounts[0], data: storageBinCode, gas: 1000000 };
undefined

>var storageInstance = storageContract.new(deployTransationObject)
```

Now, deploy the contract for mining

```
>eth.getTransactionReceipt(storageInstance.transactionHash);
```

Now, get the contract address

```
>var storageAddress = eth.getTransactionReceipt(storageInstance.transactionHash).contractAddress
undefined

>storageAddress
/*Will return contract address*/
```

## Built With

* [Ethereum](https://github.com/ethereum) - Ethereum Vrtual Machine

## Acknowledgments

* Got some great example from medium
