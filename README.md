# ClinicChain — Clinic Data Management System with Blockchain

A full-stack clinic management system where every patient medical record is
cryptographically hashed and anchored to an Ethereum smart contract,
making records tamper-proof and auditable.

---

##  Tech Stack

| Layer      | Technology                          |
|------------|--------------------------------------|
| Frontend   | React.js, Axios, React Router        |
| Backend    | Node.js, Express.js                  |
| Database   | MySQL                                |
| Blockchain | Solidity, Ganache, Hardhat, ethers.js|
| Auth       | JWT, bcrypt                          |
| Storage    | IPFS (medical file attachments)      |

---

## Features

-  **Tamper-proof records** — SHA-256 hash of every record written to Ethereum smart contract
-  **Patient-controlled access** — patients grant/revoke doctor access via smart contract
-  **Immutable audit trail** — all actions logged on-chain
-  **Role dashboards** — separate views for Patient, Doctor, and Admin
-  **IPFS file storage** — X-rays and documents stored off-chain

---

##  Smart Contracts

| Contract                  | Purpose                          |
|---------------------------|----------------------------------|
| `PatientRecordContract`   | Store and verify record hashes   |
| `AccessControlContract`   | Manage doctor access permissions |
| `AuditLogContract`        | Immutable on-chain action log    |

---

##  Setup

### Prerequisites
- Node.js >= 18
- MySQL
- Ganache (local Ethereum node)
- IPFS node (local)

### 1. Clone the repo
```bash
git clone https://github.com/your-username/clinicchain.git
cd clinicchain
```

### 2. Start Ganache
Open Ganache → New Workspace → port `7545`

### 3. Deploy contracts
```bash
cd blockchain
npm install
npx hardhat run scripts/deploy.js --network ganache
```

### 4. Backend setup
```bash
cd backend
npm install
cp .env.example .env
# Fill in DATABASE_URL, JWT_SECRET, GANACHE_PRIVATE_KEY, CONTRACT_ADDRESSES
npm run dev
```

### 5. Frontend setup
```bash
cd frontend
npm install
npm start
```

---

##  Environment Variables (`.env`)

```env
DATABASE_URL=mysql://root:password@localhost:3306/clinicchain
JWT_SECRET=your_secret_here
GANACHE_RPC_URL=http://127.0.0.1:7545
DEPLOYER_PRIVATE_KEY=<account_1_private_key_from_ganache>
PATIENT_RECORD_CONTRACT=0x...
ACCESS_CONTROL_CONTRACT=0x...
AUDIT_LOG_CONTRACT=0x...
```

>  Use the **exact private key from Ganache Account 1** — not a mnemonic-derived key.

---

##  Roles

| Role    | Capabilities                                              |
|---------|-----------------------------------------------------------|
| Patient | View records, verify integrity, manage doctor access      |
| Doctor  | Add records, view authorised patients, manage appointments|
| Admin   | Manage users, view all audit logs                         |

---


---

##  Notes

- Smart contracts are deployed to **local Ganache** (not a public testnet)
- `dotenv` must be pinned to `^16` — v17 causes silent env failures
- Route order matters: define `/records/mine` **before** `/records/:id`

---
