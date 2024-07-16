---
title: Présentation des attributs calculés
description: Les attributs calculés sont des fonctions permettant d’agréger des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 03f1dfab768e98ef4959d605cc3ead25bb5eb238
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 8%

---

# Présentation des attributs calculés

Personalization basé sur le comportement des utilisateurs est une exigence clé pour les marketeurs afin d’optimiser l’impact de la personnalisation. Par exemple, personnaliser l’e-mail marketing avec le produit récemment consulté pour générer des conversions ou personnaliser la page web en fonction du total des achats effectués par les utilisateurs pour accroître la rétention.

Les attributs calculés permettent de convertir rapidement les données comportementales de profil en valeurs agrégées au niveau du profil sans dépendre des ressources d’ingénierie pour :

- Activation de la personnalisation individuelle ou par lots ciblée avec l’activation d’agrégats comportementaux vers les destinations et l’utilisation de Real-Time Customer Data Platform dans Adobe Journey Optimizer
- Segmentation d’audience simplifiée avec stockage d’agrégats comportementaux en tant qu’attributs de profil
- Normalisation des données comportementales de profil agrégées pour une utilisation sur plusieurs plateformes et applications
- Amélioration de la gestion des données avec la consolidation des anciennes données d’événements de profil dans des informations comportementales significatives

Ces agrégats sont calculés en fonction des jeux de données d’événements d’expérience activés pour le profil ingérés dans Adobe Experience Platform. Chaque attribut calculé est un attribut de profil créé sur votre schéma d’union de profil et est regroupé sous le groupe de champs &quot;SystemComputedAttribute&quot; dans votre schéma d’union.

Voici des exemples de cas d’utilisation :

- Personnaliser des emails marketing avec un total de points de récompense pour féliciter les utilisateurs d&#39;avoir été promus à un niveau Premium
- Personnaliser les communications avec les utilisateurs en fonction du nombre et de la fréquence des achats
- Personnaliser les emails de rétention en fonction des dates d&#39;expiration d&#39;abonnement
- Reciblage des utilisateurs qui ont consulté mais n’ont pas acheté un produit avec le dernier produit consulté
- Activation d’agrégats d’événements à l’aide d’attributs calculés sur un système en aval à l’aide des destinations Real-Time CDP
- Réduction de plusieurs audiences basées sur des événements en un groupe plus condensé d’attributs calculés
- Reciblage hors site des utilisateurs non authentifiés à l’aide d’identifiants de partenaire récents provenant d’événements

Ce guide vous aidera à mieux comprendre le rôle des attributs calculés dans Platform, en plus d’expliquer les bases des attributs calculés.

## Comprendre les attributs calculés

Adobe Experience Platform vous permet d’importer et de fusionner facilement des données provenant de plusieurs sources afin de générer [!DNL Real-Time Customer Profiles]. Chaque profil contient des informations importantes liées à une personne, comme ses coordonnées de contact, ses préférences et son historique d’achat, vous offrant une vision à 360 degrés du client.

Certaines des informations collectées dans le profil sont facilement comprises lorsque vous lisez directement les champs de données (par exemple, « prénom ») tandis que d’autres données nécessitent la réalisation de plusieurs calculs ou comptent sur d’autres champs et d’autres valeurs afin de générer les informations (par exemple, « total d’achat depuis le début »). Pour faciliter la compréhension de ces données en un coup d’oeil, [!DNL Platform] vous permet de créer des attributs calculés qui exécutent automatiquement ces références et calculs, renvoyant la valeur dans le champ approprié.

Les attributs calculés incluent la création d’une expression, ou &quot;règle&quot;, qui fonctionne sur les données entrantes et stocke la valeur obtenue dans un attribut de profil. Les expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de spécifier les événements sur lesquels vous souhaitez effectuer une agrégation, les fonctions d’agrégat ou les durées de recherche en amont.

### Fonctions

Les attributs calculés vous permettent de définir des agrégats d’événements en libre-service à l’aide de fonctions prédéfinies. Vous trouverez ci-dessous des informations détaillées sur ces fonctions :

| Fonction | Description | Types de données pris en charge | Exemple d’utilisation |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Fonction qui **additionne** la valeur spécifiée pour les événements qualifiés. | Entiers, nombres, Longs | Somme de tous les achats des 7 derniers jours |
| NOMBRE | Une fonction qui **comptabilise** le nombre d’événements qui se sont produits pour la règle donnée. | S/O | Nombre d&#39;achats au cours des 3 derniers mois |
| MIN | Une fonction qui recherche la valeur **minimum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Premières données d’achat au cours des 7 derniers jours<br/>Montant minimum de la commande au cours des 4 dernières semaines |
| MAX | Une fonction qui recherche la valeur **maximum** pour les événements qualifiés. | Entiers, Nombres, Longs, Horodatages | Données du dernier achat au cours des 7 derniers jours<br/>Montant maximum de la commande au cours des 4 dernières semaines |
| MOST_RECENT | Une fonction qui recherche la valeur d’attribut spécifiée à partir du dernier événement qualifié. Cette fonction attribue à **la fois** la valeur ainsi que l’horodatage de l’attribut. | Toutes les valeurs primitives, tableaux de valeurs primitives | Dernier produit consulté au cours des 7 derniers jours |

### Périodes de recherche en amont

Les attributs calculés sont calculés par lots, ce qui vous permet de garder vos agrégats à jour et d’utiliser les derniers événements. Afin de prendre en charge ces scénarios avec un délai minimal, la fréquence d’actualisation varie en fonction de la période de recherche en amont des événements.

La période de recherche arrière fait référence à la durée passée en revue lors de l’agrégation des événements d’expérience pour l’attribut calculé. Cette période peut être définie en heures, jours, semaines ou mois.

La fréquence d’actualisation fait référence à la fréquence d’actualisation des attributs calculés. Cette valeur dépend de la période de recherche arrière et est automatiquement définie.

| Période de recherche en amont | Actualiser la fréquence |
| --------------- | ----------------- |
| Jusqu’à 24 heures | Horaire |
| Jusqu’à 7 jours | Quotidien |
| Jusqu’à 4 semaines | Hebdomadaire |
| Jusqu’à 6 mois | Mensuel |

Par exemple, si votre attribut calculé a une période de recherche arrière des 7 derniers jours, cette valeur sera calculée en fonction des valeurs des 7 derniers jours, puis actualisée quotidiennement.

>[!NOTE]
>
>Les semaines et les mois sont considérés comme des **semaines calendaires** et des **mois calendaires** lorsqu&#39;ils sont utilisés dans les recherches en amont des événements. La semaine calendaire commence le **dimanche** et se termine le **samedi** de la semaine. Le mois calendaire commence le **premier** du mois et se termine le **dernier jour** du mois.

La période de recherche en amont pour les attributs calculés est une période de recherche en amont ****. Par exemple, si une première évaluation a lieu le 15 octobre à 12h00 UTC, une période de recherche arrière de deux semaines récupère tous les événements du 1er au 15 octobre, les actualise dans une semaine à partir du 22 octobre, puis récupère tous les événements du 8 au 22 octobre.

**Actualisation rapide** {#fast-refresh}

Une actualisation rapide vous permet de garder vos attributs à jour. L’activation de cette option vous permet d’actualiser quotidiennement vos attributs calculés, même pour des périodes de recherche en amont plus longues, ce qui vous permet de réagir rapidement aux activités de l’utilisateur.

>[!NOTE]
>
>L’activation d’une actualisation rapide varie les durées de recherche en amont de vos événements, puisque la période de recherche en amont s’étend respectivement sur une base hebdomadaire ou mensuelle.
>
>Si vous créez un attribut calculé avec une période de recherche en amont de deux semaines avec l’actualisation rapide activée, cela signifie que la période de recherche en amont initiale sera de deux semaines. Toutefois, à chaque actualisation quotidienne, la période de recherche arrière inclut les événements du jour supplémentaire. Cet ajout de jours se poursuit jusqu’au début de la semaine calendaire suivante, au cours de laquelle l’intervalle de recherche en amont s’affiche et revient à deux semaines.
>
>Par exemple, si une période de recherche arrière de deux semaines a commencé le 15 mars (dimanche) avec l’actualisation rapide activée, avec actualisation quotidienne activée, la période de recherche arrière continuera à s’étendre de manière inclusive jusqu’au 22 mars, où elle reprendra deux semaines. En résumé, l’attribut calculé est **actualisé** tous les jours, la période de recherche arrière passant de **deux** semaines à **trois** semaines pendant la semaine, puis revient ensuite à **deux** semaines.

## Étapes suivantes

Pour en savoir plus sur la création et la gestion des attributs calculés, consultez le [guide de l’API des attributs calculés](./api.md) ou le [ guide de l’interface utilisateur des attributs calculés](./ui.md).
