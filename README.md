# ETHKIPUMOD3

**ETHKIPU MOD 3 – SimpleSwap**  
A minimal decentralized exchange (DEX) smart contract for swapping ERC20 token pairs and minting LP tokens. This project is a simplified version inspired by Uniswap V2.

## ✨ Features

- Add/remove liquidity to token pairs
- Issue LP tokens (TokenL - TKL) to liquidity providers
- Calculate optimal token amounts based on pool reserves
- Perform exact token swaps with slippage protection
- Internal reserve tracking using a canonical `(token0, token1)` mapping
- Uses Babylonian square root for initial liquidity calculation
- Gas-optimized with minimal duplication and storage writes

## 🔧 Tech Stack

- Solidity ^0.8.27
- OpenZeppelin ERC20 & Ownable
- Verified and deployed on Sepolia testnet

## 📦 Contract Addresses

| Component      | Address |
|----------------|---------|
| SimpleSwap     | [`0x92DDE44a13729C5D3F47dE497E990088A7D20AFD`](https://sepolia.etherscan.io/address/0x92DDE44a13729C5D3F47dE497E990088A7D20AFD) |
| Token A (ERC20)| [`0x8d25C5307A3D5A1f5caef06EbA440C3c4a0bde2E`](https://sepolia.etherscan.io/address/0x8d25C5307A3D5A1f5caef06EbA440C3c4a0bde2E) |
| Token B (ERC20)| [`0xf98D3CF8Cd25748937Ca879C9dAe8a8F313C9A12`](https://sepolia.etherscan.io/address/0xf98D3CF8Cd25748937Ca879C9dAe8a8F313C9A12) |

✅ **Verified on Sepolia using verification contract:**  
[Verification successful on Etherscan](https://sepolia.etherscan.io/tx/0xc61e375fe9373cd23fc053fb03e0acff88ff204cfa2a7036fa582ca13fb8d8a8)

## 📁 File Structure

- `SimpleSwap.sol`: Complete source code of the LP token contract with swap and liquidity functionality.
- `TokenA.sol`: Complete source code of Token A (TKA) contract.
- `TokenB.sol`: Complete source code of Token B (TKB) contract.

## 📚 Key Functions

### `addLiquidity(...)`

Adds tokens to the pool and mints LP tokens proportionally.

**Inputs:**
- `address tokenA` — First ERC20 token address  
- `address tokenB` — Second ERC20 token address  
- `uint amountADesired` — Desired amount of `tokenA` to add  
- `uint amountBDesired` — Desired amount of `tokenB` to add  
- `uint amountAMin` — Minimum acceptable `tokenA` (slippage protection)  
- `uint amountBMin` — Minimum acceptable `tokenB` (slippage protection)  
- `address to` — Recipient of LP tokens  
- `uint deadline` — Unix timestamp after which the transaction is invalid

**Returns:**
- `uint amountA` — Actual amount of `tokenA` added  
- `uint amountB` — Actual amount of `tokenB` added  
- `uint liquidity` — Amount of LP tokens minted  

---

### `removeLiquidity(...)`

Burns LP tokens and returns the corresponding token pair to the user.

**Inputs:**
- `address tokenA` — First ERC20 token address  
- `address tokenB` — Second ERC20 token address  
- `uint liquidity` — Amount of LP tokens to burn  
- `uint amountAMin` — Minimum acceptable `tokenA` to receive  
- `uint amountBMin` — Minimum acceptable `tokenB` to receive  
- `address to` — Recipient of the withdrawn tokens  
- `uint deadline` — Unix timestamp after which the transaction is invalid

**Returns:**
- `uint amountA` — Amount of `tokenA` returned  
- `uint amountB` — Amount of `tokenB` returned  

---

### `swapExactTokensForTokens(...)`

Swaps an exact input amount of one token for as many output tokens as possible.

**Inputs:**
- `uint amountIn` — Exact amount of input tokens to swap  
- `uint amountOutMin` — Minimum acceptable amount of output tokens (slippage protection)  
- `address[] path` — Must be length 2: `[tokenIn, tokenOut]`  
- `address to` — Recipient of the output tokens  
- `uint deadline` — Unix timestamp after which the transaction is invalid

**Returns:**
- `uint[] amounts` — `[amountIn, amountOut]` of tokens swapped  

---

### `getPrice(...)`

Returns the current price of one token in terms of another.

**Inputs:**
- `address tokenA` — Token to price  
- `address tokenB` — Token used as reference

**Returns:**
- `uint price` — Price of `tokenA` in `tokenB` units (scaled by 1e18)  

---

### `getAmountOut(...)`

Calculates the output amount given an input amount and pool reserves.

**Inputs:**
- `uint amountIn` — Input token amount  
- `uint reserveIn` — Reserve of the input token in the pool  
- `uint reserveOut` — Reserve of the output token in the pool

**Returns:**
- `uint amountOut` — Amount of output token received  

# 📘 Contract Events

This contract emits events for all major interactions so frontends, indexers, and external systems can listen and react to DEX operations in real time.

---

### `LiquidityAdded(...)`

Emitted when a user adds liquidity to the pool and receives LP tokens.

**Inputs:**
- `address provider` Address that added the liquidity  
- `address tokenA` Address of token A  
- `address tokenB` Address of token B  
- `uint amountA` Actual amount of token A supplied  
- `uint amountB` Actual amount of token B supplied  
- `uint liquidity` Amount of LP tokens minted  

---

### `LiquidityRemoved(...)`

Emitted when a user removes liquidity and burns LP tokens.

**Inputs:**
- `address provider` Address that removed the liquidity  
- `address tokenA` Address of token A  
- `address tokenB` Address of token B  
- `uint amountA` Amount of token A returned  
- `uint amountB` Amount of token B returned  
- `uint liquidityBurned` LP tokens burned  

---

### `Swap(...)`

Emitted when a user swaps one token for another.

**Inputs:**
- `address sender` Address initiating the swap  
- `address tokenIn` Token being sold  
- `address tokenOut` Token being bought  
- `uint amountIn` Input token amount  
- `uint amountOut` Output token amount received  
- `address to` Address that received the output token  

---

## Notes

- Tokens must be pre-approved before calling `addLiquidity` or `swapExactTokensForTokens`.
- This contract does not charge any fees and is not production-ready.
- Originally, the verification contract's getAmountOut interface differed from the requested code. To test compatibility, I wrote SimpleSwap_ForVerify.sol, a version of the contract adapted to successfully interact with the original verification function.
- After verifying functionality, I updated the verification contract to match the requested code exactly. This updated verification contract version is available as Verify_Updated.sol.

---

### 👨‍💻 Author

**Gaston Gorosito**

---

### 📝 License

MIT License
