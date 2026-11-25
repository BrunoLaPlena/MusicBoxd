# MusicBoxd — Development Roadmap

## 1. Project Overview

MusicBoxd is a music discovery and rating platform inspired by Letterboxd.

The long-term goal is to create a platform where users can discover music, maintain a personal listening history, rate and review songs, organize their libraries, and interact with other music enthusiasts.

The project will initially be developed as a personal learning project by a single developer. Development will prioritize learning, maintainability, and incremental progress over rapid feature delivery.

The initial application will be a web application consisting of an Angular frontend, a Java Spring Boot backend, and a PostgreSQL database.

## 2. Development Philosophy

The project will follow these principles:

- **Incremental development:** Build a small working application first and expand it gradually.
- **Learning by doing:** Introduce technologies and concepts when they become relevant.
- **Avoid overengineering:** Do not implement infrastructure or abstractions for hypothetical future requirements.
- **Maintainability:** Prefer understandable, organized code over unnecessarily clever solutions.
- **Separation of concerns:** Keep the frontend, backend, database, and external services appropriately separated.
- **Documentation as code:** Keep technical decisions, requirements, and development documentation in the repository.
- **Testing:** Introduce automated tests alongside functionality rather than leaving testing until the end.

## 3. Project Phases

### Phase 0 — Product Definition and Planning

**Status:** Completed

Define the purpose, initial scope, requirements, and technical direction of MusicBoxd.

Tasks:

- Define the project's vision and long-term goals.
- Establish the initial MVP scope.
- Decide which music entities will be supported initially.
- Establish functional and non-functional requirements.
- Select the initial technology stack.
- Select the initial music catalogue provider.
- Define high-level architectural principles.
- Establish initial database design principles.

Deliverables:

- Project requirements.
- Development roadmap.
- High-level architecture documentation.
- Initial Architecture Decision Records.

### Phase 1 — Development Environment and Project Setup

**Status:** In Progress

Prepare the local development environment and initialize the repository.

Tasks:

- [x] Review the existing development environment.
- [x] Install and configure the required development tools.
- [x] Select compatible versions of Java, Node.js, Angular, Spring Boot, and PostgreSQL.
  - [x] Select and verify Java JDK 21.
  - [x] Select and verify Node.js 24 and npm.
  - [x] Install and verify Angular CLI 22.
  - [x] Verify PostgreSQL 18.
  - [x] Finalize Spring Boot and Angular application versions.
- [x] Configure Git and GitHub.
- [x] Create the project repository.
- [ ] Establish the monorepo directory structure.
- [ ] Initialize the Spring Boot backend.
- [ ] Initialize the Angular frontend.
- [ ] Configure Maven Wrapper.
- [ ] Configure environment-specific settings.
- [ ] Establish a suitable `.gitignore`.
- [ ] Verify that both applications run independently.
- [ ] Verify backend connectivity to PostgreSQL.

Deliverables:

- [x] Functional initial local development environment.
- [x] Initialized GitHub repository.
- [ ] Working Spring Boot application.
- [ ] Working Angular application.
- [x] Working PostgreSQL installation and connection.

**Progress notes:**

- Initial development tools have been installed and verified.
- PostgreSQL connectivity has been tested successfully through both `psql` and pgAdmin.
- The public GitHub repository has been created and the initial documentation committed.
- Detailed environment information is maintained in `docs/DEVELOPMENT_ENVIRONMENT.md`.
- Application initialization and MusicBoxd-specific database configuration remain outstanding.

### Phase 2 — Documentation and Development Workflow

**Status:** Pending

Establish the documentation and development practices that will be used throughout the project.

Tasks:

- Create and maintain the project README.
- Create the roadmap, requirements, and architecture documents.
- Establish Architecture Decision Records (ADRs).
- Define Git branching and commit conventions.
- Establish a basic issue-tracking workflow.
- Document the development and execution procedures.
- Keep documentation synchronized with implementation decisions.

Deliverables:

- Documented repository.
- Established Git workflow.
- Initial development conventions.

### Phase 3 — Backend Foundations

**Status:** Pending

Learn the fundamentals of Spring Boot and build the initial backend structure.

Topics and tasks:

- Spring Boot project structure.
- Dependency injection and Spring beans.
- Application configuration.
- REST APIs and HTTP fundamentals.
- Controllers and request handling.
- HTTP methods and status codes.
- DTOs and request/response models.
- Service and repository layers.
- Input validation.
- Error handling and exception management.
- Logging.
- Unit and integration testing.
- JUnit and Spring Boot testing tools.

Deliverable:

- Functional backend exposing basic REST endpoints.
- Established backend structure and conventions.

### Phase 4 — Database Foundations

**Status:** Pending

Learn relational database concepts and integrate PostgreSQL with the backend.

Topics and tasks:

- Relational database fundamentals.
- Tables, columns, and data types.
- Primary and foreign keys.
- One-to-one, one-to-many, and many-to-many relationships.
- Database normalization.
- SQL CRUD operations.
- Joins and aggregations.
- Constraints and indexes.
- PostgreSQL integration.
- JPA and Hibernate fundamentals.
- Entities and repositories.
- Database migrations with Flyway.
- Persistence and integration testing.

Initial database entities:

- Users.
- Songs.
- Ratings.

Deliverable:

- PostgreSQL integrated with the backend.
- Initial database schema and persistence layer.

### Phase 5 — External Music API Integration

**Status:** Pending

Integrate the Spotify Web API to retrieve music catalogue information.

Tasks:

- Understand Spotify API authentication.
- Configure Client Credentials Flow.
- Understand HTTP requests and JSON responses.
- Implement Spotify API communication.
- Search for tracks.
- Retrieve detailed track information.
- Map Spotify responses to internal application models.
- Associate external Spotify identifiers with internal MusicBoxd records.
- Retrieve relevant album, artist, and artwork information.
- Handle API errors, timeouts, and rate limits.
- Implement appropriate caching.
- Review Spotify developer policies and data usage restrictions.
- Test search quality and metadata availability.

Deliverable:

- Backend capable of searching Spotify's music catalogue and returning application-ready song information.

### Phase 6 — Frontend Foundations

**Status:** Pending

Build the Angular frontend and connect it to the backend.

Topics and tasks:

- Angular project structure.
- Components and component communication.
- Services and dependency injection.
- Routing and navigation.
- Signals and reactive programming.
- HTTP communication with HttpClient.
- API service organization.
- Loading and error states.
- Forms and validation.
- Styling and reusable components.
- Responsive layouts.
- Basic accessibility.

Initial pages:

- Homepage.
- Search page.
- Search results.
- Song detail page.
- Login and registration pages.

Deliverable:

- Functional Angular frontend communicating with the backend.

### Phase 7 — First Complete MVP

**Status:** Pending

Combine the frontend, backend, database, and Spotify integration into a functional application.

Tasks:

**Music catalogue**

- Search for songs.
- Display search results.
- Open song detail pages.
- Display available song metadata and artwork.
- Associate Spotify tracks with internal MusicBoxd records.

**User accounts**

- User registration.
- User login and logout.
- Password hashing and secure storage.
- Authentication and authorization.
- Account information.

**Ratings**

- Rate songs.
- Enforce one active rating per user and song.
- Edit existing ratings.
- Delete ratings.
- Display community average ratings.
- Display total rating counts.

**Integration and quality**

- Connect all application layers.
- Implement appropriate validation.
- Handle errors across the application.
- Test complete user workflows.
- Review basic application security.
- Improve usability and responsive layouts.

Deliverable:

- Working MusicBoxd MVP supporting song discovery, user accounts, and song ratings.

### Phase 8 — Quality, Deployment, and Maintenance

**Status:** Pending

Prepare the MVP for deployment and more realistic usage.

Tasks:

- Review application architecture and code quality.
- Expand automated testing.
- Review security and authentication.
- Improve logging and error reporting.
- Review performance and database queries.
- Improve accessibility.
- Configure production environments.
- Introduce Docker and containerization.
- Deploy backend and frontend.
- Configure production database.
- Configure domain and HTTPS.
- Implement database backups.
- Establish basic CI pipelines.
- Document deployment and recovery procedures.

Deliverable:

- Deployed and maintainable MusicBoxd MVP.

### Phase 9 — Feature Expansion

**Status:** Future

Expand MusicBoxd beyond the initial song-rating experience.

Features will be introduced incrementally, based on learning, practical needs, and project priorities.

#### 9.1 Albums

- Album catalogue and search.
- Album detail pages.
- Track listings.
- Album ratings.
- Album reviews.
- Relationships between albums, tracks, and artists.

#### 9.2 Artists

- Artist catalogue and profiles.
- Discographies.
- Artist ratings and reviews.
- Relationships between artists, albums, and songs.

#### 9.3 Reviews and Listening History

- Written reviews.
- Listening diary.
- Listening history.
- Personal lists and collections.
- Favourites.

#### 9.4 User Profiles

- Public user profiles.
- User activity.
- Rating history.
- Personal statistics.
- Profile customization.

#### 9.5 Social Features

- Following users.
- Activity feeds.
- Likes and comments.
- Social interactions.
- Evaluate real-time functionality if it becomes necessary.

#### 9.6 Discovery and Recommendations

- Advanced search and filtering.
- Genre exploration.
- Trending music.
- Personalized recommendations.
- User statistics and insights.

#### 9.7 Additional Clients

- Native Android application.
- Desktop application.
- Reuse the existing backend API.

## 4. Roadmap Management

This roadmap represents the current intended direction, not an inflexible development contract.

Phases may be adjusted when new information, technical constraints, or learning opportunities justify doing so.

Detailed implementation tasks should be tracked separately using GitHub Issues or an equivalent issue-tracking system.

Major architectural and technology decisions should be documented through Architecture Decision Records.

Completed phases should have their deliverables reviewed before moving forward.
