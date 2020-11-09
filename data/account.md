# Account

## Account Balance

*Get an Account's Balance*

Get an array of all AccountBalances for an AccountIdentifier and the BlockIdentifier at which the balance lookup was performed. The BlockIdentifier must always be returned because some consumers of account balance data need to know specifically at which block the balance was calculated to compare balances they compute from operations with the balance returned by the node. It is important to note that making a balance request for an account without populating the SubAccountIdentifier should not result in the balance of all possible SubAccountIdentifiers being returned. Rather, it should result in the balance pertaining to no SubAccountIdentifiers being returned (sometimes called the liquid balance). To get all balances associated with an account, it may be necessary to perform multiple balance requests with unique AccountIdentifiers. It is also possible to perform a historical balance lookup (if the server supports it) by passing in an optional BlockIdentifier.

`POST https://api.lunar.dev/v1/account/balance`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "account_identifier": {
        "address": "tb1qz8q2lwfmp965cszdd5raq9m7gljs57hkzpw56d"
    }
}
```

Example Response
```json
{
    "balances": [
        {
            "currency": {
                "decimals": 8,
                "symbol": "tBTC"
            },
            "value": "39586"
        }
    ],
    "block_identifier": {
        "hash": "00000000000002e6da2c13d303dd5f5d8c1d940c1dddcd367ffd354c55523614",
        "index": 1889142
    },
    "coins": [
        {
            "amount": {
                "currency": {
                    "decimals": 8,
                    "symbol": "tBTC"
                },
                "value": "38586"
            },
            "coin_identifier": {
                "identifier": "07bdaba70e6e0a7b4dbf83733a2be914a2f9b92fb15a9d4550eb92ceedd7346e:1"
            }
        },
        {
            "amount": {
                "currency": {
                    "decimals": 8,
                    "symbol": "tBTC"
                },
                "value": "1000"
            },
            "coin_identifier": {
                "identifier": "ddd3f3224cc5c92ac1ff74f53143b169f78c815942031879427c52449d2d76a1:0"
            }
        }
    ]
}
```


<!-- NOT YET IMPLEMENTED ON ROSETTA BTC - Account Coins
*Get an Account's Unspent Coins*
Get an array of all unspent coins for an AccountIdentifier and the BlockIdentifier at which the lookup was performed. If your implementation does not support coins (i.e. it is for an account-based blockchain), you do not need to implement this endpoint. If you implementation does support coins (i.e. it is fro a UTXO-based blockchain), you MUST also complete the /account/balance endpoint. It is important to note that making a coins request for an account without populating the SubAccountIdentifier should not result in the coins of all possible SubAccountIdentifiers being returned. Rather, it should result in the coins pertaining to no SubAccountIdentifiers being returned. To get all coins associated with an account, it may be necessary to perform multiple coin requests with unique AccountIdentifiers. Optionally, an implementation may choose to support updating an AccountIdentifier's unspent coins based on the contents of the mempool. Note, using this functionality breaks any guarantee of idempotency.
POST https://api.lunar.dev/v1/account/coins

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    }
}
``` -->