# GMRemake EA Development Instructions

## Project Context
This is a MetaTrader 4 (MT4) Expert Advisor (EA) project written in **MQL4**. The core logic resides in `MT4/Experts/GMRemake_v1.0.mq4`. The EA implements a Martingale strategy with multi-level risk management, trend protection, and EMA filtering.

## Architecture & Code Structure
- **Monolithic Design**: The entire EA logic is contained within a single `.mq4` file.
- **Event-Driven**: The `OnTick()` function is the entry point for the main execution loop, triggering on every price update.
- **Statelessness**: Do not rely on persistent global variables for order counts. Always recalculate state (e.g., `CountOrders()`) at the start of `OnTick()` by iterating through open orders. This ensures resilience against terminal restarts.
- **Global Arrays**: Configuration for the 8 martingale levels (Lot Sizes, Entry Distances) is stored in global arrays (`EntryDistances[]`, `LotSizes[]`) initialized in `OnInit()`.

## Critical implementation Details

### Order Management Patterns
- **Iterating Orders**: Always iterate backwards when processing the order pool to avoid index errors if orders are modified or closed.
  ```cpp
  for(int i = OrdersTotal() - 1; i >= 0; i--) { ... }
  ```
- **Filtering**: deeply strictly filter orders by **both** `OrderMagicNumber() == MagicNumber` and `OrderSymbol() == Symbol()`.
- **Order Selection**: Always check the return value of `OrderSelect()`.

### Price & Logic Conventions
- **Points vs Pips**: Inputs are defined in **Points** (integers), not Pips. Internally, convert these to price values using `* Point` (e.g., `EntryDistances[0] = EntryDistance1 * Point;`).
- **Normalization**: Use `NormalizeDouble(price, Digits)` for all calculated prices (StopLoss, TakeProfit, pending orders) to avoid `OrderSend` error 130 or 129.
- **New Bar Logic**: Perform expensive calculations or signal checks only once per bar to save resources.
  ```cpp
  if(LastBarTime != iTime(Symbol(), Timeframe, 0)) {
      LastBarTime = iTime(Symbol(), Timeframe, 0);
      // Run bar-opening logic here
  }
  ```

### Risk Management
- **Spread Filter**: Check spread (`Ask - Bid`) against `SpreadInPoints` at the very beginning of `OnTick()` and exit if too high.
- **Hard Limits**: Respect `MaxBuyOrder` and `MaxSellOrder`. The logic relies on current order counts to prevent over-trading.

## Workflow & Debugging
- **Compilation**: The code must be compiled using `mql.exe` or MetaEditor. Syntax errors will prevent `.ex4` generation.
- **Logging**: Use `Print()` extensively for debugging. Logs appear in the "Experts" tab of the Terminal. Format logs with clear prefixes: `Print("GMRemake [Buy Logic]: Condition met ", price);`.

## Documentation
- Refer to `EA_LOGIC_FLOW.md` for understanding the exact sequence of operations in `OnTick`.
- `CONFIGURATION_GUIDE.md` sources the logic for different risk profiles (Conservative vs Aggressive).
