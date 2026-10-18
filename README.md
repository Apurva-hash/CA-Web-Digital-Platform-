CA Web Platform
A web-based platform that connects clients with Chartered Accountants (CAs) and helps manage accounting-service workflows in one place. It provides separate client and CA portals for service requests, document management, communication, and task tracking.
Configuration note: MongoDB, AWS S3, Cloudinary, and Stripe integrations require valid credentials and environment configuration. Some dashboard statistics are sample/mock values.

Features
Public Access
- Landing page introducing the platform
- User registration and login
- Role-based routing for clients and CA accounts
Client Portal
- Client dashboard
- Find a Chartered Accountant
- Submit service requests and track their status
- Upload and view documents
- Access messages and conversations
- Manage user profile
CA Portal
- CA dashboard with overview statistics and charts
- Client management
- Service-request management
- Document management
- Task management
- Messaging and account settings
Backend
- REST API built with Express
- JWT-protected routes
- MongoDB persistence using Mongoose
- Password hashing with bcryptjs
- Financial and regulatory news aggregation using RSS feeds, with fallback news content
- Payment-related routes configured for Stripe; the code also includes a simulated payment-completion route
- Document-storage integrations for AWS S3 and Cloudinary
- Security middleware using Helmet and API rate limiting
Technology Stack
Frontend
- React 19
- TypeScript
- Vite
- React Router
- Recharts
- Framer Motion
- Lucide React
- CSS
Backend
- Node.js
- Express
- MongoDB and Mongoose
- JSON Web Tokens (JWT)
- bcryptjs
- rss-parser
- Stripe SDK
- AWS SDK for S3
- Cloudinary
- Helmet
- express-rate-limit
Project Structure
CA web pro/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   │   ├── ca/
│   │   │   └── user/
│   │   ├── config/
│   │   └── App.tsx
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
└── backend/
    ├── config/
    ├── controllers/
    ├── middleware/
    ├── models/
    ├── routes/
    ├── index.js
    └── package.json
Prerequisites
Install the following before running the application:
- Node.js and npm
- A MongoDB database
- API credentials for any external services you want to enable (AWS S3, Stripe, or Cloudinary)
Getting Started
Run the frontend and backend in separate terminals.
1. Set Up the Backend
cd "CA web pro/backend"
npm install
Create a .env file in the backend directory and configure the required values:
PORT=5001
JWT_SECRET=replace_with_a_long_random_secret
MONGODB_URI=mongodb_connection_string

# AWS S3 (if using S3 document uploads)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_S3_BUCKET=

# Stripe (for Stripe payment flows/webhooks)
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

# Cloudinary (if using the Cloudinary integration)
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
Start the backend:
npm run dev
The backend defaults to port 5001 unless PORT is set to a different value.
2. Set Up the Frontend
Open a second terminal:
cd "CA web pro/frontend"
npm install
The frontend uses VITE_API_URL when it is set; otherwise, it falls back to http://localhost:5001.
For local development, you can create a .env file in the frontend directory:
VITE_API_URL=http://localhost:5001
Start the frontend:
npm run dev
Vite will display the local development URL in the terminal.
Build and Code Checks
Run these commands from the frontend directory:
npm run build
npm run lint
To preview a production build locally:
npm run preview
API Overview
The backend mounts API routes under /api.
Route Prefix	Purpose
/api/auth	Registration and authentication
/api/ca	CA-related operations
/api/dashboard	Dashboard statistics
/api/documents	Document operations
/api/news	Financial and regulatory news
/api/requests	Service requests
/api/clients	Client management
/api/chat	Messaging
/api/payments	Payment-related operations


Most account-specific endpoints require a valid bearer token.
Security and Configuration Notes
- Do not commit .env files, passwords, API keys, or other secrets to a public repository.
- If real credentials were included in a shared ZIP or committed to Git, revoke or rotate them and remove them from repository history where appropriate.
- Use a strong, private JWT_SECRET.
- Configure CORS for trusted origins before deployment.
- Test external-service configuration and payment/webhook behavior in a test environment before using real customer data or payments.
- Dashboard statistics currently include sample/mock values; do not treat them as live business metrics unless connected to real data.
Current Scope
This repository contains a React/TypeScript frontend and a Node.js/Express backend. Some external services depend on environment configuration, and some dashboard values are mock data. Test the main user journeys and integrations in your environment before presenting the application as production-ready.
License
No project-specific license was identified in the available project files. Add a LICENSE file if you plan to distribute the project publicly.
