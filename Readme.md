# StealthPass Protocol Documentation

## Overview
StealthPass is an on-chain event ticketing platform designed for anonymous users, Web2 users, and Web3 users. It offers a seamless user experience comparable to platforms like Luma, leveraging advanced cryptographic techniques like Fully Homomorphic Encryption (FHE) and Account Abstraction (AA) to ensure privacy and interoperability.

StealthPass enables event organizers to host events and users to securely purchase tickets while maintaining anonymity or interacting through traditional Web3 wallets. For anonymous users, StealthPass ensures that their identities are hidden while allowing seamless event participation.

---

## Key Features

### 1. **Multi-User Support**
- **Web3 Users**: Standard wallet-based interaction.
- **Web2 Users**: Access via Account Abstraction (AA) and gasless transactions.
- **Anonymous Users**: Encrypted wallet addresses and secure ticket validation through FHE.

### 2. **Anonymity with FHE**
StealthPass uses Fully Homomorphic Encryption (FHE) to provide anonymity for users opting for the "Anon Ticket" option. This ensures:
- The encrypted holder address is stored on the blockchain.
- Ciphertext is securely stored on-chain using the Inco platform.
- Event organizers can verify encrypted tickets without revealing user identities.

### 3. **Decentralized Architecture**
- **Base Blockchain**: Stores encrypted holder addresses.
- **Inco Storage**: Functions as encrypted on-chain storage, similar to IPFS but with privacy-preserving capabilities.
- **Hyperlane SDK**: Ensures secure cross-chain messaging.

### 4. **Enhanced User Experience**
- Local wallet generation for ticket holding.
- Gasless transactions for Web2 users.
- Ticket details embedded in QR codes for easy verification.

### 5. **FHE Integration**
- User identity and ticket ownership verification via re-encryption calls provided by the Inco gateway.
- Composable cryptographic operations allow users to interact seamlessly across events, win lotteries, and more.

---

## Workflow

### User Journey

1. **User Registration**:
   - Connect a wallet using Privy (for Web3 users).
   - Generate a fresh wallet locally (for anonymous users).

2. **Ticket Purchase**:
   - Approve USDC transfer for the event contract.
   - Generate a pair of public and private keys for ticket holding.
   - Encrypt the public key using the `fhevmjs` SDK.

3. **Data Storage**:
   - The encrypted holder address is stored on Base.
   - Ciphertext is stored on-chain on Inco L1 via Hyperlane SDK.

4. **QR Code Generation**:
   - A QR code is generated containing:
     - EIP-712 signed message.
     - Hash of ticket information.

5. **Verification**:
   - The event organizer uses Inco’s re-encrypt functionality to securely verify ticket ownership.
   - Cross-checks the QR code, signature, and ticket information.

### Organizer Workflow

1. Deploy an event contract on Base blockchain.
2. Specify event details (e.g., name, ticket price, location).
3. Verify attendee tickets by using re-encryption calls and comparing against QR code data.
4. Conduct raffles or special activities using encrypted ticket data.

---

## Why Base Blockchain is a Key Choice

Base Blockchain plays a pivotal role in the StealthPass Protocol by serving as the backbone for storing essential credentials such as NFTs, USDC, and user-specific data. While Inco is utilized as an encrypted IPFS-like gateway for secure on-chain data storage, Base ensures on-chain accessibility and integrity. Moreover, Base's composability allows encrypted keys and data to be used in advanced computations, enabling unique features like secure identity management and future data retrieval without compromising privacy. By combining Base's robust blockchain capabilities with Inco's privacy-focused encrypted storage, StealthPass provides a seamless and secure user experience.

- **Composability**:
  - FHE allows cryptographic operations to be performed directly on encrypted data.
  - Enables seamless interoperability across events.
  
- **Identity Reusability**:
  - Users can reuse their encrypted addresses (eAddresses) for interactions within an event.
  - Supports advanced functionalities like prize distribution or anonymous messaging.

- **Flexibility**:
  - Base contracts can access unique keys and perform computations.
  - Users can retrieve results in the future without revealing sensitive data.

---

## Smart Contract Design

## Protocol Architecture and User Flow

StealthPass's architecture leverages the combined power of Base Blockchain, Inco's encrypted storage, and Hyperlane's cross-chain messaging to create a seamless event ticketing experience. The protocol's user flow ensures a smooth interaction for organizers and attendees, from ticket purchases to verifications:

1. **User Registration**: Users can connect wallets using Privy or generate local wallets for anonymous interactions.
2. **Ticket Storage**: Credentials, such as NFTs and USDC, are securely stored on Base Blockchain. Encrypted ticket data is offloaded to Inco, functioning as an IPFS-like storage but with enhanced privacy features.
3. **Verification Process**: During verification, the organizer uses re-encryption calls via the Inco gateway to validate encrypted credentials. This ensures privacy while enabling seamless event access.
4. **Composable Computations**: Base Blockchain enables advanced computations with encrypted data, allowing features like lotteries, identity management, and future data retrieval without exposing sensitive information.

---

### Key Components

#### 1. **OriginEventContract**
Handles ticket purchases and communication with Inco and Hyperlane.
- **Features**:
  - User registration and USDC payment handling.
  - Encrypted data storage and QR code generation.
  - Cross-chain message dispatch to Inco.

#### 2. **IncoEventContract**
Manages encrypted ticket verification and raffle operations.
- **Features**:
  - Deterministic key generation for token management.
  - Secure re-encryption for ticket validation.
  - Encrypted random number generation for raffles.

### Data Structures
- **Mappings**:
  - `tokenKeyToEaddressToAmount`: Maps token keys to encrypted addresses and ticket amounts.
  - `requestIdToStruct`: Tracks origin chain and event contract details for callback handling.

- **Events**:
  - `TokenProcessed`: Emitted when a ticket purchase is completed.
  - `TokenPurchased`: Emitted when a user buys a ticket.

---

## Technical Details

### Cross-Chain Messaging
- **Hyperlane SDK**:
  - Facilitates communication between Base and Inco L1.
  - Handles encrypted data transfer securely.

### FHE Integration
- **fhevmjs SDK**:
  - Generates public-private key pairs for ticket holding.
  - Encrypts public keys for storage.

- **TFHE Library**:
  - Performs re-encryption for ticket validation.
  - Supports composable cryptographic operations.

### QR Code Verification
1. QR code contains:
   - Encrypted ticket data.
   - Signature for validation.

2. Organizer verifies:
   - eAddress using re-encryption.
   - User’s signed message against the QR code data.

---

## Example Use Cases

### 1. **Anonymous Event Participation**
- Users can attend events without revealing personal information.
- Participate in lotteries and receive rewards using encrypted identities.

### 2. **Seamless Web2 Integration**
- Users interact using familiar Web2 interfaces while enjoying Web3 benefits like privacy and transparency.

### 3. **Raffles and Lotteries**
- Event organizers can randomly select winners using encrypted ticket data.

---

## Future Enhancements

1. **Enhanced Interoperability**:
   - Support for additional blockchains and cross-chain messaging protocols.

2. **Anonymous Communication**:
   - Enable attendees to communicate anonymously within events using eAddresses.

3. **Dynamic Pricing Models**:
   - Allow ticket prices to adjust based on demand or time.

4. **Integration with dApps**:
   - Collaborate with DeFi and NFT platforms for ticket resales and rewards.

---

## Conclusion
StealthPass redefines event ticketing with cutting-edge cryptography and blockchain technology. By leveraging FHE, Hyperlane, and AA wallets, it creates a user-friendly platform that prioritizes privacy, security, and composability. Whether for anonymous users, Web2 adopters, or seasoned Web3 enthusiasts, StealthPass ensures a seamless and secure ticketing experience.

