# ZK Identity Attestation DApp

A privacy-preserving identity verification system using zero-knowledge proofs. This decentralized application (DApp) allows users to prove their identity meets certain criteria (age, country of residence) without revealing sensitive personal information.

## 🔒 Privacy-First Design

This application demonstrates how zero-knowledge proofs can be used to verify identity claims while maintaining complete privacy. Users can prove they meet verification requirements without exposing their actual personal data.

## ✨ Features

- **Zero-Knowledge Proof Generation**: Generate cryptographic proofs of identity claims
- **Privacy-Preserving Verification**: Verify identity without revealing sensitive data
- **Interactive UI**: Step-by-step process showcasing the privacy mechanism
- **Mock Transactions**: Safe demonstration environment with no real-world value
- **On-Chain Attestations**: Store verification results on a simulated blockchain
- **Responsive Design**: Works on both desktop and mobile devices

## 🏗️ Architecture

The application consists of three main components:

### 1. ZK Circuit (Compact Language)
- **File**: `identity_att/src/identity_attestation.compact`
- **Purpose**: Defines the zero-knowledge circuit logic for identity verification
- **Technology**: Midnight's Compact language (conceptual implementation)

### 2. Backend API (Flask)
- **Directory**: `zk_identity_backend/`
- **Purpose**: Handles proof verification and attestation storage
- **Features**:
  - Mock proof generation and verification
  - SQLite database for attestation storage
  - RESTful API endpoints
  - CORS support for frontend integration

### 3. Frontend Interface (React)
- **Directory**: `zk_identity_frontend/`
- **Purpose**: User interface for the privacy-preserving verification process
- **Features**:
  - Step-by-step verification workflow
  - Privacy controls (show/hide sensitive data)
  - Real-time proof generation and verification
  - Responsive design with Tailwind CSS

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- Node.js 20+
- pnpm (for frontend package management)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd zk_identity_attestation
   ```

2. **Set up the backend**
   ```bash
   cd zk_identity_backend
   source venv/bin/activate
   pip install -r requirements.txt
   ```

3. **Set up the frontend**
   ```bash
   cd ../zk_identity_frontend
   pnpm install
   ```

### Running the Application

1. **Start the backend server**
   ```bash
   cd zk_identity_backend
   source venv/bin/activate
   python src/main.py
   ```
   The API will be available at `http://localhost:5000`

2. **Start the frontend development server**
   ```bash
   cd zk_identity_frontend
   pnpm run dev --host
   ```
   The application will be available at `http://localhost:5173`

## 🔧 API Endpoints

### GET /api/get-public-parameters
Returns public parameters for the verification system.

### POST /api/generate-mock-proof
Generates a mock zero-knowledge proof from user input.

**Request Body:**
```json
{
  "date_of_birth": "19900515",
  "country_of_residence": "USA",
  "identity_document": "DL123456789",
  "required_age": 18,
  "required_country": "USA"
}
```

### POST /api/verify-identity
Verifies a zero-knowledge proof and creates an attestation.

**Request Body:**
```json
{
  "proof": { /* ZK proof object */ },
  "current_timestamp": 1756563021,
  "required_age": 18,
  "required_country": "USA"
}
```

### GET /api/get-attestation/{attestation_id}
Retrieves an attestation by its ID.

## 🧪 How It Works

### Step 1: Private Data Input
Users enter their private information (date of birth, country, document ID) and specify verification requirements (minimum age, required country).

### Step 2: Zero-Knowledge Proof Generation
The system generates a cryptographic proof that the user's data meets the requirements without revealing the actual data. The proof includes:
- **Public Signals**: Non-sensitive verification parameters
- **Proof Data**: Cryptographic proof components (π_a, π_b, π_c)
- **Nullifier**: Unique identifier preventing double-spending

### Step 3: Verification and Attestation
The proof is verified against the requirements, and if valid, an attestation is created and stored. The attestation serves as a permanent record of successful verification.

## 🔐 Privacy Features

- **Data Minimization**: Only necessary verification parameters are exposed
- **Cryptographic Proofs**: Mathematical guarantees of claim validity
- **Nullifiers**: Prevent replay attacks while maintaining anonymity
- **Local Processing**: Sensitive data never leaves the user's device in plain text

## 🛠️ Technology Stack

- **ZK Circuits**: Midnight's Compact language (conceptual)
- **Backend**: Python Flask with SQLAlchemy
- **Frontend**: React with Vite, Tailwind CSS, and Framer Motion
- **Database**: SQLite for development
- **Styling**: Tailwind CSS with shadcn/ui components

## 📝 Development Notes

This is a demonstration application that uses mock implementations for educational purposes:

- **Mock Proofs**: Real ZK proof generation would require the Midnight Compact compiler
- **Simulated Verification**: Actual verification would use cryptographic libraries
- **Test Data**: All transactions use mock data with no real-world value

## 🤝 Contributing

This project is open-source under the Apache 2.0 License. Contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🔗 Resources

- [Midnight Network Documentation](https://docs.midnight.network/)
- [Zero-Knowledge Proofs Explained](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)
- [Privacy-Preserving Technologies](https://privacytools.io/)

## ⚠️ Disclaimer

This is a demonstration application for educational purposes. Do not use with real personal data or in production environments without proper security audits and implementations.

