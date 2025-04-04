---
title: Présentation des attributs calculés
description: Les attributs calculés sont des fonctions permettant d’agréger les données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées dans la segmentation, l’activation et la personnalisation.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 8%

---

# Présentation des attributs calculés

Le Personalization basé sur le comportement de l’utilisateur est une exigence clé pour que les professionnels du marketing puissent maximiser l’impact de la personnalisation. Par exemple, la personnalisation des e-mails marketing avec le produit le plus récemment consulté pour stimuler la conversion ou la personnalisation des pages web en fonction du nombre total d’achats effectués par les utilisateurs pour stimuler la rétention.

Les attributs calculés permettent de convertir rapidement les données comportementales de profil en valeurs agrégées au niveau du profil sans dépendre des ressources d’ingénierie pour :

- Activation de la personnalisation par lots ou individuelle ciblée avec activation d’agrégats comportementaux vers des destinations Real-Time Customer Data Platform et utilisation dans Adobe Journey Optimizer
- Segmentation simplifiée des audiences avec stockage des agrégats comportementaux comme attributs de profil
- Normalisation des données comportementales de profil agrégées pour une utilisation sur plusieurs plateformes et applications
- Amélioration de la gestion des données avec la consolidation des données des anciens événements de profil en informations comportementales significatives

Ces agrégats sont calculés en fonction des jeux de données d’événements d’expérience activés pour Profile et ingérés dans Adobe Experience Platform. Chaque attribut calculé est un attribut de profil créé sur votre schéma d’union des profils et est regroupé sous le groupe de champs « SystemComputedAttribute » de votre schéma d’union.

Voici quelques exemples de cas d’utilisation :

- Personnalisation des e-mails marketing avec points de récompense totaux pour féliciter les utilisateurs et utilisatrices d’avoir été promus à un niveau Premium
- Personnaliser les communications destinées aux utilisateurs en fonction du nombre d’achats et de la fréquence
- Personnaliser les e-mails de rétention en fonction des dates d&#39;expiration de l&#39;abonnement
- Reciblage des utilisateurs qui ont consulté mais n’ont pas acheté un produit avec le dernier produit consulté
- Activation des agrégats d’événements par le biais d’attributs calculés vers un système en aval à l’aide de Real-Time CDP Destinations
- Réduction de plusieurs audiences basées sur un événement en un groupe plus condensé d’attributs calculés
- Reciblage des utilisateurs non authentifiés hors site à l’aide des identifiants de partenaire récents d’événements

Ce guide vous aidera à mieux comprendre le rôle des attributs calculés dans Experience Platform, en plus d’expliquer les principes de base des attributs calculés.

## Comprendre les attributs calculés

Adobe Experience Platform permet d’importer et de fusionner facilement des données provenant de plusieurs sources afin de générer des [!DNL Real-Time Customer Profiles]. Chaque profil contient des informations importantes liées à une personne, comme ses coordonnées de contact, ses préférences et son historique d’achat, vous offrant une vision à 360 degrés du client.

Certaines des informations collectées dans le profil sont facilement comprises lorsque vous lisez directement les champs de données (par exemple, « prénom ») tandis que d’autres données nécessitent la réalisation de plusieurs calculs ou comptent sur d’autres champs et d’autres valeurs afin de générer les informations (par exemple, « total d’achat depuis le début »). Pour faciliter la compréhension de ces données en un coup d’œil, [!DNL Experience Platform] vous permet de créer des attributs calculés qui effectuent automatiquement ces références et calculs, renvoyant la valeur dans le champ approprié.

Les attributs calculés incluent la création d’une expression, ou « règle », qui fonctionne sur les données entrantes et stocke la valeur obtenue dans un attribut de profil. Les expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de spécifier les événements sur lesquels effectuer l’agrégation, les fonctions d’agrégation ou les durées de recherche en amont.

### Fonctions

Les attributs calculés vous permettent de définir des agrégats d’événements en libre-service à l’aide de fonctions prédéfinies. Vous trouverez ci-dessous des informations détaillées sur ces fonctions :

| Fonction | Description | Types de données pris en charge | Exemple d’utilisation |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Une fonction qui **additionne** la valeur spécifiée pour les événements qualifiés. | Entiers, Nombres, Longs | Somme de tous les achats des 7 derniers jours |
| NOMBRE | Une fonction qui **compte** le nombre d’événements qui se sont produits pour la règle donnée. | S/O | Nombre d’achats au cours des 3 derniers mois |
| MIN | Une fonction qui trouve la valeur **minimum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Données de premier achat au cours des 7 derniers jours<br/>Montant minimum de la commande au cours des 4 dernières semaines |
| MAX | Une fonction qui trouve la valeur **maximum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Dernières données d’achat au cours des 7 derniers jours<br/>Montant maximal de la commande au cours des 4 dernières semaines |
| LAST_RECENT | Une fonction qui trouve la valeur d’attribut spécifiée à partir du dernier événement qualifié. Cette fonction fournit **à la fois** la valeur ainsi que l’horodatage de l’attribut . | Toutes les valeurs primitives, tableaux de valeurs primitives | Dernier produit consulté au cours des 7 derniers jours |

### Périodes de recherche en amont

Les attributs calculés sont calculés par lots, ce qui vous permet de conserver vos agrégats à jour et d’utiliser les derniers événements. Afin de prendre en charge ces scénarios avec un délai minimal, la fréquence d’actualisation varie en fonction de la période de recherche en amont de l’événement.

La période de recherche en amont fait référence à la durée passée en revue lors de l’agrégation des événements d’expérience pour l’attribut calculé. Cette période peut être définie en heures, jours, semaines ou mois.

La fréquence d’actualisation fait référence à la fréquence d’actualisation des attributs calculés. Cette valeur dépend de la période de recherche en amont et est automatiquement définie.

| Période de recherche en amont | Fréquence d’actualisation |
| --------------- | ----------------- |
| Jusqu’à 24 heures | Horaire |
| Jusqu’à 7 jours | Quotidien |
| Jusqu’à 4 semaines | Hebdomadaire |
| Jusqu’à 6 mois | Mensuel |

Par exemple, si votre attribut calculé comporte une période de recherche arrière des 7 derniers jours, cette valeur sera calculée en fonction des valeurs des 7 derniers jours, puis actualisée quotidiennement.

>[!NOTE]
>
>Les semaines et les mois sont considérés comme des **semaines calendaires** et des **mois calendaires** lorsqu&#39;ils sont utilisés dans des recherches en amont d&#39;événements. La semaine civile commence le **dimanche** et se termine le **samedi** de la semaine. Le mois calendaire commence le **premier** du mois et se termine le **dernier jour** du mois.

La période de recherche en amont des attributs calculés est une période de recherche en amont **variable**. Par exemple, si une première évaluation a lieu le 15 octobre à 12 h UTC, la période de recherche en amont de deux semaines récupère tous les événements du 1er au 15 octobre, s’actualise dans une semaine le 22 octobre, puis récupère tous les événements du 8 au 22 octobre.

**Actualisation rapide** {#fast-refresh}

Une actualisation rapide vous permet de garder vos attributs à jour. L’activation de cette option vous permet d’actualiser vos attributs calculés tous les jours, même pour des périodes de recherche en amont plus longues, ce qui vous permet de réagir rapidement aux activités des utilisateurs et utilisatrices.

>[!NOTE]
>
>L’activation de l’actualisation rapide fait varier les durées de recherche arrière de votre événement, car la période de recherche arrière est restaurée respectivement sur une base hebdomadaire ou mensuelle.
>
>Si vous créez un attribut calculé avec une période de recherche en amont de deux semaines avec l’actualisation rapide activée, cela signifie que la période de recherche en amont initiale sera de deux semaines. Cependant, à chaque actualisation quotidienne, la période de recherche en amont inclut les événements du jour supplémentaire. Cet ajout de jours se poursuit jusqu’au début de la semaine civile suivante, au cours de laquelle l’intervalle de recherche en amont se prolonge et revient à deux semaines.
>
>Par exemple, s’il existait une période de recherche en amont de deux semaines commençant le 15 mars (dimanche) avec l’actualisation rapide activée et l’actualisation quotidienne, la période de recherche en amont continuera à s’étendre inclusivement jusqu’au 22 mars, où elle sera réinitialisée à deux semaines. En résumé, l’attribut calculé est **actualisé** quotidiennement, la période de recherche en amont passant de **deux** semaines à **trois** semaines au cours de la semaine, puis revenant ensuite à **deux** semaines.

## Étapes suivantes

Pour en savoir plus sur la création et la gestion des attributs calculés, consultez le guide de l’API [computed attributes](./api.md) ou le guide de l’interface utilisateur [computed attributes](./ui.md).
