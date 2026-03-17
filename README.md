# Student API – Spring Boot

Ce projet est une application **Spring Boot** permettant de gérer des étudiants via une **API REST**.  
L’application permet de **créer, consulter, modifier et supprimer des étudiants** stockés dans une base **MySQL**.

Le projet utilise plusieurs technologies du framework Spring afin d’organiser l’application selon une architecture claire :

- **Spring Web** pour créer les endpoints REST
- **Spring Data JPA** pour la persistance des données
- **MySQL** comme base de données
- **DTO et Mapper manuel** pour séparer la couche API de la couche persistance
- **Swagger (springdoc-openapi)** pour la documentation interactive de l’API

---

# 📌 Objectif du TP

À travers ce TP, l’objectif est de comprendre comment construire une **API REST complète avec Spring Boot** et organiser une application backend proprement.

Ce projet m’a permis d’apprendre à :

- Générer un projet **Spring Boot avec Spring Initializr**
- Configurer une base de données **MySQL**
- Implémenter une architecture en couches (**Entity → Repository → Service → Controller**)
- Utiliser **Spring Data JPA** pour manipuler les données
- Utiliser des **DTO avec Java Record**
- Implémenter un **mapper manuel**
- Gérer les **exceptions globales**
- Tester les endpoints avec **Swagger UI**

---

# 🛠️ Technologies utilisées

- Java
- Spring Boot
- Spring Web
- Spring Data JPA
- MySQL
- Maven
- Swagger (springdoc-openapi)
- Validation (Jakarta Validation)

---

## 1️⃣ Création du projet Spring Boot

Le projet a été créé avec **Spring Initializr** en sélectionnant les dépendances suivantes :

- Spring Web
- Spring Data JPA
- MySQL Driver
- Validation
- Springdoc OpenAPI (Swagger)

Le projet généré suit la structure standard d’une application **Spring Boot avec Maven**.

---

## 2️⃣ Configuration de la base de données MySQL

Création de la base de données :

```sql
CREATE DATABASE student_db;
```

Configuration dans le fichier `application.properties`.

```
spring.datasource.url=jdbc:mysql://localhost:3306/student_db?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
server.port=8082
```

Hibernate crée automatiquement les tables à partir des entités.

---

## 3️⃣ Création de l’entité

### 🎓 Student

L’entité **Student** représente un étudiant dans la base de données.

Elle contient les attributs suivants :

- id
- firstName
- lastName
- email
- major
- age

Cette entité est annotée avec **JPA (`@Entity`)** afin d’être liée à la table `students`.

---

## 4️⃣ Implémentation du Repository

Création de l’interface `StudentRepository` qui étend :

```
JpaRepository<Student, Long>
```

Spring Data JPA génère automatiquement les méthodes CRUD :

- save()
- findAll()
- findById()
- delete()

Des méthodes personnalisées peuvent également être ajoutées comme :

- findByEmail()
- existsByEmail()

---

## 5️⃣ Création des DTO

Pour séparer la couche API de la couche base de données, deux DTO ont été créés :

### StudentRequestDTO

Utilisé pour recevoir les données envoyées par le client.

### StudentResponseDTO

Utilisé pour retourner les données au client.

Les DTO sont implémentés avec **Java Record**, ce qui permet de créer des objets immuables de manière concise.

---

## 6️⃣ Création du Mapper

La classe **StudentMapper** permet de transformer les données entre :

- DTO → Entity
- Entity → DTO

Elle contient notamment les méthodes :

- `toEntity()`
- `toResponseDTO()`
- `updateEntityFromDTO()`

Le mapper permet de **contrôler les données échangées avec l’API**.

---

## 7️⃣ Création de la couche Service

La classe **StudentService** contient la logique métier de l’application.

Elle implémente les opérations principales :

- ajout d’un étudiant
- récupération de tous les étudiants
- recherche d’un étudiant par id
- modification d’un étudiant
- suppression d’un étudiant

Le service utilise :

- `StudentRepository`
- `StudentMapper`

---

## 8️⃣ Création du contrôleur REST

La classe **StudentController** expose les endpoints REST de l’API.

Les routes principales sont :

| Méthode | Endpoint | Description |
|--------|---------|-------------|
| POST | /api/students | ajouter un étudiant |
| GET | /api/students | afficher tous les étudiants |
| GET | /api/students/{id} | afficher un étudiant |
| PUT | /api/students/{id} | modifier un étudiant |
| DELETE | /api/students/{id} | supprimer un étudiant |

---

## 9️⃣ Gestion des exceptions

Le projet inclut une **gestion globale des erreurs** avec :

- `ResourceNotFoundException`
- `GlobalExceptionHandler`


## 🔟 Lancement de l’application

L’application peut être démarrée :

Depuis l’IDE :

```
Run StudentApiApplication
```

Ou depuis le terminal :

```bash
mvn spring-boot:run
```

Une fois démarrée, l’application écoute sur :

```
http://localhost:8082
```

---

## 1️⃣1️⃣ Test des endpoints REST avec Swagger

Les endpoints ont été testés à l’aide de **Swagger UI**, qui permet de visualiser et tester les routes REST directement depuis le navigateur.

Swagger est accessible via :

```
http://localhost:8082/swagger-ui/index.html
```

---

# 🎥 Démonstration vidéo des tests Swagger

La vidéo suivante montre le test des endpoints REST via **Swagger UI** :

- POST /api/students
- GET /api/students
- GET /api/students/{id}
- PUT /api/students/{id}
- DELETE /api/students/{id}

https://github.com/user-attachments/assets/008e0500-2036-4869-9978-aee48609270e

---

# 👩‍💻 Auteur

- Nom : **Malak El Mallouky**
- Filière : **SIR**
