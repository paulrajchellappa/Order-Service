# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Build and package
mvn clean package

# Run the application (starts on port 5000)
mvn spring-boot:run

# Run tests
mvn test

# Run a single test class
mvn test -Dtest=OrderServiceApplicationTests
```

The CI/CD pipeline (AWS CodePipeline + CodeBuild) runs `mvn clean package` and publishes `target/order-service.jar`.

## Architecture

Spring Boot 2.3.3 REST service with Java 8. No database — `OrderDao` returns a hardcoded in-memory list of orders.

- **`OrderServiceApplication`** — entry point and `@RestController` combined; exposes `GET /orders` returning orders sorted by price ascending.
- **`OrderDao`** — `@Repository` that returns a static list of `Order` objects.
- **`Order`** — Lombok-annotated model (`id`, `name`, `quantity`, `price`). Note: has both Lombok-generated and manually written getters/setters (redundant, but intentional to avoid breaking changes).
- **`HealthController`** — exposes `GET /health` returning `status`, `service`, and `timestamp`.

All classes live in `com.javatechie.aws.cicd.example`. The app runs on **port 5000** (`application.properties`).
