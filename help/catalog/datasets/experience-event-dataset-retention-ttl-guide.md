---
title: Gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL
description: Découvrez comment évaluer, définir et gérer la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de configurations de durée de vie (TTL) avec des API Adobe Experience Platform. Ce guide explique comment l’expiration au niveau des lignes de TTL prend en charge les politiques de conservation des données, optimise l’efficacité du stockage et garantit une gestion efficace du cycle de vie des données. Elle fournit également des cas d’utilisation et des bonnes pratiques pour vous aider à appliquer efficacement la durée de vie.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2341'
ht-degree: 1%

---

# Gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL

Une gestion efficace des données est essentielle pour optimiser les performances, le contrôle des coûts et l’intégrité des données. Utilisez la durée de vie (TTL) de conservation des jeux de données d’événements d’expérience pour appliquer l’expiration au niveau des lignes, supprimant automatiquement les enregistrements obsolètes des jeux de données du lac de données tout en assurant une efficacité de stockage et une pertinence des données optimales.

Ce guide explique comment évaluer, définir et gérer une TTL à l’aide de l’API Catalog Service. Vous apprendrez quand et pourquoi appliquer une durée de vie, comment configurer et mettre à jour les valeurs de durée de vie à l’aide d’appels d’API, ainsi que les bonnes pratiques pour garantir une implémentation efficace.

>[!IMPORTANT]
>
> La durée de vie est conçue pour optimiser la gestion du cycle de vie des données et l’efficacité du stockage. Il ne s’agit pas d’un outil de conformité et ne doit pas être utilisé pour les exigences réglementaires. La conformité nécessite souvent des stratégies de gouvernance des données plus larges.

## Pourquoi utiliser la durée de vie pour la gestion des données au niveau des lignes ?

À mesure que les jeux de données se développent, une gestion efficace des données devient de plus en plus importante pour préserver les performances, contrôler les coûts et conserver la pertinence des données. L’expiration des données au niveau des lignes basée sur une durée de vie automatise le nettoyage des données en supprimant les enregistrements obsolètes sans intervention manuelle afin d’optimiser le stockage et d’améliorer l’efficacité du système.

La durée de vie est utile pour gérer les données sensibles au temps qui perdent de leur pertinence au fil du temps. Pensez à mettre en œuvre une durée de vie si vous devez :

- Réduisez les coûts de stockage en supprimant automatiquement les enregistrements obsolètes.
- Améliorez les performances des requêtes en réduisant au minimum les données non pertinentes.
- Maintenez l’hygiène des données en ne conservant que les informations pertinentes.
- Optimisez la conservation des données pour soutenir les objectifs commerciaux.

>[!NOTE]
>
>La rétention du jeu de données d’événement d’expérience s’applique aux données d’événement stockées dans le lac de données. Si vous gérez la rétention dans Real-Time Customer Data Platform, pensez à utiliser les options [Expiration des événements d’expérience](../../profile/event-expirations.md) et [Expiration des profils pseudonymes](../../profile/pseudonymous-profiles.md) avec les paramètres de rétention du lac de données.
>
>Les configurations de durée de vie permettent d’optimiser le stockage en fonction des droits. Bien que les données du magasin de profils (utilisées dans Real-Time CDP) puissent être considérées comme obsolètes et supprimées après 30 jours, les mêmes données d’événement dans le lac de données peuvent rester disponibles pendant 12 à 13 mois (ou plus longtemps selon les droits) pour les cas d’utilisation d’Analytics et de Data Distiller.

### Exemple de secteur {#industry-example}

Prenons l’exemple d’un service de diffusion en continu de vidéos qui effectue le suivi des interactions utilisateur, telles que les vues vidéo, les recherches et les recommandations. Bien que les données d’engagement récentes soient essentielles pour la personnalisation, les journaux d’activité plus anciens (par exemple, les interactions d’il y a plus d’un an) perdent de leur pertinence. En utilisant l’expiration au niveau des lignes, Experience Platform supprime automatiquement les journaux obsolètes, en s’assurant que seules des données actuelles et significatives sont utilisées pour les analyses et les recommandations.

## Évaluation de l’adéquation de la TTL

Avant d’appliquer une politique de rétention, évaluez si votre jeu de données est un bon candidat pour l’expiration au niveau des lignes. Tenez compte des points suivants :

- Pertinence des données au fil du temps : les données plus anciennes offrent-elles une valeur ajoutée ou deviennent-elles obsolètes ?
- Impact sur les processus en aval : la suppression des données aura-t-elle une incidence sur les rapports, les analyses ou les intégrations ?
- Coût du stockage par rapport à la valeur de rétention : la valeur des données plus anciennes justifie-t-elle le coût de leur stockage ?

Si les enregistrements historiques sont essentiels pour l’analyse à long terme ou les opérations commerciales, la durée de vie peut ne pas être la bonne approche. En examinant ces facteurs, vous vous assurez que la durée de vie correspond à vos besoins de conservation des données sans affecter négativement la disponibilité des données.

## Planifier vos requêtes

Avant d’appliquer une durée de vie, utilisez des requêtes pour analyser la taille et la pertinence des jeux de données. L’exécution de requêtes ciblées permet de déterminer la quantité de données conservée ou supprimée dans différentes configurations de TTL.

Par exemple, la requête SQL suivante comptabilise le nombre d’enregistrements créés au cours des 30 derniers jours :

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

L’exécution de requêtes similaires pour différents intervalles de temps permet de valider les paramètres de TTL et de s’assurer qu’ils équilibrent l’efficacité du stockage et l’accessibilité des données.

## Prise en main de la gestion des TTL

Avant de pouvoir évaluer, définir et gérer la conservation des jeux de données d’événement d’expérience à l’aide de l’API Catalog Service, vous devez comprendre comment formater correctement vos requêtes. Cela inclut la connaissance des chemins d’API, la fourniture des en-têtes requis et le formatage des payloads des requêtes. Reportez-vous au [guide de prise en main de l’API Catalog Service](../api/getting-started.md) pour obtenir ces informations essentielles.

>[!NOTE]
>
>Ce document couvre l’expiration au niveau des lignes, qui supprime les lignes expirées individuelles d’un jeu de données tout en conservant le jeu de données lui-même intact. Elle ne s’applique pas à l’expiration des jeux de données, qui supprime des jeux de données entiers et est gérée par une fonctionnalité distincte. Pour l’expiration au niveau du jeu de données, consultez la documentation [API d’expiration de jeu de données](../../hygiene/api/dataset-expiration.md).

### Comment vérifier les paramètres TTL actuels

Pour commencer la gestion de votre TTL, vérifiez d’abord les paramètres de TTL actuels. Envoyez une requête GET au point d’entrée `/ttl/{datasetId}` pour récupérer les paramètres de durée de vie par défaut, maximum et minimum d’un jeu de données. Cette étape est nécessaire, car les règles de durée de vie peuvent varier en fonction du type de jeu de données.

>[!TIP]
>
>L’URL de la passerelle Experience Platform et le chemin d’accès de base de l’API Catalog Service sont les suivants : `https://platform.adobe.io/data/foundation/catalog`.

**Format d’API**

```http
GET /ttl/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Chaîne générée par le système qui identifie de manière unique un jeu de données. Pour trouver un identifiant de jeu de données, utilisez le point d’entrée `/datasets`. Pour obtenir des instructions sur le filtrage des réponses pour les jeux de données pertinents](../api/list-objects.md) consultez le guide [API list catalog objects). |

**Requête**

La requête suivante récupère les paramètres de durée de vie de votre organisation pour un jeu de données spécifique.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie la configuration de durée de vie du jeu de données, y compris les valeurs de durée de vie par défaut, maximale et minimale pour le stockage `adobe_lakeHouse` et `adobe_unifiedProfile`.

+++Sélectionner pour afficher la réponse

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propriété | Description |
|--------------|-------------|
| `defaultValue` | Période de TTL par défaut appliquée si aucune durée de vie personnalisée n’est définie. |
| `maxValue` | Durée de vie la plus longue autorisée pour le jeu de données. Si cette valeur est nulle, il n’existe aucune limite maximale. |
| `minValue` | La durée de vie la plus courte autorisée pour garantir la conformité aux politiques système. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Comment définir une durée de vie pour un jeu de données {#set-ttl}

>[!IMPORTANT]
>
>L’expiration des lignes ne peut être appliquée qu’aux jeux de données d’événements qui utilisent un schéma de série temporelle. Avant de définir la durée de vie, vérifiez que le schéma du jeu de données étend `https://ns.adobe.com/xdm/data/time-series` pour vous assurer que la requête API réussit. Utilisez l’API Schema Registry pour récupérer les détails du schéma et vérifier la propriété `meta:extends`. Reportez-vous à la [documentation sur le point d’entrée du schéma](../../xdm/api/schemas.md#lookup) pour obtenir des conseils sur la manière de procéder.

Pour configurer la conservation du jeu de données d’événement d’expérience pour votre jeu de données, définissez une nouvelle valeur de TTL en adressant une requête PATCH au point d’entrée `/v2/datasets/{ID}`.

**Format d’API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | L’identifiant du jeu de données pour lequel vous souhaitez mettre à jour la valeur de TTL. |

**Requête**

Dans l’exemple de requête ci-dessous, la `ttlValue` est définie sur `P3M`. Cela permet de s’assurer que les enregistrements de plus de trois mois sont automatiquement supprimés. Vous pouvez ajuster la période de conservation en fonction des besoins de votre entreprise en utilisant des valeurs telles que `P6M` pendant six mois ou `P12M` pendant un an.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

**Réponse**

Une réponse réussie affiche la configuration de durée de vie du jeu de données. Elle comprend des détails sur les paramètres d’expiration au niveau des lignes pour le stockage `adobe_lakeHouse` et `adobe_unifiedProfile`.

+++Sélectionner pour afficher la réponse

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propriété | Description |
|----------------------------------|-------------|
| `extensions` | Conteneur pour les métadonnées supplémentaires liées au jeu de données. |
| `extensions.adobe_lakeHouse` | Spécifie les paramètres liés à l’architecture de stockage, y compris les configurations d’expiration au niveau des lignes |
| `rowExpiration` | L’objet contient des paramètres de durée de vie qui définissent la période de conservation du jeu de données. |
| `rowExpiration.ttlValue` | Définit la durée avant que les enregistrements du jeu de données ne soient automatiquement supprimés. Utilise le format de période ISO-8601 (par exemple, `P3M` pour 3 mois ou `P30D` pour une semaine). |
| `rowExpiration.valueStatus` | La chaîne indique si le paramètre de durée de vie est une valeur système par défaut ou une valeur personnalisée définie par un utilisateur. Les valeurs possibles sont : `default`, `custom`. |
| `rowExpiration.setBy` | Indique qui a effectué la dernière modification du paramètre TTL. Les valeurs possibles sont les suivantes : `user` (défini manuellement) ou `service` (affecté automatiquement). |
| `rowExpiration.updated` | Date et heure de la dernière mise à jour de TTL. Cette valeur indique la date de la dernière modification du paramètre de durée de vie. |

### Comment mettre à jour la TTL {#update-ttl}

Prolongez ou raccourcissez la période de conservation en fonction des besoins de votre entreprise en ajustant le TTL. Par exemple, en ce qui concerne la plateforme de diffusion en continu de vidéos mentionnée précédemment, la plateforme peut initialement définir la durée de vie à trois mois pour garantir de nouvelles données d’engagement à des fins de personnalisation. Cependant, si leur analyse montre que les schémas d’interaction datant de plus de trois mois fournissent toujours des informations précieuses, ils peuvent étendre la période de TTL à six mois afin de conserver des enregistrements plus anciens pour de meilleurs modèles de recommandation.

Pour modifier une valeur de durée de vie existante, utilisez la méthode `PATCH` sur le point d’entrée `/v2/datasets/{DATASET_ID}`.

#### Format d’API

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Requête**

Dans la requête suivante, la TTL est mise à jour à six mois (`P6M`) en étendant la période de conservation des enregistrements avant la suppression automatique.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Réponse**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Bonnes pratiques pour définir la durée de vie {#best-practices}

Le choix de la valeur de durée de vie appropriée est essentiel pour vous assurer que votre politique de conservation des jeux de données d’événements d’expérience équilibre la conservation des données, l’efficacité du stockage et les besoins analytiques. Une durée de vie trop courte peut entraîner une perte de données, tandis qu’une durée de vie trop longue peut augmenter les coûts de stockage et entraîner une accumulation de données inutile. Assurez-vous que la durée de vie correspond à l’objectif de votre jeu de données en tenant compte de la fréquence d’accès aux données et de la durée pendant laquelle elles restent pertinentes.

Le tableau ci-dessous fournit des recommandations courantes relatives à la durée de vie en fonction du type de jeu de données et des schémas d’utilisation :

| Type de jeu de données | Durée de vie recommandée | Cas d’utilisation standard |
|-----------------------------|------------------------|-------------------|
| Jeux de données fréquemment consultés | 30-90 jours | Journaux d’engagement des utilisateurs, données de parcours de navigation sur le site web, données de performances de campagne à court terme. |
| Archiver des jeux de données | 1 an ou plus | Journaux de transactions financières, données de conformité, analyse des tendances à long terme, jeux de données de formation en machine learning. |
| Jeux de données gérés par l’application | Jusqu’à 13 mois | Les jeux de données gérés par le système comportent des restrictions de durée de vie prédéfinies, qui sont automatiquement appliquées pour se conformer aux limites imposées par le système. |
| Jeux de données gérés par le client | 30 jours - Durée de vie maximale | Jeux de données créés via l’interface utilisateur, les API ou la Distiller de données. La durée de vie doit être d’au moins 30 jours et comprise dans la durée de vie maximale définie. |

Passez régulièrement en revue les paramètres de durée de vie pour vous assurer qu’ils continuent de s’aligner sur vos politiques de stockage, vos besoins analytiques et vos exigences commerciales.

### Considérations principales lors de la définition de la durée de vie

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Suivez ces bonnes pratiques pour vous assurer que les paramètres de durée de vie s’alignent sur votre stratégie de conservation des données :

- Le TTL d’audit change régulièrement. Chaque mise à jour de TTL déclenche un événement d’audit. Utilisez les journaux d’audit pour suivre les modifications de TTL à des fins de conformité, de gouvernance des données et de dépannage.
- Supprimer la durée de vie si les données doivent être conservées indéfiniment. Pour désactiver la durée de vie, définissez `ttlValue` sur `null`. Cela empêche l’expiration automatique et conserve tous les enregistrements de manière permanente. Tenez compte des implications du stockage avant d’effectuer cette modification.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Limites de TTL {#limitations}

Gardez à l’esprit les limites suivantes lors de l’utilisation de TTL :

- **La rétention du jeu de données d’événement d’expérience à l’aide de la durée de vie s’applique à l’expiration au niveau des lignes** et non à la suppression du jeu de données. La durée de vie supprime les enregistrements en fonction d’une période de conservation définie, mais ne supprime pas les jeux de données entiers. Pour supprimer un jeu de données, utilisez le point d’entrée [expiration du jeu de données](../../hygiene/api/dataset-expiration.md) ou la suppression manuelle.
- **TTL ne peut pas être supprimé**, uniquement mis à jour. Une fois appliquée, la durée de vie ne peut pas être supprimée. Vous pouvez toutefois [modifier la période de conservation](#update-ttl) pour la prolonger ou la raccourcir. Pour conserver les données indéfiniment, définissez une TTL suffisamment longue au lieu d’essayer de la supprimer.
- **TTL n’est pas un outil de conformité**. TTL optimise le stockage et la gestion du cycle de vie des données, mais ne répond pas aux exigences réglementaires de conservation des données. Pour la conformité, mettez en œuvre des stratégies de gouvernance des données plus larges.

## FAQ sur la politique de conservation des jeux de données {#faqs}

Cette section fournit des réponses aux questions courantes sur les politiques de conservation des jeux de données dans Adobe Experience Platform.

### À quels types de jeux de données puis-je appliquer des règles de politique de rétention ?

+++Réponse
Vous pouvez appliquer des politiques de rétention aux jeux de données créés à l’aide de la classe XDM ExperienceEvent. Pour les services de profil, les politiques de conservation ne s’appliquent qu’aux jeux de données d’événements d’expérience qui ont été activés pour Profil.
+++

### Dans combien de temps la tâche de conservation des jeux de données supprimera-t-elle les données des services de lac de données ?

+++Réponse
Les TTL des jeux de données sont évaluées et traitées chaque semaine, supprimant tous les enregistrements expirés. Un événement est considéré comme ayant expiré s’il a été ingéré dans Experience Platform il y a plus de 30 jours (date d’ingestion > 30 jours) et si sa date d’événement dépasse la période de conservation définie (TTL).
+++

### Quand la tâche de conservation des jeux de données supprimera-t-elle les données des services de profil ?

+++Réponse
Une fois qu’une politique de conservation est définie, les événements existants dans Experience Platform sont immédiatement supprimés si leur horodatage d’événement dépasse la période de conservation (TTL). Les nouveaux événements sont supprimés une fois que leur horodatage dépasse la période de conservation.

Par exemple, si vous appliquez une politique d’expiration de 30 jours le 15 mai, ce qui suit se produit :

- Les nouveaux événements sont soumis à une expiration de 30 jours lors de leur ingestion.
- Les événements existants dont la date et heure sont antérieures au 15 avril sont immédiatement supprimés.
- Les événements existants dont la date et heure sont postérieures au 15 avril sont définis pour expirer 30 jours après leur date et heure (par exemple, un événement daté du 18 avril sera supprimé le 18 mai).
+++

### Puis-je définir différentes politiques de conservation pour les services de lac de données et de profil ?

+++Réponse
Oui, vous pouvez définir différentes politiques de conservation pour les services de lac de données et de profil. Cependant, la période de conservation du profil ne doit pas être plus courte que celle définie pour le lac de données.
+++

### Comment puis-je vérifier l’utilisation actuelle de mon jeu de données ?

+++Réponse
Vous pouvez vérifier la dernière taille de stockage du jeu de données pour le lac de données et les magasins de profils en tant que mesures distinctes sur l’espace de travail d’inventaire [!UICONTROL Jeu de données]. Triez les colonnes pour identifier les jeux de données les plus volumineux et vérifiez que les politiques de conservation sont appliquées.

Pour plus d’informations sur l’utilisation au niveau du sandbox, consultez le tableau de bord Utilisation des licences . Pour plus d’informations, consultez la [documentation relative à l’utilisation des licences](../../dashboards/guides/license-usage.md).
+++

### Comment puis-je vérifier si la tâche de conservation des données a réussi ?

+++Réponse
Vous pouvez vérifier la dernière tâche de conservation des données en vérifiant sa date et l’heure dans l’[interface utilisateur de configuration de la conservation des jeux de données](./user-guide.md#data-retention-policy) ou sur la page Inventaire des données .

La création de rapports sur l’utilisation des jeux de données historiques est actuellement indisponible.
+++

### Puis-je récupérer les données supprimées ?

+++Réponse
Non, une fois qu’une politique de conservation est appliquée, toutes les données antérieures à la période de conservation sont supprimées définitivement et ne peuvent pas être récupérées.
+++

### Quelle est la durée de vie minimale que je peux configurer sur un jeu de données Événement d’expérience de lac de données ?

+++Réponse
La durée de vie minimale d’un jeu de données Événement d’expérience de lac de données est de 30 jours. Le lac de données fonctionne comme un système de sauvegarde et de récupération de traitement lors de l’ingestion et du traitement initiaux. Par conséquent, les données doivent rester dans le lac de données pendant au moins 30 jours après l’ingestion avant de pouvoir expirer.
+++

### Que se passe-t-il si je dois conserver certains champs du lac de données plus longtemps que ne le permet ma politique de TTL ?

+++Réponse
Utilisez la Distiller de données pour conserver des champs spécifiques au-delà de la durée de vie du jeu de données tout en respectant vos limites d’utilisation. Créez une tâche qui n’écrit régulièrement que les champs nécessaires dans un jeu de données dérivé. Ce workflow assure la conformité avec une durée de vie plus courte tout en préservant les données critiques pour une utilisation prolongée.

Pour plus d’informations, consultez le guide [Créer des jeux de données dérivés avec SQL](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Étapes suivantes {#next-steps}

Maintenant que vous avez appris à gérer les paramètres de TTL pour l’expiration au niveau des lignes, consultez la documentation suivante pour mieux comprendre la gestion des TTL :

- Tâches de conservation : découvrez comment planifier et automatiser les expirations de jeux de données dans l’interface utilisateur d’Experience Platform à l’aide du [ guide de l’interface utilisateur du cycle de vie des données ](../../hygiene/ui/dataset-expiration.md) ou vérifiez les configurations de conservation des jeux de données et que les enregistrements expirés sont supprimés.
- [Guide du point d’entrée de l’API d’expiration de jeu de données](../../hygiene/api/dataset-expiration.md) : découvrez comment supprimer des jeux de données entiers plutôt que seulement des lignes. Découvrez comment planifier, gérer et automatiser l’expiration des jeux de données à l’aide de l’API pour garantir une conservation efficace des données.
- [Présentation des politiques d’utilisation des données](../../data-governance/policies/overview.md) : découvrez comment aligner votre stratégie de conservation des données sur les exigences de conformité plus larges et les restrictions d’utilisation marketing.
