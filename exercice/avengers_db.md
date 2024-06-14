# Exercice avec une base de données pour des figurine Avengers :

### 1. Créez une base de données avec le nom `avengers_db` :

### 2. Sélectionnez la base de données nouvellement créée :

### 3. Créez la table "figurine" avec des colonnes telles que "id" (clé primaire), "nom", "super_pouvoir", "annee_sortie" et "description" :

### 4. Insérez des données dans la table "figurine" pour représenter des figurine Avengers :

('Iron Man', 'Armure surpuissante', 2008, 'Milliardaire et génie inventeur.'),
('Captain America', 'Force et endurance surhumaines', 2011, 'Héros emblématique de la Seconde Guerre mondiale.'),
('Thor', 'Contrôle de la foudre et marteau magique', 2011, 'Dieu nordique du tonnerre et prince d\'Asgard.'),
('Hulk', 'Force et résistance surhumaines', 2008, 'Scientifique transformé en monstre vert lorsqu\'il est en colère.'),
('Black Widow', 'Expert en arts martiaux et espionnage', 2010, 'Agent secret russe doté de grandes compétences.'),
('Black Panther', 'Force, vitesse et agilité surhumaines', 2018, 'Roi du Wakanda et protecteur de son peuple.');

### 5. Effectuez des requêtes pour afficher les figurine Avengers :

    - Afficher toutes les figurine :

    - Afficher les figurine sorties après 2010 :

    - Afficher les figurine avec le pouvoir "Force" dans leur super_pouvoir :

### 6. Modifiez une figurine dans la table "figurine" :

    - Modifiez la description de "Black Panther" pour "Prince de Wakanda et protecteur de son peuple."

### 7. Supprimez la figurine Black Widow de la table "figurine" :

### 8. Créer la table "weapon" avec des colonnes telles que "id" (clé primaire), "nom", "description" :

### 9. Insérez des données dans la table "weapon" pour représenter des armes Avengers :

### 10. Modifier la table "figurine" pour ajouter une colonne "weapon_id" :

### 11. Modifier la table "figurine" pour ajouter une contrainte de clé étrangère avec la table "weapon" :

### 12. Mettre la table "weapon" en relation avec la table "figurine" :

### 13. Afficher les figurine avec leur arme :

### 14. Afficher le nom des figurine, leurs armes et leurs années de sortie pour les figurine sorties après 2010 :

### 15. Afficher les figurine sans arme :

_Cet exercice vous permet de créer une base de données ludique pour des figurine Avengers, d'insérer des données et d'effectuer des requêtes pour obtenir des informations spécifiques.
N'hésitez pas à ajouter davantage de figurine et à explorer d'autres fonctionnalités de MySQL pour enrichir votre base de données et vos requêtes._

## Correction

### 1. Créez une base de données avec le nom `avengers_db` :

    ```sql
    CREATE DATABASE avengers_db;
    ```

### 2. Sélectionnez la base de données nouvellement créée :

    ```sql
    USE avengers_db;
    ```

### 3. Créez la table "figurine" avec des colonnes telles que "id" (clé primaire), "nom", "super_pouvoir", "année_sortie" et "description" :

    ```sql
    CREATE TABLE figurine (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100),
    super_pouvoir VARCHAR(100),
    année_sortie INT,
    description TEXT
    );
    ```

### 4. Insérez des données dans la table "figurine" pour représenter des figurine Avengers :

    ```sql
    INSERT INTO figurine (nom, super_pouvoir, année_sortie, description) VALUES
    ('Iron Man', 'Armure surpuissante', 2008, 'Milliardaire et génie inventeur.'),
    ('Captain America', 'Force et endurance surhumaines', 2011, 'Héros emblématique de la Seconde Guerre mondiale.'),
    ('Thor', 'Contrôle de la foudre et marteau magique', 2011, 'Dieu nordique du tonnerre et prince d\'Asgard.'),
    ('Hulk', 'Force et résistance surhumaines', 2008, 'Scientifique transformé en monstre vert lorsqu\'il est en colère.'),
    ('Black Widow', 'Expert en arts martiaux et espionnage', 2010, 'Agent secret russe doté de grandes compétences.'),
    ('Black Panther', 'Force, vitesse et agilité surhumaines', 2018, 'Roi du Wakanda et protecteur de son peuple.');
    ```

### 5. Effectuez des requêtes pour afficher les figurine Avengers :

-   Afficher toutes les figurine :

        ```sql
        SELECT * FROM figurine;
        ```

-   Afficher les figurine sorties après 2010 :

        ```sql
        SELECT * FROM figurine WHERE année_sortie > 2010;
        ```

-   Afficher les figurine avec le pouvoir "Force" dans leur super_pouvoir :

        ```sql
        SELECT * FROM figurine WHERE super_pouvoir LIKE '%Force%';
        ```

### 6. Modifiez une figurine dans la table "figurine" :

    ```sql
    UPDATE figurine SET description = 'Prince de Wakanda et protecteur de son peuple.' WHERE nom = 'Black Panther';
    ```

### 7. Supprimez une figurine de la table "figurine" :

    ```sql
    DELETE FROM figurine WHERE nom = 'Black Window';
    ```

### 8. Créer la table "weapon" avec des colonnes telles que "id" (clé primaire), "nom", "description" :

    ```sql
    CREATE TABLE weapon (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100),
    description TEXT
    );
    ```

### 9. Insérez des données dans la table "weapon" pour représenter des armes Avengers :

    ```sql
    INSERT INTO weapon (nom, description) VALUES
    ('Marteau', 'Marteau magique de Thor.'),
    ('Bouclier', 'Bouclier indestructible.'),
    ('Arc et flèches', 'Arc et flèches de Hawkeye.'),
    ('Armure', 'Armure spéciale conçue pour combattre Hulk.'),
    ('Vibranium Claws', 'Griffes en vibranium indestructible .');
    ```

### 10. Modifier la table "figurine" pour ajouter une colonne "weapon_id" :

    ```sql
    ALTER TABLE figurine ADD weapon_id INT;
    ```

### 11. Modifier la table "figurine" pour ajouter une contrainte de clé étrangère avec la table "weapon" :

    ```sql
    ALTER TABLE figurine ADD CONSTRAINT fk_weapon FOREIGN KEY (weapon_id) REFERENCES weapon(id);
    ```

### 12. Mettre la table "weapon" en relation avec la table "figurine" :

    ```sql
    UPDATE figurine SET weapon_id = 1 WHERE nom = 'Thor';
    UPDATE figurine SET weapon_id = 2 WHERE nom = 'Captain America';
    UPDATE figurine SET weapon_id = 5 WHERE nom = 'Black Panther';
    ```

### 13. Afficher les figurine avec leur arme :

    ```sql
    SELECT figurine.nom, weapon.nom FROM figurine JOIN weapon ON figurine.weapon_id = weapon.id;
    ```

### 14. Afficher le nom des figurine, leurs armes et leurs années de sortie pour les figurine sorties après 2010 :

    ```sql
    SELECT figurine.nom, weapon.nom, figurine.année_sortie FROM figurine JOIN weapon ON figurine.weapon_id = weapon.id WHERE figurine.année_sortie > 2010;
    ```

### 15. Afficher les figurine sans arme :

    ```sql
    SELECT figurine.nom FROM figurine WHERE weapon_id IS NULL;
    ```
