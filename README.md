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
| SimpleSwap     | [`0x11D6b705Da2c4Be5AdaFBC2AbaC95bC8c9bb539F`](https://sepolia.etherscan.io/address/0x11D6b705Da2c4Be5AdaFBC2AbaC95bC8c9bb539F) |
| Token A (ERC20)| [`0x8d25C5307A3D5A1f5caef06EbA440C3c4a0bde2E`](https://sepolia.etherscan.io/address/0x8d25C5307A3D5A1f5caef06EbA440C3c4a0bde2E) |
| Token B (ERC20)| [`0xf98D3CF8Cd25748937Ca879C9dAe8a8F313C9A12`](https://sepolia.etherscan.io/address/0xf98D3CF8Cd25748937Ca879C9dAe8a8F313C9A12) |

✅ **Verified on Sepolia using verification contract:**  
[Verification successful on Etherscan](https://sepolia.etherscan.io/tx/0x58f2bbd2352c00693bbb35266c60d3d4825bbb054d369875681281c9b15403e8)

## 📁 File Structure

- `SimpleSwap.sol`: Complete source code of the LP token contract with swap and liquidity functionality.
- `TokenA.sol`: Complete source code of Token A (TKA) contract.
- `TokenB.sol`: Complete source code of Token B (TKB) contract.

## 📚 Key Functions

| Function | Description |
|---------|-------------|
| `addLiquidity(...)` | Adds tokens to the pool and mints LP tokens |
| `removeLiquidity(...)` | Burns LP tokens and returns proportional token amounts |
| `swapExactTokensForTokens(...)` | Swaps an exact input amount for as many output tokens as possible |
| `getPrice(...)` | Returns price of one token in terms of the other |
| `_computeLiquidityAmounts(...)` | Internal logic to calculate optimal liquidity ratios |

## 📌 Notes

- Tokens must be pre-approved before calling `addLiquidity` or `swapExactTokensForTokens`.
- This contract does not charge any fees and is not production-ready.

---

### 👨‍💻 Author

**Gaston Gorosito**

---

### 📝 License

MIT License
