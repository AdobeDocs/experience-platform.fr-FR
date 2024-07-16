---
title: Jeux de données dérivés
description: Les jeux de données dérivés offrent un moyen pratique de générer des jeux de données de votre choix qui peuvent être actualisés régulièrement et éventuellement publiés dans vos données Real-time Customer Profile. Ce document présente l’utilisation de Query Service pour créer des jeux de données dérivés à utiliser avec vos données de profil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Jeux de données dérivés

La fonctionnalité des jeux de données dérivés fournit un moyen pratique de générer des jeux de données de votre choix à partir d’autres informations disponibles dans le lac de données. Ces jeux de données peuvent être actualisés à n’importe quel rythme régulier et éventuellement publiés dans vos données Real-Time Customer Profile. Les jeux de données dérivés répondent à la nécessité de créer des jeux de données complexes tels que le décile, le percentile et le quartile par rapport à des jeux plus simples tels que le maximum, le décompte et la moyenne. Ces jeux de données peuvent être calculés spécifiquement pour un utilisateur individuel ou pour une entité commerciale. Vous pouvez ainsi dériver des jeux de données qui peuvent être directement accrédités à un identifiant, comme des adresses électroniques, des identifiants d’appareil et des numéros de téléphone, et également dériver des jeux de données qui sont indirectement associés à cet utilisateur ou ce profil d’entreprise.

Des jeux de données dérivés sont nécessaires pour divers cas d’utilisation lorsque des données sont analysées sur le lac de données. Ces données peuvent ensuite être marquées pour une utilisation dans Real-time Customer Profile et utilisées dans des cas d’utilisation en aval, comme la création d’audiences fortement ciblées. Voici quelques cas d’utilisation potentiels de cette fonctionnalité :

* Identification des 10 % d’abonnés les plus bas en fonction de l’audience par canal. Cela permet aux marketeurs de cibler une audience particulière et de vendre un nouveau module d’abonné.
* Identification d’une audience qui se trouve dans le top 10 % des tracts en fonction de leur nombre total de kilomètres parcourus et dont le statut est &quot;prospectus&quot; Cette audience peut être utilisée pour cibler de manière sélective la vente d’une nouvelle offre de carte de crédit.
* Déterminez le taux de perte de clientèle en fonction de l’abonnement.
* Identifier les 1% les plus riches du revenu du ménage dans une province ou un État et fournir une mesure du nombre de personnes qui quittent ce groupe collectif au cours des &quot;n&quot; derniers mois.

## Jeux de données dérivés complexes

Pour créer un classement basé sur une ou plusieurs mesures (telles que les recettes, la durée de visionnage, etc.) sur une dimension particulière (catégorie), des jeux de données dérivés complexes sont requis. Les décimales, les quartiles et les centiles permettent une flexibilité et une précision lors du classement des données avec des jeux de données dérivés.

Un décile est une méthode permettant de diviser un ensemble de données classées en 10 parties égales. Lorsque les données sont divisées en déciles, un rang de décile est attribué à chaque ligne de l’ensemble de données. Cela permet de trier les données par ordre croissant ou décroissant.

Un classement en déciles classe les données dans l’ordre du plus petit au plus élevé, sur une échelle de 1 à 10 où chaque nombre successif correspond à une augmentation de 10 points de pourcentage.

Les intervalles par déciles représentent le nombre de groupes classés et sont utilisés pour affecter un classement à une dimension (catégorie) dans le jeu de données. Le compartiment peut être un nombre ou une expression qui évalue à une valeur entière positive pour chaque partition. Les compartiments ne doivent pas avoir de valeur nulle.

Les quartile sont utilisés pour diviser la distribution par quatre et les centiles par 100.

## Jeux de données dérivés Analytics

Query Service fournit des fonctions intégrées telles que la sessionisation et la Dernière touche, entre autres, que vous pouvez appliquer à n’importe quelle donnée de série temporelle pour générer des jeux de données dérivés liés à l’entreprise. Vous avez la possibilité de baser ces jeux de données dérivés analytiques sur une ou plusieurs identités et éventuellement de publier les données dans Real-time Customer Profile si nécessaire.

Voici quelques cas d’utilisation potentiels pour ce type d’attribut dérivé :

* Suivi des produits analysés au cours d’une session utilisateur qui étaient en rupture de stock.
* Suivi des mesures les plus utilisées, telles que la taille, la couleur ou la catégorie de produits des produits en cours de navigation ou achetés.
* Suivi de la source de la plateforme qui a conduit à un achat ou à une navigation sur un produit.
* Suivi de l’élément consulté le plus récemment par une identité.
* Mesures de suivi telles que le nombre moyen d’articles dans un panier, l’abandon de panier ou la fréquence d’achat moyenne.

## Autres jeux de données dérivés

Vous pouvez également calculer des mesures commerciales en tant qu’attribut dérivé et les utiliser conjointement avec des jeux de données simples tels que le code postal ou une mesure agrégée telle que le nombre total. Par exemple, un nombre total basé sur une ville ou une province, ou un nombre total basé sur une catégorie commerciale et une ville/province.

## Étapes suivantes et cas pratiques

En lisant ce document, vous comprenez mieux comment les jeux de données dérivés de Query Service facilitent des cas d’utilisation complexes pour optimiser l’utilité de vos données. Vous devez ensuite lire le [cas d’utilisation d’attribut dérivé basé sur des déciles](../../use-cases/deciles-use-case.md) pour voir comment cette fonctionnalité est appliquée dans un scénario réel.
