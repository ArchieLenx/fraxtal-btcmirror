
# Setting Up the Submitter
This guide will walk you through the process of setting up the submitter. Please follow the steps carefully.  
## Prerequisites
Ensure that you have Node.js and npm installed on your system. If not, you can download and install them from the official Node.js website.  
## Step 1: Install Dependencies
Navigate to the project directory and run the following command to install the necessary dependencies:

```shell
npm install
```

## Step 2: Configure Secrets on Cloudflare
You need to place your secrets on Cloudflare. These secrets include the Ethereum Submitter Private Key and the GetBlock
API Key. You can add these secrets by navigating to the secrets section in your Cloudflare dashboard.
Fill out the testnet-keys-example.json file with your specific information and 
then rename it to testnet-keys.json. The file should look like this:

```json
{
  "BTCMIRROR_CONTRACT_ADDR": "DEPLOYED_ADDRESS_HERE",
  "ETH_RPC_URL": "YOUR_NETWORK_RPC_HERE",
  "ETH_SUBMITTER_PRIVATE_KEY": "YOUR_PRIVATE_KEY_HERE",
  "GETBLOCK_API_KEY": "GET_BLOCK_API_KEY_HERE",
  "BITCOIN_NETWORK": "testnet", // testnet or mainnet
  "MAX_BLOCKS_PER_BATCH": "10" // number of blocks to process in a batch, 10 is good ish
}
```

### Step 2a: Running 1 secret prior to JSON bulk

You may have to run 1 secret on its own using wrangler secret

```shell
echo <val> | wrangler secret put <key> --env=mainnet
```
### Step 2b: Practical Example using Fraxtal Testnet Deployment

```shell
echo 0x53A633b21FC69Ff6D5aadECc56B80871C4507229 | npx wrangler secret put BTCMIRROR_CONTRACT_ADDR --env=testnet
```

## Step 3: Bulk Secret Command

Run the following command to bulk upload the secrets from the testnet-keys.json file:

```shell
npx wrangler secret:bulk testnet-keys.json --env=testnet

```

## Step 4: Update wrangler.toml
Next, update the wrangler.toml file with the BtcMirror contract address and RPC URL. After updating, you can publish the testnet deployment using the following command:

```shell
npx wrangler publish --env=testnet
```

Step 5: Mainnet Deployment
For mainnet deployment, you need to repeat the above steps using the mainnet keys. 
Make sure to replace the --env=testnet flag with --env=mainnet where necessary.  That's it! You have successfully set up the submitter. If you encounter any issues, please feel free to open a ticket!

