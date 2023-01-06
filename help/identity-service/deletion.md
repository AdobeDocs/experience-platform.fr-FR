---
title: Suppression dans Identity Service
description: Ce document présente les différents mécanismes que vous pouvez utiliser pour supprimer vos données d’identité dans Experience Platform et explique clairement comment les graphiques d’identités peuvent être affectés.
source-git-commit: 17e39f6e9d6e62e22f867de91d571593ba945c71
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 12%

---

# Suppression dans Identity Service

Adobe Experience Platform Identity Service génère des graphiques d’identités en liant de manière déterministe les identités entre les appareils et les systèmes pour une personne individuelle. Les liens des graphiques d’identités sont établis lorsque plusieurs identités marquées sont reçues au sein de la même ligne de données.

Les graphiques d’identités sont utilisés par Real-time Customer Profile pour créer une vue d’ensemble exhaustive et unique de vos attributs et comportements client, ce qui vous permet de fournir des expériences numériques personnelles et percutantes en temps réel, aux personnes et non aux appareils.

Ce document présente les différents mécanismes que vous pouvez utiliser pour supprimer vos données d’identité dans Experience Platform et explique clairement comment les graphiques d’identités peuvent être affectés.

## Prise en main

Le document ci-dessous fait référence aux fonctions suivantes d’Experience Platform :

* [Service d’identités](home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en reliant les identités entre les appareils et les systèmes.
   * [Graphique d’identités](./ui/identity-graph-viewer.md): Un graphique d’identités est une carte des relations entre différentes identités pour un client spécifique, qui vous fournit une représentation visuelle de la manière dont votre client interagit avec votre marque sur différents canaux.
   * [Espaces de noms d’identité](namespaces.md): Les espaces de noms d’identité sont des composants d’Identity Service qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur « name<span>@email.com » comme adresse e-mail ou « 443522 » comme identifiant CRM numérique.
* [Service de catalogue](../catalog/home.md): Explorez le lignage de données, les métadonnées, les descriptions de fichiers, les répertoires et les jeux de données dans le lac de données.
* [Assurance des données](../hygiene/home.md): Gérez vos données client stockées en planifiant des expirations de jeux de données automatisées ou en supprimant des enregistrements individuels d’un jeu de données ou de tous les jeux de données.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Gérez les demandes de clients pour accéder à leurs données personnelles, en refuser la vente ou les supprimer dans les applications Adobe Experience Cloud.
* [Profil client en temps réel](../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Suppression d’une seule identité

Les demandes de suppression d’identité unique vous permettent de supprimer une identité dans un graphique, ce qui entraîne la suppression des liens liés à une seule identité utilisateur associée à un espace de noms d’identité. Vous pouvez utiliser [Assurance des données](../hygiene/home.md) pour la normalisation des données, la suppression des données anonymes ou la minimisation des données que vous avez collectées. Pour les cas d’utilisation tels que les demandes de suppression des données par les clients et la conformité aux réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD), vous pouvez utiliser les mécanismes fournis par [Privacy Service](../privacy-service/home.md).

Les sections ci-dessous décrivent les mécanismes que vous pouvez utiliser pour les demandes de suppression d’identité uniques dans Experience Platform.

### Suppression d’une identité unique dans Privacy Service

Privacy Service traite les demandes de clients souhaitant accéder à leurs données personnelles, en refuser la vente, ou les effacer comme le stipulent les réglementations de confidentialité telles que le Règlement général sur la protection des données (RGPD) et le California Consumer Privacy Act (CCPA). Avec Privacy Service, vous pouvez envoyer des requêtes de tâche à l’aide de l’API ou de l’interface utilisateur. Lorsqu’Experience Platform reçoit une demande de suppression de la part de Privacy Service, Platform envoie une confirmation à Privacy Service pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. La suppression de l’identité individuelle est basée sur l’espace de noms et/ou la valeur d’identifiant fournis. En outre, la suppression a lieu pour tous les environnements de test associés à une organisation donnée. Pour plus d’informations, consultez le guide sur [traitement des demandes d’accès à des informations personnelles dans Identity Service](privacy.md).

### Suppression d’une seule identité dans le [!UICONTROL Hygiène des données] workspace

Le [[!UICONTROL Hygiène des données] workspace](../hygiene/ui/overview.md) Dans l’interface utilisateur de Platform, vous pouvez supprimer les enregistrements de consommateurs qui participent à Identity Service et à Real-time Customer Profile. Pour obtenir un guide complet sur l’utilisation de la variable [!UICONTROL Hygiène des données] workspace, consultez le tutoriel sur [suppression des enregistrements de consommateurs](../hygiene/ui/record-delete.md).

Le tableau ci-dessous présente la répartition des différences entre la suppression d’une identité unique en Privacy Service et l’hygiène des données :

| Suppression d’une identité unique | Privacy Service | Hygiène des données |
| --- | --- | --- |
| Cas d’utilisation acceptés | Demandes d’accès à des informations personnelles (RGPD, CCPA) uniquement. | Gestion des données stockées dans Experience Platform. |
| Latence estimée | Jours à semaines | Days |
| Services concernés | La suppression d’identité unique dans Privacy Service vous permet de choisir si les données seront supprimées d’Identity Service, de Real-Time Customer Profile ou du lac de données. | La suppression d’identité unique dans l’ hygiène des données supprime les données sélectionnées dans Identity Service, Real-Time Customer Profile et le lac de données. |
| Modèles de suppression | Supprimez une identité d’Identity Service. | Supprimez une identité d’Identity Service. |

{style=&quot;table-layout:auto&quot;}

## Suppression de jeux de données

Les sections suivantes décrivent les mécanismes qui peuvent être utilisés pour supprimer des jeux de données et les liens d’identité associés dans Experience Platform.

### Suppression de jeux de données dans le service de catalogue

Vous pouvez utiliser le service de catalogue pour envoyer des demandes de suppression de jeux de données. Pour plus d’informations sur la suppression de jeux de données avec Catalog Service, consultez le guide sur [suppression d’objets à l’aide de l’API Catalog Service](../catalog/api/delete-object.md). Vous pouvez également utiliser l’interface utilisateur de Platform pour envoyer des requêtes de suppression de jeux de données. Pour plus d’informations, reportez-vous à la section [guide d’utilisation des jeux de données](../catalog/datasets/user-guide.md#delete-a-dataset).

### Expiration des jeux de données dans l’hygiène des données

L’espace de travail [[!UICONTROL Hygiène des données]](../hygiene/ui/overview.md) dans l’interface utilisateur d’Adobe Experience Platform vous permet de planifier l’expiration des jeux de données. Lorsqu’un jeu de données atteint sa date d’expiration, le lac de données, Identity Service et Real-Time Customer Profile commencent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Pour plus d’informations, consultez le guide sur [gestion des expirations de jeux de données à l’aide de la fonction [!UICONTROL Hygiène des données] workspace](../hygiene/ui/dataset-expiration.md).

Le tableau ci-dessous présente une ventilation des différences entre la suppression de jeux de données dans le service de catalogue et l’hygiène des données :

| Suppression de jeux de données | Service de catalogue | Hygiène des données |
| --- | --- | --- |
| Cas d’utilisation acceptés | Supprimez les jeux de données complets et les informations d’identité associées dans Platform. | Gestion des données stockées dans Experience Platform. |
| Latence estimée | Days | Days |
| Services concernés | La suppression de jeux de données par le biais du service de catalogue supprime les données d’Identity Service, de Real-Time Customer Profile et du lac de données. | La suppression de jeux de données par le biais de l’hygiène des données supprime les données d’Identity Service, de Real-Time Customer Profile et du lac de données. |
| Modèle de suppression | Supprimez les identités liées d’Identity Service établies par un jeu de données spécifique. | Supprimez les identités liées d’Identity Service établies par un jeu de données spécifique, selon le calendrier d’expiration. |

{style=&quot;table-layout:auto&quot;}

## Différents états des graphiques d’identités après suppression

Toutes les suppressions de graphiques d’identités entraînent la suppression des liens entre plusieurs identités, comme spécifié par la demande de suppression. Pour les demandes de suppression de jeux de données, tous les liens d’identité établis par le jeu de données spécifié sont supprimés et peuvent ou non supprimer des identités des graphiques. Pour les demandes de suppression d’identité uniques, les liens d’identité sont supprimés pour l’identité spécifiée. Par conséquent, la valeur d’identité elle-même est supprimée de tous les graphiques d’identités. Les identités sans liaison unique à une autre identité ne sont pas stockées dans Identity Service.

Vous trouverez ci-dessous un aperçu des impacts potentiels des suppressions sur l’état des graphiques d’identités.

| État du graphique d’identités | Description |
| --- | --- |
| Mise à jour partielle | Une mise à jour partielle d’un graphique se produit lorsqu’au moins deux identités restent liées dans un graphique après le traitement d’une demande de suppression. Après la suppression, les liens d’identité restants peuvent rester connectés les uns aux autres ou ils peuvent être fractionnés en deux ou plusieurs graphiques distincts en fonction des identités qui ont été supprimées. |
| Suppression complète | Un graphique doit comporter au moins deux identités liées pour exister. Par conséquent, si une demande de suppression entraîne la suppression de tous les liens existants dans un graphique, le graphique est complètement supprimé. |
| Aucune modification | Un graphique ne sera pas affecté si une demande de suppression spécifique contient une identité ou un jeu de données qui n’est associé à aucun membre du graphique. En outre, un graphique n’est pas mis à jour même si la demande de suppression supprime un lien entre un jeu de données ou une combinaison de jeux de données d’identité, étant donné que le lien a été établi par un autre lien qui n’a pas été supprimé. En d’autres termes, si un lien existe dans deux jeux de données différents, le graphique n’est pas mis à jour, car un seul des jeux de données est supprimé. |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes

Ce document couvrait les différents mécanismes que vous pouvez utiliser pour supprimer des identités et des jeux de données sur Experience Platform. Ce document décrit également comment les suppressions d’identité et de jeux de données peuvent avoir un impact sur les graphiques d’identités. Pour plus d’informations sur Identity Service, consultez la [Présentation d’Identity Service](home.md).