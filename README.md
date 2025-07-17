# E-Commerce Platform – System Overview

## 🧭 Vision

This platform enables customers to purchase products online from the nearest physical retail store based on their current geolocation. It supports hundreds of stores distributed across the country, offering a hybrid experience between traditional retail and online shopping.

---

## 🏗️ Architectural Style

- **Microservices-based architecture**
- **Cloud-native & containerized**
- **Domain-driven design**
- **Geolocation-aware order fulfillment**
- **Decoupled inventory sync (event-driven)**

---

## 🛠️ Technology Stack

| Concern             | Tech Stack                        |
|---------------------|-----------------------------------|
| Language (eCommerce) | Java (Spring Boot)               |
| Language (Inventory) | Go (Golang)                      |
| API Gateway         | Spring Cloud Gateway / Kong      |
| Service Registry    | Eureka / Consul                  |
| Communication       | REST (sync), Kafka (async)       |
| Databases           | PostgreSQL, PostGIS              |
| Search (optional)   | ElasticSearch (for Geo queries)  |
| Frontend            | React / Next.js                  |
| Containerization    | Docker, Kubernetes (K8s)         |
| CI/CD               | GitHub Actions / GitLab CI       |

---

## 🧩 Microservices (Phase 1 – E-Commerce)

| Service Name         | Description |
|----------------------|-------------|
| **Auth Service**     | Manages user authentication and token generation (JWT) |
| **User Service**     | Handles user profile, addresses, and preferences |
| **Product Catalog**  | Centralized product information and categories |
| **GeoProximity Service** | Maps users to nearest stores based on location |
| **Cart Service**     | Manages shopping cart per session or user |
| **Order Service**    | Manages order placement and tracking |
| **Payment Service**  | Handles payment simulation / gateway interaction |
| **Store Directory**  | Maintains all registered store metadata |

---

## 🌍 Geolocation-Aware Flow

1. **User browses** products from nearby stores based on their current geolocation.
2. **GeoProximity Service** determines the nearest store(s) using latitude/longitude.
3. Inventory is fetched from the nearest store (future phase).
4. User places the order, which is routed to the correct store.

---

## 📡 Inter-Service Communication

| Communication Type | Usage                            |
|--------------------|----------------------------------|
| REST               | All direct service-to-service calls |
| Kafka              | Order events, Inventory sync (planned) |

---

## 🗃️ Database Strategy

- **Each service owns its database**
- **PostgreSQL** for structured services (users, orders, products)
- **PostGIS** for spatial queries (store location proximity)
- **No shared DBs**; communication only via APIs or events

---

## 🔒 Security

- **JWT-based authentication**
- **Role-based access control**
- **API Gateway as a security perimeter**

---

## 📈 Scalability Plan

- Stateless services behind load balancers
- Horizontally scalable microservices
- Kafka for eventual consistency in inventory updates (future)

---

## 📦 Future Expansion (Phase 2+)

- Go-based Inventory Services (per store)
- Real-time sync with central inventory aggregator
- Recommendation engine
- Admin dashboards (merchant, regional manager views)

---

## 🔄 CI/CD & Deployment (TBD)

- CI/CD pipelines for both Java and Go projects
- K8s for service orchestration
- Environment-based config via Spring Cloud Config or Vault

---

## 🔚 Summary

This eCommerce platform bridges the online-offline retail experience with a location-aware, scalable microservices backend. The system is built with future extensibility in mind—starting with core services for MVP, and designed to eventually support offline inventory sync, real-time analytics, and operational dashboards.

