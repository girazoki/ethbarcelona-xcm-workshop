# ethbarcelona-xcm-workshop

## PolkadotJS/apps explorers
- [Alphanet](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.api.moonbase.moonbeam.network#/explorer)
- [Relay](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Ffrag-moonbase-relay-rpc-ws.g.moonbase.moonbeam.network#/explorer)

## Pre-requisites:

### Obtain alphanet tokens via faucet
https://apps.moonbeam.network/moonbase-alpha/faucet/

### swap some alphanet tokens for relay tokens
https://moonbeam-swap.netlify.app/#/swap

### Add alphanet in metamask
- RPC: https://rpc.api.moonbase.moonbeam.network
- chainId: 1287

### Useful addresses to remember:
- xcUnit address: 0xFFFFFFFF1FCACBD218EDC0EBA20FC2308C778080
- Balances precompile address: 0x0000000000000000000000000000000000000802
- Xtokens precompile address: 0x0000000000000000000000000000000000000804

## Token transfers via XCM

## Checking & transfering your tokens through precompiles
We will use Remix for our interactions.
- Open Remix and add ERC20.sol and Xtokens.sol interfaces to the contracts and compile them.
- Inject web3 provider through metamask and load ERC20 at the xcUnit & Balances address
- Check your balance by clicking balanceOf
- Transfer to another account by clicking transfer
- Check your transaction in [moonscan](https://moonbase.moonscan.io/)

## Cross-transfering your tokens through precompiles
We will do two transfers:
- Transfer xcUnit to the relay
- Transfer DEV to another parachain

### Transfering xcUnit to the relay
We will be using the **transfer** function from the Xtokens precompile. This one asks for the following parameters:

    /** Transfer a token through XCM based on its currencyId
     *
     * @dev The token transfer burns/transfers the corresponding amount before sending
     * @param currency_address The ERC20 address of the currency we want to transfer
     * @param amount The amount of tokens we want to transfer
     * @param destination The Multilocation to which we want to send the tokens
     * @param weight The weight we want to buy in the destination chain
     * Selector: b9f813ff
     */
    function transfer(
        address currency_address,
        uint256 amount,
        Multilocation memory destination,
        uint64 weight
    ) external;

Lets say we want to send the tokens to a mutilocation that looks like this:

    MultiLocation {
        parents: 1
        interior: X1(AccountId32 {
            network: Any,
            account: 0x9c6af76cd6513e44e421ab8dc8f9d86e102200eb2e55cbc41a2d5ce214ee254
        })
    }
Here we will use the following parameters:
- **currency_address**: 0xFFFFFFFF1FCACBD218EDC0EBA20FC2308C778080 (since we are sending xcUnit)
- **amount**: 1000000000000 (1 xcUnit has 12 decimals)
- **destination**: [1, ["0x019c6af76cd6513e44e421ab8dc8f9d86e102200eb2e55cbc41a2d5ce214ee254f00"]]
- **weight**: 4000000000

### Transfering DEV to Acala DEV parachain
We will be using the **transfer** function from the Xtokens precompile. This one asks for the following parameters:

    /** Transfer a token through XCM based on its currencyId
     *
     * @dev The token transfer burns/transfers the corresponding amount before sending
     * @param currency_address The ERC20 address of the currency we want to transfer
     * @param amount The amount of tokens we want to transfer
     * @param destination The Multilocation to which we want to send the tokens
     * @param weight The weight we want to buy in the destination chain
     * Selector: b9f813ff
     */
    function transfer(
        address currency_address,
        uint256 amount,
        Multilocation memory destination,
        uint64 weight
    ) external;


This time the multilocation to which we want to send the tokens is:


    MultiLocation {
        parents: 1
        interior: X2[
            Parachain(acala_para_id),
            AccountId32 {
            network: Any,
            account: 0x9c6af76cd6513e44e421ab8dc8f9d86e102200eb2e55cbc41a2d5ce214ee254
        }]
    }

In alphanet, Acala has para_id 2000 and should be represented by 4 bytes, so 

    2000 -> 0x000007d0

Here we will use the following parameters:
- **currency_address**: 0x0000000000000000000000000000000000000802 (since we are sending DEV)
- **amount**: 1000000000000000000 (1 DEV has 18 decimals)
- **destination**: [1, ["0x00000007d0", "0x019c6af76cd6513e44e421ab8dc8f9d86e102200eb2e55cbc41a2d5ce214ee254f00"]]
- **weight**: 4000000000