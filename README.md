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

## 🚀 Quick Start

### Prerequisites

- Python 3.11+
- Node.js 20+
- pnpm (for frontend package management)

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/zk-identity-attestation.git
   cd zk-identity-attestation
   ```

2. **Backend Setup**
   ```bash
   cd zk_identity_backend
   
   # Create virtual environment
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install dependencies
   pip install -r requirements.txt
   ```

3. **Frontend Setup**
   ```bash
   cd ../zk_identity_frontend
   
   # Install dependencies
   pnpm install
   ```

### Running the Application

1. **Start the Backend Server**
   ```bash
   cd zk_identity_backend
   source venv/bin/activate
   python src/main.py
   ```
   The API will be available at `http://localhost:5000`

2. **Start the Frontend Development Server**
   ```bash
   cd zk_identity_frontend
   pnpm run dev --host
   ```
   The application will be available at `http://localhost:5173`

3. **Open your browser** and navigate to `http://localhost:5173` to use the application.

## 📱 How to Use

### Step 1: Enter Private Information
- Fill in your date of birth (YYYYMMDD format)
- Select your country of residence
- Enter an identity document ID
- Set verification requirements (minimum age, required country)

### Step 2: Generate Zero-Knowledge Proof
- Click "Generate ZK Proof" to create a cryptographic proof
- Review the proof details (private data is hidden by default)
- Examine the public signals and proof components

### Step 3: Verify Identity
- Click "Verify Identity" to submit the proof for verification
- Receive an attestation ID upon successful verification
- View attestation details stored on the simulated blockchain

## 🔧 API Endpoints

### GET /api/get-public-parameters
Returns public parameters for the verification system.

**Response:**
```json
{
  "current_timestamp": 1756563021,
  "issuer_public_key": "0x1234567890abcdef",
  "minimum_age": 18,
  "supported_countries": ["USA", "Canada", "UK", "Germany", "France"]
}
```

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

**Response:**
```json
{
  "success": true,
  "message": "Mock proof generated successfully",
  "proof": {
    "nullifier": "fd13f8411d388fdb",
    "proof_data": {
      "pi_a": ["0x389d31b917c211b9b2406a92cc2e1874"],
      "pi_b": [["0xb7941070f58f4c3a7487e2928f20e4ad"]],
      "pi_c": ["0xa62b36ad6a5c0ad62fa9e40b3b19960a"]
    },
    "public_signals": {
      "current_timestamp": 1756563435,
      "issuer_public_key": "0x1234567890abcdef",
      "required_age": 18,
      "required_country_hash": "aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046"
    }
  }
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

**Response:**
```json
{
  "success": true,
  "attestation_id": "a1b2c3d4e5f6g7h8",
  "message": "Identity successfully verified"
}
```

### GET /api/get-attestation/{attestation_id}
Retrieves an attestation by its ID.

**Response:**
```json
{
  "id": "a1b2c3d4e5f6g7h8",
  "nullifier": "fd13f8411d388fdb",
  "timestamp": 1756563435,
  "required_age": 18,
  "required_country": "USA",
  "verified": true,
  "created_at": "2025-08-30T14:17:15.123456"
}
```

## 🧪 How Zero-Knowledge Proofs Work

### The Problem
Traditional identity verification requires users to share sensitive personal information (full date of birth, address, document numbers) with verifiers, creating privacy risks and data exposure.

### The Solution
Zero-knowledge proofs allow users to prove they meet certain criteria without revealing the underlying data:

1. **Proof Generation**: User's private data is processed through a cryptographic circuit that generates a proof
2. **Public Signals**: Only non-sensitive verification parameters are made public
3. **Verification**: The proof can be verified mathematically without accessing private data
4. **Nullifiers**: Prevent double-spending while maintaining anonymity

### Example
Instead of sharing "Born: May 15, 1990", a user can prove "I am over 18 years old" without revealing their exact birth date.

## 🔐 Privacy Features

- **Data Minimization**: Only necessary verification parameters are exposed
- **Cryptographic Proofs**: Mathematical guarantees of claim validity without data exposure
- **Nullifiers**: Prevent replay attacks while maintaining user anonymity
- **Local Processing**: Sensitive data never leaves the user's device in plain text
- **No Personal Data Storage**: The system only stores proof verification results, not personal information

## 🛠️ Technology Stack

- **ZK Circuits**: Midnight's Compact language (conceptual implementation)
- **Backend**: Python Flask with SQLAlchemy ORM
- **Database**: SQLite for development (easily upgradeable to PostgreSQL)
- **Frontend**: React 19 with Vite build tool
- **Styling**: Tailwind CSS with shadcn/ui components
- **Icons**: Lucide React icons
- **Animations**: Framer Motion for smooth transitions
- **HTTP Client**: Fetch API for backend communication

## 📁 Project Structure

```
zk-identity-attestation/
├── README.md                          # This file
├── LICENSE                           # Apache 2.0 License
├── .gitignore                        # Git ignore rules
├── identity_att/                     # ZK Circuit implementation
│   ├── src/
│   │   └── identity_attestation.compact  # Compact circuit definition
│   └── Nargo.toml                    # Noir project configuration
├── zk_identity_backend/              # Flask backend
│   ├── src/
│   │   ├── main.py                   # Flask application entry point
│   │   ├── models/
│   │   │   ├── user.py              # User model (template)
│   │   │   └── attestation.py       # Attestation model
│   │   └── routes/
│   │       ├── user.py              # User routes (template)
│   │       └── identity.py          # Identity verification routes
│   └── requirements.txt              # Python dependencies
└── zk_identity_frontend/             # React frontend
    ├── src/
    │   ├── App.jsx                   # Main application component
    │   ├── App.css                   # Application styles
    │   ├── main.jsx                  # React entry point
    │   └── components/               # Reusable UI components
    ├── package.json                  # Node.js dependencies
    ├── vite.config.js               # Vite configuration
    ├── index.html                   # HTML template
    └── tailwind.config.js           # Tailwind CSS configuration
```

## 🧪 Development Notes

This is a demonstration application that uses mock implementations for educational purposes:

- **Mock Proofs**: Real ZK proof generation would require the Midnight Compact compiler
- **Simulated Verification**: Actual verification would use cryptographic libraries like snarkjs
- **Test Data**: All transactions use mock data with no real-world value
- **Local Database**: Uses SQLite for simplicity; production would use PostgreSQL or similar

## 🚀 Deployment

### Development Deployment
The application is designed to run locally for development and testing.

### Production Considerations
For production deployment, consider:

- **Database**: Migrate from SQLite to PostgreSQL or MongoDB
- **Authentication**: Implement proper user authentication and session management
- **HTTPS**: Use SSL/TLS certificates for secure communication
- **Environment Variables**: Use environment-specific configuration
- **Monitoring**: Add logging and monitoring for production use
- **Scaling**: Consider containerization with Docker and orchestration with Kubernetes

## 🤝 Contributing

This project is open-source under the Apache 2.0 License. Contributions are welcome!

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
4. **Add tests if applicable**
5. **Commit your changes**
   ```bash
   git commit -m 'Add some amazing feature'
   ```
6. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
7. **Open a Pull Request**

### Development Guidelines

- Follow existing code style and conventions
- Add comments for complex logic
- Update documentation for new features
- Test your changes thoroughly
- Ensure all tests pass before submitting

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🔗 Resources

- [Midnight Network Documentation](https://docs.midnight.network/)
- [Zero-Knowledge Proofs Explained](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)
- [Privacy-Preserving Technologies](https://privacytools.io/)
- [React Documentation](https://react.dev/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## ⚠️ Disclaimer

This is a demonstration application for educational purposes. Do not use with real personal data or in production environments without proper security audits and implementations.

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/your-username/zk-identity-attestation/issues) page
2. Create a new issue with detailed information
3. Provide steps to reproduce any bugs
4. Include system information and error messages

## 🎯 Future Enhancements

- Integration with real Midnight Compact compiler
- Support for additional identity verification criteria
- Mobile app development
- Integration with real blockchain networks
- Advanced privacy features and cryptographic protocols
- Multi-language support
- Enhanced UI/UX with more interactive elements
