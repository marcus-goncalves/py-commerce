# Py-Commerce
Um projeto modelo de e-commerce, utilizando serviços fracionados com o intuito de simular um projeto "grande"

## Technologies
- Python: FastAPI as framework
- JWT

## Services

### ✅ 1. Auth Service (`auth-service`)

**Objetivo:** Gerenciar autenticação e geração de tokens JWT.

- [ ] Inicializar projeto com FastAPI
- [ ] Criar endpoint `/login` com autenticação básica
- [ ] Criar endpoint `/register` (opcionalmente usar User Service no futuro)
- [ ] Gerar e validar tokens JWT
- [ ] Implementar middleware para validação de token (reutilizável)
- [ ] Documentar uso do JWT e política de expiração

---

### ✅ 2. User Service (`user-service`)

**Objetivo:** Gerenciar usuários e perfis.

- [ ] Setup com FastAPI + SQLAlchemy + PostgreSQL
- [ ] Modelagem da entidade `User`
- [ ] CRUD de usuários: `POST /users`, `GET /users/{id}`, `PUT`, `DELETE`
- [ ] Integração com Auth Service via token JWT
- [ ] Endpoint para alterar senha (opcional)
- [ ] Documentar payloads esperados

---

## ✅ 3. Product Service (`product-service`)

**Objetivo:** Gerenciar produtos e categorias.

- [ ] Setup inicial com FastAPI + PostgreSQL
- [ ] Modelar entidades: `Product`, `Category`
- [ ] CRUD de produtos
- [ ] CRUD de categorias
- [ ] Endpoint `GET /products` com filtros (nome, categoria, preço)
- [ ] Integração com Redis para cache de produtos listados
- [ ] Testar TTL no Redis e fallback em caso de cache miss

---

## ✅ 4. API Gateway (`api-gateway`)

**Objetivo:** Roteamento centralizado e autenticação global.

- [ ] Setup básico (FastAPI como gateway ou usar Kong/Traefik)
- [ ] Middleware para validação de token JWT
- [ ] Roteamento das chamadas: `/users`, `/products`, `/orders`
- [ ] Implementar controle de logs de acesso
- [ ] Documentar rotas disponíveis e padrões

---

## ✅ 5. Order Service (`order-service`)

**Objetivo:** Gerenciar pedidos e integração com eventos.

- [ ] Setup com FastAPI + PostgreSQL
- [ ] Modelar entidades: `Order`, `OrderItem`
- [ ] Endpoint `POST /orders` (usuário, produtos, total)
- [ ] Validação de produtos e estoque (mock inicialmente)
- [ ] Emissão de evento `order_created` via Kafka/RabbitMQ
- [ ] Documentar estrutura do evento emitido

---

## ✅ 6. Analytics Service (`analytics-service`)

**Objetivo:** Coletar e armazenar dados de eventos para relatórios.

- [ ] Setup com FastAPI + MongoDB (ou PostgreSQL)
- [ ] Criar consumidor Kafka para `order_created`
- [ ] Armazenar dados em estrutura analítica (ex: produto, quantidade, data)
- [ ] Endpoints `GET /analytics/top-products`, `GET /analytics/sales`
- [ ] Agregar dados por período (diário/semanal/mensal)
- [ ] Criar painel básico com Streamlit (opcional)

---

## ✅ 7. Redis Cache (Product Service)

**Objetivo:** Melhorar performance do serviço de produtos.

- [ ] Setup do Redis com Docker
- [ ] Integrar cache no endpoint de listagem de produtos
- [ ] Implementar chave única com base nos filtros da query
- [ ] TTL dinâmico para cache de produtos populares
- [ ] Logs para hit/miss de cache

---

## 🧰 Ambiente de Desenvolvimento

- [ ] Criar `docker-compose.yml` com serviços: PostgreSQL, Redis, Kafka/RabbitMQ
- [ ] Criar `.env` padrão para cada serviço
- [ ] Setup de rede interna para comunicação entre containers
- [ ] Incluir volumes persistentes e reinício automático

---

## 🧪 Testes e Qualidade

- [ ] Setup de testes unitários com `pytest` para todos os serviços
- [ ] Integração contínua com GitHub Actions (ou alternativa)
- [ ] Linter (Flake8 ou Ruff)
- [ ] Pre-commit hooks para formatação automática

---

## 📈 Observabilidade (Fase futura)

- [ ] Integrar Prometheus para métricas
- [ ] Setup de Grafana com dashboards básicos
- [ ] Logging estruturado com Loki ou ELK Stack

---

## 🌐 Orquestração (Fase futura)

- [ ] Criar arquivos de deployment em Kubernetes (Helm Charts ou YAML)
- [ ] Setup de ingress controller e DNS interno
- [ ] Autoescala dos serviços com base em uso