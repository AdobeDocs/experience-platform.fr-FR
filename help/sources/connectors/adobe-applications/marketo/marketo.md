---
keywords: Experience Platform;accueil;rubriques les plus consultées;Marketo Engage;marketing à engager;marketing
solution: Experience Platform
title: Connecteur Marketo Engage
topic-legacy: overview
description: Ce document présente le connecteur source du Marketo Engage, y compris des informations sur son authentification, son mappage et sa latence de données.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# (Version bêta) Connecteur [!DNL Marketo Engage]

>[!IMPORTANT]
>
>La source [!DNL Marketo Engage] de Adobe Experience Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (ci-après appelé &quot;[!DNL Marketo]&quot;) est une solution complète pour la gestion des pistes et les spécialistes du marketing B2B qui cherchent à transformer les expériences client en s’engageant à chaque étape de parcours d’achat complexes.

Avec le connecteur source [!DNL Marketo], vous pouvez importer les données B2B de [!DNL Marketo] vers Platform et garder ces données à jour à l’aide des applications connectées à Platform.

Ce document présente un aperçu du connecteur source [!DNL Marketo], y compris des informations sur la manière d’authentifier le connecteur, de mapper les champs [!DNL Marketo] au modèle de données d’expérience (XDM) et la latence des données du connecteur.

## Authentification de votre connecteur [!DNL Marketo]

Pour connecter [!DNL Marketo] à Platform, vous devez d’abord récupérer les valeurs de `munchkinId`, `clientId` et `clientSecret`.

Voir les étapes décrites dans le document [Authentifier votre connecteur source Marketo](./marketo-auth.md) pour récupérer vos informations d’identification.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes qui vous permettent d’ingérer des données provenant de sources tierces pour les utiliser dans les services Platform en aval.

Le respect des normes XDM permet d’intégrer uniformément les données dans l’écosystème de Platform, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM et son rôle dans Platform, consultez la [présentation du système XDM](../../../../xdm/home.md).

## Mappage de champs de [!DNL Marketo] à XDM

Pour établir une connexion source entre [!DNL Marketo] et Platform, les champs de données source Marketo doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Platform.

Pour plus d’informations sur les règles de mappage de champs entre les jeux de données [!DNL Marketo] et Platform, voir les sections suivantes :

* [Activités](../mapping/marketo.md#activities)
* [Programmes](../mapping/marketo.md#programs)
* [Abonnements au programme](../mapping/marketo.md#program-memberships)
* [Sociétés](../mapping/marketo.md#companies)
* [Listes statiques](../mapping/marketo.md#static-lists)
* [Abonnements à des listes statiques](../mapping/marketo.md#static-list-memberships)
* [Comptes nommés](../mapping/marketo.md#named-accounts)
* [Opportunités](../mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../mapping/marketo.md#persons)

## Latence attendue des données [!DNL Marketo] sur Platform

Le tableau suivant décrit la latence attendue pour l’introduction de données [!DNL Marketo] dans Platform, en fonction de la nature de l’ingestion et de la destination souhaitée :

| Destination | Latence attendue |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minute |
| Lac de données | &lt; 60 minutes |

## Étapes suivantes et ressources supplémentaires

La documentation suivante fournit des informations supplémentaires sur la création d’une connexion source [!DNL Marketo] :

* Pour plus d’informations sur la connexion de vos données [!DNL Marketo] à Platform, consultez le tutoriel sur la [création d’un connecteur source Marketo dans l’interface utilisateur](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Pour plus d’informations sur la configuration sous-jacente des espaces de noms et schémas B2B utilisés avec [!DNL Marketo], consultez la documentation des [espaces de noms et schémas B2B](./marketo-namespaces.md).
* Pour plus d’informations sur la recherche de votre [!DNL Marketo] munchkin ID et la génération de vos informations d’identification, consultez le [[!DNL Marketo] guide d’authentification](./marketo-auth.md).
* Pour plus d’informations sur les règles de mappage spécifiques qui s’appliquent aux jeux de données [!DNL Marketo], consultez la documentation sur les [[!DNL Marketo] mappages de champs](../mapping/marketo.md).
* Pour obtenir des informations générales sur [!DNL Real-time Customer Data Platform B2B Edition] et ses fonctionnalités, consultez la documentation sur [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
