---
title: Jeux De Données Dérivés
description: Les jeux de données dérivés offrent un moyen pratique de générer les jeux de données de votre choix qui peuvent être actualisés à n’importe quelle cadence régulière et éventuellement publiés dans vos données de profil client en temps réel. Ce document présente un aperçu de l’utilisation de Query Service pour créer des jeux de données dérivés à utiliser avec vos données de profil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
TQID: https://experienceleague.adobe.com/96Bjr5P6CXB7vb5qnqNJS-ZvCU96rstr8f2U7Whl2M8
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 767
ht-degree: 0%

---

# Jeux de données dérivés

La fonctionnalité des jeux de données dérivés offre un moyen pratique de générer des jeux de données de votre choix à partir d’autres informations disponibles dans le lac de données. Ces jeux de données peuvent être actualisés à n’importe quelle cadence régulière et éventuellement publiés dans vos données de profil client en temps réel. Les jeux de données dérivés répondent à la nécessité de créer des jeux de données complexes tels que les déciles, les percentiles et les quartiles par rapport à des jeux plus simples tels que les maximums, les nombres et les moyennes. Ces jeux de données peuvent être calculés spécifiquement pour un utilisateur individuel ou pour une entité commerciale. Vous pouvez ainsi dériver des jeux de données qui peuvent être directement accrédités pour un identifiant, tel que des adresses e-mail, des identifiants d’appareil et des numéros de téléphone, et dériver également des jeux de données indirectement associés à cet utilisateur ou à ce profil d’entreprise.

Les jeux de données dérivés sont nécessaires pour divers cas d’utilisation lorsque les données sont analysées sur le lac de données. Ces données peuvent ensuite être marquées pour être utilisées dans le profil client en temps réel et dans des cas d’utilisation en aval, comme la création d’audiences très ciblées. Voici quelques cas d’utilisation potentiels de cette fonctionnalité :

* Identifier les 10 % d&#39;abonnés les plus faibles en fonction de l&#39;auditoire par canal. Cela permettrait aux spécialistes du marketing de cibler une audience particulière et de vendre un nouveau forfait d&#39;abonnés.
* Identifier une audience qui se trouve dans les 10 % premiers des prospectus en fonction du nombre total de miles parcourus et qui a le statut de « Voyageur ». Cette audience pourrait être utilisée pour cibler de manière sélective la vente d’une nouvelle offre de carte de crédit.
* Déterminez le taux de résiliation en fonction de l’abonnement.
* Identifier les 1 % les plus riches du revenu des ménages dans une province ou un État, et fournir une mesure du nombre de personnes qui quittent ce groupe collectif au cours des « n » derniers mois.

## Jeux de données dérivés complexes

Pour créer un classement basé sur une ou plusieurs mesures (telles que le chiffre d’affaires, la durée d’audience, etc.) pour une dimension particulière (catégorie), des jeux de données dérivés complexes sont requis. Les déciles, quartiles et centiles offrent davantage de flexibilité et de précision lors du classement des données avec des jeux de données dérivés.

Un décile est une méthode de division d’un ensemble de données classées en 10 parties égales. Lorsque les données sont divisées en déciles, un rang de déciles est attribué à chaque ligne du jeu de données. Cela permet de trier les données par ordre décroissant ou croissant.

Un rang décile organise les données dans l&#39;ordre du plus bas au plus élevé et est effectué sur une échelle de 1 à 10 où chaque nombre successif correspond à une augmentation de 10 points de pourcentage.

Les intervalles de déciles représentent le nombre de groupes classés et sont utilisés pour attribuer un classement à une dimension (catégorie) dans le jeu de données. Le compartiment peut être un nombre ou une expression qui renvoie une valeur entière positive pour chaque partition. Les intervalles ne doivent pas avoir de valeur nulle.

On utilise les quartiles pour diviser la distribution par quatre et les centiles par 100.

## Jeux de données dérivés à des fins d’analyse

Query Service fournit des fonctions intégrées telles que la sessionnalisation et la dernière touche, entre autres, que vous pouvez appliquer à toutes les données de série temporelle pour générer des jeux de données dérivés liés à l’entreprise. Vous avez la possibilité de baser ces jeux de données dérivés d’analyses sur une ou plusieurs identités et de publier éventuellement les données dans le profil client en temps réel si nécessaire.

Voici quelques cas d’utilisation potentiels pour ce type d’attribut dérivé :

* Suivi des produits analysés au cours d’une session utilisateur et qui étaient en rupture de stock.
* Suivi des mesures populaires telles que la taille, la couleur ou la catégorie de produits des produits parcourus ou achetés.
* Suivi de la source de la plateforme qui a conduit à la navigation ou à l’achat d’un produit.
* Suivi de l’élément consulté le plus récemment par une identité.
* Mesures de suivi telles que le nombre moyen d’articles dans un panier, l’abandon de panier ou la fréquence d’achat moyenne.

## Autres jeux de données dérivés

Vous pouvez également calculer des mesures commerciales en tant qu’attribut dérivé et les utiliser conjointement avec des jeux de données simples tels que du code postal ou une mesure agrégée telle que le nombre total. Par exemple, un nombre total basé sur une ville ou une province, ou un nombre total basé sur une catégorie d’entreprise et une ville/province.

## Étapes suivantes et cas d’utilisation

Grâce à la lecture de ce document, vous comprenez mieux comment les jeux de données dérivés de Query Service facilitent les cas d’utilisation complexes pour optimiser l’utilité de vos données. Vous devez ensuite lire le cas d’utilisation d’attributs dérivés basés sur des déciles ](../../use-cases/deciles-use-case.md) pour voir comment cette fonctionnalité est appliquée dans un scénario réel.[
