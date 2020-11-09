# Getting Started

Using Lunar, you can query multiple blockchains with consistent requests and responses. How do you we do this?
At Lunar, we run Rosetta Nodes, which use a standardized set of requests and responses, no matter the blockchain.

We have an open source TypeScript client which can be found on our [Github](https://github.com/lunarhq/lunar-clients-ts).
A Golang client is coming soon.

Our base api endpoint is `'https://api.lunar.dev/v1'`. All requests are POST requests.

## API Key Usage

All Testnet calls are free, but rate-limited. To use Mainnet or increase your rate limit, sign up
and get a key. You can sign up [here](https://lunar.dev/login).

If you have a key, add it to the headers section of your request. 
```js
headers: {
    'X-Api-Key': key
}
```

## Available Networks

Our growing list of supported Network Identifiers:

- Bitcoin Testnet
```json
{
        "network_identifier": {
            "blockchain": "Bitcoin",
            "network": "Testnet3"
        },
}
```

- Bitcoin Mainnet
```json
{
        "network_identifier": {
            "blockchain": "Bitcoin",
            "network": "Mainnet"
        },
}
```