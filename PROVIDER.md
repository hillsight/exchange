# Exchange Provider Documentation

## Introduction
A Exchange Provider is a service in Hillsight that provides capabilities to manage orders and collect data from an exchange.

### Features
- A provider should be able to read the balance of an user.
- A provider should be able to place orders on behalf of a user.
- A provider should be able to read market data in real time as well as historical data.

## API
- `balance()`: Get the balance of an account.
- `order({ symbol, side, price, quantity })`: Place a order on the exchange.
- `stream( [symbol, interval]... )`: Stream klines for a symbol and interval.
- `history( symbol, interval, start, end )`: Get historical data for a symbol and interval.
- `symbols()`: Get a list of all available symbols.
- `time()`: Get the current time on the exchange. *(Used for time synchronization)*

## Kline

### Structure
- `time`: The unix timestamp of the kline.
- `open`: The open price of the kline.
- `high`: The highest price of the kline.
- `low`: The lowest price of the kline.
- `close`: The close price of the kline.
- `volume`: The volume of the kline.

### Intervals
The following intervals are required to be supported:
- `1m`: 1 minute
- `5m`: 5 minute
- `15m`: 15 minute
- `30m`: 30 minute
- `1h`: 1 hour
- `2h`: 2 hour
- `4h`: 4 hour
- `6h`: 6 hour
- `8h`: 8 hour
- `12h`: 12 hour
- `1d`: 1 day
- `3d`: 3 day
- `1w`: 1 week
- `1mo`: 1 month

## Implementation
To implement an Exchange Provider, you should export the default value of `createProvider` function from the `provider.ts` file.

```ts
// Example of a dummy provider (async-ish)
type Options = {
  cache_dir: string;
}

export default createProvider<Options>((options) => {
  async balance() {
    return Promise.resolve({
      USD: {
        available: 100,
        onOrder: 0,
      },
      BTC: {
        available: 0,
        onOrder: 0,
      },
    });
  },
  async order({ symbol, side, price, quantity }) {
    return Promise.resolve({
      id: '123',
      symbol,
      side,
      price,
      quantity,
    });
  },
  async *stream(symbol, interval) {
    yield Promise.resolve([1546300800, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100]);
    yield Promise.resolve([1546300900, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100]);
    yield Promise.resolve([1546301000, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100]);
  },
  async history(symbol, interval, start, end) {
    return Promise.resolve([
      [1546300800, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100],
      [1546300900, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100],
      [1546301000, 0.00000100, 0.00000100, 0.00000100, 0.00000100, 0.00000100],
    ]);
  },
  async symbols() {
    return Promise.resolve([
      ['BTC', 'USDT'],
      ['ETH', 'USDT'],
      ['LTC', 'USDT'],
    ]);
  },
  async time() {
    return Promise.resolve(1546300800);
  },
});
```