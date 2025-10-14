---
title: Gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL
description: Découvrez comment évaluer, définir et gérer la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de configurations de durée de vie (TTL) avec des API Adobe Experience Platform. Ce guide explique comment l’expiration au niveau des lignes de TTL prend en charge les politiques de conservation des données, optimise l’efficacité du stockage et garantit une gestion efficace du cycle de vie des données. Elle fournit également des cas d’utilisation et des bonnes pratiques pour vous aider à appliquer efficacement la durée de vie.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: a4662d1042122fa9c3260c0e53c50bd78935cf31
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 1%

---

# Gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL

Une gestion efficace des données est essentielle pour optimiser les performances, le contrôle des coûts et l’intégrité des données. Utilisez la durée de vie (TTL) de conservation des jeux de données d’événements d’expérience pour appliquer l’expiration au niveau des lignes, supprimant automatiquement les enregistrements obsolètes des jeux de données du lac de données tout en assurant une efficacité de stockage et une pertinence des données optimales.

Ce guide explique comment évaluer, définir et gérer une TTL à l’aide de l’API Catalog Service. Vous apprendrez quand et pourquoi appliquer une durée de vie, comment configurer et mettre à jour les valeurs de durée de vie à l’aide d’appels d’API, ainsi que les bonnes pratiques pour garantir une implémentation efficace.

>[!IMPORTANT]
>
>La durée de vie est conçue pour optimiser la gestion du cycle de vie des données et l’efficacité du stockage. Il ne s’agit pas d’un outil de conformité et ne doit pas être utilisé pour les exigences réglementaires. La conformité nécessite souvent des stratégies de gouvernance des données plus larges.

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

Utilisez les configurations de durée de vie pour optimiser le stockage en fonction des droits. Bien que les données du magasin de profils (utilisées dans Real-Time CDP) puissent être considérées comme obsolètes et supprimées après 30 jours, les mêmes données d’événement dans le lac de données peuvent rester disponibles pendant 12 à 13 mois (ou plus longtemps selon les droits) pour les cas d’utilisation d’Analytics et de Data Distiller.

>[!TIP]
>
>Les droits se rapportent aux quotas de stockage et de rétention définis par votre abonnement Adobe et vos contrats de licence.

### Exemple de secteur {#industry-example}

Prenons l’exemple d’un service de diffusion en continu de vidéos qui effectue le suivi des interactions utilisateur, telles que les vues vidéo, les recherches et les recommandations. Bien que les données d’engagement récentes soient essentielles pour la personnalisation, les journaux d’activité plus anciens (par exemple, les interactions d’il y a plus d’un an) perdent de leur pertinence. En utilisant l’expiration au niveau des lignes, Experience Platform supprime automatiquement les journaux obsolètes, en s’assurant que seules des données actuelles et significatives sont utilisées pour les analyses et les recommandations.

## Évaluation de l’adéquation de la TTL {#evaluate-ttl-suitability}

Avant d’appliquer une politique de rétention, évaluez si votre jeu de données est un bon candidat pour l’expiration au niveau des lignes. Tenez compte des points suivants :

- Pertinence des données au fil du temps : les données plus anciennes offrent-elles une valeur ajoutée ou deviennent-elles obsolètes ?
- Impact sur les processus en aval : la suppression des données aura-t-elle une incidence sur les rapports, les analyses ou les intégrations ?
- Coût du stockage par rapport à la valeur de rétention : la valeur des données plus anciennes justifie-t-elle le coût de leur stockage ?

Si les enregistrements historiques sont essentiels pour l’analyse à long terme ou les opérations commerciales, la durée de vie peut ne pas être la bonne approche. En examinant ces facteurs, vous vous assurez que la durée de vie correspond à vos besoins de conservation des données sans affecter négativement la disponibilité des données.

## Bonnes pratiques pour définir la durée de vie {#best-practices}

Sélectionnez la valeur de TTL appropriée pour vous assurer que votre politique de conservation des jeux de données d’événements d’expérience équilibre entre la conservation des données, l’efficacité du stockage et les besoins analytiques. Une durée de vie trop courte peut entraîner une perte de données, tandis qu’une durée de vie trop longue peut augmenter les coûts de stockage et entraîner une accumulation de données inutile. Assurez-vous que la durée de vie correspond à l’objectif de votre jeu de données en tenant compte de la fréquence d’accès aux données et de la durée pendant laquelle elles restent pertinentes.

Le tableau ci-dessous fournit des recommandations courantes relatives à la durée de vie en fonction du type de jeu de données et des schémas d’utilisation :

| Type de jeu de données | Durée de vie recommandée | Cas d’utilisation standard |
|-----------------------------|------------------------|-------------------|
| Jeux de données fréquemment consultés | 30-90 jours | Journaux d’engagement des utilisateurs, données de parcours de navigation sur le site web, données de performances de campagne à court terme. |
| Archiver des jeux de données | 1 an ou plus | Journaux de transactions financières, données de conformité, analyse des tendances à long terme, jeux de données de formation en machine learning. |
| Jeux de données gérés par l’application | Jusqu’à 13 mois | Les jeux de données gérés par le système comportent des restrictions de durée de vie prédéfinies, qui sont automatiquement appliquées pour se conformer aux limites imposées par le système. |
| Jeux de données gérés par le client | 30 jours - Durée de vie maximale | Jeux de données créés via l’interface utilisateur, les API ou la Distiller de données. La durée de vie doit être d’au moins 30 jours et comprise dans la durée de vie maximale définie. |

Passez régulièrement en revue les paramètres de durée de vie pour vous assurer qu’ils continuent de s’aligner sur vos politiques de stockage, vos besoins analytiques et vos exigences commerciales.

### Considérations principales lors de la définition de la durée de vie {#key-considerations}

Suivez ces bonnes pratiques pour vous assurer que les paramètres de durée de vie s’alignent sur votre stratégie de conservation des données :

- Le TTL d’audit change régulièrement. Chaque mise à jour de TTL déclenche un événement d’audit. Utilisez les journaux d’audit pour suivre les modifications de TTL à des fins de conformité, de gouvernance des données et de dépannage.
- Désactivez TTL si les données doivent être conservées indéfiniment. Pour désactiver la durée de vie, définissez `ttlValue` sur `null`. Cela empêche l’expiration automatique et conserve tous les enregistrements de manière permanente. Tenez compte des implications du stockage avant d’effectuer cette modification.

## Limites de TTL {#limitations}

Gardez à l’esprit les limites suivantes lors de l’utilisation de TTL :

- **La rétention du jeu de données d’événement d’expérience à l’aide de la durée de vie s’applique à l’expiration au niveau des lignes** et non à la suppression du jeu de données. La durée de vie supprime les enregistrements en fonction d’une période de conservation définie, mais ne supprime pas les jeux de données entiers. Pour supprimer un jeu de données, utilisez le point d’entrée [expiration du jeu de données](../../hygiene/api/dataset-expiration.md) ou la suppression manuelle.
- **La configuration de durée de vie reste active jusqu’à ce qu’elle soit explicitement désactivée**. La configuration reste en vigueur jusqu’à ce que vous la désactiviez. La désactivation de la durée de vie arrête l’expiration et garantit que tous les enregistrements du jeu de données sont conservés.
- **TTL n’est pas un outil de conformité**. Bien que la durée de vie optimise le stockage et la gestion du cycle de vie, vous devez mettre en œuvre des stratégies de gouvernance plus larges pour garantir la conformité réglementaire.

## Analyser la taille et la pertinence du jeu de données avant d’appliquer la TTL {#analyze-dataset-size}

Avant d’appliquer une durée de vie, utilisez des requêtes pour analyser la taille et la pertinence des jeux de données. Exécutez des requêtes ciblées (comme le comptage des enregistrements dans des périodes spécifiques) pour prévisualiser l’impact de différentes valeurs de durée de vie. Utilisez ensuite ces informations pour choisir une période de conservation optimale qui équilibre l’utilité des données et le rapport coût-efficacité.

![Workflow visuel pour l’implémentation de TTL sur des jeux de données d’événements d’expérience. Les étapes sont les suivantes : évaluation de la durée de vie des données et de l’impact de la suppression, validation des paramètres de TTL avec des requêtes, configuration de TTL par le biais de l’API Catalog Service et surveillance continue de l’impact de TTL et ajustements](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

L’exécution de requêtes ciblées permet de déterminer la quantité de données conservée ou supprimée dans différentes configurations de TTL. Par exemple, la requête SQL suivante comptabilise le nombre d’enregistrements créés au cours des 30 derniers jours :

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

L’exécution de requêtes similaires pour différents intervalles de temps permet de valider les paramètres de TTL et de s’assurer qu’ils équilibrent l’efficacité du stockage et l’accessibilité des données.

## Prise en main de la gestion des TTL

Avant de pouvoir évaluer, définir et gérer la conservation des jeux de données d’événement d’expérience à l’aide de l’API Catalog Service, vous devez comprendre comment formater correctement vos requêtes. Cela inclut la connaissance des chemins d’API, la fourniture des en-têtes requis et le formatage des payloads des requêtes. Reportez-vous au [guide de prise en main de l’API Catalog Service](../api/getting-started.md) pour obtenir ces informations essentielles.

>[!NOTE]
>
>Ce document couvre l’expiration au niveau des lignes, qui supprime les lignes expirées individuelles d’un jeu de données tout en conservant le jeu de données lui-même intact. Elle ne s’applique pas à l’expiration des jeux de données, qui supprime des jeux de données entiers et est gérée par une fonctionnalité distincte. Pour l’expiration au niveau du jeu de données, consultez la documentation [API d’expiration de jeu de données](../../hygiene/api/dataset-expiration.md).

### Vérifier vos contraintes de durée de vie {#check-ttl-constraints}

Utilisez le point d’entrée `/ttl/{DATASET_ID}` de l’API Data Hygiene pour planifier les configurations de TTL. Ce point d’entrée renvoie les valeurs de durée de vie minimale et maximale prises en charge pour votre organisation, ainsi qu’une valeur recommandée (`defaultValue`) pour le type de jeu de données.

Pour plus d’informations, consultez la documentation d’Adobe Developer [API Data Hygiene](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) .

Pour [vérifier la TTL actuellement appliquée à un jeu de données](#check-applied-ttl-values), envoyez plutôt une requête GET au point d’entrée de [&#128279;](https://developer.adobe.com/experience-platform-apis/references/catalog/)API Catalog Service`/dataSets/{DATASET_ID}`.

>[!TIP]
>
>L’URL de la passerelle Experience Platform et le chemin d’accès de base de l’API Catalog Service sont les suivants : `https://platform.adobe.io/data/foundation/catalog`. Le chemin d’accès de base de l’API Data Hygiene est le suivant : `https://platform.adobe.io/data/core/hygiene`

**Format d’API**

```http
GET /ttl/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Chaîne générée par le système qui identifie de manière unique un jeu de données. Pour trouver un identifiant de jeu de données, utilisez le point d’entrée `/datasets`. Pour obtenir des instructions sur le filtrage des réponses pour les jeux de données pertinents[&#x200B; consultez le guide &#x200B;](../api/list-objects.md)API list catalog objects). |

**Requête**

La requête suivante récupère les contraintes de durée de vie de votre organisation pour un jeu de données spécifique.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie les valeurs de TTL recommandées, maximales et minimales en fonction des droits de votre organisation, ainsi qu’une durée de vie suggérée (`defaultValue`) pour le jeu de données. Il s’`defaultValue` d’une durée de vie recommandée, fournie uniquement à titre indicatif. Elle n’est pas appliquée, sauf si vous la configurez explicitement. La réponse n’inclut aucune valeur de durée de vie personnalisée déjà définie. Pour afficher la TTL actuelle d’un jeu de données, utilisez le point d’entrée `/catalog/dataSets/{DATASET_ID}` GET.

+++Sélectionner pour afficher la réponse

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Propriété | Description |
|--------------|-------------|
| `defaultValue` | Valeur de durée de vie recommandée pour votre jeu de données. Cette valeur n’est **pas** appliquée automatiquement. Vous devez définir explicitement une TTL pour qu’elle prenne effet. |
| `maxValue` | Durée de vie maximale autorisée par les droits de votre organisation. En règle générale, cette durée est de 10 ans (`P10Y`). |
| `minValue` | Durée de vie minimale autorisée par les droits de votre organisation. En règle générale, cette durée est de 30 jours (`P30D`). |

### Comment vérifier les valeurs de durée de vie appliquées {#check-applied-ttl-values}

Pour vérifier la valeur de durée de vie actuelle qui a été appliquée à un jeu de données, utilisez l’appel API suivant :

```http
GET /dataSets/{DATASET_ID}
```

Cet appel renvoie la `ttlValue` actuelle (si elle est définie) dans la section `extensions.adobe_lakeHouse.rowExpiration`.

**Requête**

La requête suivante récupère la valeur de durée de vie de votre organisation pour un jeu de données spécifique.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie inclut l’objet `extensions` , qui contient la configuration de TTL actuelle appliquée au jeu de données. L’exemple de réponse ci-dessous est tronqué par souci de concision.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Définir ou mettre à jour une TTL pour un jeu de données {#set-update-ttl}

>[!IMPORTANT]
>
>L’expiration au niveau des lignes basée sur une durée de vie ne peut être appliquée qu’aux jeux de données d’événement qui utilisent un schéma de série temporelle. Cela inclut les jeux de données basés sur la classe XDM ExperienceEvent standard, ainsi que les schémas personnalisés qui étendent le schéma de série temporelle (`https://ns.adobe.com/xdm/data/time-series`).
>
>Avant d’appliquer la durée de vie, utilisez l’API Schema Registry pour vérifier que le schéma du jeu de données inclut l’extension correcte en vérifiant la propriété `meta:extends`. Consultez la [documentation sur les points d’entrée de schéma](../../xdm/api/schemas.md#lookup) pour obtenir des conseils sur la manière de procéder.

Vous pouvez configurer la conservation des jeux de données d’événements d’expérience en définissant une nouvelle TTL ou en mettant à jour une TTL existante à l’aide de la même méthode API. Utilisez une requête PATCH au point d’entrée `/v2/datasets/{DATASET_ID}` pour appliquer ou ajuster la durée de vie.

**Format d’API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | L’identifiant du jeu de données pour lequel vous souhaitez mettre à jour la valeur de TTL. |

**Requête**

Dans l’exemple ci-dessous, la `ttlValue` est définie sur `P3M`. Cela signifie que les enregistrements de plus de trois mois sont automatiquement supprimés. Ajustez la période de conservation en fonction des besoins de votre entreprise (par exemple, `P6M` pendant six mois ou `P12M` pendant un an).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Propriété | Description |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Définit la durée avant que les enregistrements du jeu de données ne soient automatiquement supprimés. Utilise le format de période ISO-8601 (par exemple, `P3M` pendant 3 mois ou `P30D` pendant 30 jours). |

**Réponse**

Une réponse réussie renvoie une référence au jeu de données mis à jour, mais n’inclut pas explicitement les paramètres de TTL. Pour confirmer la configuration de la TTL, envoyez une requête de `GET /dataSets/{DATASET_ID}` de suivi.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Exemple de scénario {#example-scenario}

Prenons l’exemple d’une plateforme de streaming vidéo qui définit initialement la durée de vie sur trois mois afin de garantir de nouvelles données d’engagement pour la personnalisation. Cependant, si l’analyse ultérieure révèle que les interactions plus anciennes fournissent toujours des informations précieuses, la durée de vie peut être étendue à six mois avec la requête suivante :

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## FAQ sur la politique de conservation des jeux de données {#faqs}

Cette FAQ aborde des questions pratiques sur les tâches de conservation des jeux de données, les effets immédiats des modifications de durée de vie, les options de récupération et les différences de périodes de conservation entre les services Platform.

### À quels types de jeux de données puis-je appliquer des règles de politique de rétention ?

+++Réponse
Vous pouvez appliquer des politiques de rétention basées sur la durée de vie à n’importe quel jeu de données qui utilise le comportement de série temporelle. Cela inclut les jeux de données basés sur la classe XDM ExperienceEvent standard, ainsi que les schémas personnalisés conçus pour capturer des données de série temporelle.

L’expiration au niveau des lignes nécessite les conditions techniques suivantes :

- Le schéma doit être conçu pour capturer des données de série temporelle.
- Le schéma doit inclure un champ de date et heure utilisé pour évaluer l’expiration.
- Le jeu de données doit stocker des données au niveau de l’événement, en utilisant ou en étendant généralement la classe XDM ExperienceEvent.
- Le jeu de données doit être enregistré dans Catalog Service, car les paramètres de TTL sont appliqués via `extensions.adobe_lakeHouse.rowExpiration`.
- Les valeurs de durée de vie doivent utiliser le format de durée ISO-8601 (par exemple, `P30D`, `P6M`, `P1Y`).
+++

### Dans combien de temps la tâche de conservation des jeux de données supprimera-t-elle les données des services de lac de données ?

+++Réponse
Les TTL des jeux de données sont évaluées et traitées tous les 30 jours, supprimant tous les enregistrements expirés. Un événement est considéré comme ayant expiré s’il a été ingéré dans Experience Platform il y a plus de 30 jours (date d’ingestion > 30 jours) et si sa date d’événement dépasse la période de conservation définie (TTL).
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### Puis-je définir différentes politiques de conservation pour les services de lac de données et de profil ?

+++Réponse

>[!NOTE]
>
>La période de conservation du service de profil ne peut être mise à jour qu’une fois tous les 30 jours.

Oui, vous pouvez définir différentes politiques de conservation pour les services de lac de données et de profil. La période de conservation de la banque de profils peut être plus courte ou plus longue que la période de conservation du lac de données, selon les besoins de votre entreprise.

+++

### Comment puis-je vérifier l’utilisation actuelle de mon jeu de données ?

+++Réponse
Vous pouvez vérifier la dernière taille de stockage du jeu de données pour le lac de données et les magasins de profils en tant que mesures distinctes sur l’espace de travail d’inventaire [!UICONTROL Jeu de données]. Triez les colonnes pour identifier les jeux de données les plus volumineux et vérifiez que les politiques de conservation sont appliquées.

Pour plus d’informations sur l’utilisation au niveau du sandbox, consultez le tableau de bord Utilisation des licences . Pour plus d’informations, consultez la [documentation relative à l’utilisation des licences](../../dashboards/guides/license-usage.md).
+++

### Comment puis-je vérifier si la tâche de conservation des données a réussi ?

+++Réponse
Vous pouvez vérifier la dernière tâche de conservation des données en vérifiant sa date et l’heure dans l’[interface utilisateur de configuration de la conservation des jeux de données](./user-guide.md#data-retention-policy) ou sur la page Inventaire des données .

Vous pouvez également envoyer une requête GET au point d’entrée suivant :

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

La réponse inclut la propriété `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, qui indique la date et l’heure Unix (en millisecondes) auxquelles la tâche TTL la plus récente a été terminée.

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

- Tâches de conservation : découvrez comment planifier et automatiser les expirations de jeux de données dans l’interface utilisateur d’Experience Platform à l’aide du [&#x200B; guide de l’interface utilisateur du cycle de vie des données &#x200B;](../../hygiene/ui/dataset-expiration.md) ou vérifiez les configurations de conservation des jeux de données et que les enregistrements expirés sont supprimés.
- [Guide du point d’entrée de l’API d’expiration de jeu de données](../../hygiene/api/dataset-expiration.md) : découvrez comment supprimer des jeux de données entiers plutôt que seulement des lignes. Découvrez comment planifier, gérer et automatiser l’expiration des jeux de données à l’aide de l’API pour garantir une conservation efficace des données.
- [Présentation des politiques d’utilisation des données](../../data-governance/policies/overview.md) : découvrez comment aligner votre stratégie de conservation des données sur les exigences de conformité plus larges et les restrictions d’utilisation marketing.
