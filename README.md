# Hääl
# Anonymous Electronic Voting System on Public Blockchains 

Hääl means voice in Estonian. Voice means power of people.

This code is a proof-of-concept of the protocol presented on the whitepaper located at the root folder.
It describes a full process for an e-voting system, using public blockchains and without a mixnet or an oracle for tallying the votes.

The full protocol makes use of:
- Zero-knowledge proofs (with zk-snarks verified on-chain)
- Homomorphic encryption (Paillier protocol + zk)
- Stealth addresses (as proposed by Peter Todd, but ported to ethereum)
- Encrypted notes (e.g Zcash, AZTEC)
- Cryptography challenges (based on Sigma protocol)
- Digital signatures
- Ethereum (or another blockchain capable of running dApps)
- other technologies described on the whitepaper

Working in progress.
All contributions are welcome.

## Pre-requisites
- ganache-cli ^6.3.0 or Ganache ^1.2.2
- Node 8
- Solidity ^0.4.5
- Yarn ^1.13.0

## Setup
```
# yarn install && yarn truffle build && yarn ganache-cli
```

## Run
```
(on a new terminal)
# yarn truffle test
```

---
## Manual step-by-step setup for debugging purpose
Install node and downgrade to correct version:
```
apt-get install node npm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash 
nvm install 8
nvm use 8
```

Download third-party binary dependencies:
```
curl -o /usr/bin/solc -fL https://github.com/ethereum/solidity/releases/download/v0.4.25/solc-static-linux
chmod u+x /usr/bin/solc

Download: https://github.com/trufflesuite/ganache/releases/download/v1.2.2/ganache-1.2.2-x86_64.AppImage
chmod +x ganache-1.2.2-x86_64.AppImage
```

Build, config and run:
```
npm install -Wno-cast-function-type 2> debug.log
node ./node_modules/truffle/build/cli.bundled.js build
```

Edit `truffle.js` and change port to 7545 if you are using `ganache-1.2.2-x86_64.AppImage` instead `ganache-cli`.

```
node ./node_modules/truffle/build/cli.bundled.js test
```


### Compile warnings

Is expected to receive the warning below during contracts compilation:
```
haal/contracts/HAAL/haal.sol:2:1: Warning: Experimental features are turned on. Do not use experimental features on live deployments.
pragma experimental ABIEncoderV2;
^-------------------------------^
```

That message appears because we're using an experimental method to fill arrays (`bytes[]`):
```
function addVote(
        bytes[] _president, 
        bytes[] _senator, 
        bytes[] _stateGovernor,
        ^-----^
[...]

function getVotes(uint _index) view public returns(bytes[], bytes[], bytes[])
                                                   ^-----------------------^
```

Apache [License!](https://www.apache.org/licenses/LICENSE-2.0)
