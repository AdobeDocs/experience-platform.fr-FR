---
solution: Experience Platform
title: Exploration et traitement des jeux de données bruts optimisant les tableaux de bord Experience Platform
type: Documentation
description: Découvrez comment utiliser Query Service pour explorer et traiter des jeux de données bruts alimentant les tableaux de bord de profils, de segments et de destinations dans Experience Platform.
source-git-commit: 1facf7079213918c2ef966b704319827eaa4a53d
workflow-type: ht
source-wordcount: '614'
ht-degree: 100%

---


# Exploration, vérification et traitement des jeux de données de tableaux de bord à l’aide de Query Service

Adobe Experience Platform fournit des informations importantes sur les données de profils, de segments et de destinations de votre entreprise par le biais de tableaux de bord disponibles dans l’interface utilisateur Experience Platform. Vous pouvez ensuite utiliser Adobe Experience Platform Query Service pour explorer, vérifier et traiter les jeux de données bruts qui alimentent ces tableaux de bord dans le lac de données.

## Prise en main de Query Service

Adobe Experience Platform Query Service vient en aide aux spécialistes du marketing pour obtenir des informations à partir de leurs données en permettant l’utilisation de SQL standard pour interroger les données dans le lac de données. Query Service offre une interface utilisateur et une API qui peuvent être utilisées pour relier tous les jeux de données dans le lac de données et capturer les résultats de la requête en tant que nouveaux jeux de données à utiliser dans les comptes-rendus de performances, le machine learning ou pour ingestion dans le profil client en temps réel.

Pour en savoir plus sur Query Service et son rôle dans Experience Platform, commencez par lire la [présentation de Query Service](../query-service/home.md).

## Jeux de données disponibles

Vous pouvez utiliser Query Service pour interroger des jeux de données bruts pour les tableaux de bord de profils, de segments et de destinations. Les sections suivantes décrivent les jeux de données bruts que vous pouvez trouver dans le lac de données.

### Jeux de données d’attributs de profils

Pour chaque stratégie de fusion principale dans le profil client en temps réel, un jeu de données d’attributs de profils est disponible dans le lac de données.

La convention d’affectation des noms de ces jeux de données est **Attribut de profil** suivi d’une valeur alphanumérique. Par exemple : `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Pour comprendre le schéma complet de chaque jeu de données, vous pouvez prévisualiser et explorer les jeux de données à l’aide de la visionneuse de jeux de données dans l’interface utilisateur d’Experience Platform.

### Jeu de données de métadonnées de segments

Un jeu de données de métadonnées de segment contenant des métadonnées pour chacun des segments de votre organisation est disponible dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **Définition de segment de profil** suivie d’une valeur alphanumérique. Par exemple : `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

Pour comprendre le schéma complet du jeu de données, vous pouvez prévisualiser et explorer le schéma à l’aide de la visionneuse de jeux de données dans l’interface utilisateur d’Experience Platform.

![](images/query/segment-metadata.png)

### Jeu de données de métadonnées de destination

Les métadonnées de toutes les destinations activées de votre organisation sont disponibles sous la forme d’un jeu de données brut dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **DIM_Destination**.

Pour comprendre le schéma complet du jeu de données, vous pouvez prévisualiser et explorer le schéma à l’aide de la visionneuse de jeux de données dans l’interface utilisateur d’Experience Platform.

![](images/query/destinations-metadata.png)

## Exemples de requêtes

Les exemples de requêtes suivants incluent des requêtes SQL pouvant être utilisées dans Query Service pour explorer, vérifier et traiter les jeux de données bruts qui alimentent vos tableaux de bord.

### Nombre de profils par identité

Cet aperçu du profil fournit une ventilation des identités pour tous les profils fusionnés du jeu de données. Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

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

## Étapes suivantes

En lisant ce guide, vous pouvez désormais utiliser Query Service pour exécuter plusieurs requêtes afin d’explorer et de traiter les jeux de données bruts qui alimentent vos tableaux de bord de profils, de segments et de destinations.

Pour en savoir plus sur ces tableaux de bord et les mesures associées, sélectionnez-les dans la liste des tableaux de bord disponibles dans la navigation de la documentation.
