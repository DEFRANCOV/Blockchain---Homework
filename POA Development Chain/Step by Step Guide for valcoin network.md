# User Guide to Running valcoin Blockchain

Navigate to the the appropriate directory.   In this case, it is C:\Users\defra\OneDrive\Documents\BootcampHomework\Blockchain.


## Create the Nodes  
A blockchain must have at least two nodes.  In our case, to keep it simple we will create just two nodes.  

### Instructions  
Type in  `./geth --datadir Valnode1 account new`  
Password:  328  
An address was created.  We named it **Valnode1**.   
Public Address for Valnode1:  **0x0a48562CA99335C6376e7Eb2663E989d62188010**  
A new subdirectory "Valnode1" has been created.  
Just in case, the path of the secret file:   Valnode1\keystore\UTC--2021-02-17T17-22-41.163168500Z--0a48562ca99335c6376e7eb2663e989d62188010  

Type in  `./geth --datadir Valnode2 account new`  
Password:  328
An address was created.  We named it **Valnode2**.  
Public Address for Valnode2:  **0x9E7Fef70488D77637B87Bfa3473E19eaEb746b37**  
A new subdirectory "Valnode2" has been created.  
Just in case, the path of the secret file: Valnode2\keystore\UTC--2021-02-17T17-27-11.114332300Z--9e7fef70488d77637b87bfa3473e19eaeb746b37  


## Create the Genesis Block  
The first block of a blockchain is important.   It sets the configuration and parameters for the future blocks.   

### Instructions  
Type in  `./puppeth`  
As indicated previously, we named the network valcoin.  
Network name:   **valcoin**  
As we are creating a new genesis block, Hit option 2;  "Configure New Genesis"  
Hit option 1;  Create New genesis from scratch  
We are using Proof of Authority algorthim to validate blocks.  Hit option 2;  "Clique proof of authority"  
To keep things simple, we will use default 15 seconds for processing time.  
The two nodes created above, will be our sealer (or miner) blocks.  
To seal, paste the two addresses, one at a time, without the 0x.   After the 2nd paste, hit enter.  
To pre-fund, paste the two addresses, one at a time, without the 0x.   After the 2nd paste, hit enter.  
To keep things clean, type No to Prefunding with 1 wei question.   

For the remaining prompts:   
Chain Id:  328  
Hit option 2; Manage Existing Genesis.  
Hit option 2; Export genesis configurations.  
Hit enter to export files to current directory.  
For now, we don't need to worry about the error files.  The most important thing is we have valcoin.json.  
Hit Ctrl C to exit puppeth  


## Initialize the nodes with the genesis json file  
Type in `./geth --datadir Valnode1 init valcoin.json`  
Type in `./geth --datadir Valnode2 init valcoin.json`  

## We're ready to start mining   

### Instructions:  
Open up a 2nd git terminal  
Go back to terminal 1.  Confirm you are still in the appropriate directory.  
Type:  
`./geth --datadir Valnode1 --unlock "0x0a48562CA99335C6376e7Eb2663E989d62188010" --mine --rpc --allow-insecure-unlock`   
You will have to type in your password from above.  
Node 1 should be up and mining.  
There will be an enode generated.   **We need to copy this.**  
In our case it is.  
enode://e6c10137e6f60ba00adc79c7e0b8bdfd1e7af98b0b2b778c1eb3e21885e134262312d4ad07685b02a24dfcf5730858650c8c3bec7609c8aecd120bf733a2d08a@127.0.0.1:30303  

Go to terminal 2.   Type:  
`./geth --datadir Valnode2 --unlock "9E7Fef70488D77637B87Bfa3473E19eaEb746b37" --mine --port 30304 --bootnodes "enode://e6c10137e6f60ba00adc79c7e0b8bdfd1e7af98b0b2b778c1eb3e21885e134262312d4ad07685b02a24dfcf5730858650c8c3bec7609c8aecd120bf733a2d08a@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`  
Notice that the enode address we copied from terminal 1 is inserted in the terminal 2 command, after the word "bootnodes".  
  


## Send a transaction through MyCrypto app 
### Set Up a Custom Network  
Navigate to the Mycrypto app  
![Custom Network Setup for MyCryto](".\Setting_up_the_network.PNG")  
Nodename = valcoin  
Network = custom  
Network Name = valcoin  
Currency = ETH  
Chain Id = 328  as note above  
URL = http://127.0.0.1:8545  
Hit "Save and Use Custom Node"  

### Send a Transaction  
Hit "View and Send" option  
Hit "Keystore File"  
Hit "Select Wallet File"  
Navigate to the keystore directory inside your Valnnode1 directory, select the file located there, provide your password when prompted and then click `Unlock`.  
This will open your account wallet inside MyCrypto.  
In the "To Address" box, type the account address from Node2, then fill in an arbitrary amount of ETH:  
Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.  
Click the "Check TX Status" when the green message pops up, confirm the logout:  
You should see the transaction go from "Pending to "Successful" in around the same blocktime you set in the genesis.
Successful Transaction Sent:  


![Successful Transaction Screen Capture](".\transaction_status.PNG")  
That's it.
