---
solution: Experience Platform
title: Exploration et traitement des jeux de données bruts optimisant les tableaux de bord des Experience Platform
type: Documentation
description: Découvrez comment utiliser Query Service pour explorer et traiter des jeux de données bruts alimentant les tableaux de bord de profil, de segment et de destination dans Experience Platform.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Exploration, vérification et traitement des jeux de données de tableau de bord à l’aide de Query Service

Adobe Experience Platform fournit des informations importantes sur les données de profil, de segment et de destination de votre entreprise par le biais de tableaux de bord disponibles dans l’interface utilisateur de l’Experience Platform. Vous pouvez ensuite utiliser Adobe Experience Platform Query Service pour explorer, vérifier et traiter les jeux de données bruts qui alimentent ces tableaux de bord dans le lac de données.

## Prise en main de Query Service

Adobe Experience Platform Query Service prend en charge les spécialistes du marketing pour obtenir des informations à partir de leurs données en permettant l’utilisation de SQL standard pour interroger les données dans le lac de données. Query Service offre une interface utilisateur et une API qui peuvent être utilisées pour joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête en tant que nouveaux jeux de données à utiliser dans les rapports, l’apprentissage automatique ou pour ingestion dans Real-time Customer Profile.

Pour en savoir plus sur Query Service et son rôle dans Experience Platform, commencez par lire la [présentation de Query Service](../query-service/home.md).

## Jeux de données disponibles

Vous pouvez utiliser Query Service pour interroger des jeux de données bruts pour les tableaux de bord de profil, de segment et de destinations. Les sections suivantes décrivent les jeux de données bruts que vous pouvez trouver dans le lac de données.

### Jeux de données d’attributs de profil

Pour chaque stratégie de fusion principale dans Real-time Customer Profile, un jeu de données d’attributs de profil est disponible dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **Attribut de profil** suivi d’une valeur numérique alphanumérique. Par exemple : `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Pour comprendre le schéma complet du jeu de données, vous pouvez prévisualiser et explorer le schéma à l’aide de la visionneuse de jeux de données dans l’interface utilisateur de l’Experience Platform.

### Jeu de données de métadonnées de segment

Un jeu de données de métadonnées de segment est disponible dans le lac de données pour chaque segment de votre entreprise.

La convention d’affectation des noms de ce jeu de données est **Définition de segment de profil** suivie d’une valeur numérique alphanumérique. Par exemple : `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

L’image suivante montre le schéma du jeu de données de métadonnées de segment.

![](images/query/segment-metadata.png)

### Jeu de données de métadonnées de destination

Les métadonnées de vos destinations activées sont disponibles sous la forme d’un jeu de données brut dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **DIM_Destination**.

L’image suivante montre le schéma du jeu de données de métadonnées de destination.

![](images/query/destinations-metadata.png)

## Exemples de requêtes

Les exemples de requêtes suivants incluent des exemples de requêtes SQL pouvant être utilisées dans Query Service pour explorer, vérifier et traiter les jeux de données bruts qui alimentent vos tableaux de bord.

### Nombre de profils par identité

Cet aperçu du profil fournit une ventilation des identités pour tous les profils fusionnés du jeu de données. Le nombre total de profils par identité (c’est-à-dire, additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent y être associés pour un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

**Requête**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Nombre de profils par segment

Cet aperçu de l’audience fournit le nombre total de profils fusionnés dans chaque segment du jeu de données. Ce nombre est le résultat de l’application de la stratégie de fusion de segments à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu du segment.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### Nombre de segments activés par destination pour toutes les destinations

## Étapes suivantes

En lisant ce guide, vous pouvez désormais utiliser Query Service pour exécuter plusieurs requêtes afin d’explorer et de traiter les jeux de données bruts qui alimentent vos tableaux de bord de profil, de segment et de destinations.

Pour en savoir plus sur chaque tableau de bord et ses mesures, sélectionnez un tableau de bord dans la liste des tableaux de bord disponibles dans le volet de navigation de la documentation.
