# 🍯 Honeypot Cybersecurity Dashboard - Backend

A production-grade backend API for the Honeypot Cybersecurity Dashboard that tracks, analyzes, and reports scammer activities in real-time.

## 🏗️ Architecture

### Tech Stack
- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Database**: PostgreSQL 15
- **Cache**: Redis 7
- **Real-time**: WebSocket (ws)
- **Logging**: Winston
- **Security**: Helmet, JWT, Rate Limiting

### Key Features
- ✅ Real-time session monitoring via WebSocket
- ✅ Intelligent data capture and analysis
- ✅ Advanced threat pattern recognition
- ✅ Automated reporting to authorities
- ✅ Comprehensive logging and audit trails
- ✅ RESTful API with rate limiting
- ✅ Redis caching for performance
- ✅ Docker support for easy deployment
- ✅ Production-ready security measures

## 📋 Prerequisites

- Node.js >= 18.0.0
- PostgreSQL >= 14
- Redis >= 7
- npm >= 9.0.0
- Docker & Docker Compose (optional)

## 🚀 Quick Start

### Option 1: Docker Deployment (Recommended)

1. **Clone the repository**
```bash
git clone <repository-url>
cd honeypot-backend
```

2. **Configure environment**
```bash
cp .env.example .env
# Edit .env with your configuration
```

3. **Start services**
```bash
docker-compose up -d
```

4. **Verify deployment**
```bash
curl http://localhost:3001/api/health
```

### Option 2: Manual Setup

1. **Install dependencies**
```bash
npm install
```

2. **Setup PostgreSQL**
```bash
# Create database
createdb honeypot_db

# Run migrations
psql -U postgres -d honeypot_db -f database/schema.sql
```

3. **Setup Redis**
```bash
# Start Redis server
redis-server
```

4. **Configure environment**
```bash
cp .env.example .env
# Edit .env with your database credentials
```

5. **Start the server**
```bash
# Development
npm run dev

# Production
npm start
```

## 🔌 API Endpoints

### Health & Status
```
GET /api/health - System health check
```

### Statistics
```
GET /api/stats/overview - Dashboard statistics
GET /api/stats/engagement-timeline - Engagement metrics
GET /api/stats/interceptions-weekly - Weekly interceptions
```

### Sessions
```
GET /api/sessions/active - Get active sessions
POST /api/sessions/create - Create new session
```

### Intelligence
```
GET /api/intelligence/recent - Recent captures
POST /api/intelligence/capture - Add new capture
```

### Scammer Database
```
GET /api/scammers/search - Search scammer database
```

### Analytics
```
GET /api/analytics/threat-patterns - Threat analysis
```

### Reporting
```
POST /api/report/authorities - Submit report to authorities
```

### Terminal Logs
```
GET /api/logs/terminal - Get terminal logs
```

## 🔐 Authentication

The API supports two authentication methods:

### 1. API Key Authentication
```bash
curl -H "X-API-Key: your-api-key" http://localhost:3001/api/stats/overview
```

### 2. JWT Authentication
```bash
curl -H "Authorization: Bearer your-jwt-token" http://localhost:3001/api/sessions/active
```

## 🌐 WebSocket Events

Connect to `ws://localhost:3001` for real-time updates.

### Client → Server Messages
```javascript
// Subscribe to topics
{
  "type": "SUBSCRIBE",
  "topics": ["sessions", "intelligence", "terminal", "stats"]
}

// Unsubscribe
{
  "type": "UNSUBSCRIBE",
  "topics": ["terminal"]
}

// Ping
{
  "type": "PING"
}
```

### Server → Client Messages
```javascript
// New session
{
  "type": "NEW_SESSION",
  "topic": "sessions",
  "data": { ... },
  "timestamp": "2026-01-31T12:00:00Z"
}

// New intelligence capture
{
  "type": "NEW_CAPTURE",
  "topic": "intelligence",
  "data": { ... },
  "timestamp": "2026-01-31T12:00:00Z"
}

// Terminal log
{
  "type": "TERMINAL_LOG",
  "topic": "terminal",
  "data": { ... },
  "timestamp": "2026-01-31T12:00:00Z"
}

// Stats update
{
  "type": "STATS_UPDATE",
  "topic": "stats",
  "data": { ... },
  "timestamp": "2026-01-31T12:00:00Z"
}
```

## 📊 Database Schema

The database consists of the following main tables:

- `interception_sessions` - Main session data
- `intelligence_captures` - Captured intelligence data
- `session_messages` - Conversation logs
- `terminal_logs` - System logs
- `authority_reports` - Reports submitted to authorities
- `scammer_profiles` - Aggregated scammer data
- `analytics_summary` - Cached analytics data
- `system_events` - Audit trail
- `api_keys` - API authentication

## 🔒 Security Features

- Helmet.js security headers
- Rate limiting (100 requests/15 minutes)
- CORS protection
- SQL injection prevention (parameterized queries)
- XSS protection
- JWT token authentication
- API key hashing (SHA-256)
- Input validation with Joi
- Secure WebSocket connections
- Non-root Docker containers

## 📝 Logging

Logs are stored in the `/logs` directory with daily rotation:

- `application-YYYY-MM-DD.log` - All application logs
- `error-YYYY-MM-DD.log` - Error logs only
- `http-YYYY-MM-DD.log` - HTTP request logs
- `security-YYYY-MM-DD.log` - Security events (90 days)
- `sessions-YYYY-MM-DD.log` - Session activities (30 days)
- `intelligence-YYYY-MM-DD.log` - Intelligence captures (90 days)

## 🐳 Docker Commands

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f backend

# Stop all services
docker-compose down

# Rebuild containers
docker-compose up -d --build

# Access database
docker-compose exec postgres psql -U postgres -d honeypot_db

# Access Redis CLI
docker-compose exec redis redis-cli

# Development mode with PgAdmin
docker-compose --profile development up -d
```

## 🧪 Testing

```bash
# Run tests
npm test

# Run tests with coverage
npm test -- --coverage

# Run specific test file
npm test -- services/websocket.test.js
```

## 📈 Performance Optimization

- Redis caching for frequently accessed data
- Database indexing on critical columns
- Connection pooling (20 max connections)
- Response compression
- Query result caching (30-300 seconds)
- WebSocket for real-time updates (no polling)

## 🔧 Configuration

Key environment variables:

```bash
# Server
NODE_ENV=production
PORT=3001

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=honeypot_db
DB_USER=postgres
DB_PASSWORD=secure_password

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=secure_password

# Security
JWT_SECRET=your-secret-key-min-32-chars
API_KEY_SALT=your-salt

# CORS
ALLOWED_ORIGINS=http://localhost:3000,https://yourdomain.com
```

## 📚 API Documentation

Full API documentation is available at `/api/docs` when running in development mode.

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 🆘 Support

For issues and questions:
- GitHub Issues: [repository-url]/issues
- Email: support@honeypot.local

## 🚨 Production Deployment Checklist

- [ ] Update all environment variables
- [ ] Generate secure JWT_SECRET (min 32 characters)
- [ ] Configure ALLOWED_ORIGINS for CORS
- [ ] Set up SSL certificates
- [ ] Configure database backups
- [ ] Set up monitoring and alerting
- [ ] Review and adjust rate limits
- [ ] Enable production logging
- [ ] Configure external services (email, SMS)
- [ ] Set up reverse proxy (Nginx)
- [ ] Implement database replication (if needed)
- [ ] Configure firewall rules
- [ ] Set up log aggregation
- [ ] Review security headers
- [ ] Test disaster recovery procedures

## 🎯 Roadmap

- [ ] GraphQL API support
- [ ] Machine learning integration for threat detection
- [ ] Multi-language support
- [ ] Advanced reporting dashboard
- [ ] Integration with external threat intelligence feeds
- [ ] Mobile app backend support
- [ ] Automated scammer profile generation
- [ ] Enhanced geolocation tracking
- [ ] Blockchain-based evidence verification

---

**Made with ❤️ for cybersecurity**
