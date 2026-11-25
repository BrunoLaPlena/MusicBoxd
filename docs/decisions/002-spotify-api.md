# ADR-002: Spotify Web API as Initial Music Catalogue Provider

- **Status:** Accepted
- **Date:** 2026-11-25
- **Decision owners:** MusicBoxd project

## Context

MusicBoxd requires a music catalogue to provide information about songs, albums, and artists.

The catalogue should ideally provide:

- Broad music coverage.
- Accurate song and artist information.
- Album associations.
- Track durations.
- Album artwork.
- Identifiers for external catalogue entries.
- Search functionality.

Several possible providers were considered, including Spotify Web API, MusicBrainz, Apple Music API, and Discogs.

MusicBrainz offers an extensive open metadata database, but its community-maintained catalogue can have uneven completeness. Spotify offers a more commercially oriented music catalogue and is expected to provide a more familiar and reliable discovery experience for the initial project.

The project is currently a personal learning and testing project. A public launch is not expected in the near future.

## Decision

Spotify Web API will be the initial external music catalogue provider.

The initial implementation will focus on searching for tracks and retrieving their associated metadata.

The application will use Spotify's Client Credentials Flow for public catalogue access.

MusicBoxd users will authenticate with MusicBoxd independently of Spotify.

## Authentication Strategy

Spotify supports different authentication flows.

### Client Credentials Flow

The application authenticates using its own Spotify application credentials.

This is suitable for public catalogue information that does not require access to an individual Spotify user's private account.

The backend will:

1. Store the Spotify application credentials securely.
2. Request an access token.
3. Use the token to access Spotify's catalogue endpoints.
4. Refresh the token when necessary.

Spotify credentials must never be exposed to the frontend.

### User Authorization

Spotify's Authorization Code Flow is intended for access to individual Spotify user data and account-specific functionality.

This is not required for the initial MVP.

MusicBoxd users will not need to connect their Spotify accounts to search for and rate songs.

## Development Mode Restrictions

Spotify Development Mode has restrictions that must be considered.

Current documented restrictions include:

- The app owner must have an eligible Spotify Premium account.
- A Development Mode application is limited to five authorized Spotify users.
- Available API endpoints are restricted.
- Development Mode is intended for development and experimentation rather than serving as an unrestricted public platform.

The five-authorized-user restriction should not be confused with the number of MusicBoxd accounts.

When using Client Credentials Flow, MusicBoxd users are not individually authorized Spotify users.

However, this does not mean that the application has unrestricted permission to serve an arbitrary public audience.

Spotify's quota and access policies must be reviewed before expanding the application beyond its intended personal development use.

Extended Quota Mode has additional eligibility requirements and should not be assumed to be available to an individual developer.

## Data Ownership

Spotify provides external music catalogue information.

MusicBoxd owns:

- Internal song identifiers.
- User accounts.
- Ratings.
- Reviews.
- Listening history.
- Favourites and lists.
- Social interactions.
- Other user-generated information.

External Spotify identifiers will be stored as references associated with internal MusicBoxd records.

User-generated information must not depend directly on Spotify identifiers.

## Integration Principles

Spotify communication will be isolated within the backend.

The application should not expose Spotify response structures directly throughout its business logic.

External responses should be mapped to internal application models.

The initial integration will prioritize:

- Track search.
- Track details.
- Artist information associated with tracks.
- Album information associated with tracks.
- Available artwork.
- External identifiers.

The integration must handle:

- Authentication failures.
- Rate limits.
- Network errors.
- Unavailable catalogue entries.
- Incomplete metadata.
- Unexpected API responses.

Caching should be considered to reduce unnecessary API requests.

## Data Usage and Policy Compliance

Spotify's developer terms and policies govern how its API data can be used.

The implementation must review and respect applicable requirements concerning:

- Attribution.
- Display of Spotify content.
- Artwork usage.
- Metadata storage and caching.
- Commercial use.
- Restrictions on modifying or combining Spotify content with other data.

The project must not assume that all metadata returned by the API can be stored indefinitely or reused without restrictions.

Applicable Spotify policies should be reviewed again before deployment or public distribution.

## Alternatives Considered

### MusicBrainz

Advantages:

- Open music metadata database.
- Extensive recording, release, and artist relationships.
- Core data is available under a permissive CC0 licence.

Disadvantages:

- Community-maintained metadata can be incomplete.
- Public API is rate-limited.
- Search and catalogue experience may be less consistent for mainstream discovery.
- Hosted API commercial usage requires separate consideration.

### Apple Music API

Advantages:

- Commercial music catalogue.
- Track, album, artist, and artwork metadata.
- Alternative versions and catalogue relationships.

Disadvantages:

- Apple developer ecosystem dependency.
- Different access and usage requirements.
- Not selected for the initial implementation.

### Discogs API

Advantages:

- Extensive release and edition information.
- Particularly useful for physical releases and discographies.

Disadvantages:

- Release-oriented data model is less suitable as the primary song catalogue for MusicBoxd.

## Consequences

### Positive

- Familiar and recognizable music catalogue.
- Strong fit for the initial song discovery experience.
- Rich track, album, and artist metadata.
- Straightforward integration through HTTP and JSON.
- Reduces uncertainty about whether commonly known music is represented.

### Negative / Trade-offs

- Dependency on Spotify's service and policies.
- Development Mode restrictions.
- Potential API availability and rate-limit constraints.
- Restrictions on storage and reuse of catalogue information.
- Future public deployment may require a different access arrangement or provider.

## Future Reassessment

Spotify will be used for the initial MVP.

The decision must be reassessed before:

- Public launch.
- Significant expansion of the user base.
- Commercial use.
- Introducing features that require individual Spotify user authorization.
- Any change in Spotify's API access or data usage policies.

MusicBoxd's internal identifiers and user-owned data must remain independent of Spotify to make future migration possible.

## References

- Spotify Web API Documentation: https://developer.spotify.com/documentation/web-api
- Spotify Authorization Documentation: https://developer.spotify.com/documentation/web-api/concepts/authorization
- Spotify Developer Policy: https://developer.spotify.com/policy
- Spotify Developer Terms: https://developer.spotify.com/terms
- Spotify Quota Modes: https://developer.spotify.com/documentation/web-api/concepts/quota-modes
