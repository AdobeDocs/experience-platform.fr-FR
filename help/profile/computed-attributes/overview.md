---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Présentation des attributs calculés
topic: guide
type: Documentation
description: Les attributs calculés sont des fonctions permettant d'agrégat des données au niveau du événement dans des attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 41%

---


# (Alpha) Présentation des attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé est actuellement en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être visualisées dans un profil, utilisées pour créer un segment ou accessibles via plusieurs modèles d’accès différents.

Ce guide vous aidera à mieux comprendre le rôle des attributs calculés dans Adobe Experience Platform.

## Comprendre les attributs calculés

Adobe Experience Platform vous permet d&#39;importer et de fusionner facilement des données provenant de plusieurs sources afin de générer [!DNL Real-time Customer Profiles]. Chaque profil contient des informations importantes liées à une personne, comme ses coordonnées de contact, ses préférences et son historique d’achat, vous offrant une vision à 360 degrés du client.

Certaines des informations collectées dans le profil sont facilement comprises lorsque vous lisez directement les champs de données (par exemple, « prénom ») tandis que d’autres données nécessitent la réalisation de plusieurs calculs ou comptent sur d’autres champs et d’autres valeurs afin de générer les informations (par exemple, « total d’achat depuis le début »). Pour faciliter la compréhension de ces données en un coup d&#39;oeil, [!DNL Platform] vous permet de créer des attributs calculés qui effectuent automatiquement ces références et calculs, renvoyant la valeur dans le champ approprié.

Les attributs calculés incluent la création d’une expression, ou &quot;règle&quot;, qui opère sur les données entrantes et stocke la valeur résultante dans un attribut de profil. Les expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de préciser qu’une règle n’évalue que les événements entrants, un événement entrant et les données du profil ou un événement entrant, les données du profil et les événements historiques.

### Cas d’utilisation

Les cas d’utilisation des attributs calculés peuvent aller de calculs simples à des références très complexes. Voici quelques exemples de cas d’utilisation des attributs calculés :

1. **[!UICONTROL Pourcentages] :** Un attribut calculé simple peut inclure la prise de deux champs numériques sur un enregistrement et leur division pour créer un pourcentage. Par exemple, vous pouvez prendre le nombre total d’e-mails envoyés à un destinataire et le diviser par le nombre d’e-mails que ce destinataire a ouvert. Un simple coup d’œil au champ attribut calculé obtenu donnerait rapidement le pourcentage total d’e-mails ouvert par ce destinataire.
1. **[!UICONTROL Utilisation] de l’application :** un autre exemple inclut la possibilité d’agrégat du nombre d’ouvertures de l’application par un utilisateur. En suivant le nombre total d’ouvertures de l’application, en fonction des événements d’ouverture individuels, vous pourriez diffuser des offres spéciales ou des messages aux utilisateurs à leur centième ouverture pour encourager un engagement plus approfondi avec votre marque.
1. **[!UICONTROL Valeurs] de durée de vie : il peut s’avérer très difficile de** rassembler des totaux d’exécution, tels qu’une valeur d’achat sur toute la durée de vie d’un client. Cela nécessite la mise à jour de l’historique total chaque fois qu’un nouvel événement d’achat se produit. Un attribut calculé vous permet de faire ceci beaucoup plus facilement en conservant la valeur de durée de vie dans un champ unique qui est mis à jour automatiquement à chaque événement d’achat réussi associé au client.

## Limites connues

### Disponibilité différée de nouveaux attributs calculés

La disponibilité de nouveaux attributs calculés peut être retardée jusqu&#39;à 2 heures après l&#39;ajout de l&#39;attribut de schéma correspondant au schéma d&#39;union.

Ce retard est dû à la configuration de mise en cache actuelle. Après Alpha, la fréquence d&#39;actualisation du cache pourrait être augmentée.

### Suivi des dépendances dans les segments

Les attributs de schéma qui ont déjà été utilisés dans une expression de définition de segment, mais qui ont été ultérieurement transformés en attribut calculé, ne seront pas suivis en tant que dépendance de ce segment.

En raison du fait qu’aucune dépendance n’a été détectée, l’Experience Platform n’évaluera pas automatiquement l’attribut calculé associé chaque fois que la définition de segment est évaluée.

Vous pouvez également gérer la création d’attributs calculés au moyen d’un mixin spécifique qui ajoute de nouveaux attributs calculés qui ne sont pas en conflit avec les attributs existants. Une autre solution consiste à simplement recréer le segment avec le suivi des dépendances correct pour les nouveaux attributs calculés.