# MusicBoxd — System Architecture

## 1. Overview

MusicBoxd will initially follow a client-server architecture consisting of three primary components:

1. Angular frontend.
2. Java Spring Boot backend.
3. PostgreSQL database.

The backend will also communicate with Spotify's Web API to retrieve music catalogue information.

The initial architecture will be implemented as a modular monolith.

## 2. Architectural Principles

### 2.1 Modular Monolith

The backend will initially be developed as a single Spring Boot application.

Its internal structure will separate responsibilities into logical modules, but all modules will run within the same application.

Microservices are explicitly out of scope.

A modular monolith provides a simpler development and deployment model while allowing the codebase to remain organized as it grows.

### 2.2 Separation of Concerns

Each application layer should have clearly defined responsibilities.

- The frontend handles presentation and user interaction.
- The backend handles application logic, validation, authentication, and external integrations.
- The database handles persistent application data.
- External providers supply catalogue information.

### 2.3 Backend Independence

The backend must expose a REST API that can be consumed independently of the Angular frontend.

Future Android and desktop applications should be able to reuse the same backend.

### 2.4 Incremental Complexity

Only introduce additional architectural patterns, abstractions, and infrastructure when they solve an actual problem.

The initial implementation should favor straightforward solutions.

## 3. High-Level System Architecture

```text
                 USER
                  |
                  v
        +--------------------+
        | Angular Frontend   |
        |                    |
        | Components         |
        | Pages              |
        | Services           |
        +--------------------+
                  |
             REST / JSON
                  |
                  v
        +--------------------+
        | Spring Boot        |
        | Backend            |
        |                    |
        | Controllers        |
        | Services           |
        | Repositories       |
        +--------------------+
             |          |
             |          |
             v          v
       +----------+  +----------------+
       |PostgreSQL|  | Spotify Web API|
       | Database |  |                |
       +----------+  +----------------+
```

The frontend communicates exclusively with the backend for application data.

The backend communicates with PostgreSQL for persistence and Spotify for external catalogue information.

Spotify credentials must never be exposed to the frontend.

## 4. Technology Stack

| Component           | Technology                  |
| ------------------- | --------------------------- |
| Frontend            | Angular                     |
| Frontend language   | TypeScript                  |
| Backend             | Java                        |
| Backend framework   | Spring Boot                 |
| Database            | PostgreSQL                  |
| ORM                 | Spring Data JPA / Hibernate |
| Database migrations | Flyway                      |
| API communication   | REST / JSON                 |
| Build system        | Maven                       |
| Version control     | Git / GitHub                |
| Backend IDE         | IntelliJ IDEA               |
| Frontend IDE        | Visual Studio Code          |
| API testing         | Postman or equivalent       |

Exact versions will be selected and verified during Phase 1.

## 5. Repository Structure

The project will initially use a monorepo.

```text
MusicBoxd/
│
├── backend/
│   ├── src/
│   ├── pom.xml
│   └── mvnw
│
├── frontend/
│   ├── src/
│   ├── package.json
│   └── angular.json
│
├── docs/
│   ├── ROADMAP.md
│   ├── REQUIREMENTS.md
│   ├── ARCHITECTURE.md
│   └── decisions/
│       ├── 001-tech-stack.md
│       ├── 002-spotify-api.md
│       └── 003-database-design.md
│
├── .gitignore
└── README.md
```

The structure may evolve as the project grows.

## 6. Backend Architecture

The backend will use a layered structure.

### 6.1 Controllers

Controllers expose REST endpoints and handle incoming HTTP requests.

Responsibilities:

- Receive requests.
- Validate request structure.
- Delegate operations to services.
- Return appropriate HTTP responses.

Controllers should not contain business logic or directly implement database operations.

### 6.2 Services

Services implement application and business logic.

Responsibilities:

- Coordinate application operations.
- Apply business rules.
- Communicate with repositories.
- Coordinate external API calls.
- Enforce application-level validation.

### 6.3 Repositories

Repositories handle database access.

Responsibilities:

- Retrieve entities.
- Persist entities.
- Update and delete records.
- Execute database queries.

Spring Data JPA will initially be used to simplify persistence operations.

### 6.4 External Integrations

Communication with Spotify should be isolated from the rest of the application.

A dedicated integration service will handle:

- Authentication.
- HTTP requests.
- Response handling.
- Mapping Spotify data to internal application models.
- Error handling and rate limits.

The rest of the application should not depend directly on Spotify response structures.

### 6.5 DTOs

Data Transfer Objects will define the information exchanged through the REST API.

They will prevent internal database entities from being exposed directly to clients.

## 7. Frontend Architecture

The frontend will use Angular.

Its initial structure will separate:

- Pages and routed components.
- Reusable UI components.
- Services responsible for API communication.
- Shared models and types.
- Application-level navigation and configuration.

Angular services will handle communication with the backend.

Components should focus primarily on presentation and user interaction rather than implementing application-wide business logic.

## 8. Database Architecture

PostgreSQL will be the primary persistent data store.

The initial schema will include:

- Users.
- Songs.
- Ratings.

MusicBoxd will own its internal identifiers and user-generated data.

External music catalogue identifiers will be stored as references.

Ratings and other user-generated records will reference internal MusicBoxd identifiers rather than external provider identifiers.

Database schema changes will be managed through Flyway migrations.

Further details are documented in `decisions/003-database-design.md`.

## 9. External Music Catalogue

Spotify Web API will be the initial source of music catalogue information.

The backend will use Client Credentials Flow for public catalogue access.

The initial integration will focus on:

- Track search.
- Track information.
- Artist and album information associated with tracks.
- Available artwork and metadata.

The application must handle incomplete metadata and external API failures.

Spotify integration should remain isolated so that another provider could potentially be introduced in the future.

The application must comply with Spotify's current developer policies and data usage restrictions.

Further details are documented in `decisions/002-spotify-api.md`.

## 10. Authentication and Authorization

The application will support its own user accounts.

MusicBoxd authentication is independent of Spotify authentication.

Spotify credentials are used by the backend to access the external catalogue. MusicBoxd users do not need individual Spotify accounts to use the initial MVP.

The backend will be responsible for:

- Password hashing.
- Authentication.
- Authorization.
- Protecting user-specific operations.

The exact authentication mechanism will be selected during backend implementation.

## 11. API Design

The backend will expose REST endpoints using JSON.

Initial endpoint groups will include:

- `/api/auth`
- `/api/users`
- `/api/songs`
- `/api/ratings`

The exact endpoint definitions will be established during implementation.

HTTP methods and status codes should follow REST conventions.

API request and response models should be documented and validated.

## 12. Testing Strategy

Testing will be introduced progressively.

### Backend

- Unit tests for business logic.
- Integration tests for persistence and services.
- API endpoint tests.
- External integration tests using controlled responses where appropriate.

### Frontend

- Component tests.
- Service tests.
- Tests for important user interactions.

### Integration

- Validate communication between frontend and backend.
- Test complete user workflows.
- Verify error handling and data consistency.

## 13. Deployment Strategy

Deployment is outside the initial development scope.

During the initial development phase:

- Backend, frontend, and PostgreSQL will run locally.
- Development configuration will be kept separate from production configuration.
- Secrets will be stored outside version control.

During Phase 8, the project will introduce appropriate deployment infrastructure, containerization, HTTPS, backups, and CI.

## 14. Future Architectural Evolution

The architecture should be able to accommodate:

- Additional music catalogue entities.
- Reviews and listening history.
- Social networking.
- Recommendations.
- Additional frontend clients.
- Additional music providers.

These capabilities do not justify implementing their infrastructure in advance.

The modular monolith will remain the default architecture unless concrete requirements justify changing it.
