# 📱 React Native SDK Assignment (Mock-Only, Historical Prices Only)

We’re evaluating your ability to design and build a **modular SDK** and integrate it into a modern **React Native demo app**.

> ✅ No backend required — all data is mocked.  
> ✅ No need to publish a real package — just structure the SDK cleanly and use it in a demo app.  

---

## 🎯 Objective

Build a **React Native SDK** that provides token pricing functionality using **mocked data**, then showcase its usage in a simple demo app styled with **nativewind** (Tailwind for React Native).

---

## ✅ Requirements

### Part 1: SDK (inside `/sdk` folder)

#### Core Features
- [ ] Fetch current price of one or more tokens.
- [ ] Support configurable currency (e.g., `USD`).
- [ ] Simulate network delay (~500ms).
- [ ] Load all data from a local `mockData.json` file (see below).
- [ ] Expose a `setup(config: ModuleConfig)` method:

```ts
interface ModuleConfig {
  currency: string;
  mockMode: boolean;
  cacheTTL: number; // in seconds
}
```

#### Caching
 Use AsyncStorage or react-native-mmkv to cache:

#### Historical price data
- TTL-based cache invalidation (default: 5 minutes, configurable).  
- Manual cache invalidation:
```ts
invalidateCache(tokenSymbols: string[]): void
```
-  Cache key format:
```ts
{tokenSymbol}_{currency}
e.g., BTC_USD
```


#### React Hook

- Provide a typed hook to fetch historical data:
```ts
const { data, isLoading, error } = useTokenPrice(['BTC', 'ETH'], 'USD');
```

#### BONUS (Not Required)
 Retry failed mock requests (up to 2 retries with exponential backoff).
 Unit tests (SDK only, not the app).

---

### Part 2: Demo App
 - Display a list of token prices (e.g., BTC, ETH).
 - Use your SDK to fetch and display the data.
 - Add a button to manually invalidate the cache.
 - Use nativewind for styling.

--- 

### 🧪 Mock Data
Create a file called mockData.json inside your SDK folder with the following content:
```ts
{
  "BTC": {
      "currency": "USD",
      "symbol": "BTC",
      "price": 85233,
      "lastUpdated": "2025-03-23T16:32:54.000Z"
    },
    "ETH": {
      "currency": "USD",
      "symbol": "ETH",
      "price": 2003.29,
      "lastUpdated": "2025-03-23T16:33:37.000Z"
    }
}
```
--- 

### 📘 Deliverables
- A GitHub repo or ZIP with:
  - sdk/ folder
  - App.tsx demo
  - mockData.json
  - README.md with:
    - Setup instructions
    - How to use the SDK
