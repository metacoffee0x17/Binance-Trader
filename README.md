## Configuration

1. Signup Binance ( Referral url: https://www.binance.com/?ref=10701111 )
2. Enable Two-factor Authentication    
3. Go API Center, https://www.binance.com/userCenter/createApi.html
4. Create New Key

        [✓] Read Info [✓] Enable Trading [X] Enable Withdrawals 
5. Rename config.sample.py to config.py / orders.sample.db to orders.db
6. Get an API and Secret Key, insert into config.py

        API key for account access
        api_key = ''
        Secret key for account access
        api_secret = ''

        API Docs: https://www.binance.com/restapipub.html
7. Optional: run as an excutable application in Docker containers

## Requirements

    sudo easy_install -U requests
    or 
    sudo pip install requests
    
    Python 2.7
        import os
        import sys
        import time
        import config
        import argparse
        import threading
        import sqlite3

## Usage

    python trader.py --symbol XVGBTC
    
    Example parameters
    
    # Profit mode (default)
    python trader.py --symbol XVGBTC --quantity 300 --profit 1.3
    or by amount
    python trader.py --symbol XVGBTC --amount 0.0022 --profit 3
    
    # Range mode
    python trader.py --symbol XVGBTC --mode range --quantity 300 --buyprice 0.00000780 --sellprice 0.00000790
    or by amount
    python trader.py --symbol XVGBTC --mode range --amount 0.0022 --buyprice 0.00000780 --sellprice 0.00000790
    
    --quantity     Buy/Sell Quantity (default 0)
    --amount       Buy/Sell BTC Amount (default 0.0022)
    --max_amount   Buy/Sell using max BTC amount (default False)
    --symbol       Market Symbol (Ex. XVGBTC or TRXETH)
    --profit       Target Profit Percentage (default 2)
    --stop_loss    Decrease sell price at loss Percentage (default 0)
    --orderid      Target Order Id (default 0)
    --wait_time    Wait Time (seconds) (default 0.7)
    --increasing   Buy Price Increasing Percentage  +(default 0.2)
    --decreasing   Sell Price Decreasing Percentage -(default 0.2)
    --prints       Scanning Profit Screen Print (default True)
    --loop         Loop (default 0 unlimited)
    
    --mode         Working modes profit or range (default profit)
                   profit: Profit Hunter. Find defined profit, buy and sell. (Ex: 1.3% profit)
                   range: Between target two price, buy and sell. (Ex: <= 0.00000780 buy - >= 0.00000790 sell )
    --buyprice     Buy price (Ex: 0.00000780)
    --sellprice    Buy price (Ex: 0.00000790)

    Symbol structure;
        XXXBTC  (Bitcoin)
        XXXETH  (Ethereum)
        XXXBNB  (Binance Coin)
        XXXUSDT (Tether)

    All binance symbols are supported.

    Every coin can be different in --profit and --quantity.

    If quantity is empty --quantity is automatically calculated to the minimum qty.
    If --stop_loss is 0. It will hold the coin until it's sold with the desired amount.

    Set --max_amount True to use all BTC amount upon setting buy order

    Variations;
        trader.py --symbol TBNBTC --quantity 50 --profit 3
        trader.py --symbol NEOBTC --amount 0.1 --profit 1.1
        trader.py --symbol ETHUSDT --quantity 0.3 --profit 1.5
        ...
    
## Run in a Docker container

    docker build -t trader .

    docker run trader
 
## Contributing

    Fork this Repo
    Commit your changes (git commit -m 'Add some feature')
    Push to the changes (git push)
    Create a new Pull Request
    
    Thanks all for your contributions...
 
---
