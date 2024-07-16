---
keywords: Experience Platform;accueil;rubriques les plus consultées;Marketo Engage;marketing à engager;marketing
solution: Experience Platform
title: Connecteur Marketo Engage
description: Ce document présente le connecteur source du Marketo Engage, y compris des informations sur son authentification, son mappage et sa latence de données.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 11%

---

# Connecteur [!DNL Marketo Engage]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) est une solution complète pour la gestion des pistes et les spécialistes du marketing B2B qui cherchent à transformer les expériences client en s’engageant à chaque étape de parcours d’achat complexes.

Avec le connecteur source [!DNL Marketo Engage], vous pouvez importer les données B2B de [!DNL Marketo Engage] vers Platform et garder ces données à jour à l’aide des applications connectées à Platform.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Adobe Real-Time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) pour utiliser tous les jeux de données Marketo pour la segmentation avec le [profil client en temps réel](../../../../profile/home.md). Sans l’édition B2B de Real-Time CDP, vous pouvez toujours utiliser la source Marketo pour importer les données des personnes et des jeux de données d’activités dans Real-time Customer Profile à des fins de segmentation.

Ce document présente un aperçu du connecteur source [!DNL Marketo Engage], y compris des informations sur la manière d’authentifier le connecteur, de mapper les champs [!DNL Marketo Engage] à Experience Data Model (XDM) et la latence des données du connecteur.

## Configuration du mappage de l’organisation Adobe

Avant de pouvoir établir des jeux de mappages pour [!DNL Marketo Engage], vous devez d’abord configurer le mappage de l’organisation Adobe. Pour obtenir des instructions détaillées sur la manière de procéder, consultez le guide sur la [configuration du mappage de l’organisation Adobe pour [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Authentification de votre connecteur [!DNL Marketo Engage]

Pour vous connecter [!DNL Marketo Engage] à Platform, vous devez d’abord récupérer les valeurs de vos `munchkinId`, `clientId` et `clientSecret`.

Pour récupérer vos informations d’identification, reportez-vous aux étapes décrites dans le document [Authentification de votre connecteur source Marketo](./marketo-auth.md) .

## Configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma

Ensuite, utilisez l’espace de noms B2B et l’utilitaire de génération automatique de schéma pour configurer votre console de développement Platform et votre environnement Postman. Cela vous permet de renseigner automatiquement vos espaces de noms et schémas B2B. Pour obtenir des instructions détaillées, consultez le guide sur la [configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma](./marketo-namespaces.md)

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes qui vous permettent d’ingérer des données provenant de sources tierces pour les utiliser dans les services Platform en aval.

Le respect des normes XDM permet d’intégrer uniformément les données dans l’écosystème de Platform, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans Platform, consultez la [présentation du système XDM](../../../../xdm/home.md).

## Mappage de champs de [!DNL Marketo Engage] à XDM

Pour établir une connexion source entre [!DNL Marketo Engage] et Platform, les champs de données source Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les jeux de données [!DNL Marketo Engage] et Platform, reportez-vous à la section suivante :

* [Activités](../mapping/marketo.md#activities)
* [Programmes](../mapping/marketo.md#programs)
* [Abonnements au programme](../mapping/marketo.md#program-memberships)
* [Sociétés](../mapping/marketo.md#companies)
* [Listes statiques](../mapping/marketo.md#static-lists)
* [Abonnements à des listes statiques](../mapping/marketo.md#static-list-memberships)
* [Comptes désignés](../mapping/marketo.md#named-accounts)
* [Opportunités](../mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../mapping/marketo.md#persons)

## Latence attendue des données [!DNL Marketo Engage] sur Platform

Le tableau suivant décrit la latence attendue pour l’importation de données [!DNL Marketo Engage] dans Platform, en fonction de la nature de l’ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minutes |
| Lac de données | &lt; 60 minutes |

>[!NOTE]
>
>Les chiffres de latence ci-dessus représentent les attentes à un degré de confiance de 95 %. Dans de rares cas, les latences réelles varient et peuvent s’étendre au-delà de ces chiffres de 50 %.

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’une connexion source [!DNL Marketo Engage] :

* Pour plus d’informations sur la connexion de vos données [!DNL Marketo Engage] à Platform, lisez le tutoriel sur la [création d’une  [!DNL Marketo Engage] connexion source dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Pour plus d’informations sur la configuration de vos schémas et l’ingestion de données d’activité personnalisées, lisez le tutoriel sur la [création d’une connexion source et d’un flux de données pour les [!DNL Marketo Engage] données d’activité personnalisées](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Pour plus d’informations sur la migration de votre mappage ECID du jeu de données [!DNL Person] vers le jeu de données [!DNL Activity], consultez le [guide de migration du mappage ECID](./migration.md).
* Pour plus d’informations sur la configuration sous-jacente des espaces de noms et schémas B2B utilisés avec [!DNL Marketo Engage], consultez la documentation des [espaces de noms et schémas B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de votre ID de munchkin [!DNL Marketo Engage] et la génération de vos informations d’identification, consultez le [[!DNL Marketo Engage] guide d’authentification](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent aux jeux de données [!DNL Marketo Engage], consultez la documentation sur les [[!DNL Marketo Engage] mappages de champs](../mapping/marketo.md).
* Pour obtenir des informations générales sur [!DNL Real-Time Customer Data Platform B2B Edition] et ses fonctionnalités, consultez la documentation sur [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
