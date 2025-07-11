# ShippingServices
DropZone is a secure CLI-based ephemeral file sharing system designed for internal teams. Built with Node.js, gRPC, RabbitMQ, and MinIO, it ensures privacy, auditability, and ease of deployment. Note: Currently this project is just in its initial phase. Play around but don't upload anything sesnsitive until further notice.

🌐 Features
⚡ Secure file upload/download with passcode-protected HMAC tokens
🪝 Event-based audit logging with RabbitMQ and MongoDB
☁️ Internal-only object storage via S3-compatible MinIO
🧾 Auto-expiry, rate-limiting, and CLI token-based access
📈 Deployable via Docker Compose or Kubernetes with ArgoCD (Yet to be added. Stay tuned!!!)
🚀 Quickstart
Prerequisites
Node.js (v18+ recommended)
Docker & Docker Compose
Client installation and usage
🛠 Build CLI
cd client/
npm install
npm run build
npm link   # Register globally as `dropzone`
📥 Upload a file
dropzone upload ./secrets.txt
📤 Download a file
dropzone download <TOKEN>
📁 Project Structure
dropzone/
├── client/              # CLI interface (dropzone upload/download)
├── services/
│   ├── file-service/    # gRPC upload/download service
│   └── audit-service/   # RabbitMQ consumer that logs events to MongoDB
├── proto/               # gRPC proto files
├── infra/
│   └── docker-compose.yml  # Local dev setup
└── README.md
