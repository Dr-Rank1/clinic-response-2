# Clinic Queue System

A production-ready, full-stack Clinic Queue Management System built with Next.js 14, TypeScript, and MongoDB. This system streamlines appointment booking, queue tracking, diagnosis recording, and provides role-based dashboards for clinic staff.

## Credits

Developed and maintained by Ian Gicheha Mbae / Dr-Rank1.

## Features

### Security and Authentication
* Secure Authentication via NextAuth.js with JWT sessions
* Role-Based Access Control (RBAC) for 7 user roles
* Rate Limiting on auth (5/15min), bookings (3/5min), notifications (10/10min)
* Input Sanitization with XSS, SQL, and NoSQL injection protection
* Security Headers (CSP, HSTS, X-Frame-Options, etc.)
* Audit Logging for admin actions
* Environment Validation with Zod schemas

### Appointment Management
* Auto-generated queue numbers
* Real-time status updates: waiting, in-progress, done
* Live queue updates via Pusher
* Email and SMS notifications (optional)
* Appointment rescheduling and cancellation
* Patient slip printing

### Role-Based Dashboards

**Admin**
* User management (view, edit roles, delete)
* System metrics dashboard
* Audit logs with full history
* Real-time analytics

**Nurse**
* Vital signs recording (temperature, BP, weight, height)
* Nurse notes
* Ready for doctor flag
* Queue filtering

**Doctor**
* Diagnosis recording
* Prescription writing
* Lab test ordering
* Follow-up scheduling
* Doctor-specific queue view

**Pharmacist**
* Prescription retrieval
* Dispense tracking
* PDF export of prescriptions
* Pharmacist notes

**Lab Technician**
* Lab test management
* Result entry with file uploads
* Status tracking (pending/completed)

**Receptionist**
* New appointment booking
* Patient registration
* Queue management
* Slip printing

### Performance and Monitoring
* Database Indexing (11 indexes for 10-100x faster queries)
* Pagination on all list endpoints
* Structured Logging with Pino (production-ready)
* Health Check endpoint (/api/health)
* Performance Monitoring utilities
* Error Boundaries for graceful failures
* Connection Pooling for MongoDB

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Next.js | 14.2.5 | App Router, SSR, API routes |
| TypeScript | 5.8.3 | Static typing |
| MongoDB | 6.16.0 | NoSQL database |
| Mongoose | 8.15.0 | ODM for MongoDB |
| NextAuth.js | 4.24.11 | Authentication |
| Tailwind CSS | 3.3.0 | UI styling |
| Zod | 3.25.20 | Schema validation |
| Pino | 10.1.0 | Structured logging |
| Jest | 29.7.0 | Testing framework |
| Pusher | 5.2.0 | Real-time updates |
| Twilio | 5.7.1 | SMS notifications |
| Nodemailer | 6.9.15 | Email notifications |

## Installation

### Prerequisites
* Node.js 18+ or 20+
* MongoDB Atlas account or local MongoDB
* npm or yarn

### Quick Start

```bash
git clone https://github.com/Dr-Rank1/clinic-response-2.git
cd clinic-response-2

npm install

cp .env.example .env

npm run dev
```

Visit http://localhost:3000

## Configuration

### Required Environment Variables

Create a .env file based on .env.example:

```bash
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/clinic-queue

NEXTAUTH_SECRET=your-super-secret-random-string-min-32-characters
NEXTAUTH_URL=http://localhost:3000

NODE_ENV=development
PORT=3000
```

### Optional Services

**Pusher (Real-time updates)**
```bash
PUSHER_APP_ID=your-app-id
PUSHER_KEY=your-key
PUSHER_SECRET=your-secret
PUSHER_CLUSTER=your-cluster
NEXT_PUBLIC_PUSHER_KEY=your-key
NEXT_PUBLIC_PUSHER_CLUSTER=your-cluster
```

**Email (SMTP)**
```bash
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-specific-password
SMTP_FROM=noreply@yourclinic.com
```

**SMS (Twilio)**
```bash
TWILIO_ACCOUNT_SID=your-account-sid
TWILIO_AUTH_TOKEN=your-auth-token
TWILIO_PHONE_NUMBER=+1234567890
```

## Deployment

### Docker Deployment (Recommended)

```bash
docker-compose up -d

docker-compose logs -f app

docker-compose down
```

### Manual Deployment

```bash
npm run build

npm start
```

## Testing

```bash
npm test

npm run test:watch

npm run test:coverage
```

## Security Features

### Implemented
* Rate limiting on critical endpoints
* Input sanitization (XSS, SQL, NoSQL injection)
* Security headers (CSP, HSTS, X-Frame-Options)
* Environment variable validation
* Password hashing with bcrypt (10 rounds)
* JWT-based sessions
* Audit logging for admin actions
* CSRF protection (via NextAuth)

### Best Practices
* Secrets never committed to git
* .env files in .gitignore
* Admin-only endpoints protected
* Strong validation on all inputs
* Database indexes for performance
* Error boundaries for graceful failures

## API Documentation

### Core Endpoints

**Authentication**
```
POST /api/auth/[...nextauth]
```

**Appointments**
```
GET    /api/appointment
POST   /api/appointment
PATCH  /api/appointment/:id
DELETE /api/appointment/:id
```

**Bookings**
```
GET    /api/bookings
POST   /api/bookings
```

**Admin**
```
GET    /api/users
PATCH  /api/users/:id/role
DELETE /api/users/:id
GET    /api/admin/metrics
GET    /api/admin/audit-logs
```

**Health**
```
GET    /api/health
```

## Database Backup and Restore

### Backup Database
```bash
chmod +x scripts/backup-db.sh
./scripts/backup-db.sh
```

### Restore Database
```bash
chmod +x scripts/restore-db.sh
./scripts/restore-db.sh backups/clinic-queue-backup-20250101_120000.tar.gz
```

## Troubleshooting

### Build Errors
* Ensure all required environment variables are set in .env.
* Verify MongoDB connection and whitelist IP.

### Runtime Errors
* Rate limit exceeded: Wait for window to reset or check Retry-After header.
* Slow database queries: Ensure MongoDB indexes are created.

## License

This project is licensed under the MIT License.

## Support

For issues, questions, or suggestions, please open an issue in the GitHub repository.

Made with care for healthcare providers.
