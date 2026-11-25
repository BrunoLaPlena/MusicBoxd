
# MusicBoxd — Requirements Specification

## 1. Introduction

### 1.1 Purpose

This document defines the functional and non-functional requirements for MusicBoxd.

It establishes the expected behaviour of the application and serves as a reference during implementation and testing.

### 1.2 Project Description

MusicBoxd is a music discovery and rating platform inspired by Letterboxd.

Users will be able to discover music, maintain personal libraries, rate songs, write reviews, track listening activity, and eventually interact with other users.

The initial application will focus on discovering and rating individual songs.

### 1.3 Initial Scope

The first version of MusicBoxd will provide:

- Music catalogue search.
- Song information pages.
- User registration and authentication.
- Song ratings.
- Community rating information.
- Basic navigation.

The application will use Spotify's Web API as its initial external music catalogue provider.

## 2. Functional Requirements

### FR-01 — Music Catalogue

The application must allow users to discover songs using the external music catalogue.

- **FR-01.1:** Users must be able to search for songs by title.
- **FR-01.2:** Users must be able to search using an artist's name.
- **FR-01.3:** Search results must display relevant song information.
- **FR-01.4:** Users must be able to open individual song detail pages.
- **FR-01.5:** Song detail pages must display available metadata.
- **FR-01.6:** The application should display available album artwork.
- **FR-01.7:** The application must associate external catalogue entries with internal MusicBoxd song records.
- **FR-01.8:** The application must handle unavailable or incomplete external metadata gracefully.

### FR-02 — User Accounts

The application must support individual user accounts.

- **FR-02.1:** Users must be able to register an account.
- **FR-02.2:** Users must be able to log in.
- **FR-02.3:** Users must be able to log out.
- **FR-02.4:** Usernames must be unique.
- **FR-02.5:** Email addresses must be unique.
- **FR-02.6:** Users must only be able to modify their own account information.
- **FR-02.7:** Passwords must be securely hashed before storage.

### FR-03 — Song Ratings

Authenticated users must be able to rate songs.

- **FR-03.1:** Authenticated users must be able to submit a rating for a song.
- **FR-03.2:** Each user may have only one active rating per song.
- **FR-03.3:** Users must be able to modify their own ratings.
- **FR-03.4:** Users must be able to delete their own ratings.
- **FR-03.5:** Song detail pages must display the community average rating.
- **FR-03.6:** Song detail pages must display the total number of ratings.
- **FR-03.7:** Unauthenticated users must not be able to submit or modify ratings.

The rating scale and its exact increments will be established during implementation.

### FR-04 — Basic Navigation

The application must provide a basic and understandable navigation structure.

- **FR-04.1:** Users must be able to access the homepage.
- **FR-04.2:** Users must be able to access the search functionality.
- **FR-04.3:** Users must be able to navigate to song detail pages.
- **FR-04.4:** Users must be able to access account-related pages.
- **FR-04.5:** Authenticated users must be able to view their own ratings.

## 3. Non-Functional Requirements

### NFR-01 — Maintainability

- The codebase must follow a clear and understandable structure.
- Responsibilities must be separated appropriately.
- Components should have focused responsibilities.
- Technical decisions should be documented when relevant.
- Avoid unnecessary complexity and premature abstractions.

### NFR-02 — Security

- Passwords must never be stored in plaintext.
- Sensitive credentials must not be committed to version control.
- Protected operations must require authentication.
- Users must only be able to modify their own private data.
- External API credentials must remain on the backend.
- Input must be validated on the server.

### NFR-03 — Data Integrity

- Database relationships must be enforced through appropriate constraints.
- Each user must have at most one active rating per song.
- Required fields must not accept invalid null values.
- External identifiers must be associated with the correct provider.

### NFR-04 — Performance

- The application should provide responsive interactions under ordinary MVP usage.
- Database queries should avoid unnecessary work.
- External API requests should be handled efficiently.
- Appropriate caching should be considered to reduce unnecessary external requests.

No strict numerical performance targets are established for the initial MVP.

### NFR-05 — Reliability

- External API failures must not crash the application.
- The application must provide understandable error messages.
- Temporary service failures should be handled gracefully.
- Database operations should preserve data consistency.

### NFR-06 — Usability

- The application should have an intuitive interface.
- Navigation should be consistent.
- The interface should be responsive across desktop and mobile browsers.
- Loading, empty, and error states should be communicated clearly.

### NFR-07 — Compatibility

- The frontend and backend must communicate through a documented REST API.
- The backend should remain independent of the frontend implementation.
- The backend API should be reusable by future clients.

### NFR-08 — Testability

- Core business logic should have automated tests.
- Important API endpoints should have integration tests.
- Database interactions should be tested.
- Critical user workflows should be validated.

### NFR-09 — Portability

- Development setup instructions must be documented.
- Project dependencies and required versions should be recorded.
- Another developer should be able to reproduce the development environment using the documentation.

### NFR-10 — Privacy

- The application should collect only the personal information required for its functionality.
- User data should be handled responsibly.
- Future public deployment must consider applicable privacy legislation, including GDPR.

## 4. Explicitly Out of Scope for the Initial MVP

The following features are part of the long-term vision but will not be implemented initially:

- Album catalogues and album ratings.
- Artist profiles and artist ratings.
- Written reviews.
- Listening diaries and history.
- User-created lists.
- Favourites and collections.
- Public user profiles.
- Following other users.
- Likes and comments.
- Activity feeds.
- Personalized recommendations.
- Advanced music discovery.
- Native Android applications.
- Desktop applications.

## 5. Future Requirements

Future versions may introduce additional requirements for:

- Albums, artists, and more complex music relationships.
- Reviews and listening history.
- User profiles and statistics.
- Social networking.
- Recommendations and discovery.
- Additional external music providers.
- Additional application clients.

These requirements will be specified in more detail when their respective development phases begin.

## 6. Requirements Management

Requirements may evolve as the project develops.

Changes that significantly affect project scope or architecture should be reflected in this document.

Detailed implementation tasks and acceptance criteria should be tracked separately through the project's issue-tracking system.
