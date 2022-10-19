---
title: Présentation des flux de données
description: Connectez votre intégration SDK Experience Platform côté client à des produits Adobe et à des destinations tierces.
keywords: configuration;flux de données;datastreamId;edge;identifiant de flux de données;Paramètres d’environnement;edgeConfigId;identité;synchronisation des identifiants activée;Identifiant de conteneur de synchronisation d’identifiant;Sandbox;Diffusion d’entrée;Jeu de données d’événement;target;code client;Jeton de propriété;Identifiant d’environnement Target;Destinations de cookie;Destinations d’url;identifiant de suite de rapports de blocs de paramètres Analytics;Préparation des données pour la collecte de données;Préparation des données;Mappeur;Mappeur XDM;Mappeur sur Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 21%

---

# Présentation des flux de données

Un flux de données représente la configuration côté serveur lors de la mise en œuvre des SDK web et mobile d’Adobe Experience Platform. Lorsque la [commande de configuration](../fundamentals/configuring-the-sdk.md) dans le SDK contrôle les éléments qui doivent être gérés sur le client (comme `edgeDomain`), les flux de données gèrent toutes les autres configurations pour le SDK. Lorsqu’une requête est envoyée à Adobe Experience Platform Edge Network, `edgeConfigId` est utilisé pour référencer le flux de données. Cela vous permet de mettre à jour la configuration côté serveur sans devoir modifier le code du site web.

Vous pouvez créer et gérer des flux de données en sélectionnant **[!UICONTROL Datastreams]** dans le volet de navigation de gauche de l’interface utilisateur de Adobe Experience Platform ou de l’interface utilisateur de collecte de données.

![Onglet Flux de données dans l’interface utilisateur](../assets/datastreams/overview/datastreams-tab.png)

Pour plus d’informations sur la configuration d’un flux de données dans l’interface utilisateur, reportez-vous à la section [guide de configuration](./configure.md).

## Gestion des données sensibles dans les flux de données {#sensitive}

>[!IMPORTANT]
>
>Le contenu de ce document n&#39;est pas un avis juridique et ne vise pas à remplacer un avis juridique. Veuillez consulter le service juridique de votre entreprise pour obtenir des conseils concernant la gestion des données sensibles.

Les politiques de gestion des données d’entreprise et les exigences réglementaires augmentent les restrictions sur la manière dont les données clients sensibles peuvent être collectées, traitées et utilisées. Cela inclut la collecte, le traitement et l’utilisation des données de santé protégées (IMS), qui sont soumises à des règlements comme la Loi sur la transférabilité et la responsabilité de l’assurance-santé (LPAH).

Datastreams propose trois méthodes pour vous aider à gérer vos données sensibles en toute sécurité :

* [Cryptage amélioré](#encryption)
* [Gouvernance des données](#governance)
* [Journaux d’audit](#audit-logs)

### Cryptage amélioré {#encryption}

Toutes les données en transit par le réseau Edge sont effectuées sur des connexions sécurisées et cryptées à l’aide de [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si la banque de données introduit des données dans l’Experience Platform, les données sont alors cryptées au repos dans le lac de données Experience Platform. Consultez le document sur [cryptage des données dans Experience Platform](../../landing/governance-privacy-security/encryption.md) pour plus d’informations.

### Gouvernance des données {#governance}

Les flux de données utilisent les fonctionnalités de gouvernance des données intégrées de l’Experience Platform pour empêcher l’envoi de données sensibles à des services non compatibles avec les HIPAA. En étiquetant des champs spécifiques qui contiennent des données sensibles dans vos schémas de flux de données, vous pouvez contrôler de manière granulaire quels champs de données peuvent être utilisés à des fins spécifiques.

La vidéo suivante présente un bref aperçu de la manière dont les restrictions d’utilisation des données sont configurées et appliquées pour les flux de données dans l’interface utilisateur :

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Dans Experience Platform, vous pouvez appliquer des [libellés d’utilisation des données sensibles](../../data-governance/labels/reference.md#sensitive) aux schémas et aux champs contenant des données que votre organisation juge sensibles. Par exemple, la variable `RHD` est utilisé pour désigner les informations sur la santé protégée (PHI), et la variable `S1` label représente les données de géolocalisation.

>[!NOTE]
>
>Pour plus d’informations sur la manière d’appliquer des libellés d’utilisation des données dans la variable [!UICONTROL Schémas] dans l’interface utilisateur de l’Experience Platform ou dans l’interface utilisateur de collecte de données, reportez-vous à la section [tutoriel sur l’étiquetage des schémas](../../xdm/tutorials/labels.md).

Lors de la création d’un nouveau flux de données, si le schéma sélectionné contient des libellés d’utilisation des données sensibles, le flux de données ne peut être configuré que pour envoyer ces données vers des destinations prêtes pour le HIPAA. Actuellement, Adobe Experience Platform est la seule destination compatible avec HIPAA prise en charge par les flux de données. Les autres services de destination, notamment Adobe Target, Adobe Analytics, Adobe Audience Manager, le transfert d’événement et les destinations Edge, sont désactivés pour les flux de données contenant des libellés d’utilisation des données sensibles.

Si un schéma est utilisé dans un flux de données existant avec des services non compatibles avec HIPAA, la tentative d’ajout d’un libellé d’utilisation des données sensibles au schéma génère un message de violation de stratégie et empêche l’action. Le message spécifie quel flux de données a déclenché la violation et suggère de supprimer tous les services non compatibles avec HIPAA du flux de données pour résoudre le problème.

### Journaux d’audit

Dans Experience Platform, les activités de la banque de données peuvent être surveillées sous la forme de journaux d’audit. Un journal d’audit indique **who** performance **what** et **when**, ainsi que d’autres données contextuelles qui peuvent vous aider à résoudre les problèmes liés aux flux de données pour aider votre entreprise à se conformer aux politiques de gestion des données d’entreprise et aux exigences réglementaires.

Chaque fois qu’un utilisateur crée, met à jour ou supprime un flux de données, un journal d’audit est créé pour enregistrer l’action. Il en va de même lorsqu’un utilisateur crée, met à jour ou supprime un mappage par le biais de [Préparation de données pour la collecte de données](./data-prep.md). Qu’il s’agisse d’un flux de données ou d’un mappage mis à jour, le journal d’audit résultant est classé sous la variable [!UICONTROL Datastreams] type de ressource.

Consultez la documentation relative à [journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md) pour plus d’informations sur la manière d’interpréter les journaux de datastreams et d’autres services pris en charge.

## Étapes suivantes

Ce guide fournit un aperçu général des flux de données et de leur utilisation dans la collecte de données et le traitement des données sensibles. Pour obtenir des instructions sur la configuration d’un nouveau flux de données, reportez-vous à la section [guide de configuration datastream](./configure.md).
