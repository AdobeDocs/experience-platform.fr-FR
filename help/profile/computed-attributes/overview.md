---
title: Présentation des attributs calculés
description: Les attributs calculés sont des fonctions permettant d’agréger des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation.
badge: « Version bêta »
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 11%

---

# Présentation des attributs calculés

>[!IMPORTANT]
>
>Les attributs calculés se trouvent actuellement dans **bêta** et est **not** disponible pour tous les utilisateurs.

La personnalisation basée sur le comportement des utilisateurs est une exigence clé pour les marketeurs afin d’optimiser l’impact de la personnalisation. Par exemple, personnaliser l’e-mail marketing avec le produit récemment consulté pour générer des conversions ou personnaliser la page web en fonction du total des achats effectués par les utilisateurs pour accroître la rétention.

Les attributs calculés permettent de convertir rapidement les données comportementales de profil en valeurs agrégées au niveau du profil sans dépendre des ressources d’ingénierie pour :

- Activation de la personnalisation ciblée avec l’activation d’agrégats comportementaux vers des destinations Real-time Customer Data Platform, l’utilisation dans Adobe Journey Optimizer ou la segmentation
- Normalisation des données comportementales de profil agrégées pour une utilisation sur plusieurs plateformes et applications
- Amélioration de la gestion des données avec la consolidation des anciennes données d’événements de profil dans des informations comportementales significatives

Ces agrégats sont calculés en fonction des jeux de données d’événements d’expérience activés pour le profil ingérés dans Adobe Experience Platform. Chaque attribut calculé est un attribut de profil créé sur votre schéma d’union de profil et est regroupé sous le groupe de champs &quot;Attribut calculé&quot; dans votre schéma d’union.

Parmi les exemples d’utilisation, citons la personnalisation des publicités avec le nom du dernier produit consulté pour les personnes n’ayant effectué aucun achat au cours des 7 derniers jours, la personnalisation des emails marketing avec le total des points de récompense pour féliciter les utilisateurs d’avoir été promus à un niveau de prime ou le calcul de la valeur de durée de vie de chaque client afin d’optimiser le ciblage.

Ce guide vous aidera à mieux comprendre le rôle des attributs calculés dans Platform, en plus d’expliquer les bases des attributs calculés.

## Comprendre les attributs calculés

Adobe Experience Platform vous permet d’importer et de fusionner facilement des données provenant de plusieurs sources afin de générer des [!DNL Real-Time Customer Profiles]. Chaque profil contient des informations importantes liées à une personne, comme ses coordonnées de contact, ses préférences et son historique d’achat, vous offrant une vision à 360 degrés du client.

Certaines des informations collectées dans le profil sont facilement comprises lorsque vous lisez directement les champs de données (par exemple, « prénom ») tandis que d’autres données nécessitent la réalisation de plusieurs calculs ou comptent sur d’autres champs et d’autres valeurs afin de générer les informations (par exemple, « total d’achat depuis le début »). Pour faciliter la compréhension de ces données en un coup d’oeil, [!DNL Platform] permet de créer des attributs calculés qui effectuent automatiquement ces références et calculs, en renvoyant la valeur dans le champ approprié.

Les attributs calculés incluent la création d’une expression, ou &quot;règle&quot;, qui fonctionne sur les données entrantes et stocke la valeur obtenue dans un attribut de profil. Les expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de spécifier les événements sur lesquels vous souhaitez effectuer une agrégation, les fonctions d’agrégat ou les durées de recherche en amont.

### Fonctions

Les attributs calculés vous permettent de définir des agrégats d’événements en libre-service à l’aide de fonctions prédéfinies. Vous trouverez ci-dessous des informations détaillées sur ces fonctions :

| Fonction | Description | Types de données pris en charge | Exemple d’utilisation |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Une fonction qui **sum** augmenter la valeur spécifiée pour les événements qualifiés. | Entiers, nombres, Longs | Somme de tous les achats des 7 derniers jours |
| COUNT | Une fonction qui **count** le nombre d’événements qui se sont produits pour la règle donnée. | S/O | Nombre d&#39;achats au cours des 3 derniers mois |
| MIN | Une fonction qui recherche la variable **minimum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Premières données d’achat au cours des 7 derniers jours<br/>Montant minimum de la commande dans les 4 dernières semaines |
| MAX | Une fonction qui recherche la variable **maximum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Données du dernier achat au cours des 7 derniers jours<br/>Montant maximum de la commande dans les 4 dernières semaines |
| MOST_RECENT | Une fonction qui recherche la valeur d’attribut spécifiée à partir du dernier événement qualifié. | Toutes les valeurs primitives, tableaux de valeurs primitives | Dernier produit consulté au cours des 7 derniers jours |

### Périodes de recherche en amont

Les attributs calculés sont calculés par lots, ce qui vous permet de garder vos agrégats à jour et d’utiliser les derniers événements. Pour prendre en charge ces scénarios en temps quasi réel, la fréquence d’actualisation varie en fonction de la période de recherche en amont des événements.

La période de recherche arrière fait référence à la durée passée en revue lors de l’agrégation des événements d’expérience pour l’attribut calculé. Cette période peut être définie en heures, jours, semaines ou mois.

La fréquence d’actualisation fait référence à la fréquence d’actualisation des attributs calculés. Cette valeur dépend de la période de recherche arrière et est automatiquement définie.

| Période de recherche en amont | Fréquence d’actualisation |
| --------------- | ----------------- |
| Jusqu’à 24 heures | Toutes les heures |
| Jusqu’à 7 jours | Quotidien |
| Jusqu’à 4 semaines | Hebdomadaire |
| Jusqu’à 6 mois | Mensuel |

Par exemple, si votre attribut calculé a une période de recherche arrière des 7 derniers jours, cette valeur sera calculée en fonction des valeurs des 7 derniers jours, puis actualisée quotidiennement.

>[!NOTE]
>
>Les semaines et les mois sont considérés comme **semaines calendaires** et **mois calendaires** lorsqu’elle est utilisée dans les recherches en amont d’événements.

**Actualisation rapide**

>[!IMPORTANT]
>
>Un maximum de **cinq** Par environnement de test, les attributs peuvent avoir une actualisation rapide activée.

Une actualisation rapide vous permet de garder vos attributs à jour. L’activation de cette option vous permet d’actualiser quotidiennement vos attributs calculés, même pour des périodes de recherche en amont plus longues. Vous pouvez ainsi réagir en temps quasi réel aux activités des utilisateurs. Cette valeur s’applique uniquement aux attributs calculés avec une période de recherche arrière supérieure à une base hebdomadaire.

>[!NOTE]
>
>L’activation d’une actualisation rapide varie les durées de recherche en amont de vos événements, puisque la période de recherche en amont s’étend respectivement sur une base hebdomadaire ou mensuelle.
>
>Par exemple, si vous créez un attribut calculé avec une période de recherche en amont de deux semaines avec l’actualisation rapide activée, cela signifie que la période de recherche en amont initiale sera de deux semaines. Toutefois, à chaque actualisation quotidienne, la période de recherche arrière inclut les événements du jour supplémentaire. Cet ajout de jours se poursuit jusqu’au début de la semaine calendaire suivante, au cours de laquelle l’intervalle de recherche en amont s’affiche et revient à deux semaines.

## Étapes suivantes

Pour en savoir plus sur la création et la gestion des attributs calculés, veuillez lire le [guide de l’API des attributs calculés](./api.md) ou le [guide de l’interface utilisateur des attributs calculés](./ui.md).
