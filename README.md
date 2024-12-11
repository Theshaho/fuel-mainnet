# fuel-mainnet

I don't know its late or not, but you can run Fuel mainnet node with this repo

## Hardware Requirements

| Hardware  | Minimum |
| ------------- | ------------- |
| Processor  | 2 Cores  |
| Memory  | 4 GB  |
| Storage  | 30 GB  |


## Installation

To install the Fuel toolchain, you can use the fuelup-init script. This will install forc, forc-client, forc-fmt, forc-lsp, forc-wallet as well as fuel-core in ~/.fuelup/bin.

```bash
curl https://install.fuel.network | sh
```
![Screenshot 2024-12-11 120726](https://github.com/user-attachments/assets/62188d62-e79b-4d2f-af6f-0c710a991f12)


press y

use below command to be sure that Fuel-up is installed correctly

```bash
 fuelup --version
```

```bash
fuelup toolchain install nightly
```

👉 Set nightly as your default toolchain with the following command:

```bash
fuelup default nightly 
```

## Getting a mainnet Ethereum API Key

signup for [Alchemy](https://www.alchemy.com/) and get a Eth mainnet endpoint

The endpoints should look like the following:

```bash
https://eth-mainnet.g.alchemy.com/v2/{YOUR_API_KEY}
```

## Generating a P2P Key

Generate a new P2P key pairing by running the following command:

```bash
fuel-core-keygen new --key-type peering
{
  "peer_id":"16Uiu2HAmEtVt2nZjzpXcAH7dkPcFDiL3z7haj6x78Tj659Ri8nrs",
  "secret":"b0ab3227974e06d236d265bd1077bb0522d38ead16c4326a5dff2f30edf88496",
  "type":"peering"
}
```

### Do not share or lose this private key! Press any key to complete. ###

Make sure you save this somewhere safe so you don't need to generate a new key pair in the future.

## Chain Configuration

clone this repo

```bash
git clone https://github.com/FuelLabs/chain-configuration.git
```

## Run the node

Finally to put everything together to start the node, run the following command:

first open a new screen

```bash
screen -S fuel-mainnet
```

then edit this command and run it in the screen. change {P2P_PRIVATE_KEY} and {ETHEREUM_RPC_ENDPOINT} to your secret and ETH mainnet rpc.

also be sure that 4000 and 30333 are useabl with this command:

```bash
lsof -i :4000
lsof -i :3000
```
if these ports are in use, change them with proper ports.

```bash
fuel-core run \
--enable-relayer \
--service-name fuel-mainnet-node \
--keypair {P2P_PRIVATE_KEY} \
--relayer {ETHEREUM_RPC_ENDPOINT} \
--ip=0.0.0.0 --port 4000 --peering-port 30333 \
--db-path ~/.fuel-mainnet \
--snapshot ./chain-configuration/ignition/ \
--utxo-validation --poa-instant false --enable-p2p \
--bootstrap-nodes /dnsaddr/mainnet.fuel.network \
--sync-header-batch-size 100 \
--relayer-v2-listening-contracts=0xAEB0c00D0125A8a788956ade4f4F12Ead9f65DDf \
--relayer-da-deploy-height=20620434 \
--relayer-log-page-size=100 \
--sync-block-stream-buffer-size 30
```

detach from screen with Ctl + A + D

## Join our Telegram Channel

For more bots and tutorials you can join our Telegram channel

[**UbuntuForNodes**](https://t.me/ubuntufornodes)

also you can follow me on [X(iamshaho)](https://x.com/iamshaho)
