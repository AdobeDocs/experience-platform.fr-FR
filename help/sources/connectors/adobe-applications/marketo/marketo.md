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

Avec la variable [!DNL Marketo Engage] connecteur source, vous pouvez importer des données B2B depuis [!DNL Marketo Engage] à Platform et tenir ces données à jour à l’aide d’applications connectées à Platform.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Adobe Real-time Customer Data Platform version B2B](../../../../rtcdp/b2b-overview.md) pour utiliser tous les jeux de données Marketo à des fins de segmentation avec la variable [Profil client en temps réel](../../../../profile/home.md). Sans l’édition B2B de Real-Time CDP, vous pouvez toujours utiliser la source Marketo pour importer les données des personnes et des jeux de données d’activités dans Real-time Customer Profile à des fins de segmentation.

Ce document présente la [!DNL Marketo Engage] connecteur source, y compris des informations sur l’authentification du connecteur, comment mapper [!DNL Marketo Engage] des champs vers le modèle de données d’expérience (XDM) et la latence des données du connecteur.

## Configuration du mappage de l’organisation Adobe

Avant d’établir des jeux de mappages pour [!DNL Marketo Engage], vous devez d’abord configurer le mappage de l’organisation Adobe. Pour obtenir des instructions détaillées sur la manière d’effectuer cette opération, consultez le guide sur [configuration du mappage de l’organisation Adobe pour [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Authentifiez votre [!DNL Marketo Engage] connector

Pour vous connecter [!DNL Marketo Engage] sur Platform, vous devez d’abord récupérer les valeurs de votre `munchkinId`, `clientId`, et `clientSecret`.

Voir les étapes décrites dans la section [Authentification de votre connecteur source Marketo](./marketo-auth.md) pour récupérer vos informations d’identification.

## Configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma

Ensuite, utilisez l’espace de noms B2B et l’utilitaire de génération automatique de schéma pour configurer votre console de développement Platform et votre environnement Postman. Cela vous permet de renseigner automatiquement vos espaces de noms et schémas B2B. Pour obtenir des instructions détaillées, consultez le guide sur la [configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma](./marketo-namespaces.md)

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes qui vous permettent d’ingérer des données provenant de sources tierces pour les utiliser dans les services Platform en aval.

Le respect des normes XDM permet d’intégrer uniformément les données dans l’écosystème de Platform, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans Platform, voir [Présentation du système XDM](../../../../xdm/home.md).

## Mappage des champs depuis [!DNL Marketo Engage] vers XDM

Pour établir une connexion source entre [!DNL Marketo Engage] et Platform, les champs de données source Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les [!DNL Marketo Engage] jeux de données et plateforme :

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

## Latence attendue de [!DNL Marketo Engage] données sur Platform

Le tableau suivant décrit la latence attendue pour l’introduction de [!DNL Marketo Engage] données dans Platform, en fonction de la nature de l’ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minutes |
| Lac de données | &lt; 60 minutes |

>[!NOTE]
>
>Les chiffres de latence ci-dessus représentent les attentes à un degré de confiance de 95 %. Dans de rares cas, les latences réelles varient et peuvent s’étendre au-delà de ces chiffres de 50 %.

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’un [!DNL Marketo Engage] connexion source :

* Pour plus d’informations sur la connexion à votre [!DNL Marketo Engage] data to Platform, lisez le tutoriel sur [création d’un [!DNL Marketo Engage] connexion source dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Pour plus d’informations sur la configuration de vos schémas et l’ingestion de données d’activité personnalisées, lisez le tutoriel sur [création d’une connexion source et d’un flux de données pour [!DNL Marketo Engage] données d’activité personnalisées](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Pour plus d’informations sur la migration de votre mappage ECID à partir de [!DNL Person] du jeu de données [!DNL Activity] jeu de données, lisez [Guide de migration de mappage ECID](./migration.md).
* Pour plus d’informations sur la configuration sous-jacente des espaces de noms et des schémas B2B utilisés avec [!DNL Marketo Engage], lisez la documentation pour [Espaces de noms et schémas B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de [!DNL Marketo Engage] Identifiant munchkin et génération de vos informations d’identification, lisez la [[!DNL Marketo Engage] guide d&#39;authentification](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent à [!DNL Marketo Engage] jeux de données, lisez la documentation sur [[!DNL Marketo Engage] mappages de champs](../mapping/marketo.md).
* Pour des informations générales sur [!DNL Real-Time Customer Data Platform B2B Edition] et ses fonctionnalités, lisez la documentation sur [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
