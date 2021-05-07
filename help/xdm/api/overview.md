---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre des schémas ; registre des Schémas ;
solution: Experience Platform
title: Guide de l'API du registre de schémas
description: L’API Schéma Registry permet aux développeurs de gérer par programmation tous les schémas et les ressources XDM (Experience Data Model) associées dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# [!DNL Schema Registry] Guide des API

[!DNL Schema Registry] est utilisé pour accéder à la bibliothèque de Schémas dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles.

L’API de registre de Schémas fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les schémas et les ressources XDM (Experience Data Model) connexes disponibles dans Platform. Cela inclut les solutions définies par Adobe, [!DNL Experience Platform] partenaires et fournisseurs dont vous utilisez les applications.

Ces points de terminaison sont décrits ci-dessous. Consultez les guides individuels des points de terminaison pour plus de détails et consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

>[!IMPORTANT]
>
>XDM utilise le formatage de Schéma JSON pour décrire et valider la structure des données d’expérience client assimilées. Avant de travailler avec l&#39;API Schéma Registry, il est vivement recommandé de consulter la [documentation officielle du Schéma JSON](https://json-schema.org/) pour mieux comprendre cette technologie sous-jacente.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la [référence de l&#39;API de registre de Schémas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schémas

Les schémas XDM représentent et valident la structure et le format des données ingérées dans la plate-forme. Un schéma est composé d&#39;une classe et de zéro ou plusieurs groupes de champs de schéma. Vous pouvez créer, vue, modifier et supprimer des schémas à l’aide du point de terminaison `/schemas`. Pour savoir comment utiliser ce point de terminaison, consultez le [guide des points de terminaison des schémas](./schemas.md).

Pour obtenir un guide détaillé sur la création d&#39;un schéma complet dans l&#39;API de registre des Schémas, y compris la création et l&#39;ajout de groupes de champs et de types de données, consultez le [didacticiel sur la création de schémas d&#39;API](../tutorials/create-schema-api.md).

## Comportements

Les comportements définissent la nature des données qu’un schéma décrit. Chaque classe XDM doit faire référence à un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Consultez le [guide des points de terminaison comportementaux](./behaviors.md) pour savoir comment vue les comportements disponibles dans l&#39;API.

## Classes

Une classe définit la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir et détermine quels groupes de champs peuvent être utilisés dans ces schémas. Chaque classe doit être associée à un comportement existant. Pour plus d&#39;informations sur l&#39;utilisation des classes dans l&#39;API, reportez-vous au [guide des points de terminaison des classes](./classes.md).

## Groupes de champs

Les groupes de champs sont des composants réutilisables qui définissent un ou plusieurs champs qui représentent un concept particulier, tel qu’une personne, une adresse postale ou un environnement de navigateur Web. Les groupes de champs sont destinés à être inclus dans un schéma qui implémente une classe compatible, en fonction du comportement des données qu’ils représentent (enregistrements ou séries chronologiques). Consultez le [guide des points de terminaison des groupes de champs](./field-groups.md) pour savoir comment utiliser les groupes de champs dans l&#39;API.

## Types de données

Les types de données sont utilisés comme champs de type référence dans les classes ou les groupes de champs de la même manière que les champs littéraux de base, la différence majeure étant que les types de données peuvent définir plusieurs sous-champs. Bien que semblables aux groupes de champs en ce qu’ils permettent l’utilisation cohérente d’une structure à champs multiples, les types de données sont plus flexibles car ils peuvent être inclus n’importe où dans la structure de schéma alors que les groupes de champs ne peuvent être ajoutés qu’au niveau racine. Pour plus d&#39;informations sur l&#39;utilisation des types de données dans l&#39;API, consultez le [guide des points de terminaison des types de données](./data-types.md).

## Descripteurs

Descripteurs sont des ensembles de métadonnées affectés à des champs spécifiques au sein d’un schéma, fournissant divers détails contextuels, notamment la manière dont ces champs (et le schéma lui-même) sont liés à d’autres schémas. Chaque schéma peut comporter une ou plusieurs entités descripteurs qui lui sont appliquées et plusieurs types de descripteurs différents peuvent servir à des fins différentes. Pour plus d&#39;informations sur l&#39;utilisation des descripteurs dans l&#39;API, consultez le [guide des points de terminaison descripteurs](./descriptors.md) et un aperçu des différents types de descripteurs et de leurs cas d&#39;utilisation.

## Unions

Bien que Plateforme vous permette de composer des schémas pour des cas d&#39;utilisation particuliers, elle vous permet également de composer une &quot;union&quot; de schémas appartenant à une classe spécifique. Un schéma d’union agrégat les champs de tous les schémas qui partagent la même classe en une seule représentation. En activant un schéma à utiliser avec [Profil client en temps réel](../../profile/home.md), ce schéma est inclus dans l’union pour sa classe particulière. En tant que tel, les schémas d&#39;union ne peuvent pas être modifiés directement et ne peuvent être affectés que par l&#39;inclusion ou l&#39;exclusion de schémas destinés à être utilisés dans le Profil.

Pour savoir comment vue des unions dans l&#39;API de registre des Schémas, consultez le [guide des points de terminaison des unions](./unions.md).

## Exporter/Importer

L&#39;API Schéma Registry vous permet de transférer et de partager des ressources XDM entre des sandbox et des organisations IMS. Pour tout schéma, groupe de champs ou type de données, vous pouvez générer une charge utile d’exportation contenant la structure de la ressource et les ressources dépendantes. Cette charge utile peut ensuite être utilisée pour importer la ressource dans un sandbox de destination et une organisation IMS.

Pour plus d&#39;informations sur l&#39;utilisation de ces points de terminaison, consultez le [guide des points de terminaison export/import](./export-import.md).

## Sample data

Vous pouvez générer des données d’exemple pour n’importe quel schéma spécifié dans la bibliothèque de Schémas. L&#39;objet de réponse renvoyé peut alors être utilisé comme source d&#39;assimilation de données.

Pour plus d’informations sur l’utilisation de ce point de terminaison, consultez le [guide des points de terminaison de données d’exemple](./sample-data.md).

## Journal d’audit

Le registre des Schémas tient un journal de toutes les modifications qui ont été apportées à une ressource (classe, groupe de champs, type de données ou schéma) entre différentes mises à jour. Vous pouvez récupérer le journal d&#39;une ressource particulière en fournissant ses `$id` ou `meta:altId` dans le chemin d&#39;une demande de GET vers ce point de terminaison.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez le [guide du point de terminaison du journal d&#39;audit](./audit-log.md).

## Étapes suivantes

Pour commencer à lancer des appels à l&#39;aide de l&#39;API Schéma Registry, lisez le [guide de prise en main](./getting-started.md), puis sélectionnez l&#39;un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques.
