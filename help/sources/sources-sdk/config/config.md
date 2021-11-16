---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Options de configuration dans le SDK Sources
topic-legacy: overview
description: Ce document présente les configurations que vous devez préparer pour utiliser le SDK Sources.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# Options de configuration dans le SDK Sources

>[!IMPORTANT]
>
>Le SDK Sources est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Les fonctionnalités décrites dans cette documentation peuvent faire l’objet de modifications.

Ce document présente les configurations que vous devez préparer pour utiliser le SDK Sources.

## Spécification de connexion

Les spécifications de connexion renvoient les propriétés du connecteur d’une source. Elles incluent des spécifications d’authentification liées à la création des connexions de base et source, ainsi qu’un identifiant de spécification de connexion fixe affecté à une source particulière. Les spécifications de connexion sont indépendantes de l’organisation du client et IMS. Une spécification de connexion type contient des informations de base sur une source donnée, ainsi que trois sections distinctes : `authSpec`, `sourceSpec`, et `exploreSpec`.

| Spécification | Description |
| --- | --- |
| `authSpec` | Le `authSpec` contient des informations sur les paramètres d’authentification requis pour connecter une source à Platform. N’importe quelle source donnée peut prendre en charge plusieurs types d’authentification différents. |
| `sourceSpec` | Le `sourceSpec` contient des informations générales relatives à une source, notamment des informations sur les attributs requis pour présenter la source dans l’interface utilisateur, un lien vers la documentation et des paramètres concernant la pagination, l’en-tête, le corps et la planification. En outre, `sourceSpec` décrit le schéma des paramètres requis pour créer une connexion source à partir d’une connexion de base. Il est nécessaire pour créer une connexion source. |
| `exploreSpec` | Le `exploreSpec` définit les paramètres requis pour explorer et inspecter les objets contenus dans votre source. Le `exploreSpec` définit également le format de réponse renvoyé lorsque des objets sont explorés et inspectés. |

{style=&quot;table-layout:auto&quot;}

## Renseigner les valeurs des spécifications de connexion

Une spécification de connexion peut être divisée en trois parties distinctes : les spécifications d’authentification, les spécifications source et les spécifications d’exploration.

Consultez les documents suivants pour obtenir des instructions sur la façon de renseigner les valeurs de chaque partie d’une spécification de connexion :

* [Configuration de votre spécification d’authentification](./authspec.md)
* [Configuration de votre spécification source](./sourcespec.md)
* [Configuration de votre spécification d’exploration](./explorespec.md)


