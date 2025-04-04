---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Options de configuration dans les sources en libre-service (SDK par lots)
description: Ce document présente un aperçu des configurations que vous devez préparer pour utiliser des sources en libre-service (SDK par lots).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 22%

---

# Options de configuration dans les sources en libre-service (SDK par lots)

Ce document présente un aperçu des configurations que vous devez préparer pour utiliser des sources en libre-service (SDK par lots).

## Spécification de connexion

Les spécifications de connexion renvoient les propriétés du connecteur d’une source. Ils incluent des spécifications d’authentification liées à la création des connexions de base et source, ainsi qu’un identifiant de spécification de connexion fixe attribué à une source particulière. Les spécifications de connexion sont indépendantes du client et de l’organisation. Une spécification de connexion type contient des informations de base sur une source donnée, ainsi que trois sections distinctes : `authSpec`, `sourceSpec` et `exploreSpec`.

| Spécifications | Description |
| --- | --- |
| `authSpec` | Le tableau `authSpec` contient des informations sur les paramètres d’authentification requis pour connecter une source à Experience Platform. Toute source donnée peut prendre en charge plusieurs types d’authentification différents. |
| `sourceSpec` | Le tableau `sourceSpec` contient des informations générales relatives à une source, notamment des informations sur les attributs requis pour présenter la source dans l’interface utilisateur, un lien de documentation et des paramètres concernant la pagination, l’en-tête, le corps et la planification. En outre, `sourceSpec` décrit le schéma des paramètres requis pour créer une connexion source à partir d’une connexion de base, et est nécessaire pour créer une connexion source. |
| `exploreSpec` | Le tableau `exploreSpec` définit les paramètres requis pour explorer et inspecter les objets contenus dans votre source. Le `exploreSpec` définit également le format de réponse renvoyé lorsque des objets sont explorés et inspectés. |

{style="table-layout:auto"}

## Renseigner les valeurs de spécification de connexion

Une spécification de connexion peut être divisée en trois parties distinctes : les spécifications d’authentification, les spécifications de la source et les spécifications d’exploration.

Consultez les documents suivants pour obtenir des instructions sur la façon de renseigner les valeurs de chaque partie d’une spécification de connexion :

* [Configurer votre spécification d’authentification](./authspec.md)
* [Configurer votre spécification de source](./sourcespec.md)
* [Configurer votre spécification d’exploration](./explorespec.md)
