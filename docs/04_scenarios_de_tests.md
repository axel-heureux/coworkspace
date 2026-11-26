# 04. Scénarios et Plans de Tests

## 1. Unit Testing (Tests Unitaires Backend)

Les tests unitaires sont développés avec **PHPUnit** dans le framework Symfony et se concentrent sur la logique métier critique.

### Test Unitaire 1 : Validation des Chevauchements de Réservation
* **Objectif :** S'assurer qu'une salle ne peut pas être réservée deux fois sur le même créneau horaire.
* **Méthode :** `ReservationServiceTest::testOverlappingReservationFails()`
* **Scénario :**
  1. Créer une réservation $R_1$ pour l'Espace A du lundi 09h00 au lundi 12h00.
  2. Tenter de créer une réservation $R_2$ pour l'Espace A du lundi 10h00 au lundi 11h00.
  3. **Résultat attendu :** Une exception `OverlappingReservationException` doit être levée.

### Test Unitaire 2 : Règle de Récurrence
* **Objectif :** Vérifier la génération correcte des dates lors d'une réservation récurrente.
* **Méthode :** `RecurrenceServiceTest::testGenerateWeeklyDates()`
* **Scénario :**
  1. Définir un créneau pour "Chaque mardi à 14h00" pendant 4 semaines.
  2. **Résultat attendu :** Le service retourne un tableau contenant exactement 4 instances d'objets `DateTime` correspondant aux mardis suivants.

---

## 2. Scénario de Test de Recette (Parcours Utilisateur Documenté)

### Parcours : Inscription $\rightarrow$ Validation Admin $\rightarrow$ Connexion $\rightarrow$ Réservation

| Étape | Acteur | Action | Résultat Attendu |
| :---: | :--- | :--- | :--- |
| **1** | Visiteur | Remplit le formulaire d'inscription sur le Frontend React. | Compte créé avec `is_validated = false`. Email de validation envoyé. |
| **2** | Visiteur | Clique sur le lien dans l'email de validation. | L'email est validé, mais le compte reste en attente de la validation Admin. |
| **3** | Admin | Connecté au dashboard `/admin`, il consulte la liste des membres en attente et clique sur "Valider". | `is_validated` passe à `true`. |
| **4** | Membre | Se connecte via le formulaire de login (`/login`). | Réception du Token JWT, redirection vers la page d'accueil des réservations. |
| **5** | Membre | Utilise les filtres pour chercher une salle avec "Vidéoprojecteur" et sélectionne un créneau sur le calendrier. | Affichage de la salle disponible en vert. |
| **6** | Membre | Valide la réservation. | Réservation enregistrée, mise à jour de la couleur du statut, envoi immédiat de l'email de confirmation. |