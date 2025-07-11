# ShippingServices

A secure CLI-based ephemeral file sharing system designed for internal teams. Built with Node.js, gRPC, RabbitMQ, and MinIO, it ensures privacy, auditability, and ease of deployment.

> **⚠️ Note:** Currently this project is just in its initial phase. Play around but don't upload anything sensitive until further notice.

## 🌐 Features

- ⚡ **Secure file upload/download** with passcode-protected HMAC tokens
- 🪝 **Event-based audit logging** with RabbitMQ and MongoDB
- ☁️ **Internal-only object storage** via S3-compatible MinIO
- 🧾 **Auto-expiry, rate-limiting, and CLI token-based access**
- 📈 **Deployable via Docker Compose or Kubernetes** with ArgoCD (Yet to be added. Stay tuned!!!)

## 🚀 Quickstart

### Prerequisites

- Node.js (v18+ recommended)
- Docker & Docker Compose

### Infrastructure Setup

1. **Start the services:**
   ```bash
   cd infra/
   docker-compose up -d
   ```

2. **Verify services are running:**
   ```bash
   docker-compose ps
   ```

### Client Installation and Usage

#### 🛠 Build CLI

```bash
cd client/
npm install
npm run build
npm link   # Register globally as `dropzone`
```

#### 📥 Upload a file

```bash
dropzone upload ./secrets.txt
```

#### 📤 Download a file

```bash
dropzone download <TOKEN>
```

## 📁 Project Structure

```
dropzone/
├── client/              # CLI interface (dropzone upload/download)
├── services/
│   ├── file-service/    # gRPC upload/download service
│   └── audit-service/   # RabbitMQ consumer that logs events to MongoDB
├── proto/               # gRPC proto files
├── infra/
│   └── docker-compose.yml  # Local dev setup
└── README.md
```

## 🏗️ Architecture

ShippingServices follows a microservices architecture with the following components:

### Core Services

- **File Service**: Handles file upload/download operations via gRPC
- **Audit Service**: Consumes events from RabbitMQ and logs to MongoDB
- **MinIO**: S3-compatible object storage for file persistence
- **RabbitMQ**: Message broker for event-driven architecture
- **MongoDB**: Database for audit logs and metadata

### Security Features

- **HMAC Token Authentication**: Each file access is protected by cryptographically signed tokens
- **Passcode Protection**: Additional layer of security for sensitive files
- **Rate Limiting**: Prevents abuse and ensures fair usage
- **Auto-expiry**: Files automatically expire after a configurable time period

## 🔧 Development

### Running Services Locally

1. **Start infrastructure:**
   ```bash
   cd infra/
   docker-compose up -d
   ```

2. **Start file service:**
   ```bash
   cd services/file-service/
   npm install
   npm run dev
   ```

3. **Start audit service:**
   ```bash
   cd services/audit-service/
   npm install
   npm run dev
   ```

### Building the CLI

```bash
cd client/
npm install
npm run build
npm link
```

### Environment Variables

Create a `.env` file in the root directory:

```env
# MinIO Configuration
MINIO_ROOT_USER=admin
MINIO_ROOT_PASSWORD=password123
MINIO_ENDPOINT=localhost:9000

# RabbitMQ Configuration
RABBITMQ_URL=amqp://guest:guest@localhost:5672

# MongoDB Configuration
MONGODB_URI=mongodb://localhost:27017/shippingservices

# Security
JWT_SECRET=your-secret-key
HMAC_SECRET=your-hmac-secret
```

## 🔒 Security Considerations

- Files are stored with encrypted names in MinIO
- All access is logged and auditable
- Tokens have configurable expiration times
- Rate limiting prevents abuse
- Internal network isolation recommended for production

## 📊 Monitoring & Logging

- All file operations are logged to MongoDB via the audit service
- RabbitMQ provides reliable event delivery
- Docker Compose includes health checks for all services

## 🚧 Roadmap

- [ ] Kubernetes deployment with ArgoCD
- [ ] Web UI for file management
- [ ] Advanced access controls and permissions
- [ ] File encryption at rest
- [ ] Metrics and monitoring dashboard
- [ ] API documentation with OpenAPI/Swagger

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For issues and questions:
- Create an issue in the GitHub repository
- Check the troubleshooting section in the documentation
- Contact the development team

## 🔗 Related Projects

- [MinIO](https://min.io/) - High-performance object storage
- [RabbitMQ](https://www.rabbitmq.com/) - Message broker
- [gRPC](https://grpc.io/) - High-performance RPC framework
- [MongoDB](https://www.mongodb.com/) - Document database

---

**Happy file sharing! 🚀**
