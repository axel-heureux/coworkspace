# 02. Diagramme et Cas d'Utilisation

## 1. Diagramme de Cas d'Utilisation (Mermaid)

```mermaid
graph LR
    subgraph Acteurs
        U[Membre / Utilisateur]
        A[Administrateur]
        S[Système / Worker Email]
    end

    subgraph CoWorkSpace_System["CoWork'Space MVP"]
        
        subgraph Auth_Module["Authentification & Profil"]
            UC1(("S'inscrire & Valider Email"))
            UC2(("S'authentifier (JWT)"))
            UC3(("Gérer son profil"))
        end

        subgraph View_Module["Visualisation & Consultation"]
            UC4(("Consulter le plan & statut des salles"))
            UC5(("Filtrer les espaces (type, équipements)"))
        end

        subgraph Booking_Module["Gestion des Réservations"]
            UC6(("Réserver un espace (ponctuelle / récurrente)"))
            UC7(("Modifier / Annuler une réservation"))
            UC8(("Exporter mes réservations en PDF"))
        end

        subgraph Admin_Module["Administration"]
            UC9(("Valider manuellement les membres"))
            UC10(("Gérer les espaces & équipements (CRUD)"))
            UC11(("Consulter le Dashboard & Taux d'occupation"))
        end

        subgraph Notif_Module["Notifications"]
            UC12(("Envoyer emails (confirmation, rappel 24h, annulation)"))
        end

    end

    U --> UC1
    U --> UC2
    U --> UC3
    U --> UC4
    U --> UC5
    U --> UC6
    U --> UC7
    U --> UC8

    A --> UC2
    A --> UC9
    A --> UC10
    A --> UC11

    S --> UC12

    UC1 ..> UC12 : <<include>>
    UC6 ..> UC12 : <<include>>
    UC7 ..> UC12 : <<include>>
    UC1 ..> UC9  : <<requires validation>>
```

---

## 2. Description des Cas d'Utilisation

### Module Authentification & Profil
* **UC1 - S'inscrire & Valider Email :** Un visiteur crée un compte. Un email de validation est envoyé automatiquement. L'accès complet nécessite la validation par un administrateur.
* **UC2 - S'authentifier :** Le membre ou l'administrateur se connecte et reçoit un token JWT.
* **UC3 - Gérer son profil :** L'utilisateur modifie ses informations personnelles (nom, prénom, téléphone, photo) et peut demander la réinitialisation de son mot de passe.

### Module Visualisation
* **UC4 - Plan & Statut :** Visualisation interactive des espaces (50 postes openspace, 4 salles de réunion) avec code couleur selon la disponibilité actuelle.
* **UC5 - Filtrer les espaces :** Recherche par capacité, équipements disponibles (vidéoprojecteur, whiteboard, etc.) ou type d'espace.

### Module Réservation
* **UC6 - Créer une réservation :** Choix d'un créneau ponctuel ou récurrent (ex: tous les mardis matin). Déclaration d'événement privé ou public.
* **UC7 - Modifier / Annuler :** Modification des dates/créneaux d'une réservation active ou annulation.
* **UC8 - Export PDF :** Téléchargement d'un récapitulatif PDF des réservations passées et à venir.

### Module Administration
* **UC9 - Validation des membres :** L'administrateur valide ou refuse manuellement les inscriptions.
* **UC10 - CRUD Espaces :** Ajout, modification, suppression des postes, salles et leurs équipements associés.
* **UC11 - Dashboard :** Visualisation des statistiques clés (réservations du jour, taux d'occupation hebdomadaire).