---
solution: Experience Platform
title: Import et utilisation d’audiences externes
description: Suivez ce tutoriel pour découvrir comment utiliser des audiences externes avec Adobe Experience Platform.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 4%

---

# Import et utilisation d’audiences externes

>[!IMPORTANT]
>
>Cette documentation contient des informations provenant d’une version précédente de la documentation Audiences. Elle est donc obsolète.

Adobe Experience Platform prend en charge la possibilité d’importer une audience externe, qui peut ensuite être utilisée comme composants pour une nouvelle audience. Ce document fournit un tutoriel sur la configuration de l’Experience Platform pour importer et utiliser des audiences externes.

## Commencer

Ce tutoriel nécessite une compréhension pratique des différents services [!DNL Adobe Experience Platform] impliqués dans la création d’audiences. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Segmentation Service](../home.md) : vous permet de créer des audiences à partir de données Real-time Customer Profile.
- [Profil client en temps réel](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md) : cadre normalisé selon lequel Platform organise les données d’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).
- [Jeu de données](../../catalog/datasets/overview.md) : la structure de stockage et de gestion pour la persistance des données dans Experience Platform.
- [Ingestion par flux](../../ingestion/streaming-ingestion/overview.md) : méthode d’ingestion et de stockage de données en temps réel par Experience Platform à partir de périphériques côté client et côté serveur.

### Audiences et définitions de segment

Avant de commencer à importer et utiliser des audiences externes, il est important de comprendre la différence entre les audiences et les définitions de segment.

Les audiences se rapportent au groupe de profils vers lequel vous essayez de filtrer. Lors de l’utilisation de définitions de segment, vous pouvez créer une audience en créant une définition de segment qui filtre vos profils sur le sous-ensemble qui répond aux critères de qualification du segment.

Les définitions de segment incluent des informations telles que le nom, la description, l’expression (le cas échéant), la date de création, la date de dernière modification et un identifiant. L’ID lie les métadonnées du segment aux profils individuels qui répondent à la qualification du segment et qui font partie de l’audience résultante.

| Audiences | Définition de segment |
| --------- | ---------------- |
| Groupe de profils que vous essayez de trouver. Lorsque vous utilisez des définitions de segment, cela signifie que ce sera le groupe de profils qui répondent à la qualification du segment. | Groupe de règles utilisé pour segmenter l’audience que vous recherchez. |

## Création d’un espace de noms d’identité pour l’audience externe

La première étape de l’utilisation d’audiences externes consiste à créer un espace de noms d’identité. Les espaces de noms d’identité permettent à Platform d’associer l’origine d’une audience.

Pour créer un espace de noms d’identité, suivez les instructions du [guide sur l’espace de noms d’identité](../../identity-service/features/namespaces.md#manage-namespaces). Lors de la création de votre espace de noms d’identité, ajoutez les détails sources à l’espace de noms d’identité et marquez son [!UICONTROL Type] comme **[!UICONTROL identifiant d’une personne autre que l’autre]**.

![L&#39;identifiant non-personne est mis en surbrillance dans le modal Créer un espace de noms d&#39;identité.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Création d’un schéma pour les métadonnées de segment

Après avoir créé un espace de noms d’identité, vous devez créer un nouveau schéma pour le segment que vous allez créer.

Pour commencer à composer un schéma, sélectionnez tout d’abord **[!UICONTROL Schémas]** dans la barre de navigation de gauche, puis **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail des schémas. À partir de là, sélectionnez **[!UICONTROL Parcourir]** pour afficher une sélection complète des types de schémas disponibles.

![La création de schéma et la navigation sont toutes deux mises en surbrillance.](../images/tutorials/external-audiences/create-schema-browse.png)

Puisque vous créez une définition de segment, qui est une classe prédéfinie, sélectionnez **[!UICONTROL Utiliser la classe existante]**. Sélectionnez maintenant la classe **[!UICONTROL Définition de segment]**, suivie de **[!UICONTROL Attribuer la classe]**.

![La classe de définition de segment est mise en surbrillance.](../images/tutorials/external-audiences/assign-class.png)

Maintenant que votre schéma a été créé, vous devez spécifier le champ qui contiendra l’identifiant du segment. Ce champ doit être marqué comme identité principale et affecté aux espaces de noms que vous avez précédemment créés.

![Les cases à cocher permettant de marquer le champ sélectionné comme identité principale sont mises en surbrillance dans l’éditeur de schémas.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Après avoir marqué le champ `_id` comme identité principale, sélectionnez le titre du schéma, suivi du bouton d’activation/désactivation **[!UICONTROL Profile]**. Sélectionnez **[!UICONTROL Activer]** pour activer le schéma pour [!DNL Real-Time Customer Profile].

![Le bouton d’activation du schéma pour Profile est mis en surbrillance dans l’éditeur de schémas.](../images/tutorials/external-audiences/schema-profile.png)

Désormais, ce schéma est activé pour Profile, l’identification principale étant affectée à l’espace de noms d’identité non-personne que vous avez créé. Par conséquent, cela signifie que les métadonnées de segment importées dans Platform à l’aide de ce schéma seront ingérées dans Profile sans être fusionnées avec d’autres données de profil liées aux personnes.

## Création d’un jeu de données pour le schéma

Après avoir configuré le schéma, vous devez créer un jeu de données pour les métadonnées de segment.

Pour créer un jeu de données, suivez les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#create). Vous devez suivre l’option **[!UICONTROL Créer un jeu de données à partir du schéma]** , à l’aide du schéma que vous avez créé précédemment.

![Le schéma sur lequel vous souhaitez baser votre jeu de données est mis en surbrillance.](../images/tutorials/external-audiences/select-schema.png)

Après avoir créé le jeu de données, continuez à suivre les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#enable-profile) pour activer ce jeu de données pour Real-time Customer Profile.

![Le bouton d’activation du schéma pour Profile est mis en surbrillance dans la page d’activité du jeu de données.](../images/tutorials/external-audiences/dataset-profile.png)

## Configuration et importation des données d’audience

Une fois le jeu de données activé, les données peuvent désormais être envoyées vers Platform soit par le biais de l’interface utilisateur, soit à l’aide des API Experience Platform. Vous pouvez ingérer ces données par le biais d’une connexion par lots ou en continu.

### Ingestion de données à l’aide d’une connexion par lots

Pour créer une connexion par lots, vous pouvez suivre les instructions du [guide d’interface utilisateur de téléchargement de fichier local](../../sources/tutorials/ui/create/local-system/local-file-upload.md) générique. Pour obtenir la liste complète des sources disponibles avec lesquelles vous pouvez utiliser les données d’ingestion, veuillez lire la [présentation des sources](../../sources/home.md).

### Ingestion de données à l’aide d’une connexion en continu

Pour créer une connexion en continu, vous pouvez suivre les instructions du [tutoriel sur l’API](../../sources/tutorials/api/create/streaming/http.md) ou du [tutoriel sur l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md).

Une fois que vous avez créé votre connexion en continu, vous avez accès à votre point de terminaison de diffusion en continu unique auquel vous pouvez envoyer vos données. Pour savoir comment envoyer des données à ces points de terminaison, consultez le [tutoriel sur la diffusion en continu de données d’enregistrement](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Le point de terminaison de diffusion en continu de la connexion en continu est mis en surbrillance dans la page des détails de la source.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Structure des métadonnées d’audience

Après avoir créé une connexion, vous pouvez désormais ingérer vos données vers Platform.

Vous trouverez ci-dessous un exemple des métadonnées de la payload d’audience externe :

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef` | Le schéma **must** se rapporte au schéma créé précédemment pour les métadonnées de segment. |
| `datasetId` | L’identifiant du jeu de données **must** se rapporte au jeu de données créé précédemment pour le schéma que vous venez de créer. |
| `xdmEntity._id` | L’ID **must** se rapporte au même ID de segment que celui que vous utilisez comme audience externe. |
| `xdmEntity.identityMap` | Cette section **must** contient le libellé d’identité utilisé lors de la création de l’espace de noms créé précédemment. |
| `{IDENTITY_NAMESPACE}` | Il s’agit du libellé de l’espace de noms d’identité créé précédemment. Par exemple, si vous appelez votre espace de noms d’identité &quot;externalAudience&quot;, vous l’utilisez comme clé du tableau . |
| `segmentName` | Nom du segment par lequel vous souhaitez que l’audience externe soit segmentée. |

## Création de segments à l’aide d’audiences importées

Une fois les audiences importées configurées, elles peuvent être utilisées dans le cadre du processus de segmentation. Pour rechercher des audiences externes, accédez au créateur de segments, puis sélectionnez l’onglet **[!UICONTROL Audiences]** dans la section **[!UICONTROL Champs]** .

![Le sélecteur d’audiences externes dans le créateur de segments est mis en surbrillance.](../images/tutorials/external-audiences/external-audiences.png)

## Étapes suivantes

Maintenant que vous pouvez utiliser des audiences externes dans vos segments, vous pouvez utiliser le créateur de segments pour créer des segments. Pour savoir comment créer des segments, consultez le [tutoriel sur la création de segments](./create-a-segment.md).

## Annexe

Outre l’utilisation de métadonnées d’audience externe importées et leur utilisation pour créer des segments, vous pouvez importer des appartenances de segment externes dans Platform.

### Configuration d’un schéma de destination d’adhésion à un segment externe

Pour commencer à composer un schéma, sélectionnez tout d’abord **[!UICONTROL Schémas]** dans la barre de navigation de gauche, puis **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail des schémas. À partir de là, sélectionnez **[!UICONTROL XDM Individual Profile]**.

![La zone XDM Individual Profile est mise en surbrillance.](../images/tutorials/external-audiences/create-schema-profile.png)

Maintenant que le schéma a été créé, vous devez ajouter le groupe de champs d’appartenance au segment dans le cadre du schéma. Pour ce faire, sélectionnez [!UICONTROL Segment Membership Details], suivi de [!UICONTROL Ajouter des groupes de champs].

![Le groupe de champs Détails de l’appartenance au segment est mis en surbrillance.](../images/tutorials/external-audiences/segment-membership-details.png)

De plus, assurez-vous que le schéma est marqué pour **[!UICONTROL Profile]**. Pour ce faire, vous devez marquer un champ comme identité principale.

![Le bouton d’activation du schéma pour Profile est mis en surbrillance dans l’éditeur de schémas.](../images/tutorials/external-audiences/external-segment-profile.png)

### Configuration du jeu de données

Après avoir créé votre schéma, vous devez créer un jeu de données.

Pour créer un jeu de données, suivez les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#create). Vous devez suivre l’option **[!UICONTROL Créer un jeu de données à partir du schéma]** , à l’aide du schéma que vous avez créé précédemment.

![Le schéma que vous utilisez pour créer la base de données est mis en surbrillance.](../images/tutorials/external-audiences/select-schema.png)

Après avoir créé le jeu de données, continuez à suivre les instructions du [guide d’utilisation du jeu de données](../../catalog/datasets/user-guide.md#enable-profile) pour activer ce jeu de données pour Real-time Customer Profile.

![Le bouton d’activation du schéma pour Profile est mis en surbrillance dans le workflow de création de jeux de données.](../images/tutorials/external-audiences/dataset-profile.png)

## Configurer et importer des données d’appartenance à une audience externe

Une fois le jeu de données activé, les données peuvent désormais être envoyées vers Platform soit par le biais de l’interface utilisateur, soit à l’aide des API Experience Platform. Vous pouvez ingérer ces données par le biais d’une connexion par lots ou en continu.

### Ingestion de données à l’aide d’une connexion par lots

Pour créer une connexion par lots, vous pouvez suivre les instructions du [guide d’interface utilisateur de téléchargement de fichier local](../../sources/tutorials/ui/create/local-system/local-file-upload.md) générique. Pour obtenir la liste complète des sources disponibles avec lesquelles vous pouvez utiliser les données d’ingestion, veuillez lire la [présentation des sources](../../sources/home.md).

### Ingestion de données à l’aide d’une connexion en continu

Pour créer une connexion en continu, vous pouvez suivre les instructions du [tutoriel sur l’API](../../sources/tutorials/api/create/streaming/http.md) ou du [tutoriel sur l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md).

Une fois que vous avez créé votre connexion en continu, vous avez accès à votre point de terminaison de diffusion en continu unique auquel vous pouvez envoyer vos données. Pour savoir comment envoyer des données à ces points de terminaison, consultez le [tutoriel sur la diffusion en continu de données d’enregistrement](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Le point de terminaison de diffusion en continu de la connexion en continu est mis en surbrillance dans la page des détails de la source.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Structure de l’adhésion au segment

Après avoir créé une connexion, vous pouvez désormais ingérer vos données vers Platform.

Vous trouverez ci-dessous un exemple de payload de l’appartenance à une audience externe :

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef` | Le schéma **must** se rapporte au schéma créé précédemment pour les données d’adhésion au segment. |
| `datasetId` | L’identifiant du jeu de données **must** se rapporte au jeu de données créé précédemment pour le schéma d’adhésion que vous venez de créer. |
| `xdmEntity._id` | Identifiant approprié utilisé pour identifier de manière unique l’enregistrement dans le jeu de données. |
| `{TENANT_NAME}.identities` | Cette section est utilisée pour connecter le groupe de champs des identités personnalisées aux utilisateurs que vous avez précédemment importés. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Il s’agit du libellé de l’espace de noms d’identité personnalisée créé précédemment. Par exemple, si vous appelez votre espace de noms d’identité &quot;externalAudience&quot;, vous l’utilisez comme clé du tableau . |

>[!NOTE]
>
>Par défaut, les appartenances à une audience externe sont supprimées au bout de 30 jours. Pour empêcher la suppression et les conserver pendant plus de 30 jours, utilisez le champ `validUntil` lors de l’ingestion de vos données d’audience. Pour plus d’informations sur ce champ, consultez le guide sur les [groupes de champs de schéma Détails de l’appartenance à un segment](../../xdm/field-groups/profile/segmentation.md).
