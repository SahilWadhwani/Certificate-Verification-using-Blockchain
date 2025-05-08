# Certificate Verification using Blockchain

## Project Description

This project implements a decentralized certificate verification system leveraging the Ethereum blockchain, Solidity smart contracts, and IPFS (via Pinata) to ensure tamper-proof and transparent validation of certificates. It features a user-friendly web-based DApp built with Streamlit and Web3.py, secured using Firebase Authentication. The system is designed to eliminate certificate fraud through blockchain's immutability and cryptographic hashing.

## Features

* Decentralized certificate issuance and verification.
* Secure access control with Firebase Authentication.
* Tamper-proof storage using IPFS (Pinata).
* Web-based interface using Streamlit.
* Multi-node blockchain network using Geth.
* Local signing for enhanced security.
* Fraud detection via cryptographic hash comparison.

## Technologies Used

* Solidity for smart contracts.
* Geth (Go-Ethereum) for private blockchain setup.
* IPFS and Pinata for decentralized file storage.
* Web3.py for blockchain interactions.
* Streamlit for front-end DApp.
* Firebase for authentication.
* Docker for containerization.
* Python 3.10 for backend logic.

## System Architecture

The system has two main nodes (Host A and Host B) running Geth on a private blockchain. The nodes communicate over a local area network (LAN) and share blocks using peer-to-peer gossip. Certificate files are stored on IPFS, and their hashes are recorded on-chain for immutability. The Streamlit DApp interacts with blockchain nodes using Web3.py and utilizes Firebase for secure authentication.

## Prerequisites

* Python 3.10+
* Node.js and npm
* Geth (Go-Ethereum)
* Docker and Docker Compose
* Truffle
* Firebase account

## Setup and Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/SahilWadhwani/Certificate-Verification-using-Blockchain.git
   cd Certificate-Verification-Blockchain
   ```
2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   npm install
   ```
3. Set up Geth nodes:

   ```bash
   geth --datadir dataA init genesis.json
   ```
4. Configure Firebase Authentication with environment variables.
5. Start IPFS daemon or Pinata service.

## Configuration

1. Set up the `.env` file in the root directory:

   ```bash
   DEPLOYER_PRIVATE_KEY=0xYourPrivateKey
   RPC_URL=http://localhost:8545
   and other API keys (Pinata, Firebase, etc)
   ```
2. Update Truffle configuration in `truffle-config.js`.

## Running the Project

### Start Geth Nodes

* Host A:

  ```bash
  geth --datadir dataA --networkid 1337 --http --http.addr 0.0.0.0 --http.port 8545 --http.api "eth,net,web3" --port 30303 --mine --miner.threads 1 console
  ```
* Host B:

  ```bash
  geth --datadir dataB --networkid 1337 --http --http.addr 0.0.0.0 --http.port 8545 --http.api "eth,net,web3" --port 30304 --mine console
  ```

### Run Streamlit DApp

```bash
streamlit run application/app.py
```

## Project Workflow

1. Institute logs in and issues a certificate (PDF + metadata).
2. PDF is pinned to IPFS, hash is recorded on-chain.
3. Verifier checks the certificate by UID or PDF hash.
4. Blockchain nodes propagate transactions, ensuring redundancy.

## Smart Contract Details

* `Certification.sol`: Defines `generateCertificate` and `getCertificateById`.
* Uses OpenZeppelin libraries for secure access.

## Testing and Validation

* Unit tests written using Truffle.
* Test command:

  ```bash
  truffle test
  ```
* Functional tests using Postman for API calls.

## Troubleshooting

* "Authentication needed": Ensure your private key is correctly set in `.env`.
* "Peer count is zero": Check Geth node connectivity.

## Future Enhancements

* Integrate mobile DApp with MetaMask.
* Implement a certificate revocation feature.

