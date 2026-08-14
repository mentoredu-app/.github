# MentorEdu API

> API REST principal de **MentorEdu**, una plataforma educativa para estudiantes **preuniversitarios**.

![Java](https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.0.6-6DB33F?logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![License](https://img.shields.io/badge/version-v1.0.0-blue)

---

## 🎯 El problema

Los estudiantes preuniversitarios preparan sus exámenes de admisión con material disperso: exámenes de años anteriores repartidos en PDFs sueltos, dudas que se resuelven en chats desordenados y sin un lugar central donde discutir pregunta por pregunta.

**MentorEdu** unifica todo en una sola plataforma:

- 📚 **Repositorio histórico de exámenes** — organizados y buscables por nombre, año y universidad.
- 💬 **Foros por pregunta** — cada pregunta de examen tiene su propio hilo de discusión.
- 🤖 **Asistente con IA** — soporte mediante **RAG** para resolver dudas sobre la plataforma, y **tool calling** para buscar recursos (por nombre, año, universidad, etc.) en lenguaje natural.

---

## 🌐 Demo y despliegue

| Componente | Enlace |
|-----------|--------|
| **API** (health check) | https://mentoredu-api.onrender.com/actuator/health |
| **Microservicio de archivos** | https://file-service-e9i8.onrender.com/actuator/health |
| **Frontend** (Angular) | https://mentor-edu-frontend.netlify.app |
| **Landing** | https://mentoredu-app.github.io/mentoredu-landing/ |

> ⚠️ La API está en el plan gratuito de Render, por lo que la primera petición puede tardar ~30 s en "despertar" el servicio.

---

## 🛠️ Stack tecnológico

| Categoría | Tecnología |
|-----------|-----------|
| Lenguaje | Java 21 |
| Framework | Spring Boot 4.0.6 |
| Seguridad | Spring Security + JWT |
| IA | Spring AI (RAG + tool calling) |
| Base de datos | PostgreSQL 16 |
| Migraciones | Flyway |
| Contenedores | Docker / Docker Compose |
| Despliegue | Render.com |

---

## 🧩 Arquitectura

El backend está organizado como un **monolito modular** siguiendo *Domain-Driven Design*: cada dominio es un **bounded context** independiente. El manejo de archivos se delega a un **microservicio separado** (`File-service`).

```
com.mentoredu
├── auth        → autenticación y autorización (JWT)
├── profile     → perfiles de usuario
├── catalog     → catálogo de exámenes y universidades
├── library     → biblioteca de recursos de estudio
├── forum       → foros de discusión por pregunta
├── community   → interacción entre estudiantes
├── pedagogy    → contenido y lógica pedagógica
├── contact     → mensajería / contacto
├── ai          → asistente con Spring AI (RAG + tool calling)
├── files       → integración con el microservicio de archivos
└── config      → configuración transversal (seguridad, CORS, etc.)
```

El ecosistema completo de MentorEdu incluye:

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│  Frontend   │────▶│ mentoredu-api│────▶│  PostgreSQL 16  │
│  (Angular)  │     │ (Spring Boot)│     └─────────────────┘
└─────────────┘     └──────┬───────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │   File-service   │
                  │  (microservicio) │
                  └──────────────────┘
```

---

## 👤 Mi rol

Trabajé en el equipo de **5 desarrolladores** como parte del **backend**, encargándome de los bounded contexts:

**`catalog` · `forum` · `community` · `pedagogy` · `contact` · `ai` · `files`**

Y su equivalente en el **frontend** (Angular, también dividido por bounded context).

Responsabilidades destacadas:

- 🤖 **Integración de IA con Spring AI**: implementé el asistente basado en **RAG** para responder dudas sobre la plataforma y el **tool calling** para búsqueda de recursos en lenguaje natural.
- 🐳 **Infraestructura y despliegue**: configuración de **Docker / Docker Compose**, migraciones con **Flyway** y **despliegue en Render.com** (producción).

---

## 🚀 Ejecución local

### Requisitos
- Java 21
- Docker y Docker Compose
- (Opcional) Maven, si prefieres correrlo sin contenedores

### Pasos

```bash
# 1. Clonar el repositorio
git clone https://github.com/mentoredu-app/mentoredu-api.git
cd mentoredu-api

# 2. Configurar variables de entorno
cp .env.example .env
# edita .env con tus credenciales (BD, JWT, API keys de IA, etc.)

# 3. Levantar la aplicación y la base de datos
docker compose up --build
```

Flyway aplica las migraciones automáticamente al iniciar. La API quedará disponible en `http://localhost:8080` y podrás verificar su estado en:

```
http://localhost:8080/actuator/health
```

### Alternativa sin Docker

```bash
# Requiere una instancia de PostgreSQL 16 activa y configurada en .env
./mvnw spring-boot:run
```

---

## 📄 Licencia

Proyecto académico desarrollado en la Universidad Peruana de Ciencias Aplicadas (UPC).
