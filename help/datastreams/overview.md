---
title: Présentation des trains de données
description: Découvrez comment les flux de données vous aident à connecter l’intégration de votre SDK Experience Platform côté client à des produits Adobe et à des destinations tierces.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: e3768a3f695abeedc9a3ce2fef591c6ecae9a897
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 70%

---

# Présentation des trains de données

Un flux de données représente la configuration côté serveur pour les SDK Web et Mobile Adobe Experience Platform. Bien que la commande [`configure`](/help/web-sdk/commands/configure/overview.md) du SDK gère les paramètres côté client (tels que `edgeDomain`), les flux de données gèrent toutes les autres configurations.

Lorsque vous envoyez une requête à l’Edge Network, `datastreamId` référence la banque de données dans laquelle les données sont envoyées. Cela vous permet de mettre à jour la configuration côté serveur sans modifier le code de votre site web.

Vous pouvez créer et gérer des trains de données en sélectionnant **[!UICONTROL Trains de données]** dans le volet de navigation de gauche de l’interface utilisateur d’Adobe Experience Platform ou de l’interface utilisateur de collecte des données.

![Onglet Trains de données dans l’interface utilisateur](assets/overview/datastreams-tab.png)

Pour plus d’informations sur la configuration d’un train de données dans l’interface utilisateur, voir le [guide de configuration](./configure.md).

## Gérer des données sensibles dans les trains de données {#sensitive}

>[!IMPORTANT]
>
>Le contenu de ce document ne constitue pas un avis juridique et n’est pas destiné à s’y substituer. Consultez le service juridique de votre entreprise pour obtenir des conseils concernant la gestion des données sensibles.

Les politiques de gestion des données d’entreprise et les exigences réglementaires augmentent les restrictions quant à la manière dont les données sensibles des clientes et des clients peuvent être collectées, traitées et utilisées. Cela concerne la collecte, le traitement et l’utilisation des données de santé protégées, qui sont soumises à des règlements comme la loi sur la portabilité et la responsabilité des assurances-maladie (Health Insurance Portability and Accountability Act, HIPAA).

Les flux de données proposent trois méthodes pour vous aider à gérer vos données sensibles en toute sécurité :

* [Chiffrement amélioré](#encryption)
* [Gouvernance des données](#governance)
* [Journaux d’audit](#audit-logs)

### Chiffrement amélioré {#encryption}

Toutes les données en transit par le réseau Edge sont transmises sur des connexions sécurisées et chiffrées à l’aide de [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si le train de données introduit des données dans Experience Platform, les données sont alors chiffrées au repos dans le lac de données d’Experience Platform. Pour plus d’informations, consultez le document sur le [chiffrement des données dans Experience Platform](../landing/governance-privacy-security/encryption.md).

### Gouvernance des données {#governance}

Les flux de données utilisent les fonctionnalités de gouvernance des données intégrées de l’Experience Platform pour empêcher l’envoi de données sensibles à des services non compatibles avec les HIPAA. En étiquetant des champs spécifiques qui contiennent des données sensibles dans vos schémas de trains de données, vous pouvez contrôler de manière granulaire quels champs de données peuvent être utilisés à des fins spécifiques.

La vidéo suivante présente une brève vue d’ensemble de la manière dont les restrictions d’utilisation des données sont configurées et appliquées pour les trains de données dans l’interface utilisateur :

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Dans Experience Platform, vous pouvez appliquer des [libellés d’utilisation des données sensibles](../data-governance/labels/reference.md#sensitive) aux schémas et aux champs contenant des données que votre organisation juge sensibles. Par exemple, le libellé `RHD` est utilisé pour désigner les informations protégées sur la santé ; le libellé `S1` représente les données de géolocalisation.

>[!NOTE]
>
>Pour plus d’informations sur la manière d’appliquer des libellés d’utilisation des données dans l’onglet [!UICONTROL Schémas] de l’interface utilisateur d’Experience Platform ou de l’interface utilisateur de collecte des données, consultez le [tutoriel sur l’étiquetage des schémas](../xdm/tutorials/labels.md).

Lorsque vous créez un flux de données, si le schéma sélectionné contient des libellés d’utilisation des données sensibles, vous pouvez uniquement configurer le flux de données pour envoyer ces données vers des destinations prêtes pour le HIPAA. Actuellement, Adobe Experience Platform est la seule destination conforme à la loi HIPAA prise en charge par les trains de données. Les autres services de destination, notamment Adobe Target, Adobe Analytics, Adobe Audience Manager, le transfert d’événement et les destinations Edge, sont désactivés pour les trains de données contenant des libellés d’utilisation des données sensibles.

Si un schéma est utilisé dans un train de données existant avec des services non conformes à la loi HIPAA, la tentative d’ajout d’un libellé d’utilisation des données sensibles au schéma génère un message de violation de politique et empêche l’action. Le message spécifie quel flux de données a déclenché la violation et suggère de supprimer tout service non compatible avec HIPAA du flux de données pour résoudre le problème.

### Journaux d’audit

Dans Experience Platform, les activités du train de données peuvent être surveillées sous la forme de journaux d’audit. Les journaux d’audit indiquent **qui** a effectué l’action **What** et **quand**, ainsi que d’autres données contextuelles qui peuvent vous aider à résoudre les problèmes liés aux jeux de données pour aider votre entreprise à se conformer aux politiques de gestion des données d’entreprise et aux exigences réglementaires.

Chaque fois qu’un utilisateur ou une utilisatrice crée, met à jour ou supprime un train de données, un journal d’audit est créé pour enregistrer l’action. Il en va de même lorsqu’un utilisateur ou une utilisatrice crée, met à jour ou supprime un mappage par le biais de la [Préparation de données pour la collecte de données](./data-prep.md). Qu’il s’agisse d’un train de données ou d’un mappage mis à jour, le journal d’audit résultant est classé sous le type de ressource [!UICONTROL Trains de données].

Consultez la documentation relative aux [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) pour plus d’informations sur la manière d’interpréter les journaux des trains de données et autres services pris en charge.

## Étapes suivantes

Ce guide fournit une vue d’ensemble complète des trains de données et de leur utilisation dans le cadre de la collecte de données et du traitement des données sensibles. Pour obtenir des instructions sur la configuration d’un nouveau train de données, voir le [guide de configuration des trains de données](./configure.md).
