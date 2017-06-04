## txnwithfriends

`txnwithfriends` is a friendly CLI to get up and running with your
cryptocurrencies of choice as quickly as possible. Manage all of your coins from
one convenient CLI!

Instead of figuring out how to compile and manage each coin on your own,
`txnwithfriends` uses Docker containers to build and run the various wallets and
defines common commands for interfacing with them. That way, you can easily jump
into using new cryptocurrencies and can store them on a computer that you
control instead of in a 3rd party exchange where your coins could be frozen or
stolen.

This way, you can use the same commands for interacting with each type of
cryptocurrency, including mining, sending and balance checking, and even
[shapeshifting](https://shapeshift.io) between various forms of currency.

_Please note_: Very few of the features listed here are fully developed yet. The
documentation is intended to serve as a guide for development.

## Installation

For now:

```
$ curl -sSL get.docker.com | sh
$ go get github.com/diffiehellboy/txnwithfriends
```

## Examples

Many `txnwithfriends` commands require `sudo` access, because:

1. It's an additional security layer around interfacing with your wallets, and
2. [Docker](https://github.com/docker/docker) actions require root access.

View all wallets under management and their current status:

```
$ sudo txnwithfriends wallet
NAME    CURRENCY BALANCE ADDRESS
btc     BTC      1.02    1F1tAaz5x1HUXrCNLbtMDqcw6o5GNn4xqX
eth     ETH      101.1   0xd12Cd8A37F074e7eAFae618C986Ff825666198bd
xmr     XMR      51.3    48NLnC8f79BUXw7uSjPscUQ5PzbE2MNXw74xYfDtWVcBJw6J9B5hGbPAMhLmJ7ePRJjJGrmGWomqX7wkjotfFwBw6ubW9zh
alt     XMR      2.0     47fn91iHkHD28GjsufbEQJgLiUE9bqrJSQ41sX4kc3mAcKqdP1bZGcm1j3UYYb2Muzh7jdCYPi9vJLwrb2PUrDLBFa17mkX 
```

Check coin market caps (uses https://coinmarketcap.com):

```
$ txnwithfriends coin
NAME                   SYMBOL  PRICE    MARKET CAP      %VOL
Bitcoin                BTC     2505.77  41,024,779,661  3.43
Ethereum               ETH     247.65   22,835,068,014  3.24
Ripple                 XRP     0.30     11,434,879,410  1.38
NEM                    XEM     0.22     1,948,500,000   0.54
Ethereum Classic       ETC     17.25    1,590,630,119   6.63
Litecoin               LTC     27.65    1,421,556,864   13.94
Dash                   DASH    141.15   1,036,474,849   2.78
Stratis                STRAT   10.00    983,997,036     4.31
Monero                 XMR     42.54    620,077,536     1.68
Waves                  WAVES   5.40     539,962,000     0.91
```

Create a new wallet:

```
$ sudo txnwithfriends wallet create --currency BTC
No name specified, using default name "btc"...
Building Docker image for BTC...
Docker image built.
No running Docker container for BTC detected, running now...

```

Create a new full node (useful for mining or participating in the network):

```
$ sudo txnwithfriends fullnode create --currency BTC
```

Shapeshift from one currency to another:

```
$ sudo txnwithfriends shapeshift \
    -o from=eth,amount=0.33,to=BTC,addr=1F1tAaz5x1HUXrCNLbtMDqcw6o5GNn4xqX
You are about to convert 0.33 ETH to 0.03 BTC.
Are you 100% sure you want to proceed? y
...
Your transaction is at: https://shapeshift.io/foo/blah
```

Back up your private keys for the wallet in question:

```
$ sudo txnwithfriends export-keys -o keys.tar btc
Output private key backup for wallet "btc" to file "keys.tar".  Protect it!
```

## Commands

#### `coin`

Information about current coin rates, market cap, and transaction volume.

#### `wallet`

Information about your local wallets.

#### `send`

Send coins from one wallet to another.

## Future

- It would be nice to have built-in ways to index and/or rebalance your
  portfolio.
