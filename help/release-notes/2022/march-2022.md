---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2022
description: Les notes de mise à jour de mars 2022 pour Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 98%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 30 mars 2022**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Journaux d’audit](#audit-logs)
- [Comptes associés dans Real-Time CDP B2B Edition](#related-accounts)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Collecte de données](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Sources](#sources)

## Journaux d’audit {#audit-logs}

Experience Platform vous permet d’auditer l’activité des utilisateurs pour plusieurs services et fonctionnalités. Les journaux d’audit fournissent des informations sur ce qui a été fait, par qui et à quel moment.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Journaux d’audit pour jeu de données, schéma, classe, groupe de champs, type de données, sandbox, destination, segment, politique de fusion, attribut calculé, profil de produit et compte (Adobe) | Ces éléments sont les ressources enregistrées par les journaux d’audit. Si la fonction est activée, les journaux d’audit sont automatiquement collectés au fur et à mesure de l’activité. Vous n’avez pas besoin d’activer manuellement la collecte des journaux. |
| Exportation des journaux d’audit | Les journaux d’audit peuvent être téléchargés en tant que fichier `CSV` ou `JSON`. Les fichiers générés sont directement enregistrés sur votre machine. |

{style="table-layout:auto"}

Pour plus d’informations sur les journaux d’audit dans Platform, consultez la [présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Comptes associés dans Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La fonctionnalité Comptes associés est disponible uniquement pour les clients de Real-Time CDP B2B Edition.

Les entreprises B2B ont souvent leurs informations client stockées dans plusieurs systèmes, chacun ne contenant que des données partielles, voire conflictuelles, pour la même entité commerciale physique. Il est donc très difficile d’avoir une visualisation précise de leurs clients, ce qui réduit l’efficacité et l’efficience de leurs efforts de marketing et de vente B2B. Grâce à la fonctionnalité Comptes associés, [!DNL Real-Time CDP B2B] vous montre désormais une liste de comptes similaires au compte que vous être en train de parcourir. Vous pouvez inclure les comptes associés dans vos définitions de segment pour élargir votre portée ou appliquer des critères plus larges dans vos segments.

Pour en savoir plus sur cette fonctionnalité, consultez les pages de documentation suivantes :

- [Présentation des comptes associés dans Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Comment utiliser les comptes associés dans les définitions de segment ?](../../rtcdp/segmentation/b2b.md#related-accounts)

Pour en savoir plus sur Real-Time CDP édition B2B, consultez la [présentation](../../rtcdp/overview.md).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles règles d’alerte | Deux nouvelles règles d’alerte sont désormais disponibles pour les sources liées à l’ingestion des données. Consultez la présentation des [règles d’alerte](../../observability/alerts/rules.md) pour obtenir la liste mise à jour des types d’alerte. |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes dans Platform, consultez l’[aperçu des alertes](../../observability/alerts/overview.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux [!DNL dashboards] grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

### Tableaux de bord des profils

Le tableau de bord Profils affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils en Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget profils non segmentés | Le widget fournit le nombre total de profils qui ne sont associés à aucun segment. Le nombre, généré à partir du dernier instantané, est précis et souligne l’opportunité d’activation de profils dans votre entreprise. Pour plus d’informations, consultez la [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget tendance des profils non segmentés | Ce widget fournit une représentation graphique linéaire du nombre de profils qui ne sont associés à aucun segment sur une période donnée. La tendance peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. Pour plus d’informations, consultez la [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget profils non segmentés par identité | Ce widget classe le nombre total de profils non segmentés en fonction de leur identifiant unique. Les données sont représentées dans un histogramme. Pour plus d’informations, consultez la [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget profils à identité unique | Ce widget fournit le nombre de profils de votre entreprise qui n’ont qu’un seul type d’identifiant qui crée leur identité, soit un email, soit un ECID (identifiant Experience Cloud). Pour plus d’informations, consultez la [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets). |

{style="table-layout:auto"}

Pour plus d’informations sur les tableaux de bord des profils, consultez la [présentation des tableaux de bord des profils](../../dashboards/guides/profiles.md).

### Tableaux de bord des destinations

Le tableau de bord des destinations affiche un instantané des destinations activées par votre entreprise dans Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget de comptage des destinations | Le widget fournit le nombre total de points d’entrée disponibles où une audience peut être activée et diffusée dans le système. Ce nombre inclut les destinations principales et inactives. Pour plus d’informations, consultez la [documentation du widget standard des destinations](../../dashboards/guides/destinations.md#standard-widgets). |

{style="table-layout:auto"}

Pour plus d’informations sur les tableaux de bord des destinations dans Platform, consultez la [présentation des tableaux de bord des destinations](../../dashboards/guides/destinations.md).

## Collecte de données {#data-collection}

Platform fournit un ensemble de technologies qui vous permettent de collecter des données d’expérience client à partir de sources côté client. Vous pouvez ensuite les envoyer au réseau Adobe Experience Platform Edge afin qu’elles soient enrichies, transformées et distribuées vers des destinations Adobe ou autres qu’Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Paramètres globaux de flux de données | Vous pouvez désormais configurer plusieurs nouveaux paramètres globaux lors de la configuration d’un flux de données : géolocalisation, cookie des identifiants internes et synchronisation des identifiants tiers. Pour plus d’informations, consultez la section sur la [configuration d’un flux de données](../../datastreams/overview.md#create) du guide de l’interface utilisateur des flux de données. |
| [API d’Edge Network Server](../../server-api/overview.md) | Le serveur API permet aux clients d’interagir avec Edge Experience Platform Network à l’aide d’un nouveau point d’entrée authentifié, afin d’alimenter plusieurs cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. |

Pour plus d’informations sur la collecte de données dans Platform, consultez la [Présentation de la collecte de données](../../collection/home.md).

## Query Service {#query-service}

[!DNL Query Service] vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| `table_exists` | La commande de la nouvelle fonctionnalité sert à confirmer si un tableau existe actuellement dans le système ou non. La commande renvoie une valeur booléenne : `true` si le tableau **existe** et `false` si le tableau **n’existe pas**. Pour plus d’informations, consultez la [documentation sur la syntaxe SQL](../../query-service/sql/syntax.md). |

{style="table-layout:auto"}

Pour plus d’informations sur les fonctionnalités disponibles, consultez la section [présentation de Query Service](../../query-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client (CRM) et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer entièrement l’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles sources désormais disponibles pour l’utilisation B2B | Vous pouvez désormais utiliser toutes les sources disponibles sur Platform pour les cas d’utilisation B2B. Pour obtenir une liste complète des sources disponibles, consultez le [catalogue des sources](../../sources/home.md). |
| Disponibilité générale de la nouvelle source [!DNL Oracle Eloqua] | Vous pouvez désormais utiliser la source [!DNL Oracle Eloqua] pour ingérer facilement des données à partir de votre instance [!DNL Oracle Eloqua] (compte, campagne, contacts) vers Platform. Pour plus d’informations, consultez la documentation sur la [création d’une connexion source  [!DNL Oracle Eloqua] ](../../sources/connectors/marketing-automation/oracle-eloqua.md). |
| Améliorations de l’API pour [!DNL Data Landing Zone] | La source [!DNL Data Landing Zone] prend désormais en charge la détection automatique des propriétés de fichier lors de l’utilisation de l’API [!DNL Flow Service]. Pour plus d’informations, consultez la documentation sur la [création d’une connexion source [!DNL Data Landing Zone] ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
