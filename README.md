<p align="center">
  <img src="docs/img/logo.svg" width="320" alt="Online Boutique" />
</p>

<h1 align="center">Online Boutique</h1>

<p align="center">
  A cloud-native e-commerce demo built as <b>11 polyglot microservices</b>
  communicating over <b>gRPC</b> — ready to deploy on <b>AWS EKS</b> or spin up
  locally with <b>Docker Compose</b>.
</p>

<p align="center">
  <a href="https://go.dev"><img alt="Go" src="https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white"></a>
  <a href="https://nodejs.org"><img alt="Node.js" src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white"></a>
  <a href="https://python.org"><img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"></a>
  <a href="https://openjdk.org"><img alt="Java" src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white"></a>
  <a href="https://dotnet.microsoft.com"><img alt=".NET" src="https://img.shields.io/badge/.NET-512BD4?style=flat-square&logo=dotnet&logoColor=white"></a>
  <a href="https://grpc.io"><img alt="gRPC" src="https://img.shields.io/badge/gRPC-244c5a?style=flat-square&logo=grpc&logoColor=white"></a>
  <a href="https://docs.docker.com/compose/"><img alt="Docker Compose" src="https://img.shields.io/badge/Docker%20Compose-2496ED?style=flat-square&logo=docker&logoColor=white"></a>
  <a href="https://aws.amazon.com/eks/"><img alt="AWS EKS" src="https://img.shields.io/badge/AWS%20EKS-232F3E?style=flat-square&logo=amazoneks&logoColor=white"></a>
</p>

---

## What is this?

**Online Boutique** is a working e-commerce storefront where users can browse products, manage a cart, and place orders from start to finish. It demonstrates a production-grade polyglot microservice architecture.

## Architecture

```mermaid
flowchart LR
    subgraph Frontend
        F[Frontend<br/>Go]
    end
    subgraph Services
        A[Ad Service<br/>Java]
        C[Cart Service<br/>C#]
        Cu[Currency Service<br/>Node.js]
        E[Email Service<br/>Python]
        P[Payment Service<br/>Node.js]
        Pr[Product Catalog<br/>Go]
        R[Recommendation<br/>Python]
        S[Shipping Service<br/>Go]
        Ch[Checkout Service<br/>Go]
        Sh[Shopping Assistant<br/>Python]
    end
    Redis[(Redis)]
    F -->|gRPC| A
    F -->|gRPC| C
    F -->|gRPC| Cu
    F -->|gRPC| Pr
    F -->|gRPC| R
    F -->|gRPC| Sh
    C -->|gRPC| Ch
    Ch -->|gRPC| P
    Ch -->|gRPC| S
    C -.->|Redis| Redis
```

## Quick Start

```bash
git clone https://github.com/grlokesh96/Online-Boutique.git
cd Online-Boutique
docker compose up --build
```

Open http://localhost:8080

## Technology Stack

- **Languages**: Go, Node.js, Python, Java, C#
- **Communication**: gRPC + Protocol Buffers
- **Data**: Redis (cart), in-memory catalog
- **Observability**: OpenTelemetry ready
- **Deployment**: Docker, Kubernetes, AWS EKS, Argo CD

## Project Structure

```
src/                  # 11 microservices
k8s/                  # Kubernetes manifests
protos/               # Shared .proto definitions
docs/                 # Architecture diagrams
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the Apache License 2.0 — see the [LICENSE](LICENSE) file.

---

*Maintained as an enterprise-grade reference implementation for cloud-native microservices.*
