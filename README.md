# ethbarcelona-xcm-workshop

## Pre-requisites:

### Obtain alphanet tokens via faucet
https://apps.moonbeam.network/moonbase-alpha/faucet/

### swap some alphanet tokens for relay tokens
https://moonbeam-swap.netlify.app/#/swap

### Add alphanet in metamask
- RPC: https://rpc.api.moonbase.moonbeam.network
- chainId: 1287

### Useful addresses to remember:
- xcDOT address: 0xFFFFFFFF1FCACBD218EDC0EBA20FC2308C778080
- Balances precompile address: 0x0000000000000000000000000000000000000802
- Xtokens precompile address: 0x0000000000000000000000000000000000000804

## Token transfers via XCM

## Checking & transfering your tokens through precompiles
We will use Remix for our interactions.
- Open Remix and add ERC20.sol and Xtokens.sol interfaces to the contracts and compile them.
- Inject web3 provider through metamask and load ERC20 at the xcDOT & Balances address

## Cross-transfering your tokens through precompiles
