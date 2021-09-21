# **Proof of Authority Development Chain**
---
![Blockchain](network.jpeg)

---
## **Background**
You have just landed a new job at ZBank, a small, innovative bank that is interested in exploring what
blockchain technology can do for them and their customers. </br>
Your first project at the company is to set up a private testnet that you and your team of developers
can use to explore potentials for blockchain at ZBank

___
## **Objective**
To set up a testnet based on Proof of Authority consensus algorithm to allow to experient with blockchain

---
## **Tools**
* [MyCrypto](https://www.mycrypto.com/)
* [Go Ethereum](https://geth.ethereum.org/)


---
## **Steps**  

1. The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks)Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

    * Create accounts for two nodes for the network with a separate `datadir` for each using `geth`.
        * ./geth --datadir node1 account new
        * ./geth --datadir node2 account new

2. Next, generate your genesis block.

    * Run `puppeth`, name your network, and select the option to configure a new genesis block.

    * Choose the `Clique (Proof of Authority)` consensus algorithm.

    * Paste both account addresses from the first step one at a time into the list of accounts to seal.

    * Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

    * You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

    * Come up with a number to use as a chain ID (e.g. 333) type it, then hit enter.

    * when you are back at the main menu, choose the "Manage existing genesis" option.

    * Export genesis configurations. This will fail to create two of the files, but you only need `networkname.json`.

3. With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

    * Using `geth`, initialize each node with the new `networkname.json`.
        * ./geth --datadir node1 init networkname.json
        * ./geth --datadir node2 init networkname.json

4. Now the nodes can be used to begin mining blocks.

    * Run the nodes in separate terminal windows with the commands:
        *  ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
        *  ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
    * **NOTE:** Type your password and hit enter - even if you can't see it visually!

5. Your private PoA blockchain should now be running!

6. With both nodes up and running, the blockchain can be added to MyCrypto for testing.

    * Open the MyCrypto app, then click `Change Network` at the bottom left:

    * Click "Add Custom Node", then add the custom network information that you set in the genesis.

    * Make sure that you scroll down to choose `Custom` in the "Network" column to reveal more options like `Chain ID`:

    * Type `ETH` in the Currency box.
    
    * In the Chain ID box, type the chain id you generated during genesis creation.

    * In the URL box type: `http://127.0.0.1:8545`.  This points to the default RPC port on your local machine.

    * Finally, click `Save & Use Custom Node`. 

7. After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

    * Select the `View & Send` option from the left menu pane, then click `Keystore file`.


    * On the next screen, click `Select Wallet File`, then navigate to the keystore directory inside your Node1 directory, select the file located there, provide your password when prompted and then click `Unlock`.

    * This will open your account wallet inside MyCrypto. 
    
    * Looks like we're filthy rich! This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for testing purposes.   


    * In the `To Address` box, type the account address from Node1, then fill in an arbitrary amount of ETH:


    * Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.  


    * Click the `Check TX Status` when the green message pops up, confirm the logout:


    * You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.

    * You can click the `Check TX Status` button to update the status

---
## **Output**
 The screenshots for the outputs are stored in the **Screenshots** folder

 1. Creation of Nodes
    ![Node creation](Screenshots/Node_creation.png)

    Node 1 Public Address : `0x232354F63f15fA3321f21BA005BD5df431d8bf84` 
    </br>
    Node 1 Password: 123

     Node 2 Public Address : `0xEF3F72Cc76E1Ff4A606A3D92C55027F26e1479e9` 
    </br>
    No Node 2 Password

  2. Generate Genisys Block
     ![Blockchain creation](Screenshots/Blockchain_creation.png)

     Test Network Name : blockchain 
  3. Export Genisys configuration
     ![Blockchain creation](Screenshots/Blockchain_export.png)
  4. Initialization of Nodes
     ![Node Initialization](Screenshots/Node1_init.png)

  5. Begin Mining 
     ![Node1 Mine](Screenshots/Node1_mine.png)

     ![Node2 Mine](Screenshots/Node1_mine.png)

     </br>

     Enode :`enode://27b66934993e60032fd7f9545f9bf470c4626bf30fc524230f1d493bf3705a78c472df86134f1b90b98df8f91fbd6033098ee4c1dd17a69adb3848319bbcd89b@127.0.0.1:30303` 

  6. MyCrypto Custom Network
     ![Custom network](Screenshots/Puppernet.png)
  7. Testing the network through transferring ETH
     ![Balance](Screenshots/mycrypto_bal.png)

     ![send](Screenshots/ETH_send.png)

     ![confirmation](Screenshots/Confirmation_transaction.png)

     ![status1](Screenshots/Transaction_status1.png)

     ![status2](Screenshots/Transaction_status2.png)
