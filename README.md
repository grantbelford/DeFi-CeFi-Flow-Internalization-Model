1inch Fusion / Binance Flow Internalization Model

Step1-WETH-USDT-pair-Binance&1inch-download.ipynb

Download (real-time) Binance 1 minute ETH/USDT OHLCV & orderbook data (as cannot download historical Binance *orderbook* (bid/ask) data) as well as historical 1inch Fusion WETH/USDT data via DUNE API query.

The Dune query for the historical 1inch WETH-USDT trade data can be run directly in the dune.com/queries/ GUI and then the csv file loaded via the above .ipynb file.
The Dune query code is in Dune-1inch-WETH-USDT-query.pdf, currently set to collect the previous 72hrs of data as can be seen in row 49 in the code.

For those wanting to begin directly on Step 2 below, the following google drive link has a zip file containing 2 directories (1inch & Binance) containing the hist data. 
Unzip & copy the 2 directories into the same folder holding the below .ipynb file. 

https://drive.google.com/file/d/1D0zzPskb0rbmYdp5622mdsdLviD87iIc/view?usp=sharing


Step2-WETH-USDT-pair-1inch-Query&Analysis.ipynb 

Backtest above data to determine if it is better immediately offset the 1inch Fusion WETH/USDT trades on Binance or warehouse the 1inch Fusion trades internally awaiting natural offset.
Subsequent code allows you to see the development of the portfolio over time.

1_Flow-Internalization-Model-1inch-Binance-1trade-drilldown.png

Using 1 of the 1inch trades the .png works through the logic in Step2 on how the hedge pnl & warehouse pnl calculations are performed leading to the decision whether to hedge or warehouse. 

Above is a work in progress - future postings to include more in-depth flow correlation analysis & ML predict.
