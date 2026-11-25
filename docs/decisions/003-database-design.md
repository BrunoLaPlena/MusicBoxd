# ADR-003: Initial Database Design and Data Ownership

- **Status:** Accepted
- **Date:** 2026-11-25
- **Decision owners:** MusicBoxd project

## Context

MusicBoxd will use an external music catalogue provider to retrieve information about songs, albums, and artists.

However, the application must also maintain its own user accounts and user-generated information.

The database design must therefore distinguish between:

- External music catalogue information.
- Internal MusicBoxd entities.
- User-generated application data.

The application should avoid tightly coupling its database to a single external provider.

## Decision

MusicBoxd will use PostgreSQL as its primary database.

The application will maintain its own internal identifiers for music entities.

External provider identifiers will be stored as references associated with internal records.

User-generated information will reference internal MusicBoxd identifiers rather than external provider identifiers.

## Data Ownership

### MusicBoxd-Owned Data

MusicBoxd is responsible for storing and managing:

- User accounts.
- Authentication information.
- Song ratings.
- Written reviews.
- Listening history.
- User-created lists.
- Favourites.
- Social interactions.
- Internal entity identifiers.

These records belong to MusicBoxd and must remain independent of external catalogue providers.

### External Catalogue Data

Spotify supplies catalogue information such as:

- Track titles.
- Artist names.
- Album names.
- Durations.
- Artwork.
- Release information.
- External identifiers.

The application must respect Spotify's developer policies when storing, displaying, caching, or reusing this information.

Not all external metadata should automatically be treated as permanently owned application data.

## Initial Database Entities

The initial database will focus on three entities:

### Users

Represents registered MusicBoxd users.

Expected information:

- Internal user ID.
- Username.
- Email.
- Password hash.
- Account creation timestamp.
- Relevant account status information.

Passwords must never be stored in plaintext.

### Songs

Represents music catalogue entries known to MusicBoxd.

Expected information:

- Internal song ID.
- External provider identifier.
- External provider name.
- Relevant timestamps.

Additional metadata may be stored only where permitted by the provider's policies and justified by the application requirements.

The initial external provider will be Spotify.

### Ratings

Represents a user's rating of a song.

Expected information:

- Internal rating ID.
- User ID.
- Song ID.
- Rating value.
- Creation timestamp.
- Last update timestamp.

Each rating must reference:

- One existing user.
- One existing MusicBoxd song.

## Initial Relationships

```text
+----------------+          +----------------+
|     USERS      |          |     SONGS      |
+----------------+          +----------------+
| id             |          | id             |
| username       |          | provider       |
| email          |          | external_id    |
| password_hash  |          | created_at     |
| created_at     |          +----------------+
+----------------+                  |
        |                           |
        | 1                         | 1
        |                           |
        |                           |
        | N                         | N
        +------------+--------------+
                     |
                     v
              +--------------+
              |   RATINGS    |
              +--------------+
              | id           |
              | user_id      |
              | song_id      |
              | rating       |
              | created_at   |
              | updated_at   |
              +--------------+
```

The relationship between users and songs is many-to-many through ratings.

A user can rate multiple songs, and a song can receive ratings from multiple users.

## Data Integrity Rules

The database must enforce important integrity rules.

### Primary Keys

Every entity must have a primary key.

Internal MusicBoxd identifiers will be used for relationships between entities.

### Foreign Keys

Ratings must reference existing users and songs.

Invalid references must be rejected by the database.

### Unique Constraints

The following values must be unique:

- Usernames.
- Email addresses.
- External provider identifiers within their provider namespace.
- The combination of user ID and song ID in the ratings table.

The `(user_id, song_id)` constraint ensures that a user cannot have multiple active ratings for the same song.

### Nullability

Required fields must not accept null values.

Optional metadata must be allowed to remain unavailable when appropriate.

### Rating Validation

Rating values must fall within the rating scale defined by the application.

The exact scale and increments will be established during implementation.

## External Identifiers

External identifiers must not be used as primary keys for internal MusicBoxd entities.

For example, a song will have:

- A MusicBoxd internal ID.
- A Spotify track ID.

Ratings will reference the MusicBoxd song ID.

This separation provides several advantages:

- User-generated data is independent of Spotify.
- External provider identifiers can change without changing internal relationships.
- Another provider may be introduced in the future.
- Provider migration can be performed without redesigning the entire application.

The initial implementation will support Spotify as the only provider.

A more complex multi-provider relationship model will only be introduced if additional providers become an actual requirement.

## Future Database Expansion

The database will eventually support additional entities.

Potential future entities include:

- Albums.
- Artists.
- Reviews.
- Listening history.
- Lists.
- Favourites.
- User follows.
- Comments.
- Likes.

Relationships between recordings, albums, artists, and releases may become more complex as the catalogue expands.

These relationships should be designed when their corresponding features are implemented.

The initial schema should not attempt to anticipate every future feature.

## Database Technology and Persistence

PostgreSQL will be used as the relational database.

The backend will use:

- Spring Data JPA.
- Hibernate.
- Flyway.

Flyway will manage schema changes through versioned database migrations.

Database schema changes should be committed to version control and applied consistently across environments.

## Consequences

### Positive

- MusicBoxd owns its user-generated data.
- Internal relationships remain stable.
- External providers can potentially be replaced.
- Database integrity is enforced.
- The initial schema remains relatively simple.
- The design can grow incrementally.

### Negative / Trade-offs

- External metadata and internal records must be associated.
- Some metadata may need to be retrieved from Spotify rather than stored permanently.
- Provider migration may require mapping and reconciliation work.
- Database design will become more complex as albums, artists, and social functionality are introduced.

## Reassessment Conditions

This decision may be revisited if:

- Another music provider is introduced.
- Spotify's data usage policies require changes to storage practices.
- New music entities require more complex relationships.
- Application requirements make the current schema insufficient.
