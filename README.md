# Istio mTLS Setup for Jenkins, SonarQube, and Postgres in `ci` Namespace

This guide documents how to enforce **mutual TLS (mTLS)** between the following Kubernetes services deployed in the `ci` namespace:

- **Jenkins**
- **SonarQube**
- **Postgres** (used by SonarQube)

All services run in the same namespace and communicate internally. This setup ensures all service-to-service communication is encrypted via Istio’s mTLS and, optionally, locked down with authorization policies.

---

## 📌 Prerequisites

- Istio is installed via `istioctl install`
- All workloads (Jenkins, SonarQube, Postgres) are deployed in the `ci` namespace

---

## ✅ Step 1: Enable Istio Sidecar Injection

Enable automatic sidecar injection for the `ci` namespace:

```bash
kubectl label namespace ci istio-injection=enabled --overwrite
