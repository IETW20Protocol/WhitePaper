## prefix
data:application/json,

## Example

### Deploy
data:application/json,{"p":"ietw-20","op":"deploy","tick":"etwi","max":"21000000","lim":"100","wlim":"10000","dec":"8","nonce":"1"}

### Mint
data:application/json,{"p":"ietw-20","op":"mint","tick":"etwi","amt":"100","nonce":"2"}

### Transfer
data:application/json,{"p": "ietw-20","op": "transfer","tick": "etwi","nonce": "45","to": [{"recv": "0x7BBAF8B409145Ea9454Af3D76c6912b9Fb99b2A9","amt": "10000"}]}

### Proxy transfer

data:application/json,{"p":"ietw-20","op":"proxy_transfer","proxy":[{"tick":"etwi","nonce":"20","from":"0x4aD4eEf4EC98c41bdfD77E267abF683Da3036a61","to":"0x4aD4eEf4EC98c41bdfD77E267abF683Da3036a61","amt":"333","value":"0.001","sign":"0x000"}]}

### Freeze sell

data:application/json,{"p":"ietw-20","op":"freeze_sell","freeze":[{"tick":"etwi","nonce":"1690469437811","platform":"0xBdaA491B50aE3653Ba3d653724497F9f756f469E","seller":"0x4aD4eEf4EC98c41bdfD77E267abF683Da3036a61","amt":"333","value":"0.001","gasPrice":"33988168450","sign":"0x00"}]}

## Detailed examples

``` js

// data:application/json,
// +

// deploy; send 0eth from self to 0x0000000000000000000000000000000000000000;
{
    "p":"ietw-20", //protocol name: ietw20 | terc-20
    "op":"deploy", //operation: deploy/mint/transfer/freeze_sell/proxy_transfer
    "tick":"etwi", //token tick, can't be repeatable, case insensitive.
    "max":"21000000", //max supply
    "lim":"100", //limit for each mint
    "wlim":"10000", //limit for each address can maximum mint, address balance < deploy.wlim (Before mint, please do not receive transfers from others, transfers are also counted as balance)
    "dec":"8", //decimal for minimum divie
    "nonce":"1", //increasing interger, suggest using address original nonce
}

// mint; send 0eth from self to 0x0000000000000000000000000000000000000000;
// The initiator of the transaction is the receiver
{
    "p":"ietw-20",
    "op":"mint", //mint operation
    "tick":"etwi",
    "amt":"100", //mint amount
    "nonce":"2"
}

// transfer; send 0eth from self to 0x0000000000000000000000000000000000000000
{
  "p": "ietw-20",
  "op": "transfer", //transfer operation
  "tick": "etwi",
  "nonce": "3",
  "to": [ //batch transfer, the sum of amt must equal the previous amt param
    {
      "recv": "0xBdaA491B50aE3653Ba3d653724497F9f756f469E", //receiver address
      "amt": "50" //receiver amount
    },
    {
      "recv": "0x0000000000085d4780B73119b644AE5ecd22b376",
      "amt": "50"
    }
  ]
}
// proxy transfer; send 0eth from self to 0x0000000000000000000000000000000000000000 or 0xBdaA491B50aE3653Ba3d653724497F9f756f469E or platform address
{
  "p": "ietw-20",
  "op": "proxy_transfer", //transfer operation
  "proxy": [
    {
      "tick": "etwi", // tick
      "nonce": (+new Date()).toString(), // nonce
      "from": sellerAddress, // seller address, verify
      "to": "0x4aD4eEf4EC98c41bdfD77E267abF683Da3036a61", // buyer address (test)
      "amt": "333",
      "value": "0.001",
      "sign": sign // the agent must carry the signature to the chain, which can be confirmed
    }
  ]
}

// The buyer is buying and the seller's token is frozen;  send x eth from self to 0x0000000000000000000000000000000000000000 or 0xBdaA491B50aE3653Ba3d653724497F9f756f469E or platform address
{
  "p": "ietw-20",
  "op": "freeze_sell",
  "freeze": [
    {
      "tick": "etwi", // Seller Signature Information
      "nonce": (+new Date()).toString(), // Seller Signature Information
      "platform": "0xBdaA491B50aE3653Ba3d653724497F9f756f469E", // Seller signature information: corresponding platform
      "seller": "0x4aD4eEf4EC98c41bdfD77E267abF683Da3036a61", // Freeze the corresponding seller
      "amt": "333", // Seller Signature Information
      "value": "0.001", // Seller Signature Information
      "gasPrice": "33988168450", // gasPrice
      "sign": sign // The seller authorizes the signature to verify the use
    }
  ]
}

// cancel approve; send 0eth from self to 0x0000000000000000000000000000000000000000
{
  "p": "ietw-20",
  "op": "cancel_approve",
  "sign": [
    {
        "message": "",
        "sign": "0xsign"
    }
  ]
}
```

## index

* Mint is invalid in the same block

### proxy_transfer

Signature Approval Example

``` ts
const message = JSON.stringify({
  title: 'ietw-20 one approve', // one approve
  to: '0xBdaA491B50aE3653Ba3d653724497F9f756f469E', // platform address
  tick: 'etwi', // token
  amt: "333", // token amt
  value: "0.01", // eth value
  nonce: (+new Date()).toString(),
}, null, 4)
```