---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;registre des schémas;modèle de données
solution: Experience Platform
title: Guide de l’API Schema Registry
description: L’API Schema Registry permet aux développeurs de gérer par programmation tous les schémas et toutes les ressources XDM (Experience Data Model) associées dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: c2ca679e046f59d05e2d12ca83bc1b2496b2288f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 10%

---

# Guide de l’API [!DNL Schema Registry]

[!DNL Schema Registry] est utilisé pour accéder à la bibliothèque de schémas dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles.

L’API Schema Registry fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les schémas et toutes les ressources XDM (Experience Data Model) associées disponibles pour vous dans Platform. Cela inclut ceux définis par Adobe, les partenaires [!DNL Experience Platform] et les fournisseurs dont vous utilisez les applications.

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

>[!IMPORTANT]
>
>XDM utilise le formatage du schéma JSON pour décrire et valider la structure des données d’expérience client ingérées. Avant d’utiliser l’API Schema Registry, il est vivement recommandé de consulter la [documentation officielle du schéma JSON](https://json-schema.org/) afin de mieux comprendre cette technologie sous-jacente.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [référence de l’API Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schémas

Les schémas XDM représentent et valident la structure et le format des données ingérées dans Platform. Un schéma est composé d’une classe et de zéro ou plusieurs groupes de champs de schéma. Vous pouvez créer, afficher, modifier et supprimer des schémas à l’aide du point de terminaison `/schemas`. Pour savoir comment utiliser ce point de terminaison, consultez le [guide du point de terminaison des schémas](./schemas.md).

Pour obtenir un guide détaillé sur la création d’un schéma complet dans l’API Schema Registry, y compris la création et l’ajout de groupes de champs et de types de données, consultez le [tutoriel sur la création de schémas d’API](../tutorials/create-schema-api.md).

## Comportements

Les comportements définissent la nature des données décrites par un schéma. Chaque classe XDM doit faire référence à un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Consultez le [guide de point de terminaison des comportements](./behaviors.md) pour savoir comment afficher les comportements disponibles dans l’API.

## Classes

Une classe définit la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir et détermine les groupes de champs pouvant être utilisés dans ces schémas. Chaque classe doit être associée à un comportement existant. Pour plus d’informations sur l’utilisation des classes dans l’API, consultez le [guide de point de terminaison des classes](./classes.md) .

## Groupes de champs

Les groupes de champs sont des composants réutilisables qui définissent un ou plusieurs champs qui représentent un concept particulier, comme une personne, une adresse postale ou un environnement de navigateur Web. Les groupes de champs sont destinés à être inclus dans un schéma qui met en oeuvre une classe compatible, en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Pour savoir comment utiliser les groupes de champs dans l’API, reportez-vous au [guide de point de terminaison des groupes de champs](./field-groups.md) .

## Types de données

Les types de données sont utilisés comme champs de type référence dans des classes ou des groupes de champs de la même manière que les champs littéraux de base. La différence majeure réside dans le fait que les types de données peuvent définir plusieurs sous-champs. Tout comme les groupes de champs dans le fait qu’ils permettent l’utilisation cohérente d’une structure à plusieurs champs, les types de données sont plus flexibles, car ils peuvent être inclus n’importe où dans la structure du schéma, tandis que les groupes de champs ne peuvent être ajoutés qu’au niveau racine. Pour plus d’informations sur l’utilisation des types de données dans l’API, consultez le [guide de point de terminaison des types de données](./data-types.md) .

## Descripteurs

Descripteurs sont des ensembles de métadonnées affectés à des champs spécifiques au sein d’un schéma, fournissant divers détails contextuels, y compris la manière dont ces champs (et le schéma lui-même) sont associés à d’autres schémas. Une ou plusieurs entités de descripteur peuvent être appliquées à chaque schéma, et plusieurs types de descripteurs différents peuvent servir à des fins différentes. Pour plus d’informations sur l’utilisation des descripteurs dans l’API, consultez le [guide de point de terminaison des descripteurs](./descriptors.md) , ainsi qu’un aperçu des différents types de descripteurs et de leurs cas d’utilisation.

## Unions

Bien que Platform vous permette de composer des schémas pour des cas d’utilisation particuliers, il vous permet également de composer une &quot;union&quot; de schémas appartenant à une classe spécifique. Un schéma d’union agrège les champs de tous les schémas qui partagent la même classe en une seule représentation. En activant un schéma à utiliser avec [Real-time Customer Profile](../../profile/home.md), ce schéma est inclus dans l’union pour sa classe particulière. Par conséquent, les schémas d’union ne peuvent pas être modifiés directement et peuvent uniquement être affectés par l’inclusion ou l’exclusion de schémas à utiliser dans Profile.

Pour savoir comment afficher les unions dans l’API Schema Registry, consultez le [guide de point de terminaison des unions](./unions.md).

## Exporter/Importer

L’API Schema Registry vous permet de transférer et de partager des ressources XDM entre des environnements de test et des organisations IMS. Pour tout schéma, groupe de champs ou type de données, vous pouvez générer une payload d’exportation contenant la structure de la ressource et les ressources dépendantes. Cette payload peut ensuite être utilisée pour importer la ressource dans un environnement de test de destination et une organisation IMS.

Pour plus d’informations sur l’utilisation de ces points de terminaison, consultez le [guide de points de terminaison export/import](./export-import.md) .

## Sample data

Vous pouvez générer des exemples de données pour n’importe quel schéma spécifié dans la bibliothèque de schémas. L’objet de réponse renvoyé peut ensuite être utilisé comme source d’ingestion de données.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide d’exemple de point de terminaison de données](./sample-data.md) .

## Journal d’audit

Le registre des schémas conserve un journal de toutes les modifications apportées à une ressource (classe, groupe de champs, type de données ou schéma) entre différentes mises à jour. Vous pouvez récupérer le journal d’une ressource particulière en fournissant ses `$id` ou `meta:altId` dans le chemin d’accès d’une requête de GET vers ce point de terminaison.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide de point de terminaison du journal d’audit](./audit-log.md) .

## Étapes suivantes

Pour commencer à effectuer des appels à lʼaide de lʼAPI Schema Registry, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez lʼun des guides des points dʼentrée pour savoir comment utiliser des points dʼentrée spécifiques.
