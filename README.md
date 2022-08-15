# Hillsight Exchange
This is a library for interacting with supported exchange APIs.

## Installation

```ts
import { binance, ... } from "https://deno.land/x/hillsight/exchange/mod.ts";
```

## Usage

```ts
registerExchange("binance", binance);

const exchange = createExchange({
  provider: "binance",
  credentials: {
    api_key: "...",
    secret_key: "...",
  },
  options: {
    // ...
  },
})
```

## Supported Exchanges

- [ ] [Binance](https://www.binance.com/)
- [ ] [Kucoin](https://www.kucoin.com/)
- [ ] [Coinbase](https://www.coinbase.com/)
- [ ] [Kraken](https://www.kraken.com/)

### Binance

#### Credentials

You will be able to get a API key and secret key with the guide from [Binance FAQ](https://www.binance.com/en/support/faq/360002502072).

> Remember to enable `Enable Spot & Margin Trading` if you want to perform live trades.

```ts
{
  // API key from Binance
  api_key: "...",
  // Secret key from Binance
  secret_key: "...",
}
```

#### Options

```ts
{
  // No options available
}
```

## Contributing

Please submit any issues or feature requests using the [github issue tracker](https://github.com/hillsight/exchange/issues).