---
title: Suppressions dans le service d’identités
description: Ce document présente les différents mécanismes que vous pouvez utiliser pour supprimer vos données d’identité dans Experience Platform et explique clairement comment les graphiques d’identités peuvent être affectés.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 91%

---

# Suppressions dans le service d’identités

Adobe Experience Platform Identity Service génère des graphiques d’identités en liant de manière déterministe les identités entre les appareils et les systèmes pour une personne individuelle. Les liens des graphiques d’identités sont établis lorsque plusieurs identités marquées sont reçues au sein de la même ligne de données.

Les graphiques d’identités sont utilisés par Real-time Customer Profile pour créer une vue d’ensemble exhaustive et unique de vos attributs et comportements client, ce qui vous permet de fournir des expériences digitales personnelles et percutantes en temps réel, aux personnes et non aux appareils.

Ce document présente les différents mécanismes que vous pouvez utiliser pour supprimer vos données d’identité dans Experience Platform et explique clairement comment les graphiques d’identités peuvent être affectés.

## Prise en main

Le document ci-dessous fait référence aux fonctions suivantes d’Experience Platform :

* [Service d’identités](../home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en reliant les identités entre les appareils et les systèmes.
   * [Graphique d’identités](./identity-graph-viewer.md) : Un graphique d’identités est une carte des relations entre différentes identités pour un client spécifique. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux.
   * [Espaces de noms d’identité](./namespaces.md) : Les espaces de noms d’identité sont des composants du service d’identités qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur de « name<span>@email.com » comme adresse e-mail ou « 443522 » comme CRMID numérique.
* [Service de catalogue](../../catalog/home.md) : découvrez le traçabilité des données, les métadonnées, les descriptions de fichiers, les répertoires et les jeux de données dans le lac de données.
* [Hygiène des données](../../hygiene/home.md) : gérez vos données client stockées en planifiant des expirations de jeux de données automatisées ou en supprimant des enregistrements individuels d’un jeu de données ou de tous les jeux de données.
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) : gère les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente ou les effacer dans différentes applications Adobe Experience Cloud.
* [Real-Time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Suppressions d’identité unique

Les demandes de suppression d’identité unique vous permettent de supprimer une identité dans un graphique, ce qui entraîne la suppression des liens liés à une seule identité utilisateur associée à un espace de noms d’identité. Vous pouvez utiliser les mécanismes fournis par [Privacy Service](../../privacy-service/home.md) pour des cas d’utilisation tels que les demandes de suppression de données de la part des clients et la conformité aux réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD).

Les sections ci-dessous décrivent les mécanismes que vous pouvez utiliser pour les demandes de suppression d’identité uniques dans Experience Platform.

### Suppression d’une identité unique dans Privacy Service

Privacy Service traite les demandes des clients en matière dʼaccès, d’opt-out de vente ou de suppression de leurs données personnelles conformément aux réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et le California Consumer Privacy Act (CCPA). Avec Privacy Service, vous pouvez envoyer des requêtes de traitement à l’aide de l’API ou de l’interface utilisateur. Lorsqu’Experience Platform reçoit une demande de suppression de Privacy Service, Experience Platform envoie une confirmation à Privacy Service pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. La suppression de l’identité individuelle est basée sur l’espace de noms et/ou la valeur d’identifiant fournis. En outre, la suppression a lieu pour tous les sandbox associés à une organisation donnée. Pour plus d’informations, consultez le guide sur le [traitement des demandes d’accès à des informations personnelles dans le service d’identités](../privacy.md).

Le tableau ci-dessous fournit une répartition de la suppression d’identité unique dans Privacy Service :

| Suppression d’une identité unique | Privacy Service |
| --- | --- |
| Cas d’utilisation acceptés | Demandes d’accès à des informations personnelles (RGPD, CCPA) uniquement. |
| Latence estimée | Plusieurs jours à plusieurs semaines |
| Services concernés | La suppression d’identité unique dans Privacy Service vous permet de choisir si les données seront supprimées du service d’identités, du profil client en temps réel ou du lac de données. |
| Modèles de suppression | Supprimer une identité du service d’identités. |

{style="table-layout:auto"}

## Suppression d’un jeu de données

Les sections suivantes décrivent les mécanismes qui peuvent être utilisés pour supprimer des jeux de données et les liens d’identité associés dans Experience Platform.

### Suppression d’un jeu de données dans Catalog Service

Vous pouvez utiliser Catalog Service pour envoyer des demandes de suppression de jeux de données. Pour plus d’informations sur la suppression de jeux de données avec Catalog Service, consultez le guide sur la [suppression d’objets à l’aide de Catalog Service](../../catalog/api/delete-object.md). Vous pouvez également utiliser l’interface utilisateur d’Experience Platform pour envoyer des demandes de suppression de jeux de données. Pour plus d’informations, consultez le [guide d’utilisation des jeux de données](../../catalog/datasets/user-guide.md#delete-a-dataset).

### Expiration des jeux de données dans l’hygiène des données

L’espace de travail [[!UICONTROL Hygiène des données]](../../hygiene/ui/overview.md) dans l’interface utilisateur d’Adobe Experience Platform vous permet de planifier l’expiration des jeux de données. Lorsqu’un jeu de données atteint sa date d’expiration, le lac de données, le service d’identités et le profil client en temps réel lancent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Pour plus d’informations, consultez le guide sur la [gestion des expirations de jeux de données dans l’espace de travail [!UICONTROL Data Hygiene]](../../hygiene/ui/dataset-expiration.md).

Le tableau ci-dessous présente les différences entre la suppression de jeux de données dans Catalog Service et dans l’hygiène des données :

| Suppression d’un jeu de données | Service de catalogue | Hygiène des données |
| --- | --- | --- |
| Cas d’utilisation acceptés | Supprimez les jeux de données complets et les informations d’identité associées dans Experience Platform. | Gestion des données stockées dans Experience Platform. |
| Latence estimée | Jours | Jours |
| Services concernés | La suppression de jeux de données par le biais de Catalog Service supprime les données du service d’identités, du profil client en temps réel et du lac de données. | La suppression de jeux de données avec l’hygiène des données supprime les données du service d’identités, du profil client en temps réel et du lac de données. |
| Modèle de suppression | Supprimer les identités liées du service d’identités établies par un jeu de données spécifique. | Supprimer les identités liées du service d’identités établies par un jeu de données spécifique, selon le calendrier d’expiration. |

{style="table-layout:auto"}

## Différents états des graphiques d’identités après suppression

Toutes les suppressions de graphiques d’identités entraînent la suppression des liens entre plusieurs identités, comme spécifié par la demande de suppression. Pour les demandes de suppression de jeux de données, tous les liens d’identité établis par le jeu de données spécifié sont supprimés et peuvent ou non supprimer les identités des graphiques. Pour les demandes de suppression d’identité uniques, les liens d’identité sont supprimés pour l’identité spécifiée. Par conséquent, la valeur d’identité elle-même est supprimée de tous les graphiques d’identités. Les identités sans liaison unique à une autre identité ne sont pas stockées dans le service d’identités.

Vous trouverez ci-dessous un aperçu des impacts potentiels des suppressions sur l’état des graphiques d’identités.

| État du graphique d’identités | Description |
| --- | --- |
| Mise à jour partielle | Une mise à jour partielle d’un graphique se produit lorsqu’au moins deux identités restent liées dans un graphique après le traitement d’une demande de suppression. Après la suppression, les liens d’identité restants peuvent rester connectés les uns aux autres ou ils peuvent être fractionnés en deux ou plusieurs graphiques distincts en fonction des identités qui ont été supprimées. |
| Suppression complète | Un graphique doit comporter au moins deux identités liées pour exister. Par conséquent, si une demande de suppression entraîne la suppression de tous les liens existants dans un graphique, le graphique est complètement supprimé. |
| Aucune modification | Un graphique ne sera pas affecté si une demande de suppression spécifique contient une identité ou un jeu de données qui n’est associé à aucun membre du graphique. En outre, un graphique n’est pas mis à jour même si la demande de suppression supprime un lien entre un jeu de données ou une combinaison de jeux de données d’identité, étant donné que le lien a été établi par un autre lien qui n’a pas été supprimé. En d’autres termes, si un lien existe dans deux jeux de données différents, le graphique n’est pas mis à jour, car un seul des jeux de données est supprimé. |

{style="table-layout:auto"}

## Étapes suivantes

Ce document a couvert les différents mécanismes que vous pouvez utiliser pour supprimer des identités et des jeux de données sur Experience Platform. Ce document a également décrit comment les suppressions d’identité et de jeux de données peuvent avoir un impact sur les graphiques d’identités. Pour plus d’informations sur le service d’identités, consultez la [présentation du service d’identités](../home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Experience Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
