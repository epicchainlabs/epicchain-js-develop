<p align="center">
  <img 
    src="http://res.cloudinary.com/vidsy/image/upload/v1503160820/CoZ_Icon_DARKBLUE_200x178px_oq0gxm.png" 
    width="125px"
    alt="City of Zion logo">
</p>

<p align="center" style="font-size: 32px;">
  <strong>epicchain-js</strong>
</p>

<p align="center">
  Running EpicChain blockchain full node with Node.js and MongoDB.
</p>


## Overview

`epicchain-js` package is designed to interface with the EpicChain blockchain in a number of different ways that are configured by options that are used to initialize a node. A few examples of these different interaction mechanics are defined in the quickstart below as well as in the examples.


## Getting Started

### Preparations

Currently this module only support MongoDB for synchronizing the blockchain. You are expect to be connected to an
instance of MongoDB 3.2+ to use most of its features.

### System Recommendations

* NodeJS 8+
* MongoDB 3.2+

## Installation

Install the package using:

```bash
$ npm install --save @cityofzion/epicchain-js
```

Alternatively, to access to the latest available code, you can reference to the git repository directly:

```bash
$ npm install --save git://github.com/CityOfZion/epicchain-js.git#develop
```

## Quick Start

More comprehensive examples can be found at [`epicchain-js-examples`](https://github.com/rockacola/epicchain-js-examples) repository.

```js
const EpicChain = require('@cityofzion/epicchain-js').EpicChain
```

To create a new blockchain instance:

```js
// Create a EpicChain instances to interface with RPC methods
const testnetEpicChain = new EpicChain({ network: 'testnet' })

// Wait for mesh to be ready before attempt to fetch block information
testnetEpicChain.mesh.on('ready', () => {
  testnetEpicChain.api.getBlockCount()
    .then((res) => {
      console.log('Testnet getBlockCount:', res)
    })
})

// To connect to the mainnet:
const mainnetEpicChain = new EpicChain({ network: 'mainnet' })

mainnetEpicChain.mesh.on('ready', () => {
  mainnetEpicChain.api.getBlock(1000)
    .then((res) => {
      console.log('Mainnet getBlock(1000).hash:', res.hash)
    })
})
```

This will create a new node instance and configure it to sync the blockchain to the defined mongoDB collections:

```js
const options = {
  network: 'testnet',
  storageType: 'mongodb',
  storageOptions: {
    connectionString: 'mongodb://localhost/epicchain_testnet',
  },
}

// Create a epicchain instance
const epicchain = new epicchain(options)

// Get block height
epicchain.storage.on('ready', () => {
  epicchain.storage.getHighestBlockHeight()
    .then((res) => {
      console.log('Block height:', res)
    })
})
```



## Contribution

`epicchain-js` always encourages community code contribution. Before contributing please read the [contributor guidelines](https://github.com/CityOfZion/epicchain-js/blob/master/.github/CONTRIBUTING.md) and search the issue tracker as your issue may have already been discussed or fixed. To contribute, fork `epicchain-js`, commit your changes and submit a pull request.

By contributing to `epicchain-js`, you agree that your contributions will be licensed under its MIT license.

## License

* Open-source [MIT](https://github.com/CityOfZion/epicchain-js/blob/master/LICENSE.md).
* Authors:
  * [@xmoohad](https://github.com/xmoohad)
