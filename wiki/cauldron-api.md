# cauldron-api

**Summary**: API documentation for the Riften Labs Indexer service powering Cauldron DEX, covering cauldron contracts, token pools, pricing, trading data, oracle feeds, BCMR metadata, Moria lending protocol, and health endpoints.

**Sources**: docs.riftenlabs.com/cauldron/API/

**Last updated**: 2026-05-31

---

The Riften Labs Indexer provides a REST API for querying Cauldron DEX data. All endpoints return JSON responses and currently require no authentication. Endpoints marked as **unstable** are subject to change or may be removed (source: docs.riftenlabs.com).

**Base URL**: `https://indexer.riften.net`

## Available Sections

- [/cauldron/](#cauldron-endpoints) — 23 endpoints for pools, prices, tokens, and transactions
- [/bcmr](#bcmr-endpoints) — 2 endpoints for BCMR token metadata
- [/oracle](#oracle-endpoints) — 5 endpoints for BCH/USD and token oracle prices
- [/moria](#moria-endpoints) — 4 endpoints for the Moria lending protocol
- [/](#root-endpoint) — 1 health check endpoint

---

## Cauldron Endpoints

Base URL: `/cauldron/`

### Contract Count

#### `GET /contract/count` (Stable)

Get the number of active and ended Cauldron contracts.

**Response:**
```json
{ "active": 100, "ended": 10 }
```

#### `GET /contract/count/<token>` (Stable)

Get the number of active and ended Cauldron contracts for a specific token.

- **token**: Token ID (32-byte hex) or symbol

**Response:**
```json
{ "active": 100, "ended": 10 }
```

### Pool Endpoints

#### `GET /pool/active` (Stable)

Get a list of active pools for a given token and/or user. Either `user` or `token` must be provided.

**Parameters:**
- `user` — 20-byte hash of a user's public key hash (pkh)
- `token` — Token ID (32-byte hex) or symbol
- `pkh` — Public key hash

**Response:**
```json
{
  "active": [
    {
      "owner_p2pkh_addr": "bitcoincash:zqmvqqsd6w08e4nvy8er0hzn6wzxvxj40u7tlk8wl3",
      "owner_pkh": "36c0020dd39e7cd66c21f237dc53d384661a557f",
      "sats": 776661580,
      "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
      "tokens": 16,
      "tx_pos": 0,
      "txid": "94a933a0fa55093a0965eb867f1b9cac2bb07488ced4825bc31f86c9371f76aa"
    }
  ]
}
```

#### `GET /pool/aggregated_apy` (Stable)

Fetch aggregated APY for a token and/or account within a given time interval. All parameters are optional; empty query returns AAPY across all users and tokens.

**Parameters:**
- `token` — 32-byte token ID
- `pkh` — Public key hash for a single wallet account
- `pool` — One or more pool IDs (for per-user APY). Cannot be combined with `token` or `pkh`.
- `start` — Unix timestamp for period start (default: 30 days)
- `end` — Unix timestamp for period end (default: now)

**Response:**
```json
{ "apy": "10.00", "pools": 100 }
```

#### `GET /pool/history/` (Unstable)

Get historical state changes (price history) for a specific pool. Returns token/BCH ratio over time.

**Parameters:**
- `pool_id` — Pool ID (obtainable via `/pool/id_from_utxo`)
- `start` — Unix timestamp for period start (default: 30 days ago)

**Response:**
```json
{
  "history": [
    {
      "sats": 1000000,
      "tokens": 500,
      "timestamp": 1709468902,
      "txid": "..."
    }
  ],
  "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
  "owner_pkh": "36c0020dd39e7cd66c21f237dc53d384661a557f"
}
```

#### `GET /pool/id_from_utxo` (Unstable)

Get a pool ID from a UTXO specified by transaction ID and output position.

**Parameters:**
- `txid` — Transaction ID (hex string)
- `n` — Output position (vout) in the transaction

**Response:**
```json
{ "pool_id": "a1b2c3d4e5f6..." }
```

### Price Endpoints

#### `GET /price/<token>/at/<timestamp>` (Stable)

Get the price of a given token at a specific timestamp.

**Parameters:**
- `token` — 32-byte token ID
- `timestamp` — Unix timestamp

**Notes:** The price field is denominated per the **smallest unit** of the token (e.g. satoshis for an 8-decimal token), not per whole token. To get the price per whole token:

```
price_per_token = api_price * (10 ** decimals)
```

**Response:**
```json
{
  "price": 34493809.347826086,
  "timestamp": 1709468902
}
```

#### `GET /price/<token>/candlesticks` (Unstable)

Fetch candlesticks in BCH satoshis for a token. If an interval has no trades, it is omitted from results.

**Parameters:**
- `start` — Unix timestamp for period start (default: 30 days)
- `end` — Unix timestamp for period end (default: now)
- `stepsize` — Seconds per interval (default: 3600)

**Response:**
```json
{
  "candlesticks": [
    {
      "close": 64654136.35714286,
      "high": 87959043.0,
      "low": 58755326.0,
      "open": 87959043.0,
      "time": 1752522150,
      "transaction_count": 4,
      "volume_sats": 3170247594,
      "volume_tokens": 43
    }
  ]
}
```

#### `GET /price/<token>/current` (Stable)

Get the current price of a given token in satoshis.

**Parameters:**
- `token` — 32-byte token ID

#### `GET /price/<token>/history` (Unstable)

Fetch historical price data in satoshis for a given token. If an interval has no trades, it is omitted.

**Parameters:**
- `start` — Unix timestamp for period start
- `end` — Unix timestamp for period end
- `stepsize` — Seconds per interval

**Response:**
```json
{
  "history": [
    {
      "avg": 33829844.78947368,
      "max": 33829844.78947368,
      "min": 33829844.78947368,
      "time": 1709470824
    }
  ]
}
```

### Token Endpoints

#### `GET /token/<token>/first_pool` (Unstable)

Get the first pool creation event for a given token. Returns 404 if no pools have ever been created.

**Parameters:**
- `token` — 32-byte token ID

**Response:**
```json
{
  "token": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
  "creation_utxo": "94a933a0fa55093a0965eb867f1b9cac2bb07488ced4825bc31f86c9371f76aa:0",
  "txid": "94a933a0fa55093a0965eb867f1b9cac2bb07488ced4825bc31f86c9371f76aa",
  "timestamp": 1709468902,
  "block_height": 880000
}
```

#### `GET /tokens/list_cached` (Unstable)

List all tokens with optional pagination and sorting. Returns a direct JSON array.

**Parameters:**
- `limit` — Maximum results (default: 250)
- `offset` — Pagination offset (default: 0)
- `by` — Sort field: `name`, `symbol`, `tvl`, `volume`, `score`
- `order` — Sort direction: `asc`, `desc`

#### `GET /tokens/list_cached_by_ids` (Unstable)

List specific tokens by their IDs in a single request.

**Parameters:**
- `ids` — Comma-separated list of token IDs (hex strings)
- `by` — Sort field
- `order` — Sort direction

#### `GET /tokens/search_by_volume` (Unstable)

Search tokens by name or symbol, sorted by trade volume. Queries BCMR and CRC20 registries, then joins with live trade volume data.

**Parameters:**
- `search_query` — Token name or symbol to search for

**Response:**
```json
[
  {
    "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
    "name": "ExampleToken",
    "ticker": "EXT",
    "trade_volume": 1459676788
  }
]
```

#### `GET /tokens/search_cached` (Unstable)

Search tokens with optional filtering and sorting. Returns a direct JSON array.

**Parameters:**
- `q` — Search query string
- `limit` — Maximum results (default: 250)
- `offset` — Pagination offset (default: 0)
- `by` — Sort field: `name`, `symbol`, `tvl`, `volume`
- `order` — Sort direction: `asc`, `desc`

**Response:**
```json
[
  {
    "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
    "name": "ExampleToken",
    "symbol": "EXT",
    "decimals": 8
  }
]
```

### Transaction Endpoints

#### `GET /tx/latest` (Stable)

Get the latest Cauldron transactions, optionally filtered by token.

**Parameters:**
- `limit` — Maximum results (default: 100, max: 10000)
- `offset` — Pagination offset (default: 0)
- `token` — 32-byte token ID to filter by (optional)

**Notes:** `blockhash` is `null` for unconfirmed transactions. `timestamp_guess` is an estimate derived from block time.

**Response:**
```json
[
  {
    "txid": "94a933a0fa55093a0965eb867f1b9cac2bb07488ced4825bc31f86c9371f76aa",
    "blockhash": "000000000000000002b4e6c0a1f4b3d2e5c7f891a2b3c4d5e6f7a8b9c0d1e2f3",
    "timestamp_guess": 1709468902
  }
]
```

### User Endpoints

#### `GET /user/unique_addresses` (Unstable)

Get the count of unique addresses that have ever interacted with Cauldron, grouped by month.

**Response:**
```json
[
  { "month": "2024-01", "count": 1234 },
  { "month": "2024-02", "count": 1456 }
]
```

### Value Locked Endpoints

#### `GET /valuelocked` (Stable)

Get total satoshis locked across all tokens.

**Parameters:**
- `time` — Unix timestamp (optional)

**Response:**
```json
{ "satoshis": 1459676788 }
```

#### `GET /valuelocked/<token>` (Stable)

Get total value locked for a single token.

**Parameters:**
- `token` — Token identifier/category
- `time` — Unix timestamp (optional)

**Response:**
```json
{
  "satoshis": 1459676788,
  "token_amount": 19,
  "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92"
}
```

### Volume Endpoints

#### `GET /volume` (Stable)

Get total volume for all tokens in a time period.

**Parameters:**
- `start` — Unix timestamp for period start (optional, default: 24 hours ago)
- `end` — Unix timestamp for period end (optional, default: now)

**Response:**
```json
{
  "total_volume_sats": 1459676788,
  "period_start": 1640995200,
  "period_end": 1641081600
}
```

#### `GET /volume/<token>` (Stable)

Get volume for a specific token in a time period.

**Parameters:**
- `token` — Token identifier/category
- `start` — Unix timestamp for period start (optional, default: 24 hours ago)
- `end` — Unix timestamp for period end (optional, default: now)

**Response:**
```json
{
  "volume_sats": 1459676788,
  "volume_tokens": 12345,
  "token_id": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
  "period_start": 1640995200,
  "period_end": 1641081600
}
```

---

## BCMR Endpoints

Base URL: `/bcmr`

#### `GET /token/<category>` (Stable)

Fetch BCMR metadata for a token from the on-chain registry.

**Parameters:**
- `category` — Token ID or symbol

Returns `null` if no BCMR data is found.

**Response:**
```json
{
  "description": "Cauldron socks",
  "filemeta": {
    "actual_hash": "c705cc90a56ac7ef9a15ef90ebbc8ba7e60e4c622e5464d52d8baf7887949fcc",
    "expected_hash": "c705cc90a56ac7ef9a15ef90ebbc8ba7e60e4c622e5464d52d8baf7887949fcc",
    "source": "onchain"
  },
  "name": "Cauldron Socks",
  "token": {
    "category": "b79bfc8246b5fc4707e7c7dedcb6619ef1ab91f494a790c20b0f4c422ed95b92",
    "decimals": 0,
    "symbol": "SOCK"
  },
  "uris": {
    "icon": "https://sock.cauldron.quest/sock.png",
    "web": "https://cauldron.quest"
  }
}
```

#### `GET /token/<category>/all` (Unstable)

Fetch BCMR data for a token from all registries (including OTR). Returns an array of BCMR entries, or an empty array if none found.

---

## Oracle Endpoints

Base URL: `/oracle`

### BCH/USD Oracle (oracles.cash)

#### `GET /cash/closest` (Stable)

Get the closest BCH/USD price from the oracles.cash feed for a given timestamp.

**Parameters:**
- `timestamp` — Unix timestamp in seconds (optional, defaults to now)

**Notes:** `oracle_price` is in **cents**. Divide by 100 to get USD. Returns `null` if no data available.

#### `GET /cash/history` (Stable)

Get historical BCH/USD prices from the oracles.cash feed.

**Parameters:**
- `start` — Unix timestamp for period start
- `end` — Unix timestamp for period end (optional, defaults to now)
- `stepsize` — Seconds per interval (optional)

**Notes:** `oracle_price` values are in cents.

**Response:**
```json
[
  { "oracle_timestamp": 1709468902, "oracle_price": 38424, "message_sequence": 12345 },
  { "oracle_timestamp": 1709472502, "oracle_price": 38501, "message_sequence": null }
]
```

### Delphi Oracle (Token-Specific)

#### `GET /delphi/<token>/history` (Unstable)

Get historical oracle prices for a given token.

**Parameters:**
- `token` — 32-byte token ID of the oracle contract
- `start` — Unix timestamp for period start
- `end` — Unix timestamp for period end (optional, defaults to now)
- `stepsize` — Seconds per interval (optional)

**Known Oracle Contract IDs:**
- BCH/USD: `d0d46f5cbd82188acede0d3e49c75700c19cb8331a30101f0bb6a260066ac972`

**Notes:** `oracle_price` values are in cents. Divide by 100 to convert to USD.

**Response:**
```json
[
  { "time": 1709468902, "price": 64320, "txid": "...", "blockhash": "...", "sequence": 12345 }
]
```

#### `GET /delphi/closest` (Stable)

Get the closest oracle price for a given token and timestamp.

**Parameters:**
- `token_id` — 32-byte token ID of the oracle contract
- `timestamp` — Unix timestamp (optional, defaults to now)

**Notes:** `oracle_price` is in cents. Divide by 100 to get USD. Returns `null` if no oracle data found.

**Response:**
```json
{
  "oracle_timestamp": 1709468902,
  "oracle_price": 64320,
  "oracle_sequence": 12345,
  "token_id": "d0d46f5cbd82188acede0d3e49c75700c19cb8331a30101f0bb6a260066ac972",
  "txid": "...",
  "blockhash": "..."
}
```

---

## Moria Endpoints

Base URL: `/moria`

Moria is a lending protocol built on Cauldron infrastructure.

#### `GET /history` (Unstable)

Get global Moria action history with pagination and optional NFT hash filtering.

**Parameters:**
- `offset` — Number of entries to skip (default: 0)
- `limit` — Maximum entries to return (default: 50, max: 200)
- `nfth` — Comma-separated list of borrower NFT hashes (64-char hex each) to filter by

#### `GET /loan/<borrower_hash>/history` (Unstable)

Get full loan history for a given borrower NFT hash.

**Parameters:**
- `borrower_hash` — 64-character hex string (32-byte P2NFTH hash identifying the loan)

Returns an array of all actions (borrow, repay, redeem, refinance, add_collateral) for this loan, sorted by timestamp.

#### `GET /loans/active` (Unstable)

List all active (not yet repaid/redeemed) loans.

#### `GET /stats` (Unstable)

Get Moria protocol statistics.

---

## Root Endpoint

#### `GET /health` (Unstable)

Health check endpoint for load balancer monitoring.

**Response when healthy (HTTP 200):**
```json
{
  "status": "healthy",
  "indexed_height": 880000,
  "chain_tip": 880000,
  "version": "0.2.0"
}
```

**Response when syncing (HTTP 503):**
```json
{
  "status": "syncing",
  "indexed_height": 850000,
  "chain_tip": 880000,
  "version": "0.2.0"
}
```

---

## Related pages

- [cauldron-intro](cauldron-intro.md)
- [cashtokens](cashtokens.md)
- [cashtokens-intro](cashtokens-intro.md)
- [bcmr-spec](bcmr-spec.md)
- [bcmr-examples](bcmr-examples.md)
- [bitcoin-cash](bitcoin-cash.md)
