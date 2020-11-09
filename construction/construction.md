# Construction Endpoints

These endpoints are used to WRITE data to the blockchain.

You will need a library to sign your payloads. For example, in TypeScript, something like bitcoinjs-lib.

To submit a transaction, you should follow the flow of operations. To read more about how a transaction is made, check out the Rosetta Docs

## Derive

*Derive an AccountIdentifier from a PublicKey*

`POST https://api.lunar.dev/v1/construction/derive`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "public_key": {
        "hex_bytes": btcKeys.publicKey.toString('hex'),
        "curve_type": "secp256k1"
    },
    "metadata": {}
}
```

Example Response
```json
{
    "address": "string",
    "account_identifier": {
        "address": "0x3a065000ab4183c6bf581dc1e55a605455fc6d61",
        "sub_account": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "metadata": {}
        },
        "metadata": {}
    },
    "metadata": {}
}
```


## Preprocess

*Create a Request to Fetch Metadata*

Preprocess is called prior to [Construction Payloads](construction/construction?id=payloads) to construct a request for any metadata that is needed for transaction construction given (i.e. account nonce). The options object returned from this endpoint will be sent to the [Construction Metadata](construction/construction?id=metadata) endpoint UNMODIFIED by the caller.

`POST https://api.lunar.dev/v1/construction/preprocess`

Example POST Request Body
*Note the accountBalance is used from the [Account Balance](data/account?id=account-balance) Data endpoint.
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "operations": [
        {
            operation_identifier: {
            index: 0
            },
            type: "INPUT",
            status: "",
            account: {
            address: senderAccount.address
            },
            amount: {
            value: `-${accountBalance.coins[0].amount.value}`,
            currency: {
                symbol: "tBTC",
                decimals: 8
            }
            },
            coin_change: {
            coin_action: "coin_spent",
            coin_identifier: accountBalance.coins[0].coin_identifier
            }
        },
        {
            operation_identifier: {
            index: 1
            },
            type: "OUTPUT",
            status: "",
            account: {
            address: recipientAddress
            },
            amount: {
            value: `2000`,
            currency: {
                symbol: "tBTC",
                decimals: 8
            }
            }
        },
        {
            operation_identifier: {
            index: 2
            },
            type: "OUTPUT",
            status: "",
            account: {
            address: senderAccount.address
            },
            amount: {
                value: `${+accountBalance.coins[0].amount.value - 2000 - 1200}`,
                currency: {
                    symbol: "tBTC",
                    decimals: 8
                }
            }
        }
    ],
    "suggested_fee_multiplier": 0.75,
    "max_fee_amount": 1200
}
```

Example Response

*Note this is passed untouched to the (Construction Metadata)[construction/construction?id=metadata] endpoint

```json
{
    "options": {},
    "required_public_keys": [
        {
            "address": "0x3a065000ab4183c6bf581dc1e55a605455fc6d61",
            "sub_account": {
                "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                "metadata": {}
            },
            "metadata": {}
        }
    ]
}
```


## Metadata

*Get Metadata for Transaction Construction*

`POST https://api.lunar.dev/v1/construction/metadata`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "options": preprocess.options // This is used untouched from the construction preprocess request
}
```

Example Response
```json
{
    "metadata": {
        "account_sequence": 23,
        "recent_block_hash": "0x52bc44d5378309ee2abf1539bf71de1b7d7be3b5"
    },
    "suggested_fee": [
        {
            "value": "1238089899992",
            "currency": {
                "symbol": "tBTC",
                "decimals": 8,
                "metadata": {
                    "Issuer": "Satoshi"
                }
            },
            "metadata": {}
        }
    ]
}
```


## Payloads

*Generate an Unsigned Transaction and Signing Payloads*

Payloads is called with an array of operations and the response from [Construction Metadata](construction/construction?id=metadata). It returns an unsigned transaction blob and a collection of payloads that must be signed by particular AccountIdentifiers using a certain SignatureType. 

`POST https://api.lunar.dev/v1/construction/payloads`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "operations": operations, // same operations array used in the construction preprocess request
    "metadata": metadata // metadata param from the construction metadata request (ie. metadataResponse.metadata)
}
```

Example Response
```json
{
    "unsigned_transaction": "string",
    "payloads": [
        {
            "address": "string",
            "account_identifier": {
                "address": "0x3a065000ab4183c6bf581dc1e55a605455fc6d61",
                "sub_account": {
                    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                    "metadata": {}
                },
                "metadata": {}
            },
            "hex_bytes": "string",
            "signature_type": "ecdsa"
        }
    ]
}
```


## Parse

*Parse a Transaction*

Parse is called on both unsigned and signed transactions to understand the intent of the formulated transaction. This is run as a sanity check before signing (after [Payloads](construction/construction?id=payloads)) and before broadcast (after [Combine](construction/construction?id=combine)).

`POST https://api.lunar.dev/v1/construction/parse`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "signed": false,
    "transaction": payloadsRes.unsigned_transaction // use the unsigned_transaction param from your payloads response
}
```

Example Response
```json
{
    "operations": [ // operations should match the operations you use in the construction preprocess and construction payloads
        {
            "operation_identifier": {
                "index": 5,
                "network_index": 0
            },
            "related_operations": [
                {
                    "index": 1
                },
                {
                    "index": 2
                }
            ],
            "type": "Transfer",
            "status": "Reverted",
            "account": {
                "address": "0x3a065000ab4183c6bf581dc1e55a605455fc6d61",
                "sub_account": {
                    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                    "metadata": {}
                },
                "metadata": {}
            },
            "amount": {
                "value": "1238089899992",
                "currency": {
                    "symbol": "BTC",
                    "decimals": 8,
                    "metadata": {
                        "Issuer": "Satoshi"
                    }
                },
                "metadata": {}
            },
            "coin_change": {
                "coin_identifier": {
                    "identifier": "0x2f23fd8cca835af21f3ac375bac601f97ead75f2e79143bdf71fe2c4be043e8f:1"
                },
                "coin_action": "coin_created"
            },
            "metadata": {
                "asm": "304502201fd8abb11443f8b1b9a04e0495e0543d05611473a790c8939f089d073f90509a022100f4677825136605d732e2126d09a2d38c20c75946cd9fc239c0497e84c634e3dd01 03301a8259a12e35694cc22ebc45fee635f4993064190f6ce96e7fb19a03bb6be2",
                "hex": "48304502201fd8abb11443f8b1b9a04e0495e0543d05611473a790c8939f089d073f90509a022100f4677825136605d732e2126d09a2d38c20c75946cd9fc239c0497e84c634e3dd012103301a8259a12e35694cc22ebc45fee635f4993064190f6ce96e7fb19a03bb6be2"
            }
        }
    ],
    "signers": [
        "string"
    ],
    "account_identifier_signers": [
        {
            "address": "0x3a065000ab4183c6bf581dc1e55a605455fc6d61",
            "sub_account": {
                "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                "metadata": {}
            },
            "metadata": {}
        }
    ],
    "metadata": {}
}
```


## Combine

*Create Network Transaction from Signatures*

Combine creates a network-specific transaction from an unsigned transaction and an array of provided signatures. The signed transaction returned from this method will be sent to the [Submit](construction/construction?id=submit) endpoint by the caller.

`POST https://api.lunar.dev/v1/construction/combine`

Example POST Request
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "unsigned_transaction": payloadsRes.unsigned_transaction, // use unsigned_transaction param from the construction payloads response
    "signatures": [
        {
            "hex_bytes": btcKeys.sign(Buffer.from(payloadsRes.payloads[0].hex_bytes, 'hex')).toString('hex'), // use an external library to sign the payload
            "signing_payload": payloadsRes.payloads[0],
            "public_key": {
                "hex_bytes": btcKeys.publicKey.toString('hex'),
                "curve_type": "secp256k1"
            },
            "signature_type": "ecdsa",
        }
    ]
}
```

Example Response
```json
{
    "signed_transaction": "string"
}
```


## Hash

*Get the Hash of a Signed Transaction*

TransactionHash returns the network-specific transaction hash for a signed transaction.

`POST https://api.lunar.dev/v1/construction/hash`

Example POST Request
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "signed_transaction": signedTx // from the construction combine response
}
```

Example Response
```json
{
    "transaction_identifier": {
        "hash": "6d87ad0e26025128f5a8357fa423b340cbcffb9703f79f432f5520fca59cd20b"
    },
    "metadata": {}
}
```


## Submit

*Submit a Signed Transaction*

Submit a pre-signed transaction to the node.

`POST https://api.lunar.dev/v1/construction/submit`

Example POST Request
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "signed_transaction": signedTx // from the construction combine response
}
```

Example Response
```json
{
    "transaction_identifier": {
        "hash": "0x2f23fd8cca835af21f3ac375bac601f97ead75f2e79143bdf71fe2c4be043e8f" // this should match the construction hash response
    },
    "metadata": {}
}
```
