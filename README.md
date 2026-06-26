# CogniDispatch Payment Service

The **Payment Service** is the transaction processing microservice within the **CogniDispatch** platform. It handles simulated checkout authorizations for dispatch bookings, credits technician account balances, updates rating scores, and shifts active dispatches into the final `COMPLETED` state.

## 🚀 Technology Stack
*   **Runtime**: Node.js (v18+)
*   **Web Framework**: Express.js
*   **Security & Networking**: CORS, Helmet
*   **Shared Modules**: Local file reference to `shared` (DB Adapter, utilities, mock schemas)

---

## 📁 Repository Structure
```
├── controllers/          # Express route controllers (Payment/Checkout logic)
│   └── paymentController.js # Checkout processing and vendor balance logic
├── shared/               # Database adapter and schema configurations
├── Dockerfile            # Container build specification
├── package.json          # Node dependencies
└── server.js             # Entry point
```

---

## ⚙️ Environment Variables & Config

This service requires database connectivity. It reads the following parameters:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `PORT` | Listening TCP Port for the service | `5006` |
| `MONGODB_URI_FILE` | Path to file containing Cosmos DB connection string | *None* |

---

## 🛣️ API Endpoints

All routes are prefixed with `/api/payments`.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| **GET** | `/api/payments/health` | Service health status check |
| **POST** | `/api/payments/checkout` | Authorizes credit card details, processes payment logic, credits 80% payout to the technician's balance, records job performance ratings, and updates the dispatch status to `COMPLETED` |

---

## 🛠️ Local Development

### 1. Prerequisites
*   Node.js (v18+)
*   A running local MongoDB instance (or Cosmos DB emulator)

### 2. Startup Commands
From the service root:
```bash
# Install dependencies
npm install

# Run the development server
npm start
```
The server will start listening at `http://localhost:5006/`.

---

## 🐳 Docker Container Build

```bash
docker build -t cogniregistry.azurecr.io/cogni-payment-service:latest .
```
