# CPU crypto currency miner
A user friendly crypto currency miner based on Alpine Linux and XMRig. 


## Features
* Easy to configure
* Supports a wide range of currencies
* Only 0,75% pool fee with referral code: <code>cgwg-4yfq</code> (default 1%)
* Optional dev fee

## Components
* [Alpine Linux](https://www.alpinelinux.org)
* [XMRig](https://xmrig.com)
* [unMineable](https://unmineable.com/?ref=cgwg-4yfq)

## Run
### Quick test
```
docker run -d --name miner kornflex/unmineable
```

### Configure miner for your coin and wallet
Replace the values in the sample code with your desired settings.<br />
Examples uses 50% of cpu to mine SOLANA to the specified wallet.

#### Docker run
```
docker run \
  -d \
  --name=unmineable \
  -e 'CPU_LIMIT_PERCENT=50' \
  -e 'COIN=SOL' \
  -e 'WALLET=...' \
  -e 'WORKER=docker' \
  -e 'DIFFICULTY=35000' \
  -e 'DONATE=1' \
  kornflex/unmineable
```

#### Docker compose
```
version: "3"
services:
  unmineable:
    image: kornflex/unmineable
    container_name: unmineable
    
    restart: unless-stopped
    
    network_mode: bridge
    
    environment:
      - CPU_LIMIT_PERCENT=50
      - COIN=SOL
      - WALLET=...
      - WORKER=docker
      - DIFFICULTY=35000
      - DONATE=1
    
    volumes:
      - /etc/localtime:/etc/localtime:ro
```

### Configuration

#### Variables

| Variable | Usage |
|----------|-------|
| CPU_LIMIT_PERCENT | Percentage of cpu to use for mining (digits only, 1-100). Default 50%. |
| COIN | Currency supported by unMineable.<br />Example:<br/>- BTC<br />- ETH<br />- DOGE<br />- XMR<br/>- ...and many more (please see [here](https://unmineable.com/coins?ref=cgwg-4yfq) for a complete list). |
| WALLET | Your wallet address for specified coin. |
| WORKER | Name of your worker (default: docker). |
| DIFFICULTY | Desired difficulty. |
| DONATE | Percentage of cpu time to use for dev donation (digits only, 0-99). Default 1%. |

## Tips
Problem allocating memory or lower hashrate than expected? Try running container in privileged mode.


## Unineable Tips
You can check how many SOL ( or other cryptos ) you earn in this URL : https://unmineable.com/coins/SOL/address/

Check "auto pay" to have your earnings on your wallet.

You can use DEX wallet ( metamask ... ) or DEX ( coinbase, binance ... ). But take care to choose the right network ( ETH, BSC ... ). Select the correct one on unmineable using "SWITCH NETWORK" button.
