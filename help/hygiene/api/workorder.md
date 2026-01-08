---
title: Supprimer les ordres de travail d'enregistrement
description: Découvrez comment utiliser le point d’entrée /workorder dans l’API Data Hygiene pour gérer les ordres de travail de suppression d’enregistrements dans Adobe Experience Platform. Ce guide couvre les quotas, la chronologie de traitement et l’utilisation des API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 1d923e6c4a344959176abb30a8757095c711a601
workflow-type: tm+mt
source-wordcount: '2541'
ht-degree: 2%

---

# Ordres de travail de suppression d&#39;enregistrements {#work-order-endpoint}

Utilisez le point d’entrée `/workorder` dans l’API Data Hygiene pour créer, afficher et gérer des ordres de travail de suppression d’enregistrements dans Adobe Experience Platform. Les ordres de travail vous permettent de contrôler, de surveiller et de suivre la suppression des données dans les jeux de données afin de vous aider à maintenir la qualité des données et à respecter les normes de gouvernance des données de votre entreprise.

>[!IMPORTANT]
>
>Les ordres de travail de suppression des enregistrements concernent le nettoyage des données, la suppression des données anonymes ou la minimisation des données. **N’utilisez pas d’ordres de travail de suppression d’enregistrements pour les demandes de droits des titulaires de données dans le cadre des réglementations de confidentialité telles que le RGPD.** Pour les cas d’utilisation de conformité, utilisez [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Commencer

Avant de commencer, consultez la [présentation](./overview.md) pour en savoir plus sur les en-têtes requis, sur la lecture d’exemples d’appels API et sur l’emplacement de la documentation connexe.

## Quotas et délais de traitement {#quotas}

Les ordres de travail de suppression d’enregistrements sont soumis à des limites d’envoi d’identifiants quotidiennes et mensuelles, déterminées par les droits de licence de votre entreprise. Ces limites s’appliquent à la fois aux requêtes de suppression d’enregistrements basées sur l’interface utilisateur et les API.

>[!NOTE]
>
>Vous pouvez envoyer jusqu’à 1 000 000 **d’identifiants par jour** mais uniquement si votre quota mensuel restant le permet. Si votre limite mensuelle est inférieure à 1 million, vos soumissions quotidiennes ne peuvent pas dépasser cette limite.

### Droit d’envoi mensuel par produit {#quota-limits}

Le tableau suivant présente les limites d’envoi des identifiants par produit et niveau de droit. Pour chaque produit, la limite mensuelle est la moins élevée des deux valeurs suivantes : un plafond d’identifiant fixe ou un seuil basé sur un pourcentage lié à votre volume de données sous licence.

| Produit | Description du droit | Plafond mensuel (le moins élevé) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 5 % de l’audience adressable |
| Real-Time CDP ou Adobe Journey Optimizer | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 10 % de l’audience adressable |
| Customer Journey Analytics | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 100 d’identifiants par million de lignes CJA de droits |
| Customer Journey Analytics | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 200 d’identifiants par million de lignes CJA de droits |

>[!NOTE]
>
>La plupart des entreprises ont des limites mensuelles inférieures en fonction de leur audience adressable réelle ou de leurs droits de ligne CJA.

>[!NOTE]
>
>Les quotas sont réinitialisés le premier jour de chaque mois civil. Le quota inutilisé n **est pas reporté**

>[!NOTE]
>
>L’utilisation du quota est basée sur les droits mensuels sous licence de votre entreprise pour les **identifiants envoyés**. Les quotas ne sont pas appliqués par les mécanismes de sécurisation du système, mais peuvent être surveillés et révisés.\
>La capacité des ordres de travail de suppression des enregistrements est un **service partagé**. Votre limite mensuelle reflète les droits les plus élevés pour Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics et tous les modules complémentaires Shield applicables.

### Chronologies de traitement des envois d’identifiants {#sla-processing-timelines}

Après l’envoi, les ordres de travail de suppression d’enregistrements sont mis en file d’attente et traités en fonction de votre niveau de droit.

| Description du produit et des droits | Durée de la file d’attente | Durée Maximale De Traitement (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | Jusqu’à 15 jours | 30 jours |
| Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | Généralement 24 heures | 15 jours |

Si votre organisation requiert des limites plus élevées, contactez votre représentant Adobe pour une révision des droits.

>[!TIP]
>
>Pour vérifier votre niveau d’utilisation ou de droit de quota actuel, consultez le [Guide de référence des quotas](../api/quota.md).

## Liste des ordres de travail de suppression d&#39;enregistrements {#list}

Récupérez une liste paginée des ordres de travail de suppression d’enregistrements pour les opérations d’hygiène des données dans votre organisation. Filtrez les résultats à l’aide des paramètres de requête. Chaque enregistrement d’ordre de travail inclut le type d’action (tel que `identity-delete`), le statut, les détails du jeu de données et de l’utilisateur associés, ainsi que les métadonnées d’audit.

**Format d’API**

```http
GET /workorder
```

Le tableau suivant décrit les paramètres de requête disponibles pour répertorier les ordres de travail de suppression d&#39;enregistrements.

| Paramètre de requête | Description |
| --------------- | ------------|
| `search` | Correspondance partielle non sensible à la casse (recherche par caractères génériques) dans les champs : auteur, displayName, description ou datasetName. Correspond également à l’ID d’expiration exact. |
| `type` | Filtrez les résultats par type d’ordre de travail (par exemple, `identity-delete`). |
| `status` | Liste des statuts d’ordres de travail séparés par des virgules. Les valeurs de statut respectent la casse.<br>Enum : `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Recherchez la personne qui a mis à jour l’ordre de travail le plus récemment (ou le créateur initial). Accepte le modèle littéral ou SQL. |
| `displayName` | Correspondance insensible à la casse pour le nom d’affichage de l’ordre de travail. |
| `description` | Correspondance insensible à la casse pour la description de l’ordre de travail. |
| `workorderId` | Correspondance exacte pour l’ID d’ordre de travail. |
| `sandboxName` | Correspondance exacte pour le nom du sandbox utilisé dans la requête, ou utilisez `*` pour inclure tous les sandbox. |
| `fromDate` | Filtrez par ordres de travail créés à cette date ou ultérieurement. Nécessite que `toDate` soit défini. |
| `toDate` | Filtrez par ordres de travail créés à cette date ou avant. Nécessite que `fromDate` soit défini. |
| `filterDate` | Renvoie uniquement les ordres de travail créés, mis à jour ou dont le statut a été modifié à cette date. |
| `page` | Index de page à renvoyer (commence à 0). |
| `limit` | Maximum de résultats par page (1-100, valeur par défaut : 25). |
| `orderBy` | Ordre de tri des résultats. Utilisez le préfixe `+` ou `-` pour l’ordre croissant/décroissant. Exemple : `orderBy=-datasetName`. |
| `properties` | Liste séparée par des virgules de champs supplémentaires à inclure par résultat. Facultatif. |


**Requête**

La requête suivante récupère tous les ordres de travail de suppression d’enregistrements terminés, limités à deux par page :

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste paginée d’ordres de travail de suppression d’enregistrements.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

Le tableau suivant décrit les propriétés de la réponse.

| Propriété | Description |
| --- | --- |
| `results` | Tableau d’objets d’ordre de travail de suppression d’enregistrement. Chaque objet contient les champs ci-dessous. |
| `workorderId` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `orgId` | Identifiant d’organisation unique. |
| `bundleId` | Identifiant unique du lot contenant cet ordre de travail de suppression d’enregistrement. Le regroupement permet de regrouper et de traiter plusieurs ordres de suppression par services en aval. |
| `action` | Type d’action demandé dans l’ordre de travail. |
| `createdAt` | Date et heure de création de l’ordre de travail. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’ordre de travail. |
| `operationCount` | Nombre d’opérations incluses dans l’ordre de travail. |
| `targetServices` | Liste des services cibles pour l’ordre de travail. |
| `status` | Statut actuel de l’ordre de travail. Les valeurs possibles sont les suivantes : `received`, `validated`, `submitted`, `ingested`, `completed` et `failed`. |
| `createdBy` | Adresse électronique et identifiant de l’utilisateur qui a créé l’ordre de travail. |
| `datasetId` | Identifiant unique du jeu de données associé à l’ordre de travail. Si la requête s’applique à tous les jeux de données, ce champ est défini sur TOUS. |
| `datasetName` | Nom du jeu de données associé à l’ordre de travail. |
| `displayName` | Libellé lisible par l’utilisateur de l’ordre de travail. |
| `description` | Description de l’objectif de l’ordre de travail. |
| `total` | Nombre total d&#39;ordres de travail de suppression d&#39;enregistrements correspondant à la requête. |
| `count` | Nombre d&#39;ordres de travail de suppression d&#39;enregistrements dans la page active. |
| `_links` | Liens de pagination et de navigation. |
| `next` | Objet avec `href` (chaîne) et `templated` (booléen) pour la page suivante. |
| `page` | Objet avec `href` (chaîne) et `templated` (booléen) pour la navigation dans les pages. |

{style="table-layout:auto"}

## Créer un ordre de travail de suppression d&#39;enregistrement {#create}

Pour supprimer des enregistrements associés à une ou plusieurs identités d’un seul jeu de données ou de tous les jeux de données, envoyez une requête POST au point d’entrée `/workorder`.

Les ordres de travail sont traités de manière asynchrone et apparaissent dans la liste d’ordres de travail après envoi.

>[!TIP]
>
>Chaque ordre de travail de suppression d’enregistrement envoyé via l’API peut inclure jusqu’à 100 000 **d’identités**. Envoyez autant d’identités par requête que possible afin d’optimiser l’efficacité. Évitez les envois de faible volume tels que les ordres de travail à ID unique.

**Format d’API**

```http
POST /workorder
```

>[!NOTE]
>
>Vous pouvez uniquement supprimer des enregistrements des jeux de données dont le schéma XDM associé définit une identité principale ou un mappage d’identités.

>[!IMPORTANT]
>
>Les ordres de travail de suppression des enregistrements agissent exclusivement sur le champ **identité principale**. Les restrictions suivantes s’appliquent :
>
>- **Les identités Secondaires ne sont pas analysées.** Si un jeu de données contient plusieurs champs d’identité, seule l’identité principale est utilisée pour la correspondance. Les enregistrements ne peuvent pas être ciblés ou supprimés en fonction d&#39;identités non principales.
>- **Les enregistrements sans identité principale renseignée sont ignorés.** Si aucune métadonnée d’identité principale n’est renseignée pour un enregistrement, celui-ci ne peut pas être supprimé.
>- **Les données ingérées avant la configuration de l’identité ne sont pas éligibles.** Si le champ Identité principale a été ajouté à un schéma après l’ingestion des données, les enregistrements précédemment ingérés ne peuvent pas être supprimés via les ordres de travail de suppression d’enregistrements.

>[!NOTE]
>
>Si vous essayez de créer un ordre de travail de suppression d’enregistrement pour un jeu de données dont l’expiration est déjà active, la requête renvoie un HTTP 400 (Bad Request). Une expiration active correspond à toute suppression planifiée qui n’est pas encore terminée.

**Requête**

La requête suivante supprime tous les enregistrements associés aux adresses e-mail spécifiées d’un jeu de données spécifique.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

Le tableau suivant décrit les propriétés de création d&#39;un ordre de travail de suppression d&#39;enregistrement.

| Propriété | Description |
| --- | --- |
| `displayName` | Libellé lisible par l&#39;utilisateur pour cet ordre de travail de suppression d&#39;enregistrement. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |
| `action` | Action demandée pour l&#39;ordre de travail de suppression d&#39;enregistrement. Pour supprimer des enregistrements associés à une identité donnée, utilisez `delete_identity`. |
| `datasetId` | Identifiant unique du jeu de données. Utilisez l’identifiant du jeu de données pour un jeu de données spécifique ou `ALL` pour cibler tous les jeux de données. Les jeux de données doivent avoir une identité principale ou un mappage d’identités. S’il existe un mappage d’identités, il est présent sous la forme d’un champ de niveau supérieur nommé `identityMap`.<br>Notez qu’une ligne de jeu de données peut avoir plusieurs identités dans son mappage d’identités, mais une seule peut être marquée comme principale. `"primary": true` doit être inclus pour forcer le `id` à correspondre à une identité principale. |
| `namespacesIdentities` | Tableau d’objets contenant chacun :<br><ul><li> `namespace` : objet avec une propriété `code` spécifiant l’espace de noms d’identité (par exemple, « email »).</li><li> `IDs` : tableau de valeurs d’identité à supprimer pour cet espace de noms.</li></ul>Les espaces de noms d’identité fournissent un contexte aux données d’identité. Vous pouvez utiliser les espaces de noms standard fournis par Experience Platform ou créer les vôtres. Pour en savoir plus, consultez la [documentation sur les espaces de noms d’identité](../../identity-service/features/namespaces.md) et la [spécification de l’API Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Réponse**

Une réponse réussie renvoie les détails du nouvel ordre de travail de suppression d’enregistrement.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

Le tableau suivant décrit les propriétés de la réponse.

| Propriété | Description |
| --- | --- |
| `workorderId` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement. Utilisez cette valeur pour rechercher le statut ou les détails de la suppression. |
| `orgId` | Identifiant d’organisation unique. |
| `bundleId` | Identifiant unique du lot contenant cet ordre de travail de suppression d’enregistrement. Le regroupement permet de regrouper et de traiter plusieurs ordres de suppression par services en aval. |
| `action` | Type d&#39;action demandé dans l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `createdAt` | Date et heure de création de l’ordre de travail. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’ordre de travail. |
| `operationCount` | Nombre d’opérations incluses dans l’ordre de travail. |
| `targetServices` | Liste des services cibles pour l’ordre de travail de suppression d’enregistrement. |
| `status` | Statut actuel de l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `createdBy` | Adresse e-mail et identifiant de l’utilisateur qui a créé l’ordre de travail de suppression d’enregistrement. |
| `datasetId` | Identifiant unique du jeu de données. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |
| `datasetName` | Nom du jeu de données pour cet ordre de travail de suppression d’enregistrement. |
| `displayName` | Libellé lisible par l’utilisateur pour l’ordre de travail de suppression d’enregistrement. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |

{style="table-layout:auto"}

>[!NOTE]
>
>La propriété action des ordres de travail de suppression d’enregistrements est actuellement `identity-delete` dans les réponses de l’API. Si l’API est modifiée pour utiliser une autre valeur (telle que `delete_identity`), cette documentation sera mise à jour en conséquence.

## Convertir les listes d’ID en JSON pour les requêtes de suppression d’enregistrements

Pour créer un ordre de travail de suppression d’enregistrement à partir de fichiers CSV, TSV ou TXT contenant des identifiants, vous pouvez utiliser des scripts de conversion afin de produire les payloads JSON requises pour le point d’entrée `/workorder`. Cette approche est particulièrement utile lorsque vous travaillez avec des fichiers de données existants. Pour obtenir des scripts prêts à l’emploi et des instructions complètes, consultez le référentiel GitHub [csv-to-data-hygiene](https://github.com/perlmonger42/csv-to-data-hygiene).

### Générer des payloads JSON

Les exemples de script bash suivants montrent comment exécuter les scripts de conversion en Python ou Ruby :

>[!BEGINTABS]

>[!TAB Exemple d&#39;exécution de script Python]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB Exemple d&#39;exécution du script Ruby]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

Le tableau ci-dessous décrit les paramètres des scripts bash.

| Paramètre | Description |
| ---           | ---     |
| `verbose` | Activez la sortie détaillée. |
| `column` | Index (basé sur 1) ou nom de l’en-tête de la colonne contenant les valeurs d’identité à supprimer. La valeur par défaut est la première colonne si elle n’est pas spécifiée. |
| `namespace` | Objet avec une propriété `code` spécifiant l’espace de noms d’identité (par exemple, « email »). |
| `dataset-id` | Identifiant unique du jeu de données associé à l’ordre de travail. Si la requête s’applique à tous les jeux de données, ce champ est défini sur `ALL`. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |
| `output-dir` | Répertoire d’écriture de la payload JSON en sortie. |

{style="table-layout:auto"}

L’exemple ci-dessous montre une payload JSON réussie convertie à partir d’un fichier CSV, TSV ou TXT. Contient des enregistrements associés à l&#39;espace de noms spécifié et sert à supprimer les enregistrements identifiés par les adresses e-mail.

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

Le tableau suivant décrit les propriétés de la payload JSON.

| Propriété | Description |
| ---          | ---     |
| `action` | Action demandée pour l&#39;ordre de travail de suppression d&#39;enregistrement. Défini automatiquement sur `delete_identity` par le script de conversion. |
| `datasetId` | Identifiant unique du jeu de données. |
| `displayName` | Libellé lisible par l&#39;utilisateur pour cet ordre de travail de suppression d&#39;enregistrement. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |
| `identities` | Tableau d’objets contenant chacun :<br><ul><li> `namespace` : objet avec une propriété `code` spécifiant l’espace de noms d’identité (par exemple, « email »).</li><li> `id` : valeur d’identité à supprimer pour cet espace de noms.</li></ul> |

{style="table-layout:auto"}

### Envoyer les données JSON générées au point d’entrée `/workorder`

Pour soumettre une demande, suivez les instructions de la section [Création d’un ordre de travail de suppression d’enregistrement](#create). Veillez à utiliser la payload JSON convertie comme corps de requête (`-d`) lors de l’envoi de votre requête POST `curl` au point d’entrée de l’API `/workorder`.

## Récupérer les détails d’un ordre de travail de suppression d’enregistrement spécifique {#lookup}

Récupérez les informations relatives à un ordre de travail de suppression d’enregistrement spécifique en adressant une requête GET à `/workorder/{WORKORDER_ID}`. La réponse inclut le type d’action, le statut, les informations associées relatives au jeu de données et à l’utilisateur, ainsi que les métadonnées d’audit.

**Format d’API**

```http
GET /workorder/{WORKORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement que vous recherchez. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l&#39;ordre de travail de suppression d&#39;enregistrement spécifié.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

Le tableau suivant décrit les propriétés de la réponse.

| Propriété | Description |
| --- | --- |
| `workorderId` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `orgId` | Identifiant unique de votre organisation. |
| `bundleId` | Identifiant unique du lot contenant cet ordre de travail de suppression d’enregistrement. Le regroupement permet de regrouper et de traiter plusieurs ordres de suppression par services en aval. |
| `action` | Type d&#39;action demandé dans l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `createdAt` | Date et heure de création de l’ordre de travail. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’ordre de travail. |
| `operationCount` | Nombre d’opérations incluses dans l’ordre de travail. |
| `targetServices` | Liste des services cibles concernés par cet ordre de travail de suppression d&#39;enregistrement. |
| `status` | Statut actuel de l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `createdBy` | Adresse e-mail et identifiant de l’utilisateur qui a créé l’ordre de travail de suppression d’enregistrement. |
| `datasetId` | Identifiant unique du jeu de données associé à l’ordre de travail. |
| `datasetName` | Nom du jeu de données associé à l’ordre de travail. |
| `displayName` | Libellé lisible par l’utilisateur pour l’ordre de travail de suppression d’enregistrement. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |

## Mettre à jour un ordre de travail de suppression d&#39;enregistrement

Mettez à jour la `name` et la `description` d’un ordre de travail de suppression d’enregistrement en effectuant une requête PUT au point d’entrée `/workorder/{WORKORDER_ID}`.

**Format d’API**

```http
PUT /workorder/{WORKORDER_ID}
```

Le tableau suivant décrit le paramètre pour cette requête.

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement à mettre à jour. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

Le tableau suivant décrit les propriétés que vous pouvez mettre à jour.

| Propriété | Description |
| --- | --- |
| `name` | Libellé lisible par l&#39;utilisateur mis à jour pour l&#39;ordre de travail de suppression des enregistrements. |
| `description` | Description mise à jour de l&#39;ordre de travail de suppression d&#39;enregistrement. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie la demande d’ordre de travail mise à jour.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Propriété | Description |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | Identifiant unique de l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `orgId` | Identifiant unique de votre organisation. |
| `bundleId` | Identifiant unique du lot contenant cet ordre de travail de suppression d’enregistrement. Le regroupement permet de regrouper et de traiter plusieurs ordres de suppression par services en aval. |
| `action` | Type d&#39;action demandé dans l&#39;ordre de travail de suppression d&#39;enregistrement. |
| `createdAt` | Date et heure de création de l’ordre de travail. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’ordre de travail. |
| `operationCount` | Nombre d’opérations incluses dans l’ordre de travail. |
| `targetServices` | Liste des services cibles concernés par cet ordre de travail de suppression d&#39;enregistrement. |
| `status` | Statut actuel de l&#39;ordre de travail de suppression d&#39;enregistrement. Les valeurs possibles sont les suivantes : `received`, `validated`, `submitted`, `ingested`, `completed` et `failed`. |
| `createdBy` | Adresse e-mail et identifiant de l’utilisateur qui a créé l’ordre de travail de suppression d’enregistrement. |
| `datasetId` | Identifiant unique du jeu de données associé à l’ordre de travail de suppression d’enregistrement. |
| `datasetName` | Nom du jeu de données associé à l’ordre de travail de suppression d’enregistrement. |
| `displayName` | Libellé lisible par l’utilisateur pour l’ordre de travail de suppression d’enregistrement. |
| `description` | Description de l&#39;ordre de travail de suppression des enregistrements. |
| `productStatusDetails` | Tableau répertoriant le statut actuel des processus en aval de la requête. Chaque objet contient :<ul><li>`productName` : le nom du service en aval.</li><li>`productStatus` : statut actuel du traitement du service en aval.</li><li>`createdAt` : la date et l’heure auxquelles le statut le plus récent a été publié par le service.</li></ul>Cette propriété est disponible une fois que l’ordre de travail a été envoyé aux services en aval pour commencer le traitement. |

{style="table-layout:auto"}
