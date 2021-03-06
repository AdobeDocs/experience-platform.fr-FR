---
keywords: Experience Platform;accueil;rubriques les plus consultées;Marketo Engage;marketing à engager;marketing
solution: Experience Platform
title: Connecteur Marketo Engage
topic-legacy: overview
description: Ce document présente le connecteur source du Marketo Engage, y compris des informations sur son authentification, son mappage et sa latence de données.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 8b8e08adb5ff3498169c1702680ea44f3bebf5c5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 13%

---

# Connecteur [!DNL Marketo Engage]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (ci-après dénommés &quot;[!DNL Marketo]&quot;) est une solution complète pour la gestion des pistes et les spécialistes du marketing B2B qui cherchent à transformer les expériences client en s’engageant à chaque étape de parcours d’achat complexes.

Avec le [!DNL Marketo] connecteur source, vous pouvez importer des données B2B à partir de [!DNL Marketo] à Platform et tenir ces données à jour à l’aide d’applications connectées à Platform.

>[!IMPORTANT]
>
>Vous devez avoir accès à [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) pour que le Marketo Engage puisse participer à [Real-time Customer Profile](../../../../profile/home.md).

Ce document présente la [!DNL Marketo] connecteur source, y compris des informations sur l’authentification du connecteur, comment mapper [!DNL Marketo] des champs vers le modèle de données d’expérience (XDM) et la latence des données du connecteur.

## Authentifiez votre [!DNL Marketo] connector

Pour vous connecter [!DNL Marketo] sur Platform, vous devez d’abord récupérer les valeurs de votre `munchkinId`, `clientId`, et `clientSecret`.

Reportez-vous aux étapes décrites dans la section [Authentification de votre connecteur source Marketo](./marketo-auth.md) pour récupérer vos informations d’identification.

## Configuration du mappage de l’organisation Adobe

Avant d’établir des jeux de mappages pour [!DNL Marketo], vous devez d’abord configurer le mappage de l’organisation Adobe. Pour obtenir des instructions détaillées sur la manière de procéder, consultez le guide sur la [configuration du mappage de l’organisation Adobe pour [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma

Ensuite, utilisez l’espace de noms B2B et l’utilitaire de génération automatique de schéma pour configurer votre console de développement Platform et votre environnement Postman. Cela vous permet de renseigner automatiquement vos espaces de noms et schémas B2B. Pour obtenir des instructions détaillées, consultez le guide sur la [configuration des espaces de noms B2B et de l’utilitaire de génération automatique de schéma](./marketo-namespaces.md)

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes qui vous permettent d’ingérer des données provenant de sources tierces pour les utiliser dans les services Platform en aval.

Le respect des normes XDM permet d’intégrer uniformément les données dans l’écosystème de Platform, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans Platform, voir [Présentation du système XDM](../../../../xdm/home.md).

## Mappage des champs à partir de [!DNL Marketo] vers XDM

Pour établir une connexion source entre [!DNL Marketo] et Platform, les champs de données source Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les [!DNL Marketo] jeux de données et plateforme :

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

## Latence attendue de [!DNL Marketo] données sur Platform

Le tableau suivant décrit la latence attendue pour l’introduction de [!DNL Marketo] données dans Platform, en fonction de la nature de l’ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’un [!DNL Marketo] connexion source :

* Pour plus d’informations sur la connexion à votre [!DNL Marketo] data to Platform, consultez le tutoriel sur [création d’un connecteur source Marketo dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Pour plus d’informations sur la configuration sous-jacente des espaces de noms et des schémas B2B utilisés avec [!DNL Marketo], voir la documentation pour [Espaces de noms et schémas B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de [!DNL Marketo] l’identifiant munchkin et la génération de vos informations d’identification, voir [[!DNL Marketo] guide d&#39;authentification](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent à [!DNL Marketo] jeux de données, consultez la documentation sur [[!DNL Marketo] mappages de champs](../mapping/marketo.md).
* Pour des informations générales sur [!DNL Real-time Customer Data Platform B2B Edition] et ses fonctionnalités, consultez la documentation sur [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
