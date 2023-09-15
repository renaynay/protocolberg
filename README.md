# ProtocolBerg Workshop
Berlin - 15 September 2023

## Prerequisites

### go
https://golang.org/doc/install

### foundry
```bash
curl -L https://foundry.paradigm.xyz | bash
```

### mage
https://magefile.org/

## Instructions

### Running a light node against `arabica-10` testnet

Clone the repo and build/install the binary

_Note: if you are using MacOS, `make install` may not work_

```bash
git clone https://github.com/celestiaorg/celestia-node.git

cd celestia-node

git checkout protocolberg

make build && make install

celestia version
```

Initialise the light node and copy its account address from the output

```bash
celestia light init --p2p.network arabica
```

Fund the account via:

https://discord.com/channels/638338779505229824/1018935905991536710

```bash
$request <account address>
```

Run the light node

```bash
celestia light start --p2p.network arabica --core.ip http://validator.consensus.celestia-arabica-10.com
```

Now let it sync (should take 1-2 minutes)

### Running Polaris x Rollkit against the light node

Clone Polaris

```bash
cd $HOME
git clone https://github.com/berachain/polaris.git
cd polaris && git checkout rollkit
```

Replace the entrypoint script (located at `e2e/testapp/entrypoint.sh`) with the one located in this repo: 

[here](https://raw.githubusercontent.com/renaynay/protocolberg/main/entrypoint.sh).

```bash
rm e2e/testapp/entrypoint.sh && curl https://raw.githubusercontent.com/renaynay/protocolberg/main/entrypoint.sh > e2e/testapp/entrypoint.sh
```

_(might have to change perms)_

Start Polaris

```bash
cd $HOME/polaris && foundryup

mage start
```

### Optional: Interact with contracts on Polaris x Rollkit

If time, follow the tutorial starting [here](https://rollkit.dev/pr-preview/pr-210/tutorials/polaris-evm#frontend) to interact with a smart contract running on top of the Polaris x Rollkit sequencer.
