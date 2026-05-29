# 📦 Système de Gestion d’Envoi de Colis

## 📌 1. Description du projet

Ce projet est une base de données SQL permettant de gérer un système d’envoi et de suivi de colis.

Il couvre :

* Gestion des clients
* Gestion des colis
* Gestion des agences
* Gestion des livreurs
* Suivi des expéditions
* Gestion des paiements

👉 Objectif : simuler un système logistique réel et pratiquer SQL (relations, jointures, agrégations).

---

## 🛠 2. Technologies utilisées

* MySQL
* SQL

---

## 🗄 3. Création de la base de données

```sql
CREATE DATABASE gestion_colis;
USE gestion_colis;
```

---

## 📂 4. Modélisation des tables

### 4.1 Table clients

```sql
CREATE TABLE clients (
    id_client INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50),
    prenom VARCHAR(50),
    telephone VARCHAR(20),
    email VARCHAR(100),
    ville VARCHAR(50)
);
```

### 4.2 Table agences

```sql
CREATE TABLE agences (
    id_agence INT PRIMARY KEY AUTO_INCREMENT,
    nom_agence VARCHAR(100),
    ville VARCHAR(50),
    adresse VARCHAR(150)
);
```

### 4.3 Table livreurs

```sql
CREATE TABLE livreurs (
    id_livreur INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50),
    prenom VARCHAR(50),
    telephone VARCHAR(20),
    vehicule VARCHAR(50),
    id_agence INT,
    FOREIGN KEY (id_agence) REFERENCES agences(id_agence)
);
```

### 4.4 Table colis

```sql
CREATE TABLE colis (
    id_colis INT PRIMARY KEY AUTO_INCREMENT,
    reference_colis VARCHAR(30) UNIQUE,
    poids DECIMAL(5,2),
    type_colis VARCHAR(50),
    valeur DECIMAL(10,2),
    statut VARCHAR(50),
    date_envoi DATE,
    id_client INT,
    FOREIGN KEY (id_client) REFERENCES clients(id_client)
);
```

### 4.5 Table expeditions

```sql
CREATE TABLE expeditions (
    id_expedition INT PRIMARY KEY AUTO_INCREMENT,
    id_colis INT,
    ville_depart VARCHAR(50),
    ville_arrivee VARCHAR(50),
    date_expedition DATE,
    date_livraison DATE,
    id_livreur INT,
    FOREIGN KEY (id_colis) REFERENCES colis(id_colis),
    FOREIGN KEY (id_livreur) REFERENCES livreurs(id_livreur)
);
```

### 4.6 Table paiements

```sql
CREATE TABLE paiements (
    id_paiement INT PRIMARY KEY AUTO_INCREMENT,
    id_colis INT,
    montant DECIMAL(10,2),
    mode_paiement VARCHAR(50),
    date_paiement DATE,
    FOREIGN KEY (id_colis) REFERENCES colis(id_colis)
);
```

---

## 📊 5. Structure de la base de données

| Table       | Description              |
| ----------- | ------------------------ |
| clients     | Informations des clients |
| agences     | Agences de livraison     |
| livreurs    | Personnel de livraison   |
| colis       | Colis envoyés            |
| expeditions | Suivi des livraisons     |
| paiements   | Transactions financières |

---

## 🔗 6. Relations entre les tables

* Un client peut envoyer plusieurs colis
* Un colis appartient à un client
* Un colis possède une expédition
* Un livreur gère plusieurs expéditions
* Une agence possède plusieurs livreurs
* Un colis possède un paiement

---

## 📥 7. Ingestion des données (jeu de test)

### 7.1 Clients

```sql
INSERT INTO clients (nom, prenom, telephone, email, ville) VALUES
('Dupont', 'Jean', '0601020304', 'jean.dupont@gmail.com', 'Paris'),
('Martin', 'Claire', '0611223344', 'claire.martin@gmail.com', 'Lyon'),
('Bernard', 'Lucas', '0622334455', 'lucas.bernard@gmail.com', 'Marseille'),
('Thomas', 'Emma', '0633445566', 'emma.thomas@gmail.com', 'Lille'),
('Robert', 'Hugo', '0644556677', 'hugo.robert@gmail.com', 'Toulouse'),
('Petit', 'Nina', '0655667788', 'nina.petit@gmail.com', 'Bordeaux'),
('Durand', 'Leo', '0666778899', 'leo.durand@gmail.com', 'Nantes'),
('Moreau', 'Sarah', '0677889900', 'sarah.moreau@gmail.com', 'Nice');
```

### 7.2 Agences

```sql
INSERT INTO agences (nom_agence, ville, adresse) VALUES
('Agence Paris Centre', 'Paris', '12 Rue Victor Hugo'),
('Agence Lyon Nord', 'Lyon', '25 Avenue Lumière'),
('Agence Marseille Sud', 'Marseille', '8 Boulevard National'),
('Agence Lille Express', 'Lille', '10 Rue du Commerce');
```

### 7.3 Livreurs

```sql
INSERT INTO livreurs (nom, prenom, telephone, vehicule, id_agence) VALUES
('Diallo', 'Moussa', '0700000001', 'Moto', 1),
('Kone', 'Aminata', '0700000002', 'Camion', 2),
('Mensah', 'David', '0700000003', 'Voiture', 3),
('Sow', 'Fatou', '0700000004', 'Moto', 1),
('Traore', 'Ibrahim', '0700000005', 'Camion', 2),
('Ndiaye', 'Awa', '0700000006', 'Moto', 3);
```

### 7.4 Colis

```sql
INSERT INTO colis (reference_colis, poids, type_colis, valeur, statut, date_envoi, id_client) VALUES
('COL001', 2.5, 'Documents', 150.00, 'Livré', '2026-01-10', 1),
('COL002', 5.0, 'Electronique', 1200.00, 'En cours', '2026-01-12', 2),
('COL003', 1.2, 'Vêtements', 300.00, 'Livré', '2026-01-13', 3),
('COL004', 10.5, 'Matériel', 2500.00, 'En attente', '2026-01-14', 4),
('COL005', 3.8, 'Alimentaire', 180.00, 'Livré', '2026-01-15', 5),
('COL006', 7.2, 'Electronique', 900.00, 'En cours', '2026-01-16', 6),
('COL007', 4.1, 'Documents', 200.00, 'Livré', '2026-01-17', 7),
('COL008', 6.0, 'Vêtements', 350.00, 'En cours', '2026-01-18', 8),
('COL009', 12.0, 'Matériel', 3000.00, 'En attente', '2026-01-19', 1),
('COL010', 2.0, 'Alimentaire', 120.00, 'Livré', '2026-01-20', 2);
```

### 7.5 Expéditions

```sql
INSERT INTO expeditions (id_colis, ville_depart, ville_arrivee, date_expedition, date_livraison, id_livreur) VALUES
(1, 'Paris', 'Lyon', '2026-01-10', '2026-01-11', 1),
(2, 'Lyon', 'Marseille', '2026-01-12', NULL, 2),
(3, 'Marseille', 'Paris', '2026-01-13', '2026-01-15', 3),
(4, 'Lille', 'Toulouse', '2026-01-14', NULL, 4),
(5, 'Paris', 'Bordeaux', '2026-01-15', '2026-01-16', 1),
(6, 'Nantes', 'Nice', '2026-01-16', NULL, 2),
(7, 'Nice', 'Paris', '2026-01-17', '2026-01-18', 3),
(8, 'Bordeaux', 'Lyon', '2026-01-18', NULL, 4);
```

### 7.6 Paiements

```sql
INSERT INTO paiements (id_colis, montant, mode_paiement, date_paiement) VALUES
(1, 25.00, 'Carte bancaire', '2026-01-10'),
(2, 80.00, 'Mobile Money', '2026-01-12'),
(3, 35.00, 'Espèces', '2026-01-13'),
(4, 120.00, 'Virement', '2026-01-14'),
(5, 40.00, 'Carte bancaire', '2026-01-15'),
(6, 60.00, 'Mobile Money', '2026-01-16'),
(7, 30.00, 'Espèces', '2026-01-17'),
(8, 55.00, 'Carte bancaire', '2026-01-18');
```

---

## 🔎 8. Questions d’analyse des données

1. Quels sont les clients enregistrés ?
2. Quels clients ont envoyé des colis ?
3. Quels clients n’ont jamais envoyé de colis ?
4. Quel client a envoyé le plus de colis ?
5. Quels colis sont en cours de livraison ?
6. Quels colis ont été livrés ?
7. Quels sont les colis les plus lourds ?
8. Quel est le poids moyen des colis ?
9. Quels types de colis sont les plus fréquents ?
10. Quelles agences ont le plus de livreurs ?
11. Quels livreurs livrent le plus de colis ?
12. Quels livreurs n’ont aucune livraison ?
13. Quelles routes sont les plus utilisées ?
14. Quel est le total des paiements ?
15. Quel mode de paiement est le plus utilisé ?
16. Quels colis ne sont pas encore payés ?
17. Quels clients génèrent le plus de revenus ?
18. Quel est le délai moyen de livraison ?
19. Quelles livraisons sont en attente ?
20. Quel est le chiffre d’affaires total ?
---

## 👨‍💻 9. Auteur

DONYOH Kossi Eric

* Data Analyst
* Développeur Web
* BI & AI Specialist

---

## 📄 11. Licence

Projet académique et pédagogique.
