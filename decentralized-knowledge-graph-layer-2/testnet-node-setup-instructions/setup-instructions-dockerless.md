# Setup instructions (Dockerless)

{% hint style="info" %}
These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements as well as a more automated process of setting up the DKGv6 node in the future.
{% endhint %}

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community!
{% endhint %}

{% hint style="warning" %}
**IMPORTANT: These instructions are not intended for migrating your current v5 node to v6. Attempting this will most likely break your v5 node at this point. You should only use these instructions in order to setup a fresh OriginTrail v6 testnet node.**
{% endhint %}

### Prerequisites <a href="#docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b" id="docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b"></a>

* A dedicated **4GB RAM/2CPUs/50GB HDD** **Ubuntu** server (minimum hardware requirements)

### Installation

### Step 1 - Create your wallets

You will need 4 wallets total.

**2 EVM wallets**
•	1 operational wallet (private key input required)
•	1 management wallet

An example of an EVM wallet is using Metamask, which is highly recommended for this process.
Make sure to add the OriginTrail Parachain Network RPC to your metamask, by adding it following the details here: https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/origintrail-parachain-network-rpc

**2 Substrate wallets**
•	1 operational wallet
•	1 management wallet

For each of the substrate wallets, have a copy of the substrate address (sometimes you need to change the address view from Polkadot relay to substrate) and the OriginTrail Parachain Devnet address. Find the substrate address is your chosen polkadot wallet.

You can find the OriginTrail Parachain Devnet address here: https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Flofar.origin-trail.network#/accounts

Make sure to have your password saved so you can enter it later in the mapping step. You will also need to have your operational wallet private key handy.

#### Step 2 - Fund your wallets

Fund your Substrate and Ethereum wallets with OTP and TRAC test tokens. Instructions are available at [fund-your-v6-testnet-node.md](fund-your-v6-testnet-node.md "mention") page.

{% hint style="info" %}
Make sure to fund both your operational and management wallets. You need test OTP in both your management wallet and your operational wallet, and then some test Trac in your operational wallet.
{% endhint %}

The address you must use for the substrate wallet command must be the OriginTrail Parachain Devnet address, which typically starts with a g.
The discord bot will only allow you to fund one substrate wallet address (starting with ‘g’ as above) and one Ethereum wallet address. Therefore you will need to split the OTP funds after receiving them, to make sure both your operational wallet and management wallet have Test OTP. Using your given wallets which have just been topped up with Test Trac and Test OTP, send a portion of the test OTP to the other wallets so that both your management wallet and your operational wallet have funds.

If you see MOTP in metamask when you change to the OriginTrail Parachain Network RPC, or you see the test OTP on the debnet as linked above, you are good to go. Remmeber OTP must be on your management wallet and your operational wallet.

#### Step 3 - Create a mapping for both operational and management wallets

Create a mapping between your Substrate and Ethereum wallets (that are pre-funded in the previous step), this can be performed through [this interface](https://parachain.origintrail.io/parachain-account-mapping).&#x20;

{% hint style="info" %}
The mapping needs to be performed for both for the node operational and management wallets.
{% endhint %}

So map your operational substrate wallet (starting with a 5) to your operational metamask wallet. Then map your management substrate wallet (starting with a 5) to your management metamask wallet.

#### Step 4 - Login to your node server

Login to the server as root. You **cannot** use sudo and run this script. The command "**npm ci**" might fail.

#### Step 5 - Run the installer

**Download the installer script:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/testnet/installer/installer.sh --output installer.sh
```

**Update permissions for the installer script:**

```
chmod +x installer.sh
```

**Run the installer script:**

```
./installer.sh
```

The installer script will guide you through the installation.

When asked for a SQL password, use _admin_ as the password.

{% hint style="success" %}
**Congratulations. Welcome to v6 beta**
{% endhint %}

**Checking node logs:**

```
journalctl -u otnode --output cat -fn 100
```

![Successfully started](<../../.gitbook/assets/Screenshot 2021-12-27 at 15.49.28.png>)

**OriginTrail node commands:**

**Start node:** otnode-start&#x20;

Note: to verify your node is running, run `otnode-logs` command

**Stop node:** otnode-stop&#x20;

**Restart node:** otnode-restart&#x20;

**Show node logs:** otnode-logs&#x20;

**Open node configuration:** otnode-config

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).
