> Mục tiêu: Xây dựng nền tảng vững chắc cho Java Backend Developer (Spring Boot), tập trung vào **concept** thay vì chỉ học framework.

---

# Triết lý học

Có một nguyên tắc rất quan trọng:

> **Framework chỉ thay đổi cách triển khai. Concept mới là thứ tồn tại lâu dài.**

Đừng cố học thật nhiều annotation của Spring Boot. Hãy hiểu:

- Tại sao cần Transaction?
- Tại sao cần Index?
- JWT hoạt động như thế nào?
- HTTP request đi từ đâu tới đâu?
- Tại sao xảy ra race condition?
- Vì sao query này chậm?

Nếu hiểu được các concept này, việc học framework mới sẽ rất nhanh.

---

# Giai đoạn 1 - Foundation (Fresher)

Mục tiêu:

> Viết được REST API đúng chuẩn, hiểu cách web hoạt động.

## Java

### Mục tiêu

- OOP
- Exception
- Collection
- Generic
- Stream API
- Lambda
- Record
- Enum

### Sách

⭐ Effective Java — Joshua Bloch

---

## SQL & Database

### Mục tiêu

- SQL thành thạo
- Thiết kế Database
- PostgreSQL

### Học

- SELECT
- JOIN
- GROUP BY
- HAVING
- Window Function
- CTE
- Recursive CTE
- Index
- Transaction

### Sách

- Practical SQL
- Database Design for Mere Mortals
- PostgreSQL: Up and Running

---

## HTTP & Networking (Concept)

Không cần trở thành Network Engineer.

Chỉ cần hiểu concept.

### HTTP

- Request
- Response
- Header
- Body
- Method
- Status Code
- Cookie
- Session
- Cache
- Compression
- Keep Alive

---

### TCP

Hiểu:

- Three-way Handshake
- Reliable Transport
- Flow Control
- Congestion Control

---

### TLS

Hiểu:

- HTTPS
- Certificate
- Public Key
- Private Key

---

### DNS

Hiểu:

- A Record
- CNAME
- TTL

---

### Reverse Proxy

Hiểu:

- Nginx
- Reverse Proxy
- Load Balancer

---

### Sách

⭐ HTTP: The Definitive Guide

Hoặc

High Performance Browser Networking

---

## Spring Boot

Mục tiêu

- REST API
- Dependency Injection
- Bean Lifecycle
- Validation
- Exception Handler
- Configuration
- Spring Data JPA

---

# Giai đoạn 2 - Junior (Core Backend)

Sau khi đã viết được API.

Lúc này bắt đầu học cách viết code tốt.

---

## Clean Code

### Sách

Clean Code

Học

- Naming
- Function
- SOLID
- Class Design

---

## Refactoring

### Sách

Refactoring

Học

- Code Smell
- Extract Method
- Replace Conditional
- Long Method

---

## REST API Design

Học

- RESTful
- Idempotency
- Pagination
- Filtering
- Sorting
- Versioning

---

## Security

**Đây là lúc nên học.**

Lý do:

Lúc này bạn đã hiểu HTTP.

Nên sẽ hiểu được:

- JWT
- OAuth2
- Session
- Cookie
- CORS
- CSRF

### Học

- Authentication
- Authorization
- JWT
- Refresh Token
- OAuth2
- OpenID Connect

### Sách

Spring Security in Action

---

## Testing

**Không nên học quá sớm.**

Lý do:

Nếu code chưa sạch thì rất khó test.

Sau khi học Clean Code + Refactoring sẽ dễ hơn nhiều.

### Học

- Unit Test
- Integration Test
- Mockito
- Test Pyramid

### Sách

Growing Object-Oriented Software Guided by Tests

---

## Docker

Học

- Dockerfile
- Compose
- Volume
- Network

---

# Giai đoạn 3 - Junior Vững

Lúc này bắt đầu hiểu hệ thống hoạt động bên trong.

---

## Java Concurrency

Đây là phần rất quan trọng.

Nhưng nên học sau khi đã có trải nghiệm làm API.

### Học

- Thread
- Executor
- Future
- CompletableFuture
- synchronized
- volatile
- Atomic
- Lock
- Deadlock
- Thread Safety

### Sách

⭐ Java Concurrency in Practice

---

## Redis

Học

- Cache
- TTL
- Pub/Sub
- Distributed Lock

---

## Message Queue

RabbitMQ hoặc Kafka

Hiểu

- Producer
- Consumer
- Exchange
- Topic
- Retry
- Dead Letter Queue

---

## Design Pattern

### Sách

Head First Design Patterns

Sau đó

Design Patterns (GoF)

---

## Architecture

### Sách

Clean Architecture

Học

- Layer
- Dependency Rule
- Use Case
- Adapter
- Hexagonal

---

## Enterprise Pattern

### Sách

Patterns of Enterprise Application Architecture

Học

- Repository
- Unit Of Work
- DTO
- Service Layer
- Identity Map
- Lazy Loading

---

# Giai đoạn 4 - Junior → Mid

Đây là lúc học cách xây dựng hệ thống lớn.

---

## Database Chuyên sâu

### Học

- MVCC
- Vacuum
- WAL
- Query Planner
- Index
- Lock

### Sách

The Art of PostgreSQL

↓

Database Internals

---

## Distributed Systems

### Sách

Designing Data Intensive Applications (DDIA)

Đây là cuốn quan trọng nhất.

Học

- Replication
- Sharding
- Partition
- Event
- Stream
- Transaction
- Consistency
- CAP
- Consensus

---

## System Design

### Sách

System Design Interview

Vol 1

↓

Vol 2

---

## Performance

### Học

- Connection Pool
- Rate Limit
- Retry
- Circuit Breaker
- Timeout
- Bulkhead
- Cache

### Sách

Release It!

---

## Observability

Học

- Logging
- Metrics
- Tracing
- Prometheus
- Grafana
- OpenTelemetry

---

## Kubernetes

Chỉ cần hiểu

- Pod
- Service
- Deployment
- ConfigMap
- Secret
- Ingress

---

# Tổng hợp sách theo từng chủ đề

| Chủ đề | Sách |
|----------|------|
| Java | Effective Java |
| Clean Code | Clean Code |
| Refactoring | Refactoring |
| SQL | Practical SQL |
| Database Design | Database Design for Mere Mortals |
| PostgreSQL | PostgreSQL: Up and Running |
| PostgreSQL nâng cao | The Art of PostgreSQL |
| Database Internals | Database Internals |
| HTTP | HTTP: The Definitive Guide |
| Networking | High Performance Browser Networking |
| Design Pattern | Head First Design Patterns |
| Design Pattern nâng cao | Design Patterns (GoF) |
| Security | Spring Security in Action |
| Testing | Growing Object-Oriented Software Guided by Tests |
| Concurrency | Java Concurrency in Practice |
| Architecture | Clean Architecture |
| Enterprise Pattern | Patterns of Enterprise Application Architecture |
| Distributed Systems | Designing Data-Intensive Applications |
| System Design | System Design Interview Vol.1 & Vol.2 |
| Performance | Release It! |

---

# Roadmap học theo thứ tự

## Phase 1

- Java Core
- Effective Java
- SQL
- Practical SQL
- Database Design
- PostgreSQL
- HTTP Concept
- Spring Boot
- JPA

---

## Phase 2

- Clean Code
- Refactoring
- REST API Design
- Spring Security
- JWT
- OAuth2
- Testing
- Docker

---

## Phase 3

- Java Concurrency
- Redis
- RabbitMQ/Kafka
- Design Patterns
- Clean Architecture
- Enterprise Patterns

---

## Phase 4

- The Art of PostgreSQL
- Database Internals
- DDIA
- System Design
- Performance
- Observability
- Kubernetes

---

# Điều quan trọng nhất

Framework chỉ là công cụ.

Một Backend Developer giỏi được đánh giá bởi việc họ hiểu:

- Database hoạt động như thế nào.
- HTTP hoạt động như thế nào.
- Authentication hoạt động như thế nào.
- Concurrency hoạt động như thế nào.
- System hoạt động như thế nào.

Nếu nắm vững các concept trên, việc chuyển từ Spring Boot sang Quarkus, Micronaut, ASP.NET Core hay Go chỉ còn là học API của framework, không phải học lại tư duy backend.