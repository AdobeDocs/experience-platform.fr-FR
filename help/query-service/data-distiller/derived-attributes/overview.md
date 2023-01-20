---
title: Attributs dérivés
description: Les attributs dérivés offrent un moyen pratique de générer des attributs de votre choix qui peuvent être actualisés à n’importe quel rythme régulier et éventuellement publiés dans vos données Real-Time Customer Profile. Ce document présente l’utilisation de Query Service pour créer des attributs dérivés à utiliser avec vos données de profil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Attributs dérivés

La fonction Attributs dérivés fournit un moyen pratique de générer des attributs de votre choix à partir d’autres informations disponibles dans le lac de données. Ces attributs peuvent être actualisés à n’importe quel rythme régulier et éventuellement publiés dans vos données Real-Time Customer Profile. Les attributs dérivés répondent à la nécessité de créer des attributs complexes tels que le décile, le percentile et le quartile par rapport à des attributs plus simples tels que le maximum, le décompte et la moyenne. Ces attributs peuvent être calculés spécifiquement pour un utilisateur individuel ou pour une entité commerciale. Vous pouvez ainsi dériver des attributs qui peuvent être directement accrédités à un identifiant, tels que les adresses électroniques, les identifiants d’appareil et les numéros de téléphone, et aussi dériver des attributs indirectement associés à cet utilisateur ou ce profil d’entreprise.

Des attributs dérivés sont nécessaires pour divers cas d’utilisation lorsque des données sont analysées sur le lac de données. Ces données peuvent ensuite être marquées pour une utilisation dans Real-time Customer Profile et utilisées dans des cas d’utilisation en aval, comme la création d’audiences fortement ciblées. Voici quelques cas d’utilisation potentiels de cette fonctionnalité :

* Identification des 10 % d’abonnés les plus bas en fonction de l’audience par canal. Cela permet aux marketeurs de cibler une audience particulière et de vendre un nouveau module d’abonné.
* Identification d’une audience qui se trouve dans le top 10 % des tracts en fonction de leur nombre total de kilomètres parcourus et dont le statut est &quot;prospectus&quot; Cette audience peut être utilisée pour cibler de manière sélective la vente d’une nouvelle offre de carte de crédit.
* Déterminez le taux de perte de clientèle en fonction de l’abonnement.
* Identifier les 1% les plus riches du revenu du ménage dans une province ou un État et fournir une mesure du nombre de personnes qui quittent ce groupe collectif au cours des &quot;n&quot; derniers mois.

## Attributs dérivés complexes

Pour créer un classement basé sur une ou plusieurs mesures (recettes, durée de consultation, etc.) pour une dimension spécifique (catégorie), des attributs dérivés complexes sont requis. Les décimales, les quartiles et les centiles permettent une flexibilité et une précision lors du classement des données avec des attributs dérivés.

Un décile est une méthode permettant de diviser un ensemble de données classées en 10 parties égales. Lorsque les données sont divisées en déciles, un rang de décile est attribué à chaque ligne de l’ensemble de données. Cela permet de trier les données par ordre croissant ou décroissant.

Un classement en déciles classe les données dans l’ordre du plus petit au plus élevé, sur une échelle de 1 à 10 où chaque nombre successif correspond à une augmentation de 10 points de pourcentage.

Les intervalles par déciles représentent le nombre de groupes classés et sont utilisés pour affecter un classement à une dimension (catégorie) dans le jeu de données. Le compartiment peut être un nombre ou une expression qui évalue à une valeur entière positive pour chaque partition. Les compartiments ne doivent pas avoir de valeur nulle.

Les quartile sont utilisés pour diviser la distribution par quatre et les centiles par 100.

## Attributs dérivés Analytics

Query Service fournit des fonctions intégrées telles que la sessionisation et la Dernière touche, entre autres, que vous pouvez appliquer à n’importe quelle donnée de série temporelle pour générer des attributs dérivés liés à l’entreprise. Vous avez la possibilité de baser ces attributs dérivés analytiques sur une ou plusieurs identités et éventuellement de publier les données dans Real-time Customer Profile si nécessaire.

Voici quelques cas d’utilisation potentiels pour ce type d’attribut dérivé :

* Suivi des produits analysés au cours d’une session utilisateur qui étaient en rupture de stock.
* Suivi des mesures les plus utilisées, telles que la taille, la couleur ou la catégorie de produits des produits en cours de navigation ou achetés.
* Suivi de la source de la plateforme qui a conduit à la navigation ou à l’achat d’un produit.
* Suivi de l’élément consulté le plus récemment par une identité.
* Mesures de suivi telles que le nombre moyen d’articles dans un panier, l’abandon de panier ou la fréquence d’achat moyenne.

## Autres attributs dérivés

Vous pouvez également calculer des mesures commerciales en tant qu’attribut dérivé et les utiliser conjointement avec des attributs simples tels que le code postal ou une mesure agrégée telle que le nombre total. Par exemple, un nombre total basé sur une ville ou une province, ou un nombre total basé sur une catégorie commerciale et une ville/province.

## Étapes suivantes et cas pratiques

En lisant ce document, vous comprenez mieux comment les attributs dérivés de Query Service facilitent les cas d’utilisation complexes pour optimiser l’utilité de vos données. Vous devriez ensuite lire le [Cas d’utilisation des attributs dérivés basés sur des déciles](../../use-cases/deciles-use-case.md) pour voir comment cette fonction est appliquée dans un scénario réel.
