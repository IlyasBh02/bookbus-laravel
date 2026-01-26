nam of project : bookbus-laravel


# BookBus – Documentation d’Analyse & Fondations

## Introduction
BookBus est une plateforme web de réservation de billets de bus inter-villes, inspirée de marKoub.ma.
Cette documentation présente l’analyse du domaine métier, l’architecture proposée et les choix techniques retenus afin de poser des bases solides pour le développement du projet.

---

## A. Analyse du domaine (Étude de marKoub.ma)

### 1. Processus de réservation (côté utilisateur)
1. L’utilisateur accède à la plateforme.
2. Il sélectionne la ville de départ, la ville d’arrivée et la date du voyage.
3. Le système affiche la liste des voyages disponibles.
4. L’utilisateur consulte les détails d’un voyage (horaire, prix, places).
5. Il crée un compte ou se connecte.
6. Il réserve un ou plusieurs sièges.
7. La réservation est confirmée (paiement simulé dans le MVP).
8. L’utilisateur peut consulter ses réservations.

---

### 2. Entités principales identifiées
- **Utilisateur** : client ou administrateur.
- **Ville** : point de départ ou d’arrivée.
- **Bus** : véhicule utilisé pour les voyages.
- **Voyage (Trip)** : trajet planifié entre deux villes.
- **Réservation** : réservation effectuée par un utilisateur.
- **Compagnie** (optionnelle – évolution future).

---

### 3. Flux d’administration
- Connexion administrateur.
- Gestion des villes (ajout, modification, suppression).
- Gestion des bus.
- Création et gestion des voyages.
- Consultation des réservations des clients.

---

## B. Proposition d’architecture

### 1. Schéma de base de données (ERD – description)

**Tables principales (MVP)**

#### users
- id
- name
- email
- password
- role (admin / client)
- created_at
- updated_at

#### cities
- id
- name

#### buses
- id
- number_plate
- capacity

#### trips
- id
- departure_city_id (FK)
- arrival_city_id (FK)
- bus_id (FK)
- departure_time
- price

#### reservations
- id
- user_id (FK)
- trip_id (FK)
- seats
- status (confirmed / cancelled)

**Relations**
- Un utilisateur peut avoir plusieurs réservations.
- Un voyage peut avoir plusieurs réservations.
- Une ville peut être liée à plusieurs voyages.
- Un bus peut être affecté à plusieurs voyages.

---

### 2. Fonctionnalités MVP

#### Client
- Inscription et connexion
- Recherche de voyages
- Réservation d’un voyage
- Consultation des réservations

#### Administrateur
- Gestion des villes (CRUD)
- Gestion des bus (CRUD)
- Gestion des voyages (CRUD)
- Consultation des réservations

---

### 3. Diagramme de cas d’utilisation

**Acteurs**
- Client
- Administrateur

**Cas d’utilisation – Client**
- Rechercher un voyage
- Consulter les détails d’un voyage
- Réserver un billet
- Consulter ses réservations
- S’inscrire / Se connecter

**Cas d’utilisation – Administrateur**
- Se connecter
- Gérer les villes
- Gérer les bus
- Gérer les voyages
- Consulter les réservations

**Relations**
- Réserver un billet <<include>> Se connecter
- Consulter ses réservations <<include>> Se connecter

---

### 4. Diagramme de classes (description)

#### Classe User
- id
- name
- email
- role
- login()
- logout()

#### Classe City
- id
- name

#### Classe Bus
- id
- numberPlate
- capacity

#### Classe Trip
- id
- departureTime
- price
- getAvailableSeats()

#### Classe Reservation
- id
- seats
- status
- confirm()
- cancel()

---

## C. Choix techniques

### 1. Choix de Laravel
- Framework PHP moderne et robuste.
- Architecture MVC claire.
- Authentification intégrée (Laravel Breeze).
- Sécurité (CSRF, validation, hash des mots de passe).
- Grande communauté et documentation riche.

---

### 2. Dépendances techniques
- PHP >= 8.2
- Laravel >= 10
- Laravel Breeze (authentification)
- MySQL ou PostgreSQL
- Composer

---

## Conclusion
Cette phase de découverte et d’analyse permet de bien comprendre le domaine de la réservation de bus et de définir une architecture claire.
Le projet BookBus est désormais prêt pour la phase d’implémentation technique avec Laravel.
