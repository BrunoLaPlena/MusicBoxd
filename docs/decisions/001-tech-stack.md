# ADR-001: Initial Technology Stack

- **Status:** Accepted
- **Date:** 2026-11-25
- **Decision owners:** MusicBoxd project

## Context

MusicBoxd is a personal software development project intended to provide practical experience with modern application development.

The project requires:

- A web frontend.
- A backend exposing an API.
- A relational database.
- External API integration.
- Authentication and user management.
- A foundation that can support future application clients.

The developer has previous exposure to Java, Angular, SQL, and related development tools, but wants to deepen their understanding of professional application architecture and development practices.

The technology stack should therefore provide a good learning experience without introducing unnecessary complexity.

## Decision

The following technologies have been selected:

| Layer               | Technology                  |
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

### Development Tools

| Purpose             | Tool                  |
| ------------------- | --------------------- |
| Backend IDE         | IntelliJ IDEA         |
| Frontend IDE        | Visual Studio Code    |
| Database management | pgAdmin               |
| API testing         | Postman or equivalent |
| Version control     | Git                   |

Exact software versions will be selected during environment setup, prioritizing compatible and supported releases.

## Architectural Decisions

### Modular Monolith

The backend will initially be a single Spring Boot application organized into logical modules.

Microservices will not be introduced.

### Monorepo

The frontend, backend, and project documentation will be stored in a single Git repository.

### Maven Wrapper

The backend will include Maven Wrapper to make builds more reproducible across environments.

### Native Development Environment

The initial development environment will use locally installed tools and PostgreSQL.

Docker will be introduced later when containerization becomes relevant.

## Alternatives Considered

### Backend

**Node.js / Express or NestJS**

Advantages:

- JavaScript or TypeScript across the stack.
- Large ecosystem.
- Good web development support.

Disadvantages:

- Less opportunity to deepen existing Java knowledge.
- Less alignment with the intended Java/Spring learning objectives.

**Decision:** Java and Spring Boot.

### Frontend

**React**

Advantages:

- Large ecosystem.
- Flexible component model.
- Extensive community support.

Disadvantages:

- Would introduce a different frontend framework from the developer's existing Angular experience.

**Decision:** Angular.

### Database

**MySQL**

Advantages:

- Mature relational database.
- Widely used.

Disadvantages:

- PostgreSQL provides a strong feature set and is already familiar to the developer.

**Decision:** PostgreSQL.

### Architecture

**Microservices**

Advantages:

- Independent deployment and scaling.
- Service-level separation.

Disadvantages:

- Significant operational and architectural complexity.
- Unnecessary for a small application developed by one person.
- Would distract from learning the core application development concepts.

**Decision:** Modular monolith.

## Consequences

### Positive

- The stack builds on existing knowledge.
- Java and Spring Boot provide a strong backend foundation.
- Angular provides a structured frontend framework.
- PostgreSQL supports relational data and complex relationships.
- REST allows future clients to reuse the backend.
- The architecture remains relatively simple.

### Negative / Trade-offs

- Java and Spring Boot introduce more configuration and concepts than some lightweight alternatives.
- Angular has a substantial framework learning curve.
- The developer must work across multiple languages and tools.
- The monorepo requires maintaining separate frontend and backend build environments.

## Reassessment Conditions

This decision may be revisited if:

- A selected technology becomes unsuitable or unsupported.
- The project develops requirements that the current architecture cannot reasonably support.
- A major change in project goals justifies a different stack.
