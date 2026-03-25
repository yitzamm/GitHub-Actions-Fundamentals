# GitHub Actions CI/CD Pipeline with Docker

March 25, 2026

<img width="2000" height="665" alt="image" src="https://github.com/user-attachments/assets/b559e08f-1fef-4a85-8070-82407e2fed23" />

This project demonstrates a CI/CD pipeline using GitHub Actions to build, test, and package a Java application with Gradle, and publish it as a Docker image to Docker Hub.

The pipeline includes:

- Multi-platform builds (Linux, Windows, macOS)
- Dependency management and security insights
- Docker image build and push
- Manual workflow triggers

Link to CI/CD Pipeline with Docker from TechWorld with Nana: https://www.youtube.com/watch?v=R8_veQiYBjI

## Tech Stack

- GitHub Actions (CI/CD)
- Gradle (Build tool)
- Java 17
- Spring Boot
- Docker
- Docker Hub
- Dependabot / Dependency Graph

## CI/CD Pipeline Flow

```
Code Push / PR
      ↓
Build & Test (Multi-OS Matrix)
      ↓
Dependency Analysis (Security)
      ↓
Docker Build & Push (Linux Only)
```

## Workflow Configuration

**Multi-OS Build Matrix**
```
runs-on: ${{ matrix.os }}
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest, macos-latest]
```

**Manual Trigger**
```
workflow_dispatch:
```

## Docker Configuration

**Updated Dockerfile**
```
<img width="320" height="192" alt="image" src="https://github.com/user-attachments/assets/e981b9da-a892-4211-9808-921083dbba65" />
```

## Troubleshooting & Fixes

### Issue #1: Gradle & Java Compatibility
- **Error:** Gradle 6 incompatible with Java 17
- **Fix:** Updated Gradle wrapper
```
</> properties
distributionUrl=https://services.gradle.org/distributions/gradle-7.6.4-bin.zip
```

### Issue #2: Deprecated Dependency Syntax
- **Error:** *compile* / *testCompile* not supported
- **Fix:** compile / testCompile not supported
```
compile       → implementation
testCompile   → testImplementation
runtime       → runtimeOnly
testRuntime   → testRuntimeOnly
```
Also updated Spring Boot version to align with Java 17.

### Issue #3: Dependency Graph Disabled
- **Error:** Dependency Graph Disabled
- **Fix:** Enabled Dependency Graph
```
GitHub → Settings → Advanced Security → Enable Dependency Graph
```
NOTE: Note: There are both repository-level and account-level settings.

### Issue #4: Deprecated Docker Image
- **Error:** *openjdk:8-jre-alpine* not found
- **Fix:** openjdk:8-jre-alpine not found
```
<img width="286" height="36" alt="image" src="https://github.com/user-attachments/assets/fa181205-2126-4344-9709-cce8a7a745cf" />
```

### Issue #5: Docker Not Found
- **Error:** *docker: command not found*
- **Fix:** Docker step only on Linux
```
if: runner.os == 'Linux'
```
IMPORTANT: Docker builds are typically executed on Linux because containers rely on the host kernel.

### Issue #6: Missing JAR File
- **Error:** JAR not found during Docker build
- **Fix:**
- Added debug step to verify JAR generation
- Removed hardcoded filename in Dockerfile

## Security & Dependency Management

- **Dependency Graph -** Insights → Dependency Graph
- **Dependabot Alerts -** Detects vulnerabilities in project dependencies
IMPORTANT: Dependabot helps automate dependency updates and improves supply chain security.

## Key Learnings

- CI pipelines must align with application dependencies and runtime
- Gradle, Java, and Spring Boot versions must be compatible
- Docker builds should be performed on Linux runners
- GitHub Actions workflows can be modular and environment-aware
- Dependency management is critical for security (DevSecOps)
- Debugging CI/CD requires distinguishing between:
1. pipeline issues
2. application/configuration issues
