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

[!DNL Real-Time Customer Profile] vous permet d’obtenir une vue d’ensemble de chacun de vos clients dans Adobe Experience Platform. [!DNL Profile] permet de consolider des données clients disparates provenant de plusieurs canaux, tels que des données en ligne, hors ligne, CRM et tierces, dans une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

La variable [!DNL Real-Time Customer Profile] L’API comprend plusieurs points de terminaison, décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [Échange de référence de l’API Real-Time Customer Profile](https://www.adobe.com/go/profile-apis-en).

Pour obtenir un guide sur l’utilisation de [!DNL Real-Time Customer Profile] des données de la variable [!DNL Experience Platform] Interface utilisateur, reportez-vous à la section [Guide d’utilisation de Profile](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative} Attributs calculés {#computed-attributes}

>[!IMPORTANT]
>
La fonctionnalité d’attribut calculé est en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être visualisées dans un profil, utilisées pour créer une audience ou accessibles via plusieurs modèles d’accès différents.

Vous pouvez créer, afficher, modifier et supprimer des attributs calculés à l’aide du `ca/attributes/` point de terminaison . Pour savoir comment utiliser des attributs calculés, reportez-vous à la section [présentation des attributs calculés](../computed-attributes/overview.md). Pour les opérations d’API, consultez la page [guide de point d’entrée de l’API des attributs calculés](../computed-attributes/api.md).

## Entités (accès au [!DNL Profile]) {#entities}

Grâce à Adobe Experience Platform, vous pouvez accéder à [!DNL Real-Time Customer Profile] données à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l’aide de l’API, suivez les étapes décrites dans la section [guide de point d’entrée des entités](entities.md). Pour accéder aux profils à l’aide de la fonction [!DNL Platform] IU, voir [Guide d’utilisation de Profile](../ui/user-guide.md).

## Tâches d’exportation (exportation de [!DNL Profile]) {#profile-export}

[!DNL Real-Time Customer Profile] les données peuvent être exportées vers un jeu de données pour un traitement ultérieur, par exemple pour exporter des audiences en vue de l’activation ou des attributs de profil pour la création de rapports. Les tâches d’exportation pour les audiences font partie du [!DNL Adobe Experience Platform Segmentation Service] API, veuillez lire la [guide d’entrée des tâches d’exportation de segmentation](../../profile/api/export-jobs.md) pour en savoir plus. Pour obtenir des instructions détaillées sur la création et la gestion de tâches d’exportation pour les attributs de profil, consultez la section [guide de point de fin des traitements d’export](export-jobs.md).

## Politiques de fusion {#merge-policies}

Lorsque vous rassemblez des données provenant de plusieurs sources dans [!DNL Experience Platform], les stratégies de fusion sont les règles qui [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées afin de créer des profils client individuels. En utilisant la variable [!DNL Real-Time Customer Profile] API, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation. Pour utiliser des stratégies de fusion à l’aide de l’API, consultez la page [guide de point de terminaison des stratégies de fusion](merge-policies.md).

Pour en savoir plus sur les stratégies de fusion et leur rôle dans Platform, veuillez commencer par lire la section [présentation des stratégies de fusion](../merge-policies/overview.md).

## Prévisualisation des exemples de statut (prévisualisation du [!DNL Profile]) {#profile-preview}

Lorsque des données sont ingérées dans Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données de Real-Time Customer Profile. Les résultats de cet exemple de tâche peuvent être affichés à l’aide de la fonction `/previewsamplestatus` point de terminaison, qui fait partie de l’API Real-time Customer Profile. Ce point de terminaison peut également être utilisé pour répertorier les distributions de profil par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de mieux comprendre la composition de la banque de profils de votre entreprise.  Pour commencer à utiliser la méthode `/profilepreviewstatus` point de fin, voir [prévisualisation d’un exemple de guide de point de terminaison d’état](preview-sample-status.md).

## Tâches de système Profile {#profile-system-jobs}

Données activées pour les profils ingérées dans [!DNL Platform] est stocké dans la variable [!DNL Data Lake] ainsi que la variable [!DNL Real-Time Customer Profile] entrepôt de données. Il peut parfois être nécessaire de supprimer de la banque de données Profile les données de profil associées à un jeu de données afin de supprimer les données devenues inutiles ou ajoutées par erreur. Cela nécessite l’utilisation de l’API pour créer une [!DNL Profile System Job], également appelé &quot;[!DNL delete request]&quot;, qui peut être modifié, surveillé ou supprimé si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l’aide de la méthode `/system/jobs` du point de terminaison [!DNL Real-Time Customer Profile] API, suivez les étapes décrites dans la section [guide de point d’entrée des tâches du système de profil](profile-system-jobs.md).

## Mise à jour des attributs de profil {#update-profile}

Il peut parfois être nécessaire de mettre à jour les données dans la banque de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../../catalog/datasets/enable-upsert.md).

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l’aide de la variable [!DNL Real-Time Customer Profile] API, lisez la [guide de prise en main](getting-started.md) sélectionnez ensuite l’un des guides de point de terminaison pour savoir comment utiliser des [!DNL Profile]Points de terminaison liés. Pour utiliser [!DNL Profile] à l’aide de la variable [!DNL Experience Platform] Interface utilisateur, reportez-vous à la section [Guide d’utilisation de Real-Time Customer Profile](../ui/user-guide.md).
