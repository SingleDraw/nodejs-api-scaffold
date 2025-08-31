# Node.js API Scaffold

A production-ready Node.js API scaffold with TypeScript, PostgreSQL, and TypeORM.

## Features

- ✅ **TypeScript** - Full TypeScript support with strict configuration
- ✅ **PostgreSQL** - Dockerized PostgreSQL database with initial schema
- ✅ **TypeORM** - Powerful ORM with decorators and migrations
- ✅ **Express.js** - Fast, minimalist web framework
- ✅ **Auto-refresh** - Development server with hot reload using ts-node-dev
- ✅ **Docker** - Containerized application and database
- ✅ **Validation** - Request validation using Joi
- ✅ **Security** - Helmet, CORS, rate limiting
- ✅ **Logging** - Morgan HTTP request logger
- ✅ **Error Handling** - Centralized error handling middleware
- ✅ **Password Hashing** - Secure password hashing with bcrypt
- ✅ **Code Quality** - ESLint and Prettier configuration

## Quick Start

### Prerequisites

- Docker and Docker Compose
- Node.js 18+ (for local development)

### Setup

1. **Clone and setup the project**
   ```bash
   git clone <your-repo>
   cd nodejs-api-scaffold
   cp .env.example .env
   ```

2. **Start with Docker (Recommended)**
   ```bash
   docker-compose up --build
   ```
   
   The API will be available at `http://localhost:3000`

3. **Or run locally**
   ```bash
   npm install
   npm run dev:ts
   ```

### API Endpoints

#### Users
- `GET /api/v1/users` - Get all users (with pagination)
- `GET /api/v1/users/:id` - Get user by ID
- `POST /api/v1/users` - Create new user
- `PUT /api/v1/users/:id` - Update user
- `DELETE /api/v1/users/:id` - Delete user
- `GET /api/v1/users/:id/posts` - Get user's posts

#### Health Check
- `GET /health` - Health check endpoint

### Example API Usage

**Get user by ID:**
```bash
curl http://localhost:3000/api/v1/users/{user-id}
```

**Create a new user:**
```bash
curl -X POST http://localhost:3000/api/v1/users \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "password123",
    "firstName": "John",
    "lastName": "Doe"
  }'
```

**Get all users with pagination:**
```bash
curl "http://localhost:3000/api/v1/users?page=1&limit=10"
```

## Project Structure

```
src/
├── entities/          # TypeORM entities
│   ├── User.ts
│   └── Post.ts
├── controllers/       # Route controllers
│   └── UserController.ts
├── services/          # Business logic services
│   └── UserService.ts
├── routes/            # Express routes
│   └── userRoutes.ts
├── middlewares/       # Custom middlewares
│   ├── errorHandler.ts
│   └── validateUUID.ts
├── validators/        # Joi validation schemas
│   └── userValidator.ts
├── dto/              # Data transfer objects
│   └── UserDto.ts
├── data-source.ts    # TypeORM configuration
└── app.ts           # Main application file
```

## Development

### Available Scripts

- `npm run dev:ts` - Start development server with hot reload
- `npm run build` - Build TypeScript to JavaScript
- `npm start` - Start production server
- `npm run migration:generate` - Generate new migration
- `npm run migration:run` - Run pending migrations
- `npm run schema:sync` - Sync database schema (development only)

### Database Migrations

Generate a new migration:
```bash
npm run migration:generate -- src/migrations/YourMigrationName
```

Run migrations:
```bash
npm run migration:run
```

### Environment Variables

Copy `.env.example` to `.env` and configure:

- `DB_HOST` - Database host
- `DB_PORT` - Database port
- `DB_USERNAME` - Database username
- `DB_PASSWORD` - Database password
- `DB_DATABASE` - Database name
- `JWT_SECRET` - JWT secret key
- `PORT` - Application port

## Security Features

- **Helmet** - Security headers
- **CORS** - Cross-origin resource sharing
- **Rate Limiting** - API rate limiting
- **Input Validation** - Request validation with Joi
- **Password Hashing** - Secure password storage with bcrypt

## Database Schema

The initial schema includes:

### Users Table
- `id` (UUID, Primary Key)
- `email` (Unique)
- `password` (Hashed)
- `first_name`
- `last_name` 
- `is_active`
- `created_at`
- `updated_at`

### Posts Table
- `id` (UUID, Primary Key)
- `title`
- `content`
- `user_id` (Foreign Key)
- `is_published`
- `created_at`
- `updated_at`

## Deployment

### Docker Production

1. Update environment variables for production
2. Build and run:
   ```bash
   docker-compose -f docker-compose.prod.yml up --build
   ```

### Manual Deployment

1. Build the application:
   ```bash
   npm run build
   ```

2. Set production environment variables

3. Run migrations:
   ```bash
   npm run migration:run
   ```

4. Start the server:
   ```bash
   npm start
   ```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests and linting
5. Submit a pull request

## License

MIT