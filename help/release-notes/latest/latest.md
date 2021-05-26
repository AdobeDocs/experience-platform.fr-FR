---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform pour le 26 mai 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 91f75f5b6a8e5adb251455f65bc2b693934ef8e2
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 34%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 26 mai 2021**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Tableaux de bord](#dashboards)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit plusieurs tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles qu’elles sont capturées lors d’instantanés quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| Informations sur les profils | Le tableau de bord des profils fournit une vue d’ensemble quotidienne des mesures de Real-time Customer Profile pour chaque stratégie de fusion organisationnelle dans Experience Platform. Ces informations sur les profils sont disponibles pour tous les utilisateurs qui peuvent accéder aux données de profil et les afficher dans Platform. |
| Informations sur les audiences | Le tableau de bord des segments fournit des informations relatives aux audiences à tous les utilisateurs qui ont accès à l’affichage des segments dans Platform. Le tableau de bord présente un aperçu quotidien des mesures d’audience pour les audiences créées avec l’interface utilisateur du créateur de segments ou importées depuis Adobe Audience Manager. |
| Informations sur l’activation | Le tableau de bord des destinations est accessible à tous les utilisateurs qui peuvent accéder aux destinations et les afficher. Le tableau de bord fournit un aperçu quotidien des mesures d’activation pour les activations sur toutes les destinations. |
| Informations spécifiques à l’utilisateur | L’aspect des tableaux de bord peut être personnalisé par chaque utilisateur, notamment la possibilité de modifier la mise en page du tableau de bord en ajoutant, supprimant, redimensionnant et réorganisant des widgets. |
| Création et gestion de widgets | Tous les widgets standard et personnalisés sont accessibles aux spécialistes du marketing dans un référentiel centralisé pour démocratiser la création et le partage d’informations :<br/><ul><li>L’onglet standard contient des widgets fournis par Adobe, accessibles dans le contexte du tableau de bord. </li><li>L’onglet personnalisé contient des widgets personnalisés créés par l’organisation, y compris une option permettant de masquer les widgets de la vue.</li><li>Le workflow de création de widgets dans les insights Profils et Audience permet de modifier, de sélectionner, de prévisualiser et de publier des widgets personnalisés.</li></ul> |
| Aperçu personnalisé | Les autorisations d’accès permettent aux ingénieurs de données et aux spécialistes du marketing de personnaliser les attributs de profil disponibles pour la création de widgets. |

Pour plus d’informations sur les tableaux de bord, notamment sur la manière d’accorder des autorisations d’accès et de créer des widgets personnalisés, commencez par lire la [présentation des tableaux de bord](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

| Fonctionnalité | Description |
| ------- | ----------- |
| Avertissements d’erreur relatifs aux loupes | Les messages d’erreur de Data Prep Mapper seront désormais plus indulgents, en fournissant des avertissements au lieu d’erreurs, ainsi que des lignes partiellement transformées. |
| Nouvelles fonctions | Ajout de fonctions pour obtenir des clés, ajouter des éléments à un tableau existant, ajouter des éléments de plusieurs tableaux à un tableau existant, utiliser des objets pour créer des tableaux et utiliser le nom de l’objet JSON comme littéral de chaîne. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation des ](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

| Fonctionnalité | Description |
| ------- | ----------- |
| Amélioration de la surveillance (version bêta) | Amélioration des fonctionnalités de surveillance des destinations, y compris des informations pour les destinations par lots et en flux continu |
| [Exportation incrémentielle plus rapide des fichiers (bêta)](../../destinations/ui/activate-destinations.md#export-incremental-files) | Ajout de la capacité d’exporter des fichiers incrémentiels vers des destinations toutes les 3, 6, 8 ou 12 heures. <br> <br>Cette fonctionnalité est actuellement en version bêta et n’est disponible que pour un certain nombre de clients. Les clients non bêta peuvent exporter des fichiers incrémentiels une fois par jour. |
| [Prise en charge des clés de déduplication (version bêta)](../../destinations/ui/activate-destinations.md#deduplication-keys) | Ajout de la possibilité de définir des espaces de noms d’identité ou des attributs de profil comme clés de déduplication. Les clés de déduplication éliminent la possibilité d’avoir plusieurs enregistrements du même profil dans un fichier d’exportation. <br> <br>Cette fonctionnalité est actuellement en version bêta et n’est disponible que pour un certain nombre de clients. |

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Groupes de champs de schéma | Le terme &quot;mixin&quot; a été mis à jour en &quot;groupe de champs&quot;. Cette modification est répercutée dans l’ensemble de l’interface utilisateur de Adobe Experience Platform. En outre, l’API Schema Registry comporte un nouveau point de terminaison [de groupes de champs](../../xdm/api/field-groups.md), tandis que le point de terminaison mixins a été abandonné en tant que point de terminaison hérité. Pour plus d’informations, consultez la [documentation XDM](../../xdm/home.md). |

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Mises à jour du workflow de stratégie de fusion | Lors de la création et de la mise à jour de stratégies de fusion dans l’interface utilisateur, les utilisateurs peuvent désormais prévisualiser 20 exemples de profils en fonction du schéma d’union. Cela permet aux utilisateurs de prévisualiser à quoi ressembleront les profils client avant d’enregistrer les configurations de stratégie de fusion. Pour plus d’informations, consultez le [guide de l’interface utilisateur des stratégies de fusion](../../profile/merge-policies/ui-guide.md). |
| Rapport de chevauchement de jeux de données | Le rapport de chevauchement des jeux de données offre une visibilité sur la composition de la banque de profils en exposant les jeux de données qui contribuent le plus à l’audience adressable. En plus de fournir des informations sur les données de profil, ce rapport permet aux utilisateurs d’agir pour optimiser l’utilisation de la licence, comme de définir une limite de durée de vie de certaines données. Pour en savoir plus, suivez le tutoriel sur la [génération du rapport de chevauchement de jeux de données](../../profile/tutorials/dataset-overlap-report.md). |

Pour plus d’informations sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données de [!DNL Profile], consultez la [présentation du profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’interface utilisateur pour l’ingestion de fichiers compressés | Vous pouvez désormais prévisualiser et ingérer des fichiers JSON compressés ou délimités à l’aide de sources de stockage dans le cloud dans l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un flux de données pour une connexion à une source de stockage dans le cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
