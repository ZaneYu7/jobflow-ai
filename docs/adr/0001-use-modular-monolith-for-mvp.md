# ADR-001: Use a Modular Monolith for the MVP

* Status: Accepted
* Date: 2026-09-12

## Decision

The MVP will use a modular monolith: one Spring Boot application organised into clearly separated business-feature modules with explicit service boundaries.

## Context

JobFlow AI is a full-stack job application and interview management platform.

The MVP needs to support authentication, companies, jobs, applications, interviews, and application status tracking.

The project is currently being developed by a single developer. At this stage, the main goal is to deliver a working and maintainable MVP without introducing unnecessary infrastructure or distributed-system complexity.

An architectural boundary needs to be defined early because package structure and module dependencies will affect maintainability, testing, and future refactoring.

## Options Considered

### Modular Monolith

A modular monolith keeps the backend as one deployable application while separating business features into clear modules.

Advantages:

* simple deployment and local development;
* clear ownership of business logic;
* straightforward transactions within one application;
* easier future extraction of selected modules if requirements change.

The main limitation is that all modules still run in the same process and are deployed together. Module boundaries therefore need to be maintained through code structure and dependency discipline.

### Microservices

Microservices would split the system into independently deployed services.

Potential advantages include independent deployment, scaling, and stronger runtime isolation.

However, they would also introduce additional complexity such as:

* network communication and failure handling;
* distributed transactions and consistency concerns;
* multiple deployment pipelines;
* more complex logging, monitoring, and local development.

For a single-developer MVP, these costs are not justified by current requirements.

### Unstructured Monolith

An unstructured monolith would also use a single Spring Boot application, but without clear feature boundaries.

This would allow controllers, services, repositories, and entities to depend freely on unrelated parts of the system. Although initially simple, this would increase coupling, make business ownership unclear, and make future refactoring or module extraction more difficult.

## Chosen Approach

The backend will be implemented as one Spring Boot deployable application.

The codebase will be organised by business feature rather than by global technical layers.

```text
com.jobflow
├── auth
├── user
├── company
├── job
├── application
├── interview
└── common
```

Each feature may contain its own controllers, services, repositories, entities, DTOs, and related classes.

Modules should collaborate through clear service boundaries rather than directly accessing another module's repositories or internal implementation details.

A module boundary does not require every service to have a Java interface. A concrete application service may act as the public boundary unless multiple implementations or another clear requirement justify introducing an interface.

The MVP will use one PostgreSQL database.

Sharing one database keeps development and deployment simple, but modules should still avoid directly manipulating persistence owned by another feature.

Notifications are outside the MVP scope. If notification functionality is introduced later, it will initially be implemented inside the modular monolith.

Only if notifications later require independent deployment, scaling, or stronger failure isolation will extracting them into a separate service be considered.

## Trade-offs

This approach keeps deployment, debugging, testing, and database transactions relatively simple while still providing clear business boundaries.

The main trade-off is that the backend remains one deployment unit, so individual modules cannot be deployed or scaled independently.

Because modules share the same process and database, boundaries are enforced mainly through code organisation and development discipline rather than infrastructure.

If a module is extracted into a separate service in the future, additional refactoring may be required around database ownership, transactions, and communication between modules.

These trade-offs are acceptable for the MVP because current requirements favour simplicity and maintainability over distributed-system flexibility.
