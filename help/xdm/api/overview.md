---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Guide de développement de l’API Schema Registry
description: 'L''API Schéma Registry vous permet de gérer par programmation tous les schémas et les ressources XDM connexes disponibles dans l''Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 7%

---


# Guide du développeur de l’API [!DNL Schema Registry]

[!DNL Schema Registry] est utilisé pour accéder à la bibliothèque de Schémas dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles.

L’API de registre de Schémas fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les schémas et les ressources XDM (Experience Data Model) connexes disponibles dans Platform. Cela inclut les solutions définies par Adobe, [!DNL Experience Platform] partenaires et fournisseurs dont vous utilisez les applications.

Ces points de terminaison sont décrits ci-dessous. Consultez les guides individuels des points de terminaison pour plus de détails et consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

>[!IMPORTANT]
>
>XDM utilise le formatage de Schéma JSON pour décrire et valider la structure des données d’expérience client assimilées. Avant de travailler avec l&#39;API Schéma Registry, il est vivement recommandé de consulter la [documentation officielle du Schéma JSON](https://json-schema.org/) pour mieux comprendre cette technologie sous-jacente.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la [référence de l&#39;API de registre de Schémas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schémas

Les schémas XDM représentent et valident la structure et le format des données ingérées dans la plate-forme. Un schéma est composé d’une classe et de zéro, un ou plusieurs mixins. Vous pouvez créer, vue, modifier et supprimer des schémas à l’aide du point de terminaison `/schemas`. Pour savoir comment utiliser ce point de terminaison, consultez le [guide des points de terminaison des schémas](./schemas.md).

Pour obtenir un guide détaillé sur la création d&#39;un schéma complet dans l&#39;API de registre des Schémas, y compris la création et l&#39;ajout de mixins et de types de données, consultez le [didacticiel sur la création de schémas d&#39;API](../tutorials/create-schema-api.md).

## Comportements

Les comportements définissent la nature des données qu’un schéma décrit. Chaque classe XDM doit faire référence à un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Consultez le [guide des points de terminaison comportementaux](./behaviors.md) pour savoir comment vue les comportements disponibles dans l&#39;API.

## Classes

Une classe définit la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir et détermine quels mixins peuvent être utilisés dans ces schémas. Chaque classe doit être associée à un comportement existant. Pour plus d&#39;informations sur l&#39;utilisation des classes dans l&#39;API, reportez-vous au [guide des points de terminaison des classes](./classes.md).

## Mélanges

Les mixins sont des composants réutilisables qui définissent un ou plusieurs champs qui représentent un concept particulier, tel qu’une personne individuelle, une adresse postale ou un environnement de navigateur Web. Les mixins sont destinés à être inclus dans un schéma qui implémente une classe compatible, en fonction du comportement des données qu&#39;ils représentent (enregistrement ou séries chronologiques). Consultez le [guide des points de terminaison des mixins](./mixins.md) pour savoir comment utiliser les mixins dans l’API.

## Types de données

Les types de données sont utilisés comme champs de type référence dans les classes ou les mixins de la même manière que les champs littéraux de base, la différence majeure étant que les types de données peuvent définir plusieurs sous-champs. Bien que semblables aux mixins en ce qu&#39;ils permettent l&#39;utilisation cohérente d&#39;une structure à champs multiples, les types de données sont plus flexibles parce qu&#39;ils peuvent être inclus n&#39;importe où dans la structure de schéma alors que les mixins ne peuvent être ajoutés qu&#39;au niveau racine. Pour plus d&#39;informations sur l&#39;utilisation des types de données dans l&#39;API, consultez le [guide des points de terminaison des types de données](./data-types.md).

## Descripteurs

Descripteurs sont des ensembles de métadonnées affectés à des champs spécifiques au sein d’un schéma, fournissant divers détails contextuels, notamment la manière dont ces champs (et le schéma lui-même) sont liés à d’autres schémas. Chaque schéma peut comporter une ou plusieurs entités descripteurs qui lui sont appliquées et plusieurs types de descripteurs différents peuvent servir à des fins différentes. Pour plus d&#39;informations sur l&#39;utilisation des descripteurs dans l&#39;API, consultez le [guide des points de terminaison descripteurs](./descriptors.md) et un aperçu des différents types de descripteurs et de leurs cas d&#39;utilisation.

## Unions

Bien que Plateforme vous permette de composer des schémas pour des cas d&#39;utilisation particuliers, elle vous permet également de composer une &quot;union&quot; de schémas appartenant à une classe spécifique. Un schéma d’union agrégat les champs de tous les schémas qui partagent la même classe en une seule représentation. En activant un schéma à utiliser avec [Profil client en temps réel](../../profile/home.md), ce schéma est inclus dans l’union pour sa classe particulière. En tant que tel, les schémas d&#39;union ne peuvent pas être modifiés directement et ne peuvent être affectés que par l&#39;inclusion ou l&#39;exclusion de schémas destinés à être utilisés dans le Profil.

Pour savoir comment vue des unions dans l&#39;API de registre des Schémas, consultez le [guide des points de terminaison des unions](./unions.md).

## Exporter/Importer

L&#39;API Schéma Registry vous permet de transférer et de partager des ressources XDM entre des sandbox et des organisations IMS. Pour tout schéma, mixin ou type de données, vous pouvez générer une charge utile d’exportation contenant la structure de la ressource et les ressources dépendantes. Cette charge utile peut ensuite être utilisée pour importer la ressource dans un sandbox de destination et une organisation IMS.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez la [référence de l&#39;API de registre de Schéma](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Sample data

Vous pouvez générer des données d’exemple pour n’importe quel schéma spécifié dans la bibliothèque de Schémas. L&#39;objet de réponse renvoyé peut alors être utilisé comme source d&#39;assimilation de données.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez la [référence de l&#39;API de registre de Schéma](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Journal d’audit

Le registre des Schémas tient un journal de toutes les modifications apportées à une ressource (classe, mixin, type de données ou schéma) entre différentes mises à jour. Vous pouvez récupérer le journal d&#39;une ressource particulière en fournissant ses `$id` ou `meta:altId` dans le chemin d&#39;une demande de GET vers ce point de terminaison.

Pour plus d&#39;informations sur l&#39;utilisation de ce point de terminaison, consultez la [référence de l&#39;API de registre de Schéma](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Étapes suivantes

Pour commencer à lancer des appels à l&#39;aide de l&#39;API Schéma Registry, lisez le [guide de prise en main](./getting-started.md), puis sélectionnez l&#39;un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques.