# Project Title: Decentralized Secure Mobile Chat Application
<img width="1408" height="768" alt="2" src="https://github.com/user-attachments/assets/fdd0a46c-81c7-4c39-b51f-e7c6675f181d" />

## 1. System Architecture Overview
This project is a peer-to-peer (P2P) messaging system that removes the need for a central server[cite: 1]. It is designed as a mobile application to overcome the 5MB storage limits found in standard web browsers[cite: 1].

### Layer 1: The Client Layer (Mobile App)
* **Technology**: Svelte (for the user interface) and Capacitor.js (to turn the code into a mobile app)[cite: 1].
* **Function**: This is where the user interacts with the app[cite: 1]. Unlike a browser, the mobile app can access the phone’s internal storage to save larger amounts of data[cite: 1].
* **Security**: All encryption and decryption happen locally on the user's phone using the SEA (Security, Encryption, and Authorization) module[cite: 1].

### Layer 2: The Communication Layer (Signaling)
* **Technology**: Gun.js and WebRTC[cite: 1].
* **Function**: Gun.js creates a "mesh network" where every phone acts as a small server[cite: 1]. It uses WebRTC to send data directly from one phone to another without a middleman[cite: 1].
* **Signaling**: Instead of sending the whole message through the network, Gun.js is used to send the IPFS address (CID) of the message.

### Layer 3: The Persistence Layer (Distributed Storage)
* **Technology**: IPFS (Interplanetary File System).
* **Function**: This layer solves the "Offline Problem." In standard P2P, both users must be online at the same time.
* **How it works**: Encrypted messages are stored on IPFS nodes. This ensures that even if the receiver is offline, the message is held safely in the decentralized network until they log back in.

## 2. Detailed Technical Workflow (Step-by-Step)

### Step 1: User Registration (No Central Database)
* The user enters their Phone Number (acting as an alias) and a Password[cite: 1].
* The app uses the SEA module to generate a unique Cryptographic Key Pair (Public Key and Private Key) based on these details[cite: 1].
* **Public Key**: Shared with the network so others can find you[cite: 1].
* **Private Key**: Stored only on your phone to prove you own the account and to unlock your messages[cite: 1].

### Step 2: Sending a Message (Encryption & Upload)
* User A writes a message and hits 'Send'.
* The app encrypts the text using User B’s Public Key.
* The encrypted data is uploaded to IPFS, which returns a CID (Content Identifier). This CID is like a unique digital fingerprint or address for that specific message.

### Step 3: Message Routing (The Handshake)
* User A’s app sends only the CID to User B via the Gun.js network.
* Because the CID is very small, it moves through the P2P network almost instantly with very low latency.

### Step 4: Receiving and Decoding
* When User B’s app receives the CID, it automatically pulls the encrypted data from IPFS.
* The app then uses User B’s Private Key to decrypt the data.
* The message becomes readable text on User B's screen.

## 3. Why This Is Better (Key Advantages)
* **Zero Server Costs**: Since the users provide the storage and bandwidth, there are no expensive central servers to maintain[cite: 1].
* **Privacy by Design**: Because only the user has the Private Key, not even the developers can read the chats[cite: 1].
* **No Single Point of Failure**: If one part of the network goes down, the rest of the users stay connected[cite: 1].
* **Unlimited Storage**: By moving from a browser (5MB limit) to a Mobile App with IPFS integration, users can share photos and large files without running out of space[cite: 1].
