# 5. Deployment

## Create Deployment Scripts

1. **Create A Bash Script**: Named `deploy.sh` outside of the token project directory. Head to your Leo folder and run:

```bash
nano deploy.sh
```

2. **Enter the Following Script**: Copy and paste the following content into the deploy.sh file:

```bash
PROGRAM_ID="<Your Token Project Name>"

snarkos developer deploy \
--private-key <PRIVATEKEY> \
--query https://api.explorer.aleo.org/v1 \
--priority-fee 0 \
"${PROGRAM_ID}.aleo" \
--path ./build/ \
--broadcast https://api.explorer.aleo.org/v1/testnet/transaction/broadcast
--network 1
```

3. **Save the Script**

```
To save the file, press Ctrl + X, then Y, and then Enter.
```

## **Request for Faucets**

Follow [this guide](https://www.leo.app/blog/aleo-faucet) from Leo Wallet to request test tokens.

**We highly recommend installing the** [**Leo Wallet**](https://www.leo.app/) **if you want to explore the Aleo ecosystem!**

## Deploy

Once you get your token for your account, Run the deploy script:

```bash
bash ./deploy.sh
```

Example output: 
```
PROGRAM_ID="jimmys_token"

snarkos developer deploy \
--private-key <PRIVATE KEY> \
--query https://api.explorer.aleo.org/v1 \
--priority-fee 0 \
"${PROGRAM_ID}.aleo" \
--path ./jimmys_token/build/ \
--broadcast https://api.explorer.aleo.org/v1/testnet3/transaction/broadcast
```

## **Test Mint and Transfer Functions On-Chain**

1. **Mint Token**:

```bash
snarkos developer execute \
--broadcast https://api.explorer.aleo.org/v1/testnet3/transaction/broadcast \
--private-key <PRIVATEKEY> \
--query https://api.explorer.aleo.org/v1 \
"${PROGRAM_ID}.aleo" mint 100u32
```

2. **Transfer Token**:

```bash
snarkos developer execute \
--broadcast https://api.explorer.aleo.org/v1/testnet3/transaction/broadcast \
--private-key APrivateKey1zkpDZLpPdRhc2xNgyhbgPB7LY2KCfk1Yakn1RVwtaAEQAqe \
--query https://api.explorer.aleo.org/v1 \
"${PROGRAM_ID}.aleo" transfer <recipient_address> 20u32 <token_record>
```
