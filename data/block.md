# Block

## Block

*Get a Block*

`POST https://api.lunar.dev/v1/block`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "block_identifier": {
        "index": 1889073,
        "hash": "00000000000002c6a6de1bfbebcc17c161c8b0206d807e441da8787c0755eef1"
    }
}
```

Example Response
```json
{
    "block": {
        "block_identifier": {
            "hash": "00000000000002c6a6de1bfbebcc17c161c8b0206d807e441da8787c0755eef1",
            "index": 1889073
        },
        "metadata": {
            "bits": "1a02f3e4",
            "difficulty": 5681909.019575418,
            "mediantime": 1604723031,
            "merkleroot": "a6a357de1b8ff20065432c9e88d73cbe6e126bf3ac857599ec596a8deb2e38d1",
            "nonce": 2115413179,
            "size": 327,
            "version": 939515904,
            "weight": 1200
        },
        "parent_block_identifier": {
            "hash": "00000000000001c0642e79d0df9c1fc65dd6530d7e5f21ea15ab5279e806ce90",
            "index": 1889072
        },
        "timestamp": 1604723195000,
        "transactions": null
    },
    "other_transactions": [
        {
            "hash": "a6a357de1b8ff20065432c9e88d73cbe6e126bf3ac857599ec596a8deb2e38d1"
        }
    ]
}
```

## Block Transaction

*Get a Transaction in a block*

`POST https://api.lunar.dev/v1/block/transaction`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "block_identifier": {
        "hash": "0000000000000039cb4188075df03c38fd8239cc64b8581b84754a85da01da22",
        "index": 1354482
    },
    "transaction_identifier": {
        "hash": "2a7303719f351aa81837baf347286c6dae74ffe9eca71b7734425969d7282aa1"
    }
}
```

Example Response
```json
{
    "transaction": {
        "metadata": {
            "size": 282,
            "version": 1,
            "vsize": 282,
            "weight": 1128
        },
        "operations": [
            {
                "account": {
                    "address": "mh7JYYLN52tbToXeULWLD3JALTJgMrUeP6"
                },
                "amount": {
                    "currency": {
                        "decimals": 8,
                        "symbol": "tBTC"
                    },
                    "value": "-21207200"
                },
                "coin_change": {
                    "coin_action": "coin_spent",
                    "coin_identifier": {
                        "identifier": "b787fd878fa60b19e78e63b7ceeb628ccc819d3e4151bc46430cf7425478ec5f:1"
                    }
                },
                "metadata": {
                    "scriptsig": {
                        "asm": "3043022000f7463e951d4426ce407fd1caaa9fcfd03a69e237b9263beb62a6e6ba5d3d06021f099fbb7e132adc3b4b8c2435d9056b5a5d15c9c84655ef1175867ef2be4af1[ALL] 0335c7f7a94ed9d66dc3f57d2da1472f5b2e4717b3f2104e02eee2030bf9055749",
                        "hex": "463043022000f7463e951d4426ce407fd1caaa9fcfd03a69e237b9263beb62a6e6ba5d3d06021f099fbb7e132adc3b4b8c2435d9056b5a5d15c9c84655ef1175867ef2be4af101210335c7f7a94ed9d66dc3f57d2da1472f5b2e4717b3f2104e02eee2030bf9055749"
                    },
                    "sequence": 4294967295
                },
                "operation_identifier": {
                    "index": 0,
                    "network_index": 0
                },
                "status": "SUCCESS",
                "type": "INPUT"
            },
            {
                "account": {
                    "address": "mhMuH9FVPFDNQwCgbopLUe5bcEZFLiWYWR"
                },
                "amount": {
                    "currency": {
                        "decimals": 8,
                        "symbol": "tBTC"
                    },
                    "value": "21101000"
                },
                "coin_change": {
                    "coin_action": "coin_created",
                    "coin_identifier": {
                        "identifier": "2a7303719f351aa81837baf347286c6dae74ffe9eca71b7734425969d7282aa1:0"
                    }
                },
                "metadata": {
                    "scriptPubKey": {
                        "addresses": [
                            "mhMuH9FVPFDNQwCgbopLUe5bcEZFLiWYWR"
                        ],
                        "asm": "OP_DUP OP_HASH160 1439fd9326a963c18330800bac55fc8e55e2af95 OP_EQUALVERIFY OP_CHECKSIG",
                        "hex": "76a9141439fd9326a963c18330800bac55fc8e55e2af9588ac",
                        "reqSigs": 1,
                        "type": "pubkeyhash"
                    }
                },
                "operation_identifier": {
                    "index": 1,
                    "network_index": 0
                },
                "status": "SUCCESS",
                "type": "OUTPUT"
            },
            {
                "account": {
                    "address": "6a4c50000051690001eb42b22d2f9ab1bd3b294d949c686b2a3e8bc156496e0da486169fdcf2757e3ecba88823b8f326b498f3fb1890465b509c85051f749db1fc1dc2206c494c0b8d2fda93fcf861649dd15b"
                },
                "amount": {
                    "currency": {
                        "decimals": 8,
                        "symbol": "tBTC"
                    },
                    "value": "0"
                },
                "metadata": {
                    "scriptPubKey": {
                        "asm": "OP_RETURN 000051690001eb42b22d2f9ab1bd3b294d949c686b2a3e8bc156496e0da486169fdcf2757e3ecba88823b8f326b498f3fb1890465b509c85051f749db1fc1dc2206c494c0b8d2fda93fcf861649dd15b",
                        "hex": "6a4c50000051690001eb42b22d2f9ab1bd3b294d949c686b2a3e8bc156496e0da486169fdcf2757e3ecba88823b8f326b498f3fb1890465b509c85051f749db1fc1dc2206c494c0b8d2fda93fcf861649dd15b",
                        "type": "nulldata"
                    }
                },
                "operation_identifier": {
                    "index": 2,
                    "network_index": 1
                },
                "status": "SUCCESS",
                "type": "OUTPUT"
            }
        ],
        "transaction_identifier": {
            "hash": "2a7303719f351aa81837baf347286c6dae74ffe9eca71b7734425969d7282aa1"
        }
    }
}
```