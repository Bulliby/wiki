# SQL Anti-Patterns

## Jay Walking

Pour ne pas modifier le schéma on stocke des foreign key que l'on concatène (*avec une virgule par exemple*). 

On transforme ainsi un One to Many en Many to Many sans créer de table d'intersection. C'est de la **dé-normalisation**.

## Naive Trees

> Utiliser MySQL pour stocker des arbres complets.

**Adjacency List** c'est le fait de stocker l'ID du parent dans la ligne qui représente un des enfants. Ce modèle est valable pour retrouver les éléments d'un parent mais est in-maintenable pour des arbres d'une profondeur arbitraire.

Il n'y a pas de solution simple pour stocker et intéragire avec un arbre.

##	Ambigous Groups

### The Single-Value Rule

```
Every column in the select-list of a query must have a single value row per row group. This is called the Single-Value Rule
```

Le `GROUP BY` sur une colonne, regroupe les entrées par cette colonne. Si on choisit de **SÉLECTIONNER** une colonne qui n'est pas regroupable, comme celle du `GROUP BY`. **MYSQL** ne peut pas déterminer la donnée à afficher.

On peut ajouter cette colonne dans le `GROUP BY`, ou utiliser une fonction d'Aggrégation pour la sélectionner (type MAX(), SUM()...) qui elles garantissent la **Single Value Rule**

### Functional dependency

C'est quand on peut ramener des éléments sans ambiguïté même si la colonne n'est pas dans le `GROUP BY

### Solutions :

#### Query Only Functionally Dependent Columns

```sql
SELECT product_id, MAX(date_reported) AS latest
FROM Bugs JOIN BugsProducts USING (bug_id)
GROUP BY product_id;
```

#### Using a Correlated Subquery

```sql
SELECT bp1.product_id, b1.date_reported AS latest, b1.bug_id
FROM Bugs b1 JOIN BugsProducts bp1 USING (bug_id)
WHERE NOT EXISTS
(SELECT * FROM Bugs b2 JOIN BugsProducts bp2 USING (bug_id)
WHERE bp1.product_id = bp2.product_id
AND b1.date_reported < b2.date_reported);
```

#### Using a Derived Table

```sql
SELECT m.product_id, m.latest, MAX(b1.bug_id) AS latest_bug_id
FROM Bugs b1 JOIN
(SELECT product_id, MAX(date_reported) AS latest
FROM Bugs b2 JOIN BugsProducts USING (bug_id)
GROUP BY product_id) m
ON (b1.date_reported = m.latest)
GROUP BY m.product_id, m.latest;
```

#### Using a JOIN

```sql
SELECT bp1.product_id, b1.date_reported AS latest, b1.bug_id
FROM Bugs b1 JOIN BugsProducts bp1 ON (b1.bug_id = bp1.bug_id)
LEFT OUTER JOIN (Bugs AS b2 JOIN BugsProducts AS bp2 ON (b2.bug_id = bp2.bug_id))
ON (bp1.product_id = bp2.product_id AND (b1.date_reported < b2.date_reported
OR b1.date_reported = b2.date_reported AND b1.bug_id < b2.bug_id))
WHERE b2.bug_id IS NULL;
```

> Ici on fait un left join pour récupérer la partie de droite à nul, qui indique que l'élément de gauche est le **max** car il n'a pas de correspondance : `b1.date_reported < b2.date_reported`