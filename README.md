# base-smart-contracts-2025

Smart contract templates and utilities for Base blockchain development - 2025 edition

## Overview

This repository contains a comprehensive collection of smart contract templates, utilities, and development tools specifically designed for the Base blockchain ecosystem. Built with modern Solidity practices and optimized for Base's Layer 2 infrastructure.

## Features

### Core Templates
- **ERC-20 Token Contracts**: Standard and advanced token implementations
- **ERC-721 NFT Contracts**: Basic and feature-rich NFT contracts
- **ERC-1155 Multi-Token**: Efficient multi-token standard implementations
- **Governance Contracts**: DAO and voting mechanism templates
- **DeFi Protocols**: DEX, lending, and yield farming contracts

### Base-Specific Optimizations
- Gas-optimized contract designs for L2 efficiency
- Cross-chain bridge integration utilities
- Base fee structure considerations
- Optimism compatibility layers

### Development Tools
- Hardhat configuration for Base networks
- Deployment scripts and migration tools
- Testing frameworks and mock contracts
- Security audit checklists

## Quick Start

```bash
# Clone the repository
git clone https://github.com/wearedood/base-smart-contracts-2025.git
cd base-smart-contracts-2025

# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run tests
npx hardhat test

# Deploy to Base testnet
npx hardhat run scripts/deploy.js --network base-goerli
```

## Contract Templates

### ERC-20 Token
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract BaseToken is ERC20, Ownable {
    constructor(
        string memory name,
        string memory symbol,
        uint256 initialSupply
    ) ERC20(name, symbol) {
        _mint(msg.sender, initialSupply * 10**decimals());
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

### NFT Collection
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract BaseNFT is ERC721, Ownable {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    string private _baseTokenURI;
    uint256 public maxSupply;
    uint256 public mintPrice;

    constructor(
        string memory name,
        string memory symbol,
        uint256 _maxSupply,
        uint256 _mintPrice
    ) ERC721(name, symbol) {
        maxSupply = _maxSupply;
        mintPrice = _mintPrice;
    }

    function mint(address to) public payable {
        require(_tokenIds.current() < maxSupply, "Max supply reached");
        require(msg.value >= mintPrice, "Insufficient payment");

        _tokenIds.increment();
        uint256 newTokenId = _tokenIds.current();
        _mint(to, newTokenId);
    }
}
```

## Network Configuration

### Base Mainnet
- **Chain ID**: 8453
- **RPC URL**: https://mainnet.base.org
- **Block Explorer**: https://basescan.org

### Base Goerli Testnet
- **Chain ID**: 84531
- **RPC URL**: https://goerli.base.org
- **Block Explorer**: https://goerli.basescan.org
- **Faucet**: https://bridge.base.org

## Security Considerations

- All contracts use OpenZeppelin's audited implementations
- Reentrancy protection on all external calls
- Access control mechanisms properly implemented
- Gas optimization without compromising security
- Comprehensive test coverage (>95%)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add comprehensive tests
4. Ensure all tests pass
5. Submit a pull request

## License

MIT License - see LICENSE file for details

## Support

For questions and support:
- GitHub Issues: [Create an issue](https://github.com/wearedood/base-smart-contracts-2025/issues)
- Documentation: [Wiki](https://github.com/wearedood/base-smart-contracts-2025/wiki)
- Community: [Discord](https://discord.gg/base)

---

**Built for Base Builders 2025** 🔵
