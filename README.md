# 🎓 Student API — Spring Boot

## Présentation

Application REST développée avec **Spring Boot** pour la gestion des étudiants. Elle permet d'effectuer les opérations CRUD (Create, Read, Update, Delete) sur des données persistées dans une base **MySQL**, en suivant une architecture en couches bien structurée.

---

## 🧱 Architecture du projet

L'application repose sur une séparation claire des responsabilités :
```
Entity → Repository → Service → Controller
```

| Couche | Rôle |
|---|---|
| **Entity** | Modélisation de la base de données |
| **Repository** | Accès aux données via Spring Data JPA |
| **Service** | Logique métier |
| **Controller** | Exposition des endpoints REST |
| **DTO / Mapper** | Isolation de la couche API |

---

## 🛠️ Stack technique

- **Java** + **Spring Boot**
- **Spring Web** — création des endpoints REST
- **Spring Data JPA** — persistance des données
- **MySQL** — base de données relationnelle
- **Jakarta Validation** — validation des entrées
- **Swagger (springdoc-openapi)** — documentation interactive
- **Maven** — gestion des dépendances

---

## ⚙️ Configuration

### Base de données
```sql
CREATE DATABASE student_db;
```

### `application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3307/student_db?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect

server.port=8080
```

> Hibernate génère automatiquement les tables à partir des entités JPA.

---

## 🔗 Endpoints REST

| Méthode | Endpoint | Description |
|---|---|---|
| `POST` | `/api/students` | Créer un étudiant |
| `GET` | `/api/students` | Lister tous les étudiants |
| `GET` | `/api/students/{id}` | Récupérer un étudiant |
| `PUT` | `/api/students/{id}` | Modifier un étudiant |
| `DELETE` | `/api/students/{id}` | Supprimer un étudiant |

---

## 🚀 Lancement

**Depuis l'IDE :**
```
Run → StudentApiApplication
```

**Depuis le terminal :**
```bash
mvn spring-boot:run
```

L'application démarre sur → `http://localhost:8080`

---

## 📖 Documentation Swagger
```
http://localhost:8080/swagger-ui/index.html
```

---

## 📌 Objectifs pédagogiques

Ce TP a permis de mettre en pratique :

- La génération d'un projet via **Spring Initializr**
- La configuration d'une base **MySQL**
- L'implémentation d'une architecture en couches
- L'utilisation de **DTO** avec `Java Record`
- La création d'un **mapper manuel**
- La gestion globale des **exceptions** (`ResourceNotFoundException`, `GlobalExceptionHandler`)
- Le test des endpoints via **Swagger UI**

---

## 🎥 Vidéo Démo


https://github.com/user-attachments/assets/c917b234-5ff9-4eeb-94ff-cc72fb5ab073



