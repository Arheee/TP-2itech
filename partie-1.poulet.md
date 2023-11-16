## Docker

Si vous avez déjà vu Docker, créez via docker un conteneur MySQL et importez le fichier `beer.sql` dans votre conteneur.

Si vous n'avez pas encore vu Docker, importez le fichier `beer.sql` dans votre base de données MySQL ou demandez à votre
formateur de vous aider ou de vous donner le docker-compose.

### Prérequis

- Vous devez avoir un dockerfile et un docker-compose.yml
- Vous ne devez pas utiliser de `bind mount` !
- Vous avez le droit d'utiliser un `volume`

## Etude du modèle

### Effectuez un reverse engineering du modèle

- Quelles sont les tables ?

### Il y a des mauvaises pratiques dans ce modèle, lesquelles ?

- Regardez bien les tables et les colonnes, vous devriez trouver des choses qui ne vont pas

## Exercices

Réalisez les requêtes suivantes :

### Quels sont les tickets qui comportent l’article d’ID 500, afficher le numéro de ticket uniquement ?

```mysql
SELECT NUMERO_TICKET
FROM ventes 
WHERE ID_ARTICLE = 500
```

- Il n'y a pas de jointure à faire : tout est déjà dans la table `ventes`

### Afficher les tickets du 15/01/2014.

```mysql
SELECT NUMERO_TICKET 
FROM ticket 
WHERE DATE_VENTE = "2014-01-15 00:00:00"
```

- La requête est très similaire à la précédente

### Afficher les tickets émis du 15/01/2014 et le 17/01/2014.

```mysql
SELECT NUMERO_TICKET , DATE_VENTE 
FROM ticket 
WHERE DATE_VENTE BETWEEN "2014-01-15 00:00:00" AND "2014-01-17 00:00:00"
```

- Vous aurez besoin de la clause `BETWEEN` pour cette requête


### Afficher la liste des articles apparaissant à 50 et plus exemplaires sur un ticket.

```mysql
SELECT NUMERO_TICKET, NOM_ARTICLE 
FROM ventes INNER JOIN  article
WHERE QUANTITE >= 50 
```

- La table qui vous intéresse est la table `ventes`
- Vous devrez faire une jointure avec la table `article`

### Quelles sont les tickets émis au mois de mars 2014.

```mysql
SELECT ANNEE , NUMERO_TICKET 
FROM ticket 
WHERE month('2014-03-01') AND year('2014-03-01')
```

- Vous aurez besoin de fonctions de temps pour cette requête


### Quelles sont les tickets émis entre les mois de mars et avril 2014 ?

```mysql
SELECT ANNEE , NUMERO_TICKET , DATE_VENTE 
FROM ticket 
WHERE year(DATE_VENTE)= 2014 AND month(DATE_VENTE) IN ('3' , '4')
```

- Vous devrez utiliser la clause `IN` pour cette requête

### Quelles sont les tickets émis au mois de mars et juin 2014 ?

```mysql
SELECT ANNEE , NUMERO_TICKET , DATE_VENTE 
FROM ticket 
WHERE year(DATE_VENTE)= 2014 AND month(DATE_VENTE) IN ('3' , '6')
```

### Afficher la liste des bières classée par couleur. (Afficher l’id et le nom)

```mysql
SELECT ID_ARTICLE, NOM_ARTICLE, NOM_COULEUR
FROM article 
JOIN beer.couleur ON article.ID_Couleur = Couleur.ID_Couleur
ORDER BY NOM_COULEUR
```

- Vous aurez besoin d'une jointure avec la table `couleur`
- Vous devrez utiliser la clause `ORDER BY`

### Afficher la liste des bières n’ayant pas de couleur. (Afficher l’id et le nom)

```mysql
SELECT ID_ARTICLE, NOM_ARTICLE, ID_Couleur 
FROM article 
WHERE ID_Couleur IS NULL
```

- La table qui vous intéresse est la table `article`
