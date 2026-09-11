# JobFlow AI

## Overview

JobFlow AI is a full-stack web application for managing job applications and interview processes.

The project is being built as a production-oriented portfolio project to practise modern full-stack software development, including frontend development with React and TypeScript, backend development with Spring Boot, testing, deployment, and cloud engineering.

The project will be developed incrementally. The initial focus is on establishing a clean project structure and development environment before implementing business features.

## Current Status

**Milestone 0 — Project initialization and development environment setup**

The repository currently contains the initial frontend and backend application skeletons.

At this stage:

* the frontend application can be started locally;
* the backend Spring Boot application can be started locally;
* the basic repository structure has been established;
* the initial architecture decision has been documented;
* frontend and backend test suites can be executed locally;
* frontend linting and production build verification are available.

Authentication, database integration, job application management, interviews, and other business features have **not** been implemented yet.

## Technology Stack

### Frontend

Currently installed and configured:

* React
* TypeScript
* Vite
* Tailwind CSS
* ESLint
* Vitest
* React Testing Library

Additional frontend libraries will be introduced only when required by later milestones.

### Backend

Currently installed and configured:

* Java 21
* Spring Boot
* Spring MVC
* Bean Validation
* Spring Boot Actuator
* Maven
* Maven Wrapper
* JUnit 5

Additional backend dependencies such as Spring Security, Spring Data JPA, and PostgreSQL integration will be introduced in later milestones.

## Repository Structure

```text
jobflow-ai/
├── frontend/
├── backend/
├── docs/
│   └── adr/
└── README.md
```

### `frontend/`

Contains the React and TypeScript frontend application.

It also contains the frontend test, linting, and build configuration used to verify the development environment.

### `backend/`

Contains the Java 21 and Spring Boot backend application.

The backend uses the Maven Wrapper, so Maven does not need to be installed globally.

### `docs/adr/`

Contains Architecture Decision Records (ADRs).

ADRs document significant architectural decisions, the context behind them, alternatives considered, and their trade-offs.

## Prerequisites

Before running the project locally, install:

* Java 21
* Node.js 22+
* npm
* Git

Maven does not need to be installed globally because the backend includes the Maven Wrapper.

PostgreSQL is not required during Milestone 0 because database integration has not yet been implemented.

## Running the Backend

From the project root:

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

The Spring Boot application should start successfully using Java 21.

Verify the backend health endpoint:

[http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)

To stop the application, press:

```text
Ctrl + C
```

## Running the Frontend

From the project root:

```powershell
cd frontend
npm ci
npm run dev
```

`npm ci` installs the exact dependency versions recorded in `package-lock.json`, providing a reproducible installation for a fresh clone.

Vite will start the frontend development server and display the local development URL in the terminal.

To stop the development server, press:

```text
Ctrl + C
```

## Verification

The following commands can be used to verify that the local development environment is configured correctly.

### Backend

Run the backend test suite:

```powershell
cd backend
.\mvnw.cmd test
```

A successful test run confirms that the backend project can compile and execute its current automated tests.

### Frontend

Install dependencies from a fresh clone:

```powershell
cd frontend
npm ci
```

Run the frontend test suite:

```powershell
npm test
```

Run ESLint:

```powershell
npm run lint
```

Run the production build:

```powershell
npm run build
```

All commands should complete successfully before Milestone 0 is considered verified.

## Architecture

The MVP uses a modular monolith architecture.

The backend will remain a single Spring Boot deployable application while business features are organised into clearly separated modules.

Architecture decisions are documented in:

* [ADR-001: Use a Modular Monolith for the MVP](docs/adr/0001-use-modular-monolith-for-mvp.md)

## Development Roadmap

The project is currently focused on completing Milestone 0.

Future milestones will introduce application features and supporting infrastructure incrementally rather than adding the entire planned technology stack at once.

## License

This project is licensed under the [MIT License](LICENSE).
