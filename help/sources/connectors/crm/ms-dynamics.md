---
keywords: Experience Platform;accueil;rubriques populaires;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Présentation du connecteur Source de Microsoft Dynamics
description: Découvrez comment connecter Microsoft Dynamics à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 50%

---

# Connecteur Microsoft Dynamics

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’un système CRM tiers. La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Microsoft Dynamics].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Mappage des champs de [!DNL Microsoft Dynamics] à XDM

Pour établir une connexion source entre [!DNL Microsoft Dynamics] et Experience Platform, les champs de données sources [!DNL Microsoft Dynamics] doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Experience Platform.

Pour plus d’informations sur les règles de mappage des champs entre les jeux de données [!DNL Microsoft Dynamics] et Experience Platform, consultez les sections suivantes :

- [Contacts](../adobe-applications/mapping/dynamics.md#contacts)
- [Prospects](../adobe-applications/mapping/dynamics.md#leads)
- [Comptes](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunités](../adobe-applications/mapping/dynamics.md#opportunities)
- [Rôles de contact d’opportunité](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagnes](../adobe-applications/mapping/dynamics.md#campaigns)
- [Liste marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Personnes membres de la liste marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Microsoft Dynamics] à [!DNL Experience Platform] à l’aide d’API ou de l’interface utilisateur :

## Connecter [!DNL Microsoft Dynamics] à [!DNL Experience Platform] à lʼaide dʼAPI

- [Créer une connexion de base Microsoft Dynamics à l’aide de l’API Flow Service](../../tutorials/api/create/crm/ms-dynamics.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connecter [!DNL Microsoft Dynamics] à [!DNL Experience Platform] à lʼaide de l’interface utilisateur

- [Créer une connexion source Microsoft Dynamics dans l’interface utilisateur](../../tutorials/ui/create/crm/dynamics.md)
- [Créer un flux de données pour une connexion CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
