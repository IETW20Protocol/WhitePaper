# IETW-20 Protocols

## Introduction
IETW-20 is an ethscription protocol based on the EthereumPoW (ETHW) blockchain that allows users to share information and perform computations. IETW-20 is an an alternative to smart contracts. 

## Introducing ETWI
ETWI is the first token deployed using the IETW-20 protocol. 

- Protocol name: ietw-20
- Token tick: etwi
- Maximum supply: 21000000
- Limit amount per mint: 100
- Maximum amount per address: 10000
- Decimal for minimum divide: 8

## Deploy

https://www.oklink.com/cn/ethw/tx/0x5f3c835a0a9d5e64a3f6a4ae7dd46e3aa31531312f23a0efe6489516fdbf49a3

`data:application/json,{"p":"ietw-20","op":"deploy","tick":"etwi","max":"21000000","lim":"100","wlim":"10000","dec":"8","nonce":"1"}`

## Mint

Send 0 ETHW from self to `0x0000000000000000000000000000000000000000`:

`data:application/json,{"p":"ietw-20","op":"mint","tick":"etwi","amt":"100","nonce":"x"}`

Nonce is an interger and can't be repeatable.

## See [IETW-20](protocol/IETW-20.md) for details
