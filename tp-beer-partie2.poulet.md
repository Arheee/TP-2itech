## 10 Listez pour chaque ticket la quantité totale d’articles vendus. (Classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as QuantiteTotale 
fROM ventes
GROUP BY NUMERO_TICKET ORDER BY QuantiteTotale DESC
```

- Vous aurez besoin de la fonction `SUM`



## 11 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. (Classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as QuantiteTotale 
FROM ventes
GROUP BY NUMERO_TICKET 
HAVING QuantiteTotale > 500 
ORDER by QuantiteTotale DESC
```

- Vous devrez utiliser la fonction `GROUP BY`
- Vous devrez utiliser `ORDER BY`

## 12 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. On exclura du total, les ventes ayant une quantité supérieure à 50 (classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as QuantiteTotale 
FROM ventes
GROUP BY NUMERO_TICKET 
HAVING QuantiteTotale > 500 
AND MAX(QUANTITE) <= 50
ORDER by QuantiteTotale DESC
```

- Vous réaliserez la somme des quantités vendues avec la fonction `SUM` dans le `SELECT`

## 13 Listez les bières de type ‘Trappiste’. (id, nom de la bière, volume et titrage)

```mysql
SELECT ID_ARTICLE , NOM_ARTICLE, VOLUME, TITRAGE, NOM_TYPE
FROM article
INNER JOIN `type`
WHERE NOM_TYPE ='Trappiste'
```

- Vous devrez faire une jointure avec la table `type`

## 14 Listez les marques de bières du continent ‘Afrique’

```mysql
SELECT NOM_MARQUE, NOM_CONTINENT
FROM marque
INNER JOIN pays , continent
WHERE NOM_CONTINENT ='Afrique'
```

- Vous devrez faire deux jointures

## 15 Lister les bières du continent ‘Afrique’

```mysql
SELECT NOM_ARTICLE, NOM_MARQUE, NOM_CONTINENT
FROM article
INNER JOIN marque, pays , continent
WHERE NOM_CONTINENT ='Afrique'
```

- Vous devrez faire trois jointures

## 16. Lister les tickets (année, numéro de ticket, montant total payé). En sachant que le prix de vente est égal au prix d’achat augmenté de 15%.

```mysql
SELECT ticket.ANNEE, ticket.NUMERO_TICKET, ticket.DATE_VENTE, 
SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) AS 'Montant_total'
FROM ticket
JOIN ventes USING (ANNEE, NUMERO_TICKET)
JOIN article ON article.ID_ARTICLE= ventes.ID_ARTICLE
GROUP BY ticket.ANNEE, ticket.NUMERO_TICKET
```

- Vous devrez faire un `SUM` sur la quantité multipliée par le prix d'achat, et ajouter 15% 
- Vous devrez faire deux jointures

> Vous aurez certainement besoin du mot `USING` dans votre requête.

## 17  Donner le C.A. par année.

```mysql
SELECT ventes.ANNEE, 
SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) AS 'Chiffre-affaire'
FROM ventes
JOIN article ON ventes.ID_ARTICLE= article.ID_ARTICLE
GROUP BY ventes.ANNEE
ORDER BY ventes.ANNEE
```

- Vous devrez faire la somme des quantités multipliées par le prix d'achat, et ajouter 15% au résultat (*1.15)

## 18. Lister les quantités vendues de chaque article pour l’année 2016.

```mysql
SELECT article.ID_ARTICLE, ventes.ANNEE, article.NOM_ARTICLE,
SUM(ventes.QUANTITE) AS 'Quantites-vendues'
FROM ventes
JOIN article ON ventes.ID_ARTICLE= article.ID_ARTICLE
WHERE ventes.ANNEE = 2016
GROUP BY article.ID_ARTICLE, article.NOM_ARTICLE
ORDER BY 'Quantites-vendues'
```

- Vous devrez faire une jointure

## 19. Lister les quantités vendues de chaque article pour les années 2014, 2015, 2016.

```mysql
SELECT article.ID_ARTICLE, ventes.ANNEE, article.NOM_ARTICLE,
SUM(ventes.QUANTITE) AS 'Quantites-vendues'
FROM ventes
JOIN article ON ventes.ID_ARTICLE= article.ID_ARTICLE
WHERE ventes.ANNEE BETWEEN 2014 AND 2016
GROUP BY article.ID_ARTICLE, article.NOM_ARTICLE, ventes.ANNEE
ORDER BY 'Quantites-vendues' ;
```

- Vous devrez faire la somme des quantités vendues avec la fonction `SUM` dans le `SELECT`
