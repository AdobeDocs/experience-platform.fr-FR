---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des jeux de données
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad

---


# Présentation des jeux de données

Toutes les données correctement assimilées à Adobe Experience Platform sont conservées sous forme de jeux de données dans Data Lake. Un jeu de données est un concept de  et de gestion  pour une collection de données, généralement un tableau, qui contient un (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données qu’ils stockent.

Ce présente un aperçu général des jeux de données dans la plateforme d’expérience.

## Création de jeux de données et suivi des métadonnées

Le service de catalogue est le système d’enregistrement de l’emplacement et de la lignée des données dans la plateforme d’expérience. Il est utilisé pour créer et gérer des jeux de données. Le catalogue suit les métadonnées de chaque jeu de données, ce qui inclut une référence au modèle de données d’expérience (XDM)  le jeu de données est conforme (expliqué dans la section suivante) et le nombre d’enregistrements assimilés à ce jeu de données.

See the [Catalog Service overview](../home.md) for more information.

## Application de contraintes sur les données de jeu de données

Le modèle de données d’expérience (XDM) est le cadre normalisé selon lequel la plateforme organise les données d’expérience client. Toutes les données ingérées dans Platform doivent être conformes à un XDM prédéfini avant de pouvoir être conservées dans Data Lake en tant qu&#39;ensemble de données.

Tous les jeux de données contiennent une référence au XDM qui limite le format et la structure des données qu’ils peuvent stocker. Toute tentative de transfert de données vers un jeu de données non conforme au XDM du jeu de données entraînera l’échec de l’assimilation.

Pour plus d&#39;informations sur XDM, consultez la présentation [du système](../../xdm/home.md)XDM.

## Incorporation de données dans des jeux de données

L’administration des données d’Adobe Experience Platform représente les méthodes multiples par lesquelles Platform imprime des données de diverses sources. Quelle que soit la méthode d’assimilation, toutes les données assimilées sont converties en fichiers de commandes. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Ces fichiers de commandes sont ensuite ajoutés aux jeux de données dédiés et conservés dans Data Lake.

See the [Data Ingestion overview](../../ingestion/home.md) for more information.

## Application de libellés d’utilisation aux jeux de données

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données client afin de vous assurer de la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. L’utilisation de l’outil d’étiquetage et d’application de la loi (DULE) en tant que cadre de base de l’utilisation des données vous permet d’appliquer des étiquettes d’utilisation afin de classer les données en fonction des stratégies d’utilisation qui s’appliquent à ces données.

Les libellés d’utilisation des données peuvent être appliqués à des jeux de données entiers ou à des champs de jeux de données individuels. Les étiquettes ajoutées au niveau du jeu de données sont héritées par tous les champs de ce jeu de données.

Pour plus d’informations sur le service, consultez l’aperçu [de la gouvernance des](../../data-governance/home.md) données. Pour savoir comment utiliser les libellés d’utilisation dans l’interface utilisateur de la plateforme d’expérience, voir le guide [d’utilisation des libellés d’utilisation des](../../data-governance/labels/user-guide.md)données.

## Jeu de données dans les services Plateforme en aval

Une fois que les jeux de données ont été utilisés pour stocker les données assimilées, ces jeux de données sont ensuite utilisés par les services Plateforme en aval pour mettre à jour les  du client, obtenir des informations grâce à l’apprentissage automatique, etc.

Voici un  de services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour plus d&#39;informations.

* [API](../../data-access/home.md)d&#39;accès aux données : Permet d’accéder au contenu des fichiers stockés dans des jeux de données et de le télécharger.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Associe les identités entre les périphériques et les systèmes, en liant les jeux de données en fonction des champs d’identité définis par le XDM  auxquels ils se conforment.
* [](../../profile/home.md)du client en temps réel : Exploite Identity Service pour créer en temps réel des clients détaillés à partir de vos jeux de données. Le client en temps réel extrait les données du lac Data et conserve les  des clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Permet de créer des segments et de générer des   à partir de vos données d’client en temps réel. Ces  de  peuvent ensuite être exportés vers leurs propres jeux de données dans le lac Data.
* [Espace de travail](../../data-science-workspace/home.md)des données de la plateforme Adobe Experience Platform : Utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour découvrir des informations dans des jeux de données volumineux.
* [Service](../../query-service/home.md)de Adobe Experience Platform : Vous permet d’utiliser SQL standard pour des données dans la plateforme d’expérience, de joindre des jeux de données dans Data Lake et de capturer les résultats  du sous la forme d’un nouveau jeu de données à utiliser dans le cadre de l’utilisation de la plateforme de données, de l’espace de travail des sciences de données ou de l’client en temps réel.
* [Service](../../decisioning-service/home.md)de prise de décision Adobe Experience Platform : Exploite les  du client en temps réel pour déterminer le choix le plus probable qu&#39;un client fera à partir d&#39;un ensemble d&#39;options, en fonction des données comportementales que le  extrait des jeux de données activés.

## Étapes suivantes

En lisant ce , vous avez été familiarisé avec les principales utilisations des jeux de données dans Experience Platform, ainsi qu’avec les différents services de plateformes qui utilisent les jeux de données. Pour plus d&#39;informations sur les nombreuses manières dont les jeux de données sont utilisés dans Platform, veuillez consulter la documentation du service liée tout au long de cet aperçu.

Pour savoir comment interagir avec des jeux de données dans l’interface utilisateur de la plateforme d’expérience, voir le guide [de l’utilisateur](user-guide.md)des jeux de données.