---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des jeux de données
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Présentation des jeux de données

Toutes les données qui ont été correctement ingérées dans Adobe Experience Platform sont conservées dans Data Lake en tant que jeux de données. Un jeu de données est un concept d&#39;enregistrement et de gestion pour une collection de données, généralement un tableau, qui contient un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données qu’ils stockent.

Ce document fournit un aperçu général des jeux de données dans la plateforme d’expérience.

## Création de jeux de données et suivi des métadonnées

Catalog Service est le système d’enregistrement de l’emplacement et du lignage des données dans la plate-forme d’expérience. Il est utilisé pour créer et gérer des jeux de données. Le catalogue suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma de modèle de données d’expérience (XDM) auquel le jeu de données est conforme (expliqué dans la section suivante) et le nombre d’enregistrements ingérés dans ce jeu de données.

See the [Catalog Service overview](../home.md) for more information.

## Imposer des contraintes aux données des jeux de données

Le modèle de données d’expérience (XDM) est le cadre normalisé selon lequel la plate-forme organise les données d’expérience client. Toutes les données ingérées dans Platform doivent être conformes à un schéma XDM prédéfini avant de pouvoir être conservées dans Data Lake en tant que jeu de données.

Tous les jeux de données contiennent une référence au schéma XDM qui limite le format et la structure des données qu’ils peuvent stocker. Si vous tentez de transférer des données vers un jeu de données non conforme au schéma XDM du jeu de données, l&#39;assimilation échouera.

Pour plus d&#39;informations sur XDM, consultez la présentation [du système](../../xdm/home.md)XDM.

## Incorporation de données dans des jeux de données

L’importation de données de la plate-forme Adobe Experience représente les multiples méthodes par lesquelles la plate-forme ingère des données provenant de diverses sources. Quelle que soit la méthode d’assimilation, toutes les données correctement assimilées sont converties en fichiers de commandes. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Ces fichiers de commandes sont ensuite ajoutés aux jeux de données dédiés et conservés dans Data Lake.

See the [Data Ingestion overview](../../ingestion/home.md) for more information.

## Application de libellés d’utilisation à des jeux de données

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données client afin de garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. L’utilisation de l’étiquette et de l’application de l’utilisation des données (DULE) en tant que cadre de base vous permet d’appliquer des étiquettes d’utilisation afin de classer les données en fonction des stratégies d’utilisation qui s’appliquent à ces données.

Les étiquettes d’utilisation des données peuvent être appliquées à des jeux de données entiers ou à des champs de jeux de données individuels. Les étiquettes ajoutées au niveau du jeu de données sont héritées de tous les champs de ce jeu de données.

Pour plus d’informations sur le service, consultez l’aperçu [de la gouvernance des](../../data-governance/home.md) données. Pour savoir comment utiliser les libellés d’utilisation dans l’interface utilisateur de la plateforme d’expérience, voir le guide [d’utilisation des libellés d’utilisation des](../../data-governance/labels/user-guide.md)données.

## Jeu de données dans les services de plateformes en aval

Une fois que les jeux de données ont été utilisés pour stocker des données imbriquées, ces jeux de données sont ensuite utilisés par les services Plateforme en aval pour mettre à jour les profils client, obtenir des informations grâce à l’apprentissage automatique, etc.

Voici une liste de services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour plus d&#39;informations.

* [API](../../data-access/home.md)d&#39;accès aux données : Permet d’accéder au contenu des fichiers stockés dans des jeux de données et de le télécharger.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Associe les identités entre les périphériques et les systèmes, en liant les jeux de données en fonction des champs d&#39;identité définis par les schémas XDM auxquels ils se conforment.
* [Profil](../../profile/home.md)client en temps réel : Utilise Identity Service pour créer des profils clients détaillés à partir de vos jeux de données en temps réel. Le client en temps réel extrait les données de Data Lake et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Permet de créer des segments et de générer des audiences à partir des données de Profil client en temps réel. Ces audiences peuvent ensuite être exportées vers leurs propres ensembles de données dans le lac Data.
* [Espace de travail](../../data-science-workspace/home.md)des données de la plateforme Adobe Experience Platform : Utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour découvrir des informations dans des jeux de données volumineux.
* [Adobe Experience Platform Requête Service](../../query-service/home.md): Permet d’utiliser des données SQL standard pour la requête dans la plateforme Experience Platform, de joindre des jeux de données dans Data Lake et de capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans rapports, Data Science Workspace ou le Profil client en temps réel.
* [Service](../../decisioning-service/home.md)de prise de décision Adobe Experience Platform : Exploite le Profil client en temps réel pour déterminer le choix le plus probable qu&#39;un client fera à partir d&#39;un ensemble d&#39;options, en fonction des données comportementales que le Profil extrait des jeux de données activés.

## Étapes suivantes

En lisant ce document, vous avez été familiarisé avec les principales utilisations des jeux de données dans la plate-forme d’expérience, ainsi qu’avec les divers services de plateformes qui utilisent les jeux de données. Pour plus d&#39;informations sur les nombreuses manières d&#39;utiliser les jeux de données dans Platform, veuillez consulter la documentation du service liée dans cette présentation.

Pour savoir comment interagir avec des jeux de données dans l’interface utilisateur de la plate-forme d’expérience, voir le guide [d’utilisation](user-guide.md)des jeux de données.