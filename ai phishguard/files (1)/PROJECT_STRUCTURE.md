# 🍯 Honeypot Backend - Project Structure

## 📁 Directory Structure

```
honeypot-backend/
├── server.js                    # Main application entry point
├── package.json                 # Dependencies and scripts
├── Dockerfile                   # Container configuration
├── docker-compose.yml           # Multi-container setup
├── .env.example                 # Environment template
├── .gitignore                   # Git ignore rules
├── README.md                    # Main documentation
│
├── database/
│   └── schema.sql              # PostgreSQL database schema
│
├── middleware/
│   └── auth.js                 # Authentication & authorization
│
├── services/
│   ├── websocket.js            # WebSocket manager
│   └── logger.js               # Winston logging service
│
├── validators/
│   └── schemas.js              # Joi validation schemas
│
├── nginx/
│   └── nginx.conf              # Reverse proxy configuration
│
├── docs/
│   └── API.md                  # Complete API documentation
│
└── logs/                       # Application logs (auto-generated)
    ├── application-*.log
    ├── error-*.log
    ├── http-*.log
    ├── security-*.log
    ├── sessions-*.log
    └── intelligence-*.log
```

## 🔧 Core Files

### server.js
Main Express application with:
- RESTful API endpoints
- WebSocket server integration
- Database connection pooling
- Redis caching
- Security middleware
- Rate limiting
- Error handling

### database/schema.sql
Complete PostgreSQL schema including:
- 8 main tables with relationships
- Indexes for performance
- Triggers for automation
- Views for common queries
- Sample data for development

### middleware/auth.js
Authentication system with:
- API key validation
- JWT token handling
- Permission checking
- Key generation utilities

### services/websocket.js
Real-time communication with:
- Client connection management
- Topic-based subscriptions
- Broadcasting capabilities
- Automatic reconnection handling

### services/logger.js
Comprehensive logging with:
- Multiple log levels
- Daily log rotation
- Specialized loggers (security, sessions, intelligence)
- Express middleware integration

### validators/schemas.js
Input validation for:
- Session creation
- Intelligence captures
- Authority reports
- Scammer searches
- API requests

## 🚀 Deployment Options

### Option 1: Docker Compose (Recommended)
```bash
docker-compose up -d
```
Includes:
- PostgreSQL database
- Redis cache
- Node.js backend
- Nginx reverse proxy
- PgAdmin (development)

### Option 2: Manual Setup
```bash
npm install
psql -U postgres -d honeypot_db -f database/schema.sql
npm start
```

## 🔐 Security Features

1. **Helmet.js** - Security headers
2. **CORS** - Cross-origin protection
3. **Rate Limiting** - DDoS prevention
4. **JWT/API Keys** - Authentication
5. **Input Validation** - SQL injection prevention
6. **Parameterized Queries** - Database security
7. **Non-root Containers** - Docker security
8. **SSL/TLS** - Encrypted connections

## 📊 Database Tables

1. **interception_sessions** - Main session tracking
2. **intelligence_captures** - Captured scammer data
3. **session_messages** - Conversation logs
4. **terminal_logs** - System activity logs
5. **authority_reports** - Law enforcement reports
6. **scammer_profiles** - Aggregated scammer intelligence
7. **analytics_summary** - Cached analytics
8. **system_events** - Audit trail
9. **api_keys** - Authentication keys

## 🌐 API Endpoints

### Statistics
- `GET /api/stats/overview`
- `GET /api/stats/engagement-timeline`
- `GET /api/stats/interceptions-weekly`

### Sessions
- `GET /api/sessions/active`
- `POST /api/sessions/create`

### Intelligence
- `GET /api/intelligence/recent`
- `POST /api/intelligence/capture`

### Scammers
- `GET /api/scammers/search`

### Analytics
- `GET /api/analytics/threat-patterns`

### Reporting
- `POST /api/report/authorities`

### Logs
- `GET /api/logs/terminal`

### System
- `GET /api/health`

## 📡 WebSocket Topics

- **sessions** - New and updated sessions
- **intelligence** - Intelligence captures
- **terminal** - Terminal logs
- **stats** - Real-time statistics

## 🔄 Data Flow

```
Scammer → Honeypot System
    ↓
Session Created (DB)
    ↓
Intelligence Extracted
    ↓
WebSocket Broadcast
    ↓
Dashboard Update (Real-time)
    ↓
Analysis & Reporting
    ↓
Authorities (Optional)
```

## 🧪 Testing

```bash
# Unit tests
npm test

# Integration tests
npm run test:integration

# Coverage report
npm test -- --coverage
```

## 📈 Performance Optimization

1. **Redis Caching** - 30-300 second TTL
2. **Database Indexing** - Optimized queries
3. **Connection Pooling** - 20 max connections
4. **Response Compression** - Gzip enabled
5. **WebSocket** - No HTTP polling
6. **Query Optimization** - Prepared statements

## 🔗 Technology Stack

- **Runtime**: Node.js 18+
- **Framework**: Express.js 4.18
- **Database**: PostgreSQL 15
- **Cache**: Redis 7
- **WebSocket**: ws 8.16
- **Logging**: Winston 3.11
- **Validation**: Joi 17
- **Security**: Helmet 7, JWT
- **Container**: Docker, Docker Compose
- **Proxy**: Nginx

## 📝 Environment Variables

Required:
- `DB_PASSWORD` - Database password
- `REDIS_PASSWORD` - Redis password
- `JWT_SECRET` - JWT signing key
- `API_KEY_SALT` - API key salt

Optional:
- `PORT` - Server port (default: 3001)
- `NODE_ENV` - Environment (development/production)
- `ALLOWED_ORIGINS` - CORS origins
- `LOG_LEVEL` - Logging level

## 🆘 Troubleshooting

### Database Connection Failed
```bash
# Check PostgreSQL is running
docker-compose ps postgres
# View logs
docker-compose logs postgres
```

### Redis Connection Failed
```bash
# Check Redis is running
docker-compose ps redis
# View logs
docker-compose logs redis
```

### WebSocket Not Connecting
- Check CORS settings in `.env`
- Verify WebSocket port is not blocked
- Check Nginx configuration for WebSocket upgrade

### High Memory Usage
- Adjust connection pool size
- Check for memory leaks in logs
- Monitor Redis memory usage
- Review log file sizes

## 📞 Support

- Documentation: `/docs/API.md`
- GitHub Issues: [repository-url]/issues
- Email: support@honeypot.local

## 🎯 Next Steps

1. Configure `.env` file
2. Run `docker-compose up -d`
3. Access API at `http://localhost:3001`
4. Check health: `curl http://localhost:3001/api/health`
5. Review API documentation in `/docs/API.md`
6. Connect frontend dashboard
7. Test WebSocket connection
8. Configure external services (email, SMS)
9. Set up monitoring and alerts
10. Deploy to production

---

**Built with security and performance in mind** 🔒⚡
