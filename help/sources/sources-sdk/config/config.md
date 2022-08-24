---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Options de configuration dans les sources en libre-service (SDK par lots)
topic-legacy: overview
description: Ce document présente les configurations que vous devez préparer pour utiliser les sources en libre-service (SDK par lots).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 23%

---

# Options de configuration dans les sources en libre-service (SDK par lots)

Ce document présente les configurations que vous devez préparer pour utiliser les sources en libre-service (SDK par lots).

## Spécification de connexion

Les spécifications de connexion renvoient les propriétés du connecteur d’une source. Elles incluent des spécifications d’authentification liées à la création des connexions de base et source, ainsi qu’un identifiant de spécification de connexion fixe affecté à une source particulière. Les spécifications de connexion sont indépendantes du client et de l’organisation. Une spécification de connexion type contient des informations de base sur une source donnée, ainsi que trois sections distinctes : `authSpec`, `sourceSpec`, et `exploreSpec`.

| Spécification | Description |
| --- | --- |
| `authSpec` | Le `authSpec` contient des informations sur les paramètres d’authentification requis pour connecter une source à Platform. N’importe quelle source donnée peut prendre en charge plusieurs types d’authentification différents. |
| `sourceSpec` | Le `sourceSpec` contient des informations générales relatives à une source, notamment des informations sur les attributs requis pour présenter la source dans l’interface utilisateur, un lien vers la documentation et des paramètres concernant la pagination, l’en-tête, le corps et la planification. En outre, `sourceSpec` décrit le schéma des paramètres requis pour créer une connexion source à partir d’une connexion de base. Il est nécessaire pour créer une connexion source. |
| `exploreSpec` | Le `exploreSpec` définit les paramètres requis pour explorer et inspecter les objets contenus dans votre source. Le `exploreSpec` définit également le format de réponse renvoyé lorsque des objets sont explorés et inspectés. |

{style=&quot;table-layout:auto&quot;}

## Renseigner les valeurs des spécifications de connexion

Une spécification de connexion peut être divisée en trois parties distinctes : les spécifications d’authentification, les spécifications de la source et les spécifications d’exploration.

Consultez les documents suivants pour obtenir des instructions sur la façon de renseigner les valeurs de chaque partie d’une spécification de connexion :

* [Configurer votre spécification d’authentification](./authspec.md)
* [Configurer votre spécification de source](./sourcespec.md)
* [Configurer votre spécification d’exploration](./explorespec.md)
