# 03. Modèle de Données (MCD / MLD)

## 1. Modèle Logique de Données (MLD)

```text
USER (id, email, password, roles, first_name, last_name, phone, photo_url, is_validated, is_active, created_at)
SPACE (id, name, type, capacity, is_active, position_x, position_y)
EQUIPMENT (id, name, icon)
SPACE_EQUIPMENT (space_id, equipment_id)
RESERVATION (id, user_id, space_id, start_at, end_at, is_private, is_recurring, recurrence_rule, status, created_at)
```

---

## 2. Dictionnaire de Données

### Table : `USER` (Membres & Administrateurs)
| Champ | Type | Contraintes | Description |
| :--- | :--- | :--- | :--- |
| `id` | INT / UUID | PK, Auto-increment | Identifiant unique |
| `email` | VARCHAR(180) | UNIQUE, NOT NULL | Adresse email (login) |
| `password` | VARCHAR(255) | NOT NULL | Mot de passe (haché Bcrypt/Argon2i) |
| `roles` | JSON | NOT NULL | Rôles (`ROLE_USER`, `ROLE_ADMIN`) |
| `first_name` | VARCHAR(100) | NOT NULL | Prénom |
| `last_name` | VARCHAR(100) | NOT NULL | Nom |
| `phone` | VARCHAR(20) | NULLABLE | Numéro de téléphone |
| `photo_url` | VARCHAR(255) | NULLABLE | Chemin vers la photo de profil |
| `is_validated`| BOOLEAN | DEFAULT FALSE | Validé par l'administrateur |
| `is_active` | BOOLEAN | DEFAULT TRUE | Statut du compte (actif/inactif) |

### Table : `SPACE` (Postes & Salles)
| Champ | Type | Contraintes | Description |
| :--- | :--- | :--- | :--- |
| `id` | INT / UUID | PK, Auto-increment | Identifiant unique |
| `name` | VARCHAR(100) | NOT NULL | Nom (ex: "Poste 12", "Salle Kepler") |
| `type` | VARCHAR(50) | NOT NULL | Type (`OPENSPACE`, `MEETING_ROOM`) |
| `capacity` | INT | NOT NULL | Nombre de places disponibles |
| `position_x` | INT | NULLABLE | Coordonnée X pour le plan 2D |
| `position_y` | INT | NULLABLE | Coordonnée Y pour le plan 2D |

### Table : `EQUIPMENT` (Équipements)
| Champ | Type | Contraintes | Description |
| :--- | :--- | :--- | :--- |
| `id` | INT | PK, Auto-increment | Identifiant unique |
| `name` | VARCHAR(100) | NOT NULL | Nom (ex: "Vidéoprojecteur", "Écran") |

### Table : `RESERVATION` (Réservations)
| Champ | Type | Contraintes | Description |
| :--- | :--- | :--- | :--- |
| `id` | INT / UUID | PK, Auto-increment | Identifiant unique |
| `user_id` | INT | FK -> USER(id) | Membre ayant réservé |
| `space_id` | INT | FK -> SPACE(id) | Espace réservé |
| `start_at` | DATETIME | NOT NULL | Date et heure de début |
| `end_at` | DATETIME | NOT NULL | Date et heure de fin |
| `is_private` | BOOLEAN | DEFAULT FALSE | Indique si l'événement est privé |
| `is_recurring`| BOOLEAN | DEFAULT FALSE | Réservation récurrente |
| `status` | VARCHAR(30) | DEFAULT 'CONFIRMED'| Statut (`CONFIRMED`, `CANCELLED`) |