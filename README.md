# Robot Shop Microservices E-Commerce Demo

![Architecture](https://miro.medium.com/v2/resize:fit:736/1*Ld1z5tAB6SP3Toq64MpExQ.png)

## Overview

**Robot Shop** is a cloud-native, microservices-based e-commerce demo application. It showcases a modern 3-tier architecture, with each component running as an independent service. The project is designed for learning, testing, and demonstrating cloud-native patterns, observability, and scalable deployments on Kubernetes (EKS), OpenShift, or Docker Swarm.

---

## Architecture

- **Presentation Layer:**
  - `web/` — Nginx + AngularJS frontend serving the shop UI, proxies API calls to backend services.
- **Application Layer (Microservices):**
  - `user/` — Node.js REST API for user management (registration, login, etc.), uses MongoDB and Redis.
  - `cart/` — Shopping cart service (Node.js, not shown in detail).
  - `catalogue/` — Product catalog (MongoDB-backed).
  - `payment/` — Python Flask service for payment processing, integrates with a payment gateway and RabbitMQ.
  - `shipping/` — Java Spring Boot service for shipping calculations and logistics.
  - `ratings/` — PHP (Symfony) service for product ratings, uses MySQL.
- **Data Layer:**
  - `mongo/` — MongoDB initialization scripts for catalogue and users.
  - `mysql/` — MySQL initialization scripts for ratings.
  - `redis/` — Used for caching/session (referenced in configs).
  - `rabbitmq/` — Message broker for asynchronous communication.
- **Observability & Utilities:**
  - `fluentd/` — Log shipping for observability (to ELK, Humio, etc.).
  - `load-gen/` — Python-based load generator for testing.
- **Deployment:**
  - `K8s/` — Kubernetes manifests and Helm chart for deployment.
  - `OpenShift/`, `Swarm/` — Platform-specific deployment scripts.

---

## Prerequisites

- [kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)
- [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
- [Helm](https://helm.sh/)
- Docker (for local builds)
- Access to an AWS account (for EKS)

---

## Quick Start (Kubernetes/EKS)

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/dushf12/microservices-robot-shop
   cd microservices-robo-shop/microservices-app/K8s/helm
   ```

2. **Create EKS Cluster:**
   (See AWS EKS documentation for details)

3. **Install Helm Chart:**
   ```bash
   kubectl create ns robot-shop
   helm install robot-shop --namespace robot-shop .
   ```

4. **Verify Deployment:**
   ```bash
   kubectl get pods -n robot-shop
   ```

5. **(Optional) Expose via Ingress or LoadBalancer:**
   - Apply your ingress or service manifest as needed.

---

## Service Breakdown

| Service     | Language/Tech | Purpose                                 |
|-------------|--------------|-----------------------------------------|
| web         | Nginx, AngularJS | Frontend UI, API gateway              |
| user        | Node.js, MongoDB, Redis | User management, authentication |
| cart        | Node.js, Redis | Shopping cart management               |
| catalogue   | MongoDB       | Product catalog                         |
| payment     | Python, Flask, RabbitMQ | Payment processing             |
| shipping    | Java, Spring Boot | Shipping calculations                |
| ratings     | PHP, Symfony, MySQL | Product ratings                    |
| load-gen    | Python        | Load testing utility                    |
| fluentd     | Fluentd       | Log aggregation/shipping                |

---

## Observability & Logging

- **Fluentd** is used for log shipping (see `fluentd/`).
- Prometheus metrics are exposed by some services (e.g., payment).
- Easily integrate with ELK, Humio, or other observability stacks.

---

## Load Testing

- Use the `load-gen/` directory to generate synthetic load for testing and demos.
- See `load-gen/README.md` for usage instructions.

---

## Platform-Specific Deployment

- **Kubernetes/EKS:** Use manifests and Helm chart in `K8s/`.
- **OpenShift:** See `OpenShift/README.md` for setup.
- **Docker Swarm:** See `Swarm/` scripts for deployment.

---

## Contributing

Contributions, issues, and feature requests are welcome! Please open an issue or submit a pull request.

---

## Author & Contact

**Dushyanth Bandaru**  
[LinkedIn: Dushyanth Bandaru](https://www.linkedin.com/in/dushyanthbandaru/)

---

## ⭐ Support

If you found this project helpful, please consider starring ⭐ the repository and sharing it with your network!
