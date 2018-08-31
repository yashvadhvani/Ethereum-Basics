# BlockChain

## What is Geth
Geth is a multipurpose command line tool that runs a full Ethereum node implemented in Go. We won't go in much detail as there are articles for the same.

## Installation of geth
Please follow the official documentation for the same the link is given [here](https://github.com/ethereum/go-ethereum/wiki/Installing-Geth).

Without wasting anyone's time let's come to the point. Here are the steps to follow to learn some ethereum basics [web3](https://web3js.readthedocs.io/en/1.0/web3-eth.html).

## Geth Importan Stuff

### Step 1 : Create a Gensis File

* Genesis is a JSON file indicates 0th block of an Etherum Blockchain.

* Basically contains the Configuration of a Block.

* Example of a Genesis File is Given Below.

### Example

```JSON
{
    "config": {
        "chainId": 15, 
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "20",
    "gasLimit": "2100000",
    "alloc": {

    }
}
```

---

## Genesis Contents


### Configuration

#### chainId

* Protection of the replay attack(an unauthorized user acting as the original sender)

* For example, if an action is validated by matching certain value that depends on the chain id, attackers cannot easily get the same value with a different id. (A video about replay attack: (https://www.youtube.com/watch?v=ZeuWpL-7EwY)

#### homesteadBlock

* Homestead is the second major release of Ethereum(the first release is Frontier). The value 0 means that you are using this release.

#### epi155Block

* epi stands for Ethereum Improvement Proposal, where developers propose ideas on how to improve Ethereum and contribute to this project.

### Difficulty

* mining difficulty // set this value low so you don’t have to wait too long for mining blocks.

### gasLimit

* the limit of gas cost per block // set this value high to avoid being limited when testing.

### alloc

* pre-funded address, the first parameter of each is the address . Need to be a 40 digits hex string(160 bit, one hex digit is 4 bit). Note that this does not create an account

### Step 2 : Initialize the BlockChain

``` go
geth init --datadir "<path-to-json>" filename.json
```

* Here, Datadir refers to the location of the Genesis File.
* Filename is the filename of the genesis file.

### Step 3 : Start the Chain Console

``` go
geth --datadir ./myDataDir --networkid 1114 --port 900 console
```

### Step 4 : Create Account for Transactions

``` js
personal.newAccount()
```

### Step 5: Start Mining in new terminal 

* Attach a new Console

``` go
geth attach  "<ipc-file-path>"
```

* Start Mining

``` go
> miner.start([<No_of_Threads>])
```

### Step 6: Perform Transactions

``` js
> personal.sendTransaction({from:'addr1',to:'addr2',value:'1'})
```

### Step 7: Stop Mining

``` js
> miner.stop()
```

---

## Connecting Private Blockchain With Remix

* Start Your private bloackchain with rpc

``` go
geth --datadir "." --port 30304 --networkid 123 --rpc --rpcport "8545" --rpccorsdomain "*" console 2>console.log

```

* Write Your Smart Contract
* In Run tab select **Web3 Provider** as **Environment**
  * Are you sure you want to connect to an ethereum node? press OK
  * Provide **Web3 Provider Endpoint**. Generelly it's **http://localhost:8545**

* You Will able to see Your Accounts Under Accounts Dropdown.
* Run Your Smart Contract.

---

## Performing with **meteor.js**

### Steps

* **Install curl**

``` linux
sudo apt-get install curl
```

* **Install  meteor**

``` linux
curl https://install.meteor.com/ | sh
```

* **Create a meteor project by command.**
  
  * It will create bunch of files and folders the server folder will contain the server side code.
  * The client folder will contain the client side code.
  * If You create another folder in the current project then the code inside it will be executed both sides.
  * The package.json file contains the packages or dependencies which we will need in the meteor project.


``` linux
meteor create "<project_name>"
```

  
* Add Web3 Library in meteor project

``` linux
meteor npm install --save web3@0.20.0
```

* Start Your private bloackchain with rpc

``` go
geth --datadir "." --port 30304 --networkid 123 --rpc --rpcport "8545" --rpccorsdomain "*" console 2>console.log

```

* Start Coding.

## Example for getting Account Information

**Filename:** server > main.js

``` js
//Importing Web3 and storing it in Variable
var Web3 = require('web3');
//providing the Blockchain Address and Port
web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
//Running Geth Command using Web3 module 
console.log(web3.eth.accounts);
```
