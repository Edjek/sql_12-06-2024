Voici un exemple d'exercice avec une base de données pour des bandes dessinées belges, en incluant plusieurs tables telles que "BD", "auteur" et "editeur" :

1. Créez une base de données :

    CREATE DATABASE bd_collection_db;


2. Sélectionnez la base de données nouvellement créée :

    USE bd_collection_db;


3. Créez la table "auteur" avec des colonnes telles que "id" (clé primaire), "nom" et "nationalite" :

    CREATE TABLE auteur (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100),
    nationalite VARCHAR(50)
    );


4. Insérez des données dans la table "auteur" pour représenter les auteur des bandes dessinées :

    INSERT INTO auteur (nom, nationalite) VALUES
    ('Hergé', 'Belge'),
    ('René Goscinny', 'Français'),
    ('Albert Uderzo', 'Français');


5. Créez la table "editeur" avec des colonnes telles que "id" (clé primaire), "nom" et "pays" :

    CREATE TABLE editeur (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100),
    pays VARCHAR(50)
    );


6. Insérez des données dans la table "editeur" pour représenter les éditeurs des bandes dessinées :

    INSERT INTO editeur (nom, pays) VALUES
    ('Casterman', 'Belgique'),
    ('Dargaud', 'France'),
    ('Dupuis', 'Belgique');

7. Créez la table "bd" avec des colonnes telles que "id" (clé primaire), "titre", "auteur_id" (clé étrangère faisant référence à la table auteur), "editeur_id" (clé étrangère faisant référence à la table editeur) et "annee_parution" :

    CREATE TABLE bd (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titre VARCHAR(100),
    auteur_id INT,
    editeur_id INT,
    annee_parution INT,
    FOREIGN KEY (auteur_id) REFERENCES auteur(id),
    FOREIGN KEY (editeur_id) REFERENCES editeur(id)
    );

8. Insérez des données dans la table "bd" pour représenter différentes bandes dessinées avec leurs auteur et éditeurs :

    INSERT INTO bd (titre, auteur_id, editeur_id, annee_parution) VALUES
    ('Tintin au Tibet', 1, 1, 1960),
    ('Astérix le Gaulois', 2, 2, 1961),
    ('Les Aventures de Blake et Mortimer', 1, 3, 1946);

9. Effectuez des requêtes pour afficher les informations sur les bandes dessinées, les auteur et les éditeurs :

    - Afficher toutes les bandes dessinées avec les informations complètes :

        SELECT bd.titre, auteur.nom AS auteur, editeur.nom AS editeur, bd.annee_parution
        FROM bd
        JOIN auteur ON bd.auteur_id = auteur.id
        JOIN editeur ON bd.editeur_id = editeur.id;

    - Afficher les bandes dessinées publiées par un éditeur spécifique (par exemple, "Casterman") :

        SELECT bd.titre, auteur.nom AS auteur, editeur.nom AS editeur, bd.annee_parution
        FROM bd
        JOIN auteur ON bd.auteur_id = auteur.id
        JOIN editeur ON bd.editeur_id = editeur.id
        WHERE editeur.nom = 'Casterman';

    - Afficher les bandes dessinées publiées après une certaine année (par exemple, après 1960) :

        SELECT bd.titre, auteur.nom AS auteur, editeur.nom AS editeur, bd.annee_parution
        FROM bd
        JOIN auteur ON bd.auteur_id = auteur.id
        JOIN editeur ON bd.editeur_id = editeur.id
        WHERE bd.annee_parution > 1960;

Cet exercice vous permet de créer une base de données pour des bandes dessinées belges, de gérer les relations entre les tables "bd", "auteur" et "editeur", et d'effectuer des requêtes pour obtenir des informations spécifiques.
Vous pouvez ajouter davantage de données, de tables et d'autres fonctionnalités de MySQL pour enrichir votre base de données selon vos besoins.