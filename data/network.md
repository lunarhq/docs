# Network

## Network List

*Get List of Available Networks*

This endpoint returns a list of NetworkIdentifiers that the Lunar Node supports.

`POST https://api.lunar.dev/v1/network/list`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    },
    "metadata": {}
}
```

Example Response
```json
{
    "network_identifiers": [
        {
            "blockchain": "Bitcoin",
            "network": "Testnet3"
        }
    ]
}
```


## Network Options

*Get Network Options*

This endpoint returns the version information and allowed network-specific types for a NetworkIdentifier. Any NetworkIdentifier returned by /network/list should be accessible here. Because options are retrievable in the context of a NetworkIdentifier, it is possible to define unique options for each network.

`POST https://api.lunar.dev/v1/network/options`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    }
}
```

Example Response
```json
{
    "allow": {
        "errors": [
            {
                "code": 0,
                "message": "Endpoint not implemented",
                "retriable": false
            },
            {
                "code": 1,
                "message": "Endpoint unavailable offline",
                "retriable": false
            },
            {
                "code": 2,
                "message": "Bitcoind is not ready",
                "retriable": false
            },
            {
                "code": 3,
                "message": "Bitcoind error",
                "retriable": false
            },
            {
                "code": 4,
                "message": "Block not found",
                "retriable": false
            },
            {
                "code": 5,
                "message": "Unable to derive address",
                "retriable": false
            },
            {
                "code": 6,
                "message": "Unable to parse intent",
                "retriable": false
            },
            {
                "code": 7,
                "message": "Unable to parse intermediate result",
                "retriable": false
            },
            {
                "code": 8,
                "message": "Missing ScriptPubKeys",
                "retriable": false
            },
            {
                "code": 9,
                "message": "Coin is invalid",
                "retriable": false
            },
            {
                "code": 10,
                "message": "Unable to decode address",
                "retriable": false
            },
            {
                "code": 11,
                "message": "Unable to decode ScriptPubKey",
                "retriable": false
            },
            {
                "code": 12,
                "message": "Unable to calculate signature hash",
                "retriable": false
            },
            {
                "code": 13,
                "message": "Script type is not supported",
                "retriable": false
            },
            {
                "code": 14,
                "message": "Unable to compute PK script",
                "retriable": false
            },
            {
                "code": 15,
                "message": "Unable to get coins",
                "retriable": false
            },
            {
                "code": 16,
                "message": "Transaction not found",
                "retriable": false
            },
            {
                "code": 17,
                "message": "Could not get suggested fee rate",
                "retriable": false
            }
        ],
        "historical_balance_lookup": false,
        "operation_statuses": [
            {
                "status": "SUCCESS",
                "successful": true
            },
            {
                "status": "SKIPPED",
                "successful": false
            }
        ],
        "operation_types": [
            "INPUT",
            "OUTPUT",
            "COINBASE"
        ]
    },
    "version": {
        "middleware_version": "0.0.3",
        "node_version": "0.20.1",
        "rosetta_version": "1.4.4"
    }
}
```

## Network Status

*Get Network Status*

This endpoint returns the current status of the network requested. Any NetworkIdentifier returned by /network/list should be accessible here.

`POST https://api.lunar.dev/v1/network/status`

Example POST Request Body
```json
{
    "network_identifier": {
        "blockchain": "Bitcoin",
        "network": "Testnet3"
    }
}
```

Example Response
```json
{
    "current_block_identifier": {
        "hash": "00000000000002c6a6de1bfbebcc17c161c8b0206d807e441da8787c0755eef1",
        "index": 1889073
    },
    "current_block_timestamp": 1604723195000,
    "genesis_block_identifier": {
        "hash": "000000000933ea01ad0ee984209779baaec3ced90fa3f408719526f8d77f4943",
        "index": 0
    },
    "peers": [
        {
            "metadata": {
                "addr": "93.190.142.127:18333",
                "banscore": 0,
                "lastrecv": 1604723252,
                "lastsend": 1604723288,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.18.0/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "93.190.142.127:18333"
        },
        {
            "metadata": {
                "addr": "35.206.112.240:18333",
                "banscore": 0,
                "lastrecv": 1604723288,
                "lastsend": 1604723288,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.18.0(bitcoin)/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "35.206.112.240:18333"
        },
        {
            "metadata": {
                "addr": "165.227.101.132:18333",
                "banscore": 0,
                "lastrecv": 1604723221,
                "lastsend": 1604723291,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.20.0/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "165.227.101.132:18333"
        },
        {
            "metadata": {
                "addr": "95.179.180.255:18333",
                "banscore": 0,
                "lastrecv": 1604723253,
                "lastsend": 1604723288,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.20.1/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "95.179.180.255:18333"
        },
        {
            "metadata": {
                "addr": "157.230.252.82:18333",
                "banscore": 0,
                "lastrecv": 1604723252,
                "lastsend": 1604723289,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.19.0.1/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "157.230.252.82:18333"
        },
        {
            "metadata": {
                "addr": "190.120.241.37:18333",
                "banscore": 0,
                "lastrecv": 1604723255,
                "lastsend": 1604723288,
                "relaytxes": true,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.20.1/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "190.120.241.37:18333"
        },
        {
            "metadata": {
                "addr": "217.172.178.44:18333",
                "banscore": 0,
                "lastrecv": 1604723265,
                "lastsend": 1604723265,
                "relaytxes": false,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.17.1/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "217.172.178.44:18333"
        },
        {
            "metadata": {
                "addr": "35.226.17.222:18333",
                "banscore": 0,
                "lastrecv": 1604723285,
                "lastsend": 1604723285,
                "relaytxes": false,
                "startingheight": 1866370,
                "subver": "/Satoshi:0.18.0/",
                "synced_blocks": 1889068,
                "synced_headers": 1889068,
                "version": 70015
            },
            "peer_id": "35.226.17.222:18333"
        },
        {
            "metadata": {
                "addr": "93.55.242.131:18333",
                "banscore": 0,
                "lastrecv": 1604723290,
                "lastsend": 1604723252,
                "relaytxes": true,
                "startingheight": 1866614,
                "subver": "/Satoshi:0.20.1/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "93.55.242.131:18333"
        },
        {
            "metadata": {
                "addr": "13.76.217.4:18333",
                "banscore": 0,
                "lastrecv": 1604723293,
                "lastsend": 1604723293,
                "relaytxes": true,
                "startingheight": 1872605,
                "subver": "/Satoshi:0.20.0/",
                "synced_blocks": 1889073,
                "synced_headers": 1889073,
                "version": 70015
            },
            "peer_id": "13.76.217.4:18333"
        }
    ]
}
```