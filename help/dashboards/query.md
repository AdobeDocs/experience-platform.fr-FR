---
solution: Experience Platform
title: Exploration et traitement des jeux de données bruts optimisant les tableaux de bord Platform
type: Documentation
description: Découvrez comment utiliser Query Service pour explorer et traiter des jeux de données bruts alimentant les tableaux de bord de profils, de segments et de destinations dans Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

Les informations contenues dans le tableau de bord du profil sont liées aux stratégies de fusion qui ont été définies par votre organisation. Pour chaque stratégie de fusion active, un jeu de données d’attributs de profil est disponible dans le lac de données.

La convention d’affectation des noms de ces jeux de données est **Profile-Snapshot-Export** suivie d’une valeur alphanumérique aléatoire générée par le système. Par exemple : `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Pour comprendre le schéma complet de chaque jeu de données d’exportation d’instantané de profil, vous pouvez prévisualiser et explorer les jeux de données [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

![](images/query/profile-attribute.png)

#### Mappage des jeux de données d’attributs de profil aux ID de stratégie de fusion

Chaque jeu de données d’attributs de profil est intitulé **Exportation d’instananés de profils** suivi d’une valeur alphanumérique aléatoire générée par le système. Par exemple : `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Cette valeur alphanumérique est une chaîne aléatoire générée par le système qui fournit un mappage vers l’ID de l’une des stratégies de fusion créées par votre organisation. Le mappage de chaque ID de stratégie de fusion à sa chaîne de jeu de données d’attributs de profil correspondante est conservé dans le jeu de données `adwh_dim_merge_policies`.

Le jeu de données `adwh_dim_merge_policies` contient les champs suivants :

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Ce jeu de données peut être exploré à l’aide de l’interface utilisateur de l’éditeur de requêtes dans Experience Platform. Pour en savoir plus sur l’utilisation de l’éditeur de requêtes, reportez-vous au [Guide de l’interface utilisateur de l’éditeur de requêtes](../query-service/ui/user-guide.md).

### Jeu de données de métadonnées de segments

Un jeu de données de métadonnées de segment contenant des métadonnées pour chacun des segments de votre organisation est disponible dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **Segmentdefinition-Snapshot-Export** suivi d’une valeur alphanumérique. Par exemple : `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Pour comprendre le schéma complet de chaque jeu de données d’exportation d’instantané de définition de segment, vous pouvez prévisualiser et explorer les jeux de données [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

![](images/query/segment-metadata.png)

### Jeu de données de métadonnées de destination

Les métadonnées de toutes les destinations activées de votre organisation sont disponibles sous la forme d’un jeu de données brut dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **DIM_Destination**.

Pour comprendre le schéma complet du jeu de données de destination DIM, vous pouvez prévisualiser et explorer le schéma [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

![](images/query/destinations-metadata.png)

## Exemples de requêtes

Les exemples de requêtes suivants incluent des requêtes SQL pouvant être utilisées dans Query Service pour explorer, vérifier et traiter les jeux de données bruts qui alimentent vos tableaux de bord.

### Nombre de profils par identité

Cet aperçu du profil fournit une ventilation des identités pour tous les profils fusionnés du jeu de données.

>[!NOTE]
>
>Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Étapes suivantes

En lisant ce guide, vous pouvez désormais utiliser Query Service pour exécuter plusieurs requêtes afin d’explorer et de traiter les jeux de données bruts qui alimentent vos tableaux de bord de profils, de segments et de destinations.

Pour en savoir plus sur ces tableaux de bord et les mesures associées, sélectionnez-les dans la liste des tableaux de bord disponibles dans la navigation de la documentation.
