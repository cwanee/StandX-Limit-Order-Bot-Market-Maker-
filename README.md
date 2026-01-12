# Standx Limit Order Bot

## Introduction
**Standx Limit Order Bot** is a JavaScript-based automation tool designed to run directly in the browser's developer console on the Standx exchange. It automates the process of market making by maintaining a ladder of limit orders, managing open positions, and adjusting strategies based on real-time market volatility (ATR).

This script is ideal for traders looking to automate:
- **Laddering Orders:** Automatically placing and maintaining buy/sell limit orders at specific Basis Point (BPS) distances.
- **Risk Management:** Monitoring Average True Range (ATR) to pause trading during high volatility.
- **Position Management:** Automatically closing positions and cleaning up stale orders that drift too far from the market price.

## Menu / Table of Contents
- [Features](#features)
- [Configuration](#configuration)
- [Installation & Usage](#installation--usage)
- [Safety & Risk](#safety--risk)

## Features
*   **Dynamic Order Laddering**: Automatically places multiple limit orders at configured BPS steps (e.g., 6, 7, 8 bps).
*   **Volatility Protection**: Scrapes trading indicators (ATR) from TradingView charts to halt new orders if volatility spikes.
*   **Auto-Cleanup**: Cancels orders that are "too far" (stale) or "too close" (risk of immediate execution) to the current price.
*   **Position Auto-Close**: Detects and closes open positions immediately to reset the cycle.
*   **DOM Interaction**: Works by interacting directly with the exchange's UI elements (buttons, inputs) rather than an API, making it easy to run without API keys.

## Configuration
You can adjust the `CONFIG` object at the top of the script to tailor the bot's behavior:

```javascript
static CONFIG = {
    QUANTITY: 0.001,           // Order size
    SYMBOL: 'btc-usd',         // Trading pair
    BPS_LADDER: [6, 7, 8],     // Ladder steps in Basis Points
    REPLACEMENT_BPS: 6,        // BPS for replacing missing orders
    MIN_DISTANCE_BPS: 1.5,     // Cancel if too close
    MAX_DISTANCE_BPS: 10,      // Cancel if too far
    USE_INDICATORS: true,      // Enable ATR/Volatility checks
    MAX_ATR: 20.0              // Max ATR allowed for trading
};
```

## Installation & Usage

1.  **Open the Exchange**: Navigate to `standx.com` (or your target exchange URL).
2.  **Open Developer Console**: Press `F12` or `Ctrl+Shift+I` to open the browser's developer tools.
3.  **Paste the Script**: Copy the entire content of `standx_limit_order.js` and paste it into the **Console** tab.
4.  **Initialize**:
    ```javascript
    const orderPlacer = new StandxLimitOrder();
    ```
5.  **Start**:
    ```javascript
    orderPlacer.start();
    ```
    *The bot will now run every 30 seconds.*

6.  **Stop**:
    To stop the bot at any time, run:
    ```javascript
    orderPlacer.stop();
    ```

## Disclaimer
This software is for educational purposes only. Use it at your own risk. The authors are not responsible for any financial losses incurred while using this script. Always test with small amounts first.
