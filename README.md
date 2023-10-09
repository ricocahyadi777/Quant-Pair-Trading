# Quant Pair Trading
 
A small project to do pair trading on Pepsi (PEP) and Coca Cola (KO)

Code can be found on [pair_trading.ipynb](https://github.com/ricocahyadi777/Quant-Pair-Trading/blob/main/pair_trading.ipynb)

## Overview
Pairs trading is a non-directional, relative value investment strategy that does long-short strategies on 2 companies or funds with similar characteristics whose equity securities are currently diverge with the hope of converging. The techniques need to find the diverge or the spread between the two stocks, then does long and short on the underperform and overperform securities respectively.

- Advantages: </br>
  Mitigation against systemic risk. Since we are doing both long and short, we are hedged against systemic risk which happened during market collapse.
- Disadvantages: </br>
  It relies heavily on cointegration. Thus it is very challenging to identify. Furthermore, sometimes the cointegration of the 2 equities breaks, thus the spread are getting bigger. In this scenario, we need to close our position quickly to avoid big losses.
  

There are some rules that need to be addressed first before executing it.
1. Cointegration
2. Stationary

## Addressing the rules

### Cointegration

Cointegration
```python
print('PEP KO Cointegration')
(ts.coint(data['PEP'], data['KO']))[1]
```
![image](https://github.com/ricocahyadi777/Quant-Pair-Trading/assets/63791918/fd7162e8-3bf4-4c9f-a6d8-2f82652323c0)


### Stationary
![image](https://github.com/ricocahyadi777/Quant-Pair-Trading/assets/63791918/b0514a1f-98c7-4460-bc85-a07ab57a8a7b)


## Execution
```python
data['PEPKOposition'] = 0
data.loc[data['PEPKOspread']>0, 'PEPKOposition'] = -1
data.loc[data['PEPKOspread']<0, 'PEPKOposition'] = 1
data['PEPKOposition'] = data['PEPKOposition'].shift(1)
data['PEPposition'] = data['PEPKOposition']
data['KOposition'] = data['PEPKOposition']*result.params[1]*-1
```
## Result
![image](https://github.com/ricocahyadi777/Quant-Pair-Trading/assets/63791918/a9a36248-af51-4bc3-82db-0f60c9ef4f5e)

