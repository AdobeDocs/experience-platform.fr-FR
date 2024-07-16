---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;profil unifié;unifié;profil;unifié;profil;rtcp;activer le profil;activer le profil
title: Guide de l’API Real-Time Customer Profile
description: L’API Real-time Customer Profile permet aux développeurs d’explorer et d’utiliser les données de profil, notamment d’afficher les profils, de créer et de mettre à jour des stratégies de fusion, d’exporter ou d’échantillonner des données de profil, ainsi que de supprimer les données de profil qui ne sont plus requises ou qui ont été ajoutées par erreur. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 19%

---

# Guide de l’API [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] vous permet d’obtenir une vue d’ensemble de chaque client dans Adobe Experience Platform. [!DNL Profile] vous permet de consolider des données client disparates provenant de plusieurs canaux, tels que des données en ligne, hors ligne, CRM et tierces, dans une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L’API [!DNL Real-Time Customer Profile] comprend plusieurs points de terminaison, décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez le [swagger de référence de l’API Real-Time Customer Profile](https://www.adobe.com/go/profile-apis-en).

Pour obtenir un guide sur l’utilisation des données [!DNL Real-Time Customer Profile] dans l’interface utilisateur de [!DNL Experience Platform], reportez-vous au [guide d’utilisation du profil](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative} Attributs calculés {#computed-attributes}

>[!IMPORTANT]
>
La fonctionnalité d’attribut calculé est en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être visualisées dans un profil, utilisées pour créer une audience ou accessibles via plusieurs modèles d’accès différents.

Vous pouvez créer, afficher, modifier et supprimer des attributs calculés à l’aide du point d’entrée `ca/attributes/`. Pour savoir comment utiliser les attributs calculés, reportez-vous à la [présentation des attributs calculés](../computed-attributes/overview.md). Pour les opérations d’API, consultez le [guide de point d’entrée de l’API des attributs calculés](../computed-attributes/api.md).

## Entités (accès au [!DNL Profile]) {#entities}

Grâce à Adobe Experience Platform, vous pouvez accéder aux données [!DNL Real-Time Customer Profile] à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l’aide de l’API, suivez les étapes décrites dans le [guide des points de terminaison d’entités](entities.md). Pour accéder aux profils à l’aide de l’interface utilisateur de [!DNL Platform], reportez-vous au [guide d’utilisation du profil](../ui/user-guide.md).

## Tâches d’exportation (exportation de [!DNL Profile]) {#profile-export}

Les données [!DNL Real-Time Customer Profile] peuvent être exportées vers un jeu de données pour un traitement ultérieur, comme l’exportation d’audiences pour activation ou d’attributs de profil pour la création de rapports. Les tâches d’exportation pour les audiences font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Pour en savoir plus, consultez le [guide de point de terminaison des tâches d’exportation de segmentation](../../profile/api/export-jobs.md). Pour obtenir des instructions détaillées sur la création et la gestion des tâches d’exportation pour les attributs de profil, consultez le [guide de point de terminaison des tâches d’exportation](export-jobs.md).

## Politiques de fusion {#merge-policies}

Lorsque vous rassemblez des données provenant de plusieurs sources dans [!DNL Experience Platform], les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer des profils client individuels. À l’aide de l’API [!DNL Real-Time Customer Profile], vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation. Pour utiliser des stratégies de fusion à l’aide de l’API, consultez le [guide de point de terminaison des stratégies de fusion](merge-policies.md).

Pour en savoir plus sur les stratégies de fusion et leur rôle dans Platform, commencez par lire la [présentation des stratégies de fusion](../merge-policies/overview.md).

## Prévisualisation des exemples de statut (prévisualisation du [!DNL Profile]) {#profile-preview}

Lorsque des données sont ingérées dans Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données de Real-Time Customer Profile. Les résultats de cet exemple de tâche peuvent être visualisés à l’aide du point de terminaison `/previewsamplestatus`, qui fait partie de l’API Real-time Customer Profile. Ce point de terminaison peut également être utilisé pour répertorier les distributions de profil par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de mieux comprendre la composition de la banque de profils de votre entreprise.  Pour commencer à utiliser le point d’entrée `/profilepreviewstatus`, reportez-vous au [guide d’aperçu de point d’entrée d’état](preview-sample-status.md).

## Tâches de système Profile {#profile-system-jobs}

Les données activées pour le profil qui sont ingérées dans [!DNL Platform] sont stockées dans [!DNL Data Lake] ainsi que dans l’entrepôt de données [!DNL Real-Time Customer Profile]. Il peut parfois être nécessaire de supprimer de la banque de données Profile les données de profil associées à un jeu de données afin de supprimer les données devenues inutiles ou ajoutées par erreur. Cela nécessite l’utilisation de l’API pour créer un [!DNL Profile System Job], également appelé &quot;[!DNL delete request]&quot;, qui peut être modifié, surveillé ou supprimé si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l’aide du point de terminaison `/system/jobs` de l’API [!DNL Real-Time Customer Profile], suivez les étapes décrites dans le [guide de point de terminaison des tâches du système de profil](profile-system-jobs.md).

## Mise à jour des attributs de profil {#update-profile}

Il peut parfois être nécessaire de mettre à jour les données dans la banque de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../../catalog/datasets/enable-upsert.md).

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l’aide de l’API [!DNL Real-Time Customer Profile], lisez le [guide de prise en main](getting-started.md) , puis sélectionnez l’un des guides de point de terminaison pour savoir comment utiliser des points de terminaison spécifiques [!DNL Profile]. Pour utiliser les données [!DNL Profile] à l’aide de l’interface utilisateur [!DNL Experience Platform], reportez-vous au [guide d’utilisation de Real-Time Customer Profile](../ui/user-guide.md).
