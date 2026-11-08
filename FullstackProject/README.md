# Full-Stack DevOps Project

An individual full-stack and DevOps project demonstrating automated build and test workflows, code-quality analysis, containerization, Kubernetes deployment, and monitoring.

## Application architecture
- Frontend: Angular
- Backend: Spring Boot (Java 17)
- Database: MySQL

## DevOps toolchain
- Jenkins for CI/CD
- SonarQube for code-quality analysis
- Docker for containerization
- Kubernetes for orchestration and deployment
- Prometheus and Grafana for monitoring
- Ansible (included in the project toolchain)

## Repository structure
- `frontend/` — Angular application
- `demo/` — Spring Boot backend
- `k8s/` — Kubernetes manifests
- `Jenkinsfile` — Jenkins pipeline

## Security and configuration
No real Kubernetes Secret values are stored in this repository. Before deploying, create the required secret in the `fullstack-app` namespace using values appropriate for your environment:

```bash
kubectl create namespace fullstack-app
kubectl create secret generic mysql-secret \
  --namespace fullstack-app \
  --from-literal=username=root \
  --from-literal=password='REPLACE_WITH_A_STRONG_PASSWORD'
```

Do not commit Kubernetes Secret manifests containing real credentials. For local Spring Boot runs, set `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, and `SPRING_DATASOURCE_PASSWORD` as environment variables. The defaults in `application.properties` are intended only for local development; provide your own local database credentials.

For Jenkins email notifications, configure the `NOTIFY_EMAIL` environment variable in Jenkins before running the pipeline. Configure Docker credentials in Jenkins Credentials using the ID expected by the pipeline (`docker`). Configure the Jenkins tools and SonarQube installation names referenced in the `Jenkinsfile`.

## Important notes
- Review the Kubernetes storage and Ingress settings for your own cluster before deployment.
- Update container image names and registry settings if using a different registry account.
- This repository is a demonstration project, not a production-hardened deployment template.
