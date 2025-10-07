## 🎯 Objectifs
- Créer une base de données et des tables MySQL.
- Insérer, lire, mettre à jour et supprimer des données (CRUD SQL).
- Exécuter des requêtes avec filtres, jointures simples.
- Comprendre les notions de contraintes (clé primaire, clé étrangère, NOT NULL, UNIQUE).
- Tester les requêtes dans MySQL Shell ou via un client (MySQL Workbench, CLI).

---

## 1️⃣ Connexion & création de la base

```sql
-- Se connecter (via CLI ou client) :
mysql -u root -p

-- Créer une base de données
CREATE DATABASE atelier_sql;
USE atelier_sql;
```

---

## 2️⃣ Création des tables

```sql
CREATE TABLE authors (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE
);

CREATE TABLE books (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(200) NOT NULL,
  published_year INT,
  author_id INT,
  FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

---

## 3️⃣ Insertion de données

```sql
INSERT INTO authors (name, email) VALUES
  ('Alice Dupont', 'alice@example.com'),
  ('Bob Martin', 'bob@example.com');

INSERT INTO books (title, published_year, author_id) VALUES
  ('Le premier livre', 2020, 1),
  ('Un autre livre', 2023, 2),
  ('Livre sans auteur', 2025, NULL);
```

---

## 4️⃣ Lecture des données (SELECT)

```sql
SELECT * FROM authors;

SELECT * FROM books;

SELECT b.id, b.title, b.published_year, a.name AS author_name
FROM books b
LEFT JOIN authors a ON b.author_id = a.id;

SELECT * FROM books WHERE published_year > 2021;
```

---

## 5️⃣ Mise à jour (UPDATE)

```sql
UPDATE books
SET title = 'Titre modifié'
WHERE id = 1;

UPDATE books
SET author_id = 2
WHERE id = 3;
```

---

## 6️⃣ Suppression (DELETE)

```sql
DELETE FROM books WHERE id = 3;

DELETE FROM authors WHERE id = 2;
```

---

## 7️⃣ Requêtes avancées

```sql
SELECT a.name, COUNT(b.id) AS book_count
FROM authors a
LEFT JOIN books b ON b.author_id = a.id
GROUP BY a.id;

SELECT * FROM books WHERE title LIKE '%livre%';
```

---

## 8️⃣ Exercices pratiques

1. Ajouter une colonne `genre VARCHAR(50)` dans `books`.  
2. Mettre à jour le genre de certains livres avec `UPDATE`.  
3. Trouver les auteurs n’ayant aucun livre (LEFT JOIN + condition).  
4. Supprimer tous les livres publiés avant l’année 2022.  
5. Créer une table `reviews` liée aux livres, avec champs `rating INT`, `comment TEXT`, `book_id` clé étrangère.  
6. Insérer des reviews, puis lister les livres avec leur moyenne de notes (`AVG(rating)`).

---

## 9️⃣ Corrigé & points de contrôle

- Vérifier que les contraintes FK fonctionnent.  
- Toujours vérifier le nombre de lignes affectées.  
- Tester les jointures et filtres.  
- Vérifier les résultats des agrégats (COUNT, AVG).  
- Ajouter des index si besoin (`author_id`, `title`).

---

✅ **Fin de l’atelier MySQL CRUD**
