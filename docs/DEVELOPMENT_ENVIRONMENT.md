# MusicBoxd — Development Environment

## 1. Overview

This document describes the local development environment used for MusicBoxd, including the required software, installed versions, and basic verification procedures.

The initial development environment uses locally installed tools and services, following the native development approach established in ADR-001.

The versions documented here reflect the development machine's verified state. They should not automatically be treated as the versions required by the application itself.

## 2. Operating System

| Component        | Version    |
| ---------------- | ---------- |
| Operating System | Windows 11 |
| Architecture     | x64        |

## 3. Development Tools

### 3.1 Java

| Component        | Version         |
| ---------------- | --------------- |
| JDK Distribution | Eclipse Temurin |
| Java Version     | 21.0.10 LTS     |

Java 21 is the selected development JDK for the Spring Boot backend.

Verification:

```powershell
java -version
javac -version
```

### 3.2 Node.js and npm

| Component | Version |
| --------- | ------- |
| Node.js   | 24.20.0 |
| npm       | 12.0.2  |

Node.js provides the JavaScript runtime required by Angular tooling.

Verification:

```powershell
node --version
npm --version
```

### 3.3 Angular CLI

| Component   | Version |
| ----------- | ------- |
| Angular CLI | 22.3.0  |

Angular CLI is installed globally to provide the Angular development commands.

The Angular framework version used by the actual frontend application will be established when the application is initialized.

Verification:

```powershell
ng version
```

### 3.4 Maven

| Component    | Version |
| ------------ | ------- |
| Apache Maven | 3.9.14  |

Maven is installed globally. However, the backend project will use Maven Wrapper to ensure consistent builds and avoid depending on the globally installed Maven version.

Once initialized, Maven commands should be executed through the project wrapper.

Verification:

```powershell
mvn -version
```

### 3.5 Integrated Development Environments

| Purpose              | Application        |
| -------------------- | ------------------ |
| Backend development  | IntelliJ IDEA      |
| Frontend development | Visual Studio Code |

Both applications are installed.

## 4. Database Environment

### 4.1 PostgreSQL

| Component         | Version           |
| ----------------- | ----------------- |
| PostgreSQL Server | 18.3              |
| Host              | localhost         |
| Port              | 5432              |
| Windows Service   | postgresql-x64-18 |

PostgreSQL is installed locally and running as a Windows service.

Database connectivity has been verified through an authenticated connection using `psql`.

Verification:

```powershell
psql --version
pg_isready
```

To test an authenticated connection:

```powershell
psql -h localhost -p 5432 -U postgres -d postgres
```

The local PostgreSQL installation contains databases from previous development coursework. MusicBoxd will use its own dedicated database and application credentials.

Existing databases and credentials must not be reused indiscriminately.

### 4.2 pgAdmin

pgAdmin 4 is installed and successfully connected to the local PostgreSQL 18 server.

It will be used for database inspection, SQL execution, and database administration.

## 5. Version Control

| Component  | Version |
| ---------- | ------- |
| Git        | 2.55.0  |
| GitHub CLI | 2.105.0 |

Git is configured with a global user identity, and GitHub CLI authentication has been established.

The project repository is hosted on GitHub:

https://github.com/BrunoLaPlena/MusicBoxd

Verification:

```powershell
git --version
gh --version
gh auth status
```

## 6. Application Version Management

The installed development tools and the application dependencies are separate concerns.

The following versions must be established during application initialization:

- Spring Boot version.
- Angular framework version.
- Maven Wrapper version.

Version selection must prioritize compatibility, supported releases, and reproducible builds.

The project should document the actual application dependency versions rather than assuming they match globally installed tools.

## 7. Environment Configuration

Development configuration should be kept separate from production configuration.

Sensitive information, including database passwords and external API credentials, must not be committed to the repository.

Environment-specific configuration should be supplied through appropriate environment variables or local configuration files excluded by `.gitignore`.

## 8. Verification Checklist

The following checks have been completed on the initial development machine:

- [x] Java JDK installed and verified.
- [x] Node.js and npm installed and verified.
- [x] Angular CLI installed and verified.
- [x] Maven installed and verified.
- [x] IntelliJ IDEA installed.
- [x] Visual Studio Code installed.
- [x] PostgreSQL server installed and running.
- [x] PostgreSQL authenticated connection verified.
- [x] pgAdmin installed and connected.
- [x] Git installed and configured.
- [x] GitHub CLI installed and authenticated.
- [x] GitHub repository created and initialized.

The following tasks remain:

- [ ] Finalize Spring Boot and Angular application versions.
- [ ] Initialize the backend and frontend applications.
- [ ] Configure Maven Wrapper.
- [ ] Create the dedicated MusicBoxd database and application user.
- [ ] Configure environment-specific application settings.
- [ ] Verify both applications run independently.
- [ ] Verify backend connectivity to the MusicBoxd database.

---

This document should be updated whenever the development environment or required tooling changes significantly.
