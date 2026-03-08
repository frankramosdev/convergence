# Convergence Market

Convergence Chainlink Hackathon 2026

## AI Powered Prediction Market

[![Chainlink Convergence Hackathon 2026](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://www.youtube.com "Chainlink Convergence Hackathon 2026")

### 1. Create a Prediction Market (HTTP Trigger)

```bash
cd ..  # Back to prediction-market/
cre workflow simulate my-workflow --broadcast
```

Select HTTP trigger (option 1) and enter:

```json
{ "question": "Will the New England Patriots win Super Bowl LX in 2026?" }
```

### 1. Place a prediction

```bash
export MARKET_ADDRESS=0xYOUR_DEPLOYED_ADDRESS

cast send $MARKET_ADDRESS \
  "predict(uint256,uint8)" 0 0 \
  --value 0.01ether \
  --rpc-url "https://ethereum-sepolia-rpc.publicnode.com" \
  --private-key $CRE_ETH_PRIVATE_KEY
```

> Note: `0 0` above corresponds to do the Market Id and the prediction (Yes = 0, No = 1). See the `predict()` function in `./prediction-market/contracts/src/PredictionMarket.sol`

### 3. Request settlement

Request settlement by passing in the relevant Market Id.

```bash
cast send $MARKET_ADDRESS \
  "requestSettlement(uint256)" 0 \
  --rpc-url "https://ethereum-sepolia-rpc.publicnode.com" \
  --private-key $CRE_ETH_PRIVATE_KEY
```

Save the transaction hash!

### 4. Settle the market (Log Trigger)

```bash
cre workflow simulate my-workflow --broadcast
```

Select Log trigger (option 2), enter the tx hash from step 7 and event index `0`.

### 5. Claim winnings

```bash
cast send $MARKET_ADDRESS \
  "claim(uint256)" 0 \
  --rpc-url "https://ethereum-sepolia-rpc.publicnode.com" \
  --private-key $CRE_ETH_PRIVATE_KEY
```
