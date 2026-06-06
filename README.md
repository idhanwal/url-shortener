# URL Shortener

A high-performance URL shortening service built with Spring Boot, PostgreSQL, and Redis. This application converts long URLs into concise, shareable short URLs with caching and persistence capabilities.

## 📋 Overview

The URL Shortener is a robust backend service designed to:
- Generate short, unique identifiers for long URLs
- Store URL mappings persistently in PostgreSQL
- Cache frequently accessed URLs in Redis for improved performance
- Provide RESTful APIs for URL creation and redirection
- Support high throughput with optimized database queries

## 🛠️ Technology Stack

- **Language**: Java 17
- **Framework**: Spring Boot 3.2.0
- **Web**: Spring Boot Starter Web
- **Database**: PostgreSQL 16
- **ORM**: Spring Data JPA with Hibernate
- **Caching**: Redis 7
- **Validation**: Spring Boot Starter Validation
- **Build Tool**: Maven
- **Containerization**: Docker & Docker Compose

## 📁 Project Structure

```
url-shortner/
├── src/main/java/com/idhanwal/urlshortener/
│   ├── UrlShortenerApplication.java       # Spring Boot Application Entry Point
│   ├── config/                            # Configuration Classes
│   ├── controller/                        # REST Controllers
│   ├── dto/                               # Data Transfer Objects
│   ├── model/                             # JPA Entity Models
│   ├── repository/                        # Data Access Layer
│   ├── service/                           # Business Logic
│   └── util/                              # Utility Classes
├── src/main/resources/
│   └── application.yml                    # Application Configuration
├── pom.xml                                # Maven Dependencies
├── docker-compose.yml                     # Docker Compose Configuration
├── Dockerfile                             # Docker Image Definition
└── mvnw                                   # Maven Wrapper
```

## 🚀 Getting Started

### Prerequisites

- Java 17 or higher
- Docker and Docker Compose (recommended)
- PostgreSQL 16 (if not using Docker)
- Redis 7 (if not using Docker)
- Maven 3.6+ or use the included Maven wrapper

### Quick Start with Docker Compose

1. **Clone the repository**:
   ```bash
   git clone https://github.com/idhanwal/url-shortener.git
   cd url-shortener/url-shortner
   ```

2. **Start services with Docker Compose**:
   ```bash
   docker-compose up -d
   ```

   This will start:
   - PostgreSQL database on port 5434
   - Redis cache on port 6379

3. **Build and run the application**:
   ```bash
   ./mvnw clean spring-boot:run
   ```

   The application will start on `http://localhost:8080`

### Manual Setup (Without Docker)

1. **Install PostgreSQL and Redis** on your machine

2. **Configure database connection** in `src/main/resources/application.yml`:
   ```yaml
   spring:
     datasource:
       url: jdbc:postgresql://localhost:5432/urlshortener
       username: postgres
       password: your_password
     jpa:
       hibernate:
         ddl-auto: update
   ```

3. **Build the application**:
   ```bash
   ./mvnw clean install
   ```

4. **Run the application**:
   ```bash
   ./mvnw spring-boot:run
   ```

## ⚙️ Configuration

### Application Settings (`application.yml`)

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:postgresql://localhost:5434/urlshortener
    username: postgres
    password: postgres
  jpa:
    hibernate:
      ddl-auto: update
    open-in-view: false
```

**Configuration Details**:
- **Server Port**: API runs on port 8080
- **Database**: PostgreSQL instance on port 5434 (when using Docker Compose)
- **JPA**: Hibernate auto-updates schema; `open-in-view` disabled for better performance

### Docker Compose Services

- **PostgreSQL**:
  - Image: `postgres:16`
  - Port: `5434:5432`
  - Database: `urlshortener`
  - Credentials: `postgres:postgres`

- **Redis**:
  - Image: `redis:7`
  - Port: `6379:6379`

## 📚 API Endpoints

The application provides RESTful endpoints for URL management (detailed documentation would be added based on your controllers):

### Example Endpoints

- `POST /api/urls/shorten` - Create a shortened URL
- `GET /api/urls/{shortCode}` - Retrieve the original URL by short code
- `GET /{shortCode}` - Redirect to original URL (if implemented)
- `DELETE /api/urls/{shortCode}` - Delete a shortened URL

*Note: Specific endpoint details depend on your controller implementations*

## 🏗️ Architecture

### Layered Architecture

```
Controller Layer
    ↓
Service Layer (Business Logic)
    ↓
Repository Layer (Data Access)
    ↓
Database (PostgreSQL) + Cache (Redis)
```

### Key Components

- **Controllers**: Handle HTTP requests and responses
- **Services**: Implement business logic and URL shortening algorithms
- **Models**: JPA entities representing database tables
- **DTOs**: Data transfer objects for API contracts
- **Repositories**: Spring Data JPA repositories for database operations
- **Config**: Spring configuration classes (Redis, Security, etc.)
- **Util**: Helper classes for URL encoding, hashing, etc.

## 💾 Database Schema

The application uses JPA/Hibernate for automatic schema management. Key entities include:

- **URL Entity**: Stores original URL, short code, creation timestamp, expiration date
- Additional entities as defined in the model package

## ⚡ Performance Optimization

- **Redis Caching**: Frequently accessed URLs are cached to reduce database queries
- **Connection Pooling**: Efficient database connection management
- **Lazy Loading**: Disabled `open-in-view` for better performance
- **Indexed Queries**: Database indexing on short codes for fast lookups

## 🔒 Security Features

- **Input Validation**: Spring Boot validation ensures data integrity
- **SQL Injection Prevention**: JPA parameterized queries
- **CORS Configuration**: Available in config layer (if implemented)

## 📦 Dependencies

Key dependencies in `pom.xml`:

- `spring-boot-starter-web`: Web framework
- `spring-boot-starter-data-jpa`: ORM support
- `spring-boot-starter-data-redis`: Redis integration
- `spring-boot-starter-validation`: Input validation
- `postgresql`: PostgreSQL JDBC driver
- `spring-boot-starter-test`: Testing framework

## 🧪 Testing

Run tests with Maven:

```bash
./mvnw test
```

## 📝 License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.

## 👤 Author

Created by [idhanwal](https://github.com/idhanwal)

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

For issues and questions:
- Open a [GitHub Issue](https://github.com/idhanwal/url-shortener/issues)
- Check existing documentation

## 🔗 Links

- [GitHub Repository](https://github.com/idhanwal/url-shortener)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Redis Documentation](https://redis.io/documentation)

---

**Last Updated**: December 2025