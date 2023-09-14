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

_Note: if you are using MacOS, `make install` may not work_, use `make go-install` instead

```bash
git clone https://github.com/celestiaorg/celestia-node.git

cd celestia-node && git checkout tags/v0.11.0-rc13

make build && make install

celestia version
```

Initialise the light node and copy its account address from the output

```bash
celestia light init --p2p.network arabica
```

Fund the account via the [faucet](https://faucet.celestia-arabica-10.com).

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
cd polaris && git checkout rollkit_v0.11.0-rc13-celestia-node
```

Start Polaris

```bash
cd $HOME/polaris && foundryup

mage start
```
