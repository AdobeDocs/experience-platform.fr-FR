---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;
solution: Experience Platform
title: Guide de l’API Schema Registry
description: L’API Schema Registry permet aux développeurs de gérer par programmation tous les schémas et les ressources de modèle de données d’expérience (XDM) associées dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 8%

---

# Guide de l’API [!DNL Schema Registry]

Le [!DNL Schema Registry] permet d’accéder à la bibliothèque de schémas dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles.

L’API Schema Registry fournit plusieurs points d’entrée vous permettant de gérer par programmation tous les schémas et les ressources de modèle de données d’expérience (XDM) associées disponibles pour vous dans Experience Platform. Cela inclut ceux définis par Adobe, les partenaires [!DNL Experience Platform] et les fournisseurs dont vous utilisez les applications.

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

>[!IMPORTANT]
>
>XDM utilise la mise en forme de schéma JSON pour décrire et valider la structure des données d’expérience client ingérées. Avant de travailler avec l’API Schema Registry, il est vivement recommandé de consulter la [documentation officielle sur les schémas JSON](https://json-schema.org/) pour mieux comprendre cette technologie sous-jacente.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez la [référence de l’API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schémas

Les schémas XDM représentent et valident la structure et le format des données ingérées dans Experience Platform. Un schéma est composé d’une classe et de zéro ou plusieurs groupes de champs. Vous pouvez créer, afficher, modifier et supprimer des schémas à l’aide du point d’entrée `/schemas`. Pour savoir comment utiliser ce point d’entrée, consultez le guide [sur les points d’entrée des schémas](./schemas.md).

Pour obtenir un guide détaillé sur la création manuelle d’un schéma complet dans l’API Schema Registry, notamment sur la création et l’ajout de groupes de champs et de types de données, consultez le tutoriel [Création de schéma d’API](../tutorials/create-schema-api.md).

Si vous ingérez des données CSV, consultez la section sur la conversion [CSV en schéma](#csv-to-schema).

## Comportements

Les comportements définissent la nature des données décrites par un schéma. Chaque classe XDM doit référencer un comportement spécifique, dont tous les schémas qui utilisent cette classe hériteront. Consultez le [guide des points d’entrée des comportements](./behaviors.md) pour savoir comment afficher les comportements disponibles dans l’API.

## Classes

Une classe définit la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir et détermine les groupes de champs éligibles à l’utilisation dans ces schémas. Chaque classe doit être associée à un comportement existant. Consultez le [guide du point d’entrée des classes](./classes.md) pour plus d’informations sur l’utilisation des classes dans l’API.

## Groupes de champs

Les groupes de champs sont des composants réutilisables qui définissent un ou plusieurs champs représentant un concept particulier, comme une personne, une adresse postale ou un environnement de navigateur web. Les groupes de champs sont destinés à être inclus dans le cadre d’un schéma qui implémente une classe compatible, en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Consultez le [guide des points d’entrée des groupes de champs](./field-groups.md) pour savoir comment utiliser les groupes de champs dans l’API.

## Types de données

Les types de données sont utilisés comme champs de type référence dans les classes ou les groupes de champs de la même manière que les champs littéraux de base, la principale différence étant que les types de données peuvent définir plusieurs sous-champs. Bien qu’ils soient similaires aux groupes de champs en ce qu’ils permettent l’utilisation cohérente d’une structure à champs multiples, les types de données sont plus flexibles, car ils peuvent être inclus n’importe où dans la structure du schéma, tandis que les groupes de champs ne peuvent être ajoutés qu’au niveau racine. Pour plus d’informations sur l’utilisation des types de données dans l’API[&#128279;](./data-types.md) consultez le  guide des points d’entrée des types de données .

>[!NOTE]
>
>Si un champ est défini comme un type de données spécifique, vous ne pouvez pas créer le même champ avec un type de données différent dans un autre schéma. Cette contrainte s’applique à l’ensemble du client de votre organisation.

## Descripteurs

Les descripteurs sont des ensembles de métadonnées qui sont affectés à des champs spécifiques dans un schéma, fournissant divers détails contextuels, y compris la manière dont ces champs (et le schéma lui-même) sont liés à d’autres schémas. Chaque schéma peut être associé à une ou plusieurs entités de descripteur. Il existe plusieurs types de descripteur différents pour atteindre des objectifs différents. Consultez le [guide des points d’entrée des descripteurs](./descriptors.md) pour plus d’informations sur l’utilisation de descripteurs dans l’API et pour obtenir un aperçu des différents types de descripteurs et de leurs cas d’utilisation.

## Unions

Experience Platform vous permet non seulement de composer des schémas pour des cas d’utilisation spécifiques, mais aussi de composer une « union » de schémas appartenant à une classe spécifique. Un schéma d’union agrège les champs de tous les schémas qui partagent la même classe dans une représentation unique. En activant un schéma à utiliser avec [Real-Time Customer Profile](../../profile/home.md), ce schéma est inclus dans l’union pour sa classe particulière. Par conséquent, les schémas d’union ne peuvent pas être modifiés directement et peuvent uniquement être affectés par l’inclusion ou l’exclusion de schémas à utiliser dans Profile.

Pour savoir comment afficher les unions dans l’API Schema Registry, consultez le guide [point d’entrée des unions](./unions.md).

## Conversion CSV en schéma {#csv-to-schema}

Vous pouvez générer automatiquement un schéma XDM à l’aide d’un fichier CSV en tant que modèle, ce qui vous permet de créer des modèles pour importer en masse des champs de schéma et réduire les tâches manuelles de l’API ou de l’interface utilisateur.

Pour plus d’informations, consultez le guide [CSV to schema conversion endpoint](./export.md).

>[!NOTE]
>
>Vous pouvez également utiliser l’interface utilisateur pour [mapper un fichier CSV à un schéma à l’aide de recommandations générées par l’IA](../../ingestion/tutorials/map-csv/recommendations.md) (actuellement en version bêta).

## Exporter {#export}

L’API Schema Registry vous permet de transférer et de partager des ressources XDM entre les sandbox et les organisations. Pour tout schéma, groupe de champs ou type de données, vous pouvez générer une payload d’exportation contenant la structure de la ressource et des ressources dépendantes. Cette payload peut ensuite être utilisée pour importer la ressource dans un sandbox et une organisation de destination.

Pour plus d’informations sur la création d’une payload d’exportation pour une ressource XDM existante[&#128279;](./export.md) consultez le  guide de point d’entrée d’exportation .

## Importer

Si vous utilisez les points d’entrée [export](#export) ou [CSV vers la conversion de schéma](./import.md) pour créer une payload d’exportation, vous pouvez envoyer cette payload à une organisation cible et à un sandbox pour importer les ressources spécifiées.

Pour plus d’informations sur la génération de ressources XDM à partir de payloads d’exportation[&#128279;](./export.md) consultez le  guide de point d’entrée d’importation .

## Données d’exemple

Vous pouvez générer des données d’exemple pour n’importe quel schéma spécifié dans la bibliothèque de schémas. L’objet de réponse renvoyé peut ensuite être utilisé comme source d’ingestion de données.

Pour plus d’informations sur l’utilisation de ce point d’entrée[&#128279;](./sample-data.md) consultez le  guide de point d’entrée d’exemple de données .

## Journal d’audit

Le registre des schémas conserve un journal de toutes les modifications apportées à une ressource (classe, groupe de champs, type de données ou schéma) entre différentes mises à jour. Vous pouvez récupérer le journal d’une ressource spécifique en fournissant son `$id` ou son `meta:altId` dans le chemin d’accès d’une requête GET vers ce point d’entrée.

Pour plus d’informations sur l’utilisation de ce point d’entrée[&#128279;](./audit-log.md) consultez le  guide de point d’entrée du journal d’audit .

## Étapes suivantes

Pour commencer à effectuer des appels à lʼaide de lʼAPI Schema Registry, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez lʼun des guides des points dʼentrée pour savoir comment utiliser des points dʼentrée spécifiques.
