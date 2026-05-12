
# Django + Docker Containerized Application (Hands-on Practice)

This project demonstrates the end-to-end flow of building and testing a Django application inside a Docker container on macOS. It documents the transition from local development to a containerized architecture, specifically focusing on architecture-specific troubleshooting and professional DevOps workflows.

---

## Project Workflow

The following pipeline represents the actual path taken from source code to a fully operational container:

```text
Django Application Code  
↓  
Dockerfile Configuration  
↓  
Docker Image Build (docker build)  
↓  
BuildKit / Buildx Error Occurs  
↓  
Fix: DOCKER_BUILDKIT=0 (Legacy Builder)  
↓  
Successful Docker Image Creation  
↓  
Docker Run (Container Execution)  
↓  
Port Mapping (8000:8000)  
↓  
Browser Access (localhost:8000)  
↓  
Django Application Running Successfully
```

---

## Troubleshooting: Resolving BuildKit Failures

### The Error

As captured in the terminal logs (see 1000075751_2.jpg), the build failed with:

```text
failed to fetch metadata: fork/exec /Users/sushma/.docker/cli-plugins/docker-buildx: exec format error

ERROR: BuildKit is enabled but the buildx component is missing or broken.
```

---

### The Solution

This issue was resolved by disabling BuildKit and using the legacy Docker builder. This bypassed the broken buildx plugin and allowed the image to build successfully.

**Fix Command:**

```bash
DOCKER_BUILDKIT=0 docker build -t django-practice-app .
```

---

## Docker Run & Verification

The container started successfully and launched the Django development server. The application was verified to be running inside the container without errors.

---

## Browser Output

The application is accessible at:

```text
http://localhost:8000
```

---

## What I Learned

* Dockerization pipeline from Dockerfile to running container
* Debugging architecture-specific BuildKit and exec format errors
* Container networking and port mapping (8000:8000)
* DevOps workflow improvements using SSH authentication for Git
* Linux terminal and Docker CLI troubleshooting skills

---

## Tech Stack

* Backend: Python, Django
* Containerization: Docker
* Environment: macOS, Linux Terminal
* Version Control: Git (SSH authentication)



---

## Project Outcome

Successfully containerized a Django application using Docker, resolved a real-world BuildKit issue, and gained practical DevOps troubleshooting experience.
