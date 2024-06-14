Créer la base de données

    CREATE DATABASE school;

Utiliser la base de données

    USE school;

Créer la table "student" avec une clé primaire auto-incrémentée

    CREATE TABLE student (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nom VARCHAR(50),
        prénom VARCHAR(50),
        date_naissance DATE,
        adresse VARCHAR(100),
        email VARCHAR(100)
    );

Créer la table "subject" avec une clé primaire auto-incrémentée

    CREATE TABLE subject (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nom VARCHAR(50),
        description VARCHAR(100)
    );

Créer la table "note" avec une clé primaire auto-incrémentée et des clés étrangères

    CREATE TABLE note (
        id INT AUTO_INCREMENT PRIMARY KEY,
        student_id INT,
        matière_id INT,
        note FLOAT,
        FOREIGN KEY (student_id) REFERENCES student(id),
        FOREIGN KEY (matière_id) REFERENCES subject(id)
    );

Insérez des données dans les tables :

-- Insertion des étudiants
INSERT INTO student (nom, prénom, date_naissance, adresse, email)
VALUES
('Doe', 'John', '2000-01-01', '123 Main Street', 'john.doe@example.com'),
('Smith', 'Emma', '1999-03-15', '456 Elm Street', 'emma.smith@example.com'),
('Johnson', 'Michael', '2001-05-10', '789 Oak Street', 'michael.johnson@example.com'),
('Brown', 'Olivia', '2002-07-20', '321 Pine Street', 'olivia.brown@example.com'),
('Taylor', 'Sophia', '2003-09-25', '654 Maple Street', 'sophia.taylor@example.com'),
('Anderson', 'Liam', '2000-12-05', '987 Cedar Street', 'liam.anderson@example.com'),
('Clark', 'Ava', '1998-02-14', '741 Birch Street', 'ava.clark@example.com'),
('Lewis', 'Noah', '1999-04-30', '852 Walnut Street', 'noah.lewis@example.com'),
('Walker', 'Mia', '2001-06-08', '369 Oakwood Street', 'mia.walker@example.com'),
('Hall', 'Elijah', '2002-08-16', '258 Cherry Street', 'elijah.hall@example.com');

-- Insertion des matières
INSERT INTO subject (nom, description)
VALUES
('Mathématiques', 'Calcul et algèbre'),
('Sciences', 'Physique et chimie'),
('Histoire', 'Événements historiques'),
('Français', 'Grammaire et littérature'),
('Anglais', 'Conversation et grammaire');

-- Insertion des notes pour chaque étudiant (exemples)
INSERT INTO note (student_id, matière_id, note)
VALUES
(1, 1, 15.5),
(1, 2, 12.0),
(2, 3, 14.5),
(2, 4, 16.0),
(3, 5, 13.5),
(3, 1, 17.0),
(4, 2, 13.0),
(4, 3, 11.5),
(5, 4, 18.0),
(5, 5, 16.5);

---

Voici quelques exemples de requêtes SQL avec des conditions, des limites et du tri appliqués à la table "étudiant" :

1. Sélectionner tous les étudiants dont le nom est "Doe" :

    SELECT \*
    FROM student
    WHERE nom = 'Doe';

2. Sélectionner tous les étudiants âgés de moins de 20 ans :

    SELECT \*
    FROM student
    WHERE date_naissance > DATE_SUB(CURDATE(), INTERVAL 20 YEAR);

3. Sélectionner les 5 premiers étudiants dans l'ordre alphabétique des noms :

    SELECT \*
    FROM student
    ORDER BY nom
    LIMIT 5;

4. Sélectionner les étudiants par ordre décroissant de leur date de naissance :

    SELECT \*
    FROM student
    ORDER BY date_naissance DESC;

5. Sélectionner les étudiants dont l'adresse contient le mot "Street" et limiter les résultats à 3 :

    SELECT \*
    FROM student
    WHERE adresse LIKE '%Street%'
    LIMIT 3;

6. Sélectionner les étudiants dont le nom commence par "S" et trier les résultats par prénom :

    SELECT \*
    FROM student
    WHERE nom LIKE 'S%'
    ORDER BY prénom;

Ces exemples montrent comment appliquer des conditions, des limites et du tri dans vos requêtes SQL pour la table "student". N'hésitez pas à les ajuster en fonction de vos critères de recherche spécifiques.

---

Voici quelques exemples de requêtes SQL qui utilisent les fonctions MIN, MAX, COUNT, GROUP BY et HAVING :

1. Sélectionner la note minimale, maximale et le nombre total de notes pour chaque matière :

    SELECT matière_id, MIN(note) AS note_minimale, MAX(note) AS note_maximale, COUNT(\*) AS nombre_notes
    FROM notes
    GROUP BY matière_id;

2. Sélectionner les étudiants ayant une moyenne supérieure à 15 :
   SELECT étudiant_id, AVG(note) AS moyenne
   FROM note
   GROUP BY étudiant_id
   HAVING AVG(note) > 15;

3. Sélectionner le nombre d'étudiants ayant obtenu une note supérieure à 16 dans chaque matière :

    SELECT matière*id, COUNT(\*) AS nombre*étudiants
    FROM note
    WHERE note > 16
    GROUP BY matière_id;

4. Sélectionner les matières ayant au moins cinq étudiants :

    SELECT matière*id, COUNT(\*) AS nombre*étudiants
    FROM note
    GROUP BY matière_id
    HAVING COUNT(\*) >= 5;

5. Sélectionner les étudiants ayant obtenu une note maximale dans chaque matière :

    SELECT matière_id, étudiant_id, MAX(note) AS note_maximale
    FROM note
    GROUP BY matière_id;

Ces exemples illustrent l'utilisation des fonctions MIN, MAX, COUNT, GROUP BY et HAVING pour effectuer des calculs et filtrer les données en fonction de certaines conditions.
N'hésitez pas à les adapter en fonction de votre base de données et de vos besoins spécifiques.

---

Cette requête sélectionne les noms d'étudiants dont la date de naissance est postérieure au 1er janvier 2000, groupe les résultats par nom, filtre les groupes ayant plus de 2 étudiants, trie les résultats par nom et limite les résultats à 10.

SELECT nom, COUNT(_) AS nombre
FROM student
WHERE date_naissance > '2000-01-01'
GROUP BY nom
HAVING COUNT(_) > 2
ORDER BY nom
LIMIT 10;

---

SELECT student.nom, prénom, subject.nom, MAX(note) AS 'note maximal'
FROM student
JOIN note ON student.id = note.étudiant_id
JOIN subject ON note.matière_id = subject.id
WHERE student.date_naissance > '2000-01-01'
GROUP BY student.nom
HAVING Max(note) > 2
ORDER BY student.nom
LIMIT 10;
