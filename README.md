# BitRealm Game Smart Contract

A comprehensive blockchain-based gaming platform that enables players to collect, trade, and battle with digital assets across multiple game worlds.

## Overview

BitRealm is a full-featured gaming ecosystem implemented as a smart contract that combines NFT-based assets, player progression systems, multiple game worlds, and trading mechanisms. The platform provides a secure and decentralized environment for players to engage with digital assets and compete across various game worlds.

## Core Features

### NFT Asset System

- Unique digital assets with customizable attributes
- Experience-based leveling system for assets
- Rarity classifications
- Power level mechanics
- World-specific asset compatibility

### Player Avatar System

- Personalized player profiles
- Experience and leveling progression
- Achievement tracking
- Equipment management
- World access permissions

### Game Worlds

- Multiple distinct gaming environments
- Entry requirements for each world
- Active player tracking
- Reward distribution system
- World-specific leaderboards

### Trading System

- Secure peer-to-peer asset trading
- Time-based trade expiration
- STX-based pricing
- Trade status tracking
- Ownership verification

### Leaderboard System

- Global player rankings
- Score-based progression
- Achievement tracking
- Reward distribution
- Paginated leaderboard views

## Technical Specifications

### Constants

- Maximum level cap: 100
- Maximum experience per level: 1,000
- Base experience required: 100
- Rate limit window: 144 blocks (approximately 24 hours)
- Maximum calls per window: 100

### Security Features

- Row-level security
- Rate limiting mechanisms
- Protocol admin system
- Input validation
- Authorization checks

### Events

The contract emits events for major actions:

- Asset minting
- Asset transfers
- Avatar creation
- Experience gains
- Level-ups
- World creation
- Trade activities

## Smart Contract Functions

### Asset Management

```clarity
(mint-bitrealm-asset (name (string-ascii 50))
                     (description (string-ascii 200))
                     (rarity (string-ascii 20))
                     (power-level uint)
                     (world-id uint)
                     (attributes (list 10 (string-ascii 20))))
```

Creates a new game asset with specified properties.

### Avatar System

```clarity
(create-avatar (name (string-ascii 50))
               (world-access (list 10 uint)))
```

Creates a new player avatar with initial properties.

### Experience System

```clarity
(update-avatar-experience (avatar-id uint)
                         (experience-gained uint))
```

Updates an avatar's experience points and handles level-ups.

### Trading System

```clarity
(create-trade (asset-id uint)
              (price uint)
              (expiry uint))
```

Creates a new trade listing for an asset.

```clarity
(execute-trade (trade-id uint))
```

Executes a trade between buyer and seller.

## Error Codes

| Code | Description        |
| ---- | ------------------ |
| u1   | Not authorized     |
| u2   | Invalid game asset |
| u3   | Insufficient funds |
| u4   | Transfer failed    |
| u5   | Leaderboard full   |
| u6   | Already registered |
| u7   | Invalid reward     |
| u8   | Invalid input      |
| u9   | Invalid score      |
| u10  | Invalid fee        |

## Usage Examples

### Creating a New Asset

```clarity
(contract-call? .bitrealm mint-bitrealm-asset
    "Legendary Sword"
    "A powerful ancient weapon"
    "legendary"
    u100
    u1
    (list "sharp" "magical" "ancient"))
```

### Creating a Player Avatar

```clarity
(contract-call? .bitrealm create-avatar
    "CryptoWarrior"
    (list u1 u2 u3))
```

### Creating a Trade

```clarity
(contract-call? .bitrealm create-trade
    u1  ;; asset-id
    u1000  ;; price in STX
    u1000)  ;; expiry block height
```

## Best Practices

1. **Asset Management**

   - Always verify asset ownership before operations
   - Maintain proper metadata for all assets
   - Use appropriate rarity classifications

2. **Trading**

   - Set reasonable expiration times
   - Verify sufficient balances
   - Check asset availability

3. **Experience System**

   - Balance experience gains
   - Implement proper level-up mechanics
   - Maintain fair progression

4. **Security**
   - Use rate limiting for sensitive operations
   - Implement proper access controls
   - Validate all inputs

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
