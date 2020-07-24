# Secret Raffle

## Description
This is a simple raffle game. The 'Raffle Host' will deploy an instance of this contract. 

Anyone can join the raffle, by submitting a transaction from their account. Each account can enter only once.

When the raffle host decides to end the raffle, a winner will be chosen at random from all the accounts that registered

## Disclaimer
This is only a usage example, and does not imply on how to correctly and safely use or write `Secret Contracts`. You should always make sure to read and understand `Secret Contract` API's disclaimers and limitations before deploying a contract in production!

## Usage

### As a participant 

#### Join the raffle

To join, you simply submit a `join` transaction, and choose a lucky phrase or number (and keep it secret!). This will be used as entropy for the required randomness.

```bash
secretcli tx compute execute <contract-address> '{ "join": { "phrase": "<write something fun here>" }}' --from account
```

`phrase` is expected to be a string, so choose whatever you want as long as you don't forget to surround it by double quotes
For example:
* right: `"5"` 
* wrong: `5`

### As a raffle host

### Store the contract on-chain
```bash
secretcli tx compute store contract.wasm.gz --from account --gas auto
```

#### Instantiate contract
```bash
secretcli tx compute instantiate <code_id> '{"seed": "<some long secret here>"}' --label <label> --from account
```

#### End raffle - will select a winner
```bash
secretcli tx compute execute <contract-address> '{ "end_lottery": {} }' --from account
```

For more details, check out the [messages module](https://github.com/toml01/SecretLottery/blob/master/src/msg.rs).
