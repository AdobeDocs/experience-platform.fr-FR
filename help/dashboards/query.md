---
solution: Experience Platform
title: Explorer, vérifier et traiter des jeux de données de tableau de bord à l’aide de Query Service
type: Documentation
description: Découvrez comment utiliser Query Service pour explorer et traiter des jeux de données bruts alimentant les tableaux de bord de profils, d’audiences et de destinations dans Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
TQID: https://experienceleague.adobe.com/K3OyZlBF2FKa8P74e-cbztUx-nKZXRO3v9S-Ix2kr0k
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: ed0d8d0e-04b9-4326-be72-a0fbca265377id: eec185bd-7d60-4193-ba3f-da427569936a
subfeature_v2: id: b784da9a-7978-4766-bf1f-5ab2b23d894aid: d1823595-9241-4128-8a33-e4ac3bf08773id: f6ac78a3-5b59-40f5-a37d-45df5303d3a3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 958
ht-degree: 37%

---

# Explorer, vérifier et traiter des jeux de données de tableau de bord à l’aide de [!DNL Query Service]

Adobe Experience Platform fournit des informations importantes sur les données de profil, d’audience et de destinations de votre entreprise par le biais de tableaux de bord disponibles dans l’interface utilisateur d’Experience Platform. Vous pouvez ensuite utiliser Adobe Experience Platform [!DNL Query Service] pour explorer, vérifier et traiter les jeux de données bruts qui alimentent ces tableaux de bord dans le lac de données.

## Prise en main de [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] aide les spécialistes du marketing à obtenir des informations à partir de leurs données en permettant l’utilisation de SQL standard pour interroger les données dans le lac de données. [!DNL Query Service] offre une interface utilisateur et une API qui peuvent être utilisées pour joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête en tant que nouveaux jeux de données à utiliser dans les rapports, le machine learning ou pour ingestion dans le profil client en temps réel.

Pour en savoir plus sur [!DNL Query Service] et son rôle dans Experience Platform, commencez par lire la [[!DNL Query Service] présentation](../query-service/home.md).

## Accès aux jeux de données disponibles

Vous pouvez utiliser [!DNL Query Service] pour interroger des jeux de données bruts pour les tableaux de bord de profils, d’audiences et de destinations. Pour afficher les jeux de données disponibles, dans l’interface utilisateur d’Experience Platform, sélectionnez **Jeux de données** dans le volet de navigation de gauche pour ouvrir le tableau de bord Jeux de données. Le tableau de bord répertorie tous les jeux de données disponibles pour votre organisation. Des détails s’affichent pour chaque jeu de données répertorié, notamment son nom, le schéma auquel le jeu de données adhère et le statut de l’exécution d’ingestion la plus récente.

![Tableau de bord Parcourir les jeux de données avec l’onglet Jeux de données en surbrillance dans le volet de navigation de gauche.](./images/query/browse-datasets.png)

### Jeux de données générés par le système {#system-generated-datasets}

>[!IMPORTANT]
>
>Les jeux de données générés par le système sont masqués par défaut. Par défaut, l’onglet [!UICONTROL Parcourir] n’affiche que les jeux de données dans lesquels vous avez ingéré des données.

Pour afficher les jeux de données générés par le système, sélectionnez l’icône de filtre (![Icône Filtrer.](/help/images/icons/filter.png)) situé à gauche de la barre de recherche.

![Onglet Parcourir les jeux de données avec l’icône de filtre mise en surbrillance.](./images/query/filter-datasets.png)

Une barre latérale s’affiche avec deux boutons (bascule), [!UICONTROL Inclus dans le profil] et [!UICONTROL Afficher les jeux de données système]. Sélectionnez le bouton (bascule) [!UICONTROL Afficher les jeux de données système] pour inclure les jeux de données générés par le système dans la liste navigable des jeux de données.

![Onglet Parcourir les jeux de données avec le bouton bascule Afficher les jeux de données système en surbrillance.](./images/query/show-system-datasets.png)

### Jeux de données d’attributs de profils {#profile-attribute-datasets}

Les informations contenues dans le tableau de bord du profil sont liées aux politiques de fusion qui ont été définies par votre organisation. Pour chaque politique de fusion active, un jeu de données d’attributs de profil est disponible dans le lac de données.

La convention d’affectation des noms de ces jeux de données est **Profile-Snapshot-Export** suivie d’une valeur alphanumérique aléatoire générée par le système. Par exemple : `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Pour comprendre le schéma complet de chaque jeu de données d’exportation d’instantané de profil, vous pouvez prévisualiser et explorer les jeux de données [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

![Aperçu du jeu de données Profile-Snapshot-Export.](images/query/profile-attribute.png)

#### Mappage des jeux de données d’attributs de profil aux ID de politique de fusion

La valeur alphanumérique affectée à chaque jeu de données d’attributs de profil généré par le système est une chaîne aléatoire qui mappe vers un ID de politique de fusion de l’une des politiques de fusion créées par votre organisation. Le mappage de chaque ID de politique de fusion à sa chaîne de jeu de données d’attributs de profil correspondante est conservé dans le jeu de données `adwh_dim_merge_policies`.

Le jeu de données `adwh_dim_merge_policies` contient les champs suivants :

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Ce jeu de données peut être exploré à l’aide de l’interface d’utilisation du requêteur dans Experience Platform. Pour en savoir plus sur l’utilisation du requêteur, reportez-vous au [Guide de l’interface d’utilisation du requêteur](../query-service/ui/user-guide.md).

### Jeu de données de métadonnées d’audience

Un jeu de données de métadonnées d’audience contenant des métadonnées pour chacune des audiences de votre organisation est disponible dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **Segmentdefinition-Snapshot-Export** suivi d’une valeur alphanumérique. Par exemple : `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Pour comprendre le schéma complet de chaque jeu de données d’exportation d’instantané de définition de segment, vous pouvez prévisualiser et explorer les jeux de données [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

### Jeu de données de métadonnées de destination

Les métadonnées de toutes les destinations activées de votre organisation sont disponibles sous la forme d’un jeu de données brut dans le lac de données.

La convention d’affectation des noms de ce jeu de données est **DIM_Destination**.

Pour comprendre le schéma complet du jeu de données de destination DIM, vous pouvez prévisualiser et explorer le schéma [à l’aide de la visionneuse de jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur d’Experience Platform.

![Aperçu du jeu de données DIM_Destination.](images/query/destinations-metadata.png)

## Rapports d’informations Customer Data Platform (CDP)

La fonctionnalité Modèles de données d’informations CDP expose le langage SQL qui alimente les informations pour divers widgets de profil, de destination et de segmentation. Vous pouvez personnaliser ces modèles de requête SQL afin de créer des rapports CDP pour vos cas d’utilisation de marketing et de KPI.

Les rapports CDP fournissent des informations sur vos données de profil et leur relation avec les audiences et les destinations. Consultez la documentation du modèle de données d’informations CDP pour obtenir des informations détaillées sur la manière d’[appliquer les modèles de données d’informations CDP à vos cas d’utilisation d’indicateurs clés de performance spécifiques](./data-models/cdp-insights-data-model-b2c.md).

## Exemples de requêtes

Les exemples de requêtes suivants incluent des requêtes SQL qui peuvent être utilisées dans [!DNL Query Service] pour explorer, vérifier et traiter les jeux de données bruts qui alimentent vos tableaux de bord.

### Nombre de profils par identité

Ces informations de profil fournissent une répartition des identités pour tous les profils fusionnés du jeu de données.

>[!NOTE]
>
>Le nombre total de profils par identité (c’est-à-dire en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur au nombre total de profils fusionnés, car plusieurs espaces de noms peuvent être associés à un profil. Par exemple, si un client ou une cliente interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à cette personne.

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

### Nombre de profils par audience

Cette audience insight fournit le nombre total de profils fusionnés dans chaque audience du jeu de données. Ce nombre est le résultat de l’application de la politique de fusion d’audience à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu de l’audience.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Étapes suivantes

En lisant ce guide, vous pouvez désormais utiliser [!DNL Query Service] pour exécuter plusieurs requêtes afin d’explorer et de traiter les jeux de données bruts qui alimentent vos tableaux de bord de profils, d’audiences et de destinations.

Pour en savoir plus sur ces tableaux de bord et les mesures associées, sélectionnez-les dans la liste des tableaux de bord disponibles dans la navigation de la documentation.
