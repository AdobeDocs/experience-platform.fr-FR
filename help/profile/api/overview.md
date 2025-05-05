---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;Profil unifié;unifié;Profil;rtcp;activer le profil;Activer le profil
title: Guide de l’API Real-Time Customer Profile
description: L’API Real-Time Customer Profile permet aux développeurs d’explorer et d’utiliser les données de profil, notamment d’afficher les profils, de créer et de mettre à jour des politiques de fusion, d’exporter ou des exemples de données de profil et de supprimer les données de profil qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 19%

---

# Guide de l’API [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] vous permet d’obtenir une vue d’ensemble de chacun de vos clients dans Adobe Experience Platform. [!DNL Profile] vous permet de consolider des données client disparates issues de plusieurs canaux, tels que des données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L’API [!DNL Real-Time Customer Profile] comprend plusieurs points d’entrée, comme indiqué ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez le document Swagger [Real-Time Customer Profile API Reference](https://www.adobe.com/go/profile-apis-en).

Pour obtenir un guide sur l’utilisation des données de [!DNL Real-Time Customer Profile] dans l’interface utilisateur de [!DNL Experience Platform], reportez-vous au [guide d’utilisation de Profile](../ui/user-guide.md).

## Attributs calculés {#computed-attributes}

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées dans la segmentation, l’activation et la personnalisation.

Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être affichées dans un profil, utilisées pour créer une audience ou accessibles via plusieurs modèles d’accès différents.

Vous pouvez créer, afficher, modifier et supprimer des attributs calculés à l’aide du point d’entrée `ca/attributes/`. Pour savoir comment utiliser les attributs calculés, reportez-vous à la [présentation des attributs calculés](../computed-attributes/overview.md). Pour les opérations de l’API, consultez le [guide des points d’entrée de l’API des attributs calculés](../computed-attributes/api.md).

## Entités (accès au [!DNL Profile]) {#entities}

Adobe Experience Platform vous permet d’accéder aux données [!DNL Real-Time Customer Profile] à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées « profils », à l’aide de l’API, suivez les étapes décrites dans le guide [Guide des points d’entrée d’entités](entities.md). Pour accéder aux profils à l’aide de l’interface utilisateur de [!DNL Experience Platform], reportez-vous au guide d’utilisation [Profile](../ui/user-guide.md).

## Tâches d’exportation (exportation de [!DNL Profile]) {#profile-export}

[!DNL Real-Time Customer Profile] données peuvent être exportées vers un jeu de données pour un traitement ultérieur, comme l&#39;exportation d&#39;audiences pour l&#39;activation ou d&#39;attributs de profil pour la création de rapports. Les tâches d’exportation des audiences font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Pour en savoir plus, consultez le guide [guide des points d’entrée des tâches d’exportation de segmentation](../../profile/api/export-jobs.md). Pour obtenir des instructions détaillées sur la création et la gestion des tâches d’exportation pour les attributs de profil, consultez le guide [point d’entrée des tâches d’exportation](export-jobs.md).

## Politiques de fusion {#merge-policies}

Lorsque des données provenant de plusieurs sources sont rassemblées dans [!DNL Experience Platform], les politiques de fusion sont les règles utilisées par [!DNL Experience Platform] pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer des profils clients individuels. Grâce à l’API [!DNL Real-Time Customer Profile], vous pouvez créer des politiques de fusion, gérer des politiques existantes et définir une politique de fusion par défaut pour votre organisation. Pour utiliser des politiques de fusion à l’aide de l’API, consultez le [guide des points d’entrée des politiques de fusion](merge-policies.md).

Pour en savoir plus sur les politiques de fusion et leur rôle dans Experience Platform, commencez par lire la [présentation des politiques de fusion](../merge-policies/overview.md).

## Prévisualisation des exemples de statut (prévisualisation du [!DNL Profile]) {#profile-preview}

Lorsque les données sont ingérées dans Experience Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données du profil client en temps réel. Les résultats de cet exemple de tâche peuvent être affichés à l’aide du point d’entrée `/previewsamplestatus`, qui fait partie de l’API Real-Time Customer Profile. Ce point d’entrée peut également être utilisé pour répertorier les distributions de profils à la fois par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de bénéficier d’une meilleure visibilité sur la composition de la banque de profils de votre organisation.  Pour commencer à utiliser le point d’entrée `/profilepreviewstatus`, consultez le guide [prévisualisation d’un exemple de point d’entrée de statut](preview-sample-status.md).

## Tâches de système Profile {#profile-system-jobs}

Les données activées pour le profil et ingérées dans [!DNL Experience Platform] sont stockées dans le [!DNL Data Lake] ainsi que dans la banque de données [!DNL Real-Time Customer Profile]. Il peut parfois être nécessaire de supprimer les données de profil associées à un jeu de données de la banque de profils afin de supprimer des données qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API pour créer un [!DNL Profile System Job], également appelé « [!DNL delete request] », qui peut être modifié, surveillé ou supprimé si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l’aide du point d’entrée `/system/jobs` de l’API [!DNL Real-Time Customer Profile], suivez les étapes décrites dans le guide [Guide du point d’entrée des tâches système de profil](profile-system-jobs.md).

## Mettre à jour les attributs de profil {#update-profile}

Il peut parfois être nécessaire de mettre à jour les données du magasin de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../../catalog/datasets/enable-upsert.md).

## Étapes suivantes {#next-steps}

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Real-Time Customer Profile], lisez le guide de prise en main [&#128279;](getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques liés à l’[!DNL Profile]. Pour utiliser les données [!DNL Profile] à l’aide de l’interface utilisateur de [!DNL Experience Platform], reportez-vous au [guide d’utilisation du profil client en temps réel](../ui/user-guide.md).
