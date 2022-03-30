---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
source-git-commit: 04d35137a301492794ab8c0c67183cf5c76f2105
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 30%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 30 mars 2022**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Journaux d’audit](#audit-logs)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Modèle de données d’expérience (XDM)](#xdm)
- [[!DNL Query Service]](#query-service)
- [Sources](#sources)

## Journaux d’audit {#audit-logs}

Experience Platform vous permet de contrôler l’activité des utilisateurs pour divers services et fonctionnalités. Les journaux d’audit fournissent des informations sur qui a effectué quoi et quand.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Logs d’audit pour le jeu de données, le schéma, la classe, le groupe de champs, le type de données, le sandbox, la destination, le segment, la stratégie de fusion, l’attribut calculé, le profil de produit et le compte (Adobe). | Il s’agit des ressources enregistrées par les journaux d’audit. Si la fonction est activée, les journaux d’audit sont automatiquement collectés au fur et à mesure de l’activité. Vous n’avez pas besoin d’activer manuellement la collecte des journaux. |
| Exportation des journaux d’audit | Les journaux d’audit peuvent être téléchargés en tant que `CSV` ou `JSON` fichier . Les fichiers générés sont enregistrés directement sur votre machine. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les journaux d’audit dans Platform, reportez-vous à la section [aperçu des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles règles d’alerte | Deux nouvelles règles d’alerte sont désormais disponibles pour les sources liées à l’ingestion de données. Consultez la présentation des [règles d’alerte](../../observability/alerts/rules.md) pour obtenir la liste mise à jour des types d’alerte. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les alertes dans Platform, consultez l’[aperçu des alertes](../../observability/alerts/overview.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit plusieurs [!DNL dashboards] grâce à laquelle vous pouvez afficher des informations importantes sur les données de votre organisation, telles qu’elles sont capturées lors d’instantanés quotidiens.

### Tableaux de bord de profil

Le tableau de bord Profils affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils en Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget Profils non segmentés | Le widget fournit le nombre total de tous les profils qui ne sont associés à aucun segment. Le nombre généré est précis à partir du dernier instantané et représente l’opportunité d’activation du profil à l’échelle de votre organisation. Voir [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets) pour plus d’informations. |
| Widget de tendance Profils non segmentés | Ce widget fournit une représentation graphique linéaire pour le nombre de profils qui ne sont associés à aucun segment sur une période donnée. La tendance peut être visualisée sur des périodes de 30 jours, 90 jours et 12 mois. Voir [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets) pour plus d’informations. |
| Profils non segmentés par widget Identité | Ce widget classe le nombre total de profils non segmentés en fonction de leur identifiant unique. Les données sont visualisées dans un graphique à barres. Voir [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets) pour plus d’informations. |
| Widget de profils d’identité unique | Ce widget fournit un comptage des profils de votre organisation qui n’ont qu’un seul type d’ID qui crée leur identité, soit un email, soit un ECID. Voir [documentation sur les widgets standard des profils](../../dashboards/guides/profiles.md#standard-widgets) pour plus d’informations. |

Pour plus d’informations sur les tableaux de bord des profils, reportez-vous à la section [Présentation des tableaux de bord des profils](../../dashboards/guides/profiles.md).

### Tableaux de bord des destinations

Le tableau de bord Destinations affiche un instantané des destinations que votre entreprise a activées dans Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget de comptage des destinations | Le widget fournit le nombre total de points de terminaison disponibles où une audience peut être activée et diffusée dans le système. Ce nombre inclut les destinations principales et inactives. Voir [documentation du widget standard des destinations](../../dashboards/guides/destinations.md#standard-widgets) pour plus d’informations. |

Pour plus d’informations sur les tableaux de bord des destinations dans Platform, reportez-vous à la section [Présentation des tableaux de bord des destinations](../../dashboards/guides/destinations.md).

## Modèle de données d’expérience (XDM) {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Ajout ou suppression de champs standard individuels pour un schéma | L’interface utilisateur de l’éditeur de schémas vous permet désormais d’ajouter des parties de groupes de champs standard à vos schémas, offrant ainsi plus de flexibilité aux champs que vous choisissez d’inclure sans avoir à créer de ressources personnalisées à partir de zéro.<br><br>Vous pouvez désormais également définir des champs personnalisés ad hoc directement dans la structure du schéma et les affecter à un nouveau groupe de champs personnalisés ou existant sans avoir à créer ni à modifier au préalable le groupe de champs.<br><br>Consultez le guide sur la [création et modification de schémas dans l’interface utilisateur](../../xdm/ui/resources/schemas.md) pour plus d’informations sur ces nouveaux workflows. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, voir [Présentation du système XDM](../../xdm/home.md).

## Query Service {#query-service}

[!DNL Query Service] vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans Data Science Workspace ou pour l’ingestion dans Real-time Customer Profile.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| `table_exists` | La nouvelle commande de fonctionnalité permet de confirmer si un tableau existe actuellement dans le système. La commande renvoie une valeur booléenne : `true` si le tableau **does** existent et `false` si le tableau fonctionne **not** existent. Voir [Documentation sur la syntaxe SQL](../../query-service/sql/syntax.md) pour plus d’informations. |

Pour plus d’informations sur les fonctionnalités disponibles, reportez-vous à la section [Présentation de Query Service](../../query-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services CRM et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer l’ingestion des données tout au long de l’opération.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles sources désormais disponibles pour l’utilisation B2B | Vous pouvez désormais utiliser toutes les sources disponibles sur Platform pour les cas d’utilisation B2B. Voir [catalogue de sources](../../sources/home.md) pour obtenir une liste complète des sources disponibles. |
| Disponibilité générale des nouvelles [!DNL Oracle Eloqua] source | Vous pouvez désormais utiliser la variable [!DNL Oracle Eloqua] pour ingérer facilement des données à partir de vos [!DNL Oracle Eloqua] instance (compte, campagne, contacts) vers Platform. Consultez la documentation relative à [création d’un [!DNL Oracle Eloqua] connexion source](../../sources/connectors/oracle-eloqua.md) pour plus d’informations. |
| Améliorations de l’API pour [!DNL Data Landing Zone] | Le [!DNL Data Landing Zone] La source prend désormais en charge la détection automatique des propriétés de fichier lors de l’utilisation de la fonction [!DNL Flow Service] API. Consultez la documentation relative à [création d’un [!DNL Data Landing Zone] connexion source](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
