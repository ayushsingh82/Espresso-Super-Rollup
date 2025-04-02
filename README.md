# Arbitrum Nitro Rollup Contracts

This is the package with the smart contract code that powers Arbitrum Nitro and Espresso integration.
It includes the rollup and fraud proof smart contracts, as well as interfaces for interacting with precompiles.

## Deploy contracts to Sepolia

For the deployed addresses of these contracts for Arbitrum chains see [https://docs.arbitrum.io/for-devs/dev-tools-and-resources/chain-info#core-contracts](https://docs.arbitrum.io/for-devs/dev-tools-and-resources/chain-info#core-contracts)

### 1. Compile contracts

Compile these contracts locally by running

```bash
git clone https://github.com/offchainlabs/nitro-contracts
cd nitro-contracts
yarn install
yarn build
yarn build:forge
```

### 2. Setup environment variables and config files

Copy `.env.sample.goerli` to `.env` and fill in the values. Add an [Etherscan api key](https://docs.etherscan.io/getting-started/viewing-api-usage-statistics), [Infura api key](https://docs.infura.io/dashboard/create-api) and a private key which has some funds on sepolia.
This private key will be used to deploy the rollup. We have already deployed a `ROLLUP_CREATOR_ADDRESS` which has all the associated espresso contracts initialized.

If you want to deploy your own rollup creator, you can leave the `ROLLUP_CREATOR_ADDRESS` empty and follow the steps on step 3.

If you want to use the already deployed `RollupCreator`, you can update the `ROLLUP_CREATOR_ADDRESS` with the address of the deployed rollup creator [here](espresso-deployments/sepolia.json) and follow the steps on step 4 to create the rollup.

### 3. Deploy Rollup Creator and initialize the espresso contracts

Run the following command to deploy the rollup creator and initialize the espresso contracts.

`npx hardhat run scripts/deployment.ts --network sepolia`

This will deploy the rollup creator and initialize the espresso contracts.

### 4. Create the rollup

Change the `config.ts.example` to `config.ts` and update the config specific to your rollup. Then run the following command to create the rollup if you haven't already done so.

`npx hardhat run scripts/createEthRollup.ts --network sepolia`

## Deployed contract addresses

Deployed contract addresses can be found in the [espress-deployments folder](./espresso-deployments/).

## License

Nitro is currently licensed under a [Business Source License](./LICENSE.md), similar to our friends at Uniswap and Aave, with an "Additional Use Grant" to ensure that everyone can have full comfort using and running nodes on all public Arbitrum chains.

The Additional Use Grant also permits the deployment of the Nitro software, in a permissionless fashion and without cost, as a new blockchain provided that the chain settles to either Arbitrum One or Arbitrum Nova.

For those that prefer to deploy the Nitro software either directly on Ethereum (i.e. an L2) or have it settle to another Layer-2 on top of Ethereum, the [Arbitrum Expansion Program (the "AEP")](https://docs.arbitrum.foundation/aep/ArbitrumExpansionProgramTerms.pdf) was recently established. The AEP allows for the permissionless deployment in the aforementioned fashion provided that 10% of net revenue is contributed back to the Arbitrum community in accordance with the requirements of the AEP.


# Layer 2 Optimization Contracts

This collection of smart contracts implements various Layer 2 specific optimizations for the Espresso rollup, focusing on data compression, calldata optimization, and custom precompiles.

## Overview

The system consists of four main contracts that work together to optimize L2 operations:

1. DataCompression.sol
2. CalldataOptimizer.sol
3. CustomPrecompiles.sol
4. L2OptimizationRegistry.sol




## Contract Details

### DataCompression.sol

Handles efficient data compression for L2 transactions to reduce calldata costs.

Key features:
- RLP encoding for data compression
- Automatic threshold detection for compression
- Lossless decompression capabilities


### CalldataOptimizer.sol

Optimizes transaction calldata by batching and restructuring calls.

Key features:
- Transaction batching
- Similar call grouping
- Parameter optimization
- Configurable batch sizes


### CustomPrecompiles.sol

Implements commonly used operations as precompiles for gas optimization.

Key features:
- Batch string operations
- Optimized cryptographic functions
- Efficient mathematical computations


### L2OptimizationRegistry.sol

Main registry contract that coordinates all optimization features.

Key features:
- Central management of optimization contracts
- Automated optimization pipeline
- Transaction parsing and routing


## Gas Optimization Benefits

- Reduced calldata costs through compression
- Efficient batch processing
- Optimized precompiles for common operations
- Reduced storage operations

## Security Considerations

- All compression is lossless to maintain data integrity
- Batch size limits prevent DOS attacks
- Pure functions used where possible to prevent state changes
- Input validation on all public functions

## Development

### Prerequisites
- Solidity ^0.8.0
- Hardhat or Truffle development environment




## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

MIT

## Future Improvements

1. **Data Compression**
   - Implement additional compression algorithms
   - Add dynamic compression ratio selection
   - Optimize for specific data types

2. **Calldata Optimization**
   - Add more sophisticated batching strategies
   - Implement cross-transaction optimization
   - Add priority-based execution

3. **Custom Precompiles**
   - Add more commonly used operations
   - Implement specialized L2 operations
   - Optimize for specific use cases

## Contact

For questions and support, please open an issue in the repository.
