---
description: Découvrez comment utiliser l’API de test de destination pour générer un modèle de transformation de message de test pour la destination.
title: Génération d’un modèle type de transformation des messages
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 96%

---


# Génération d’un modèle type de transformation des messages {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée `/authoring/testing/template/sample` de l’API pour générer un [modèle de transformation des messages](../../functionality/destination-server/message-format.md#using-templating) pour la destination. Pour une description des fonctionnalités prises en charge par ce point d’entrée, consultez la section [Créer un modèle](create-template.md).

## Prise en main des opérations de l’API des modèles type {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Obtention d’un modèle type {#generate-sample-template}

Vous pouvez obtenir un modèle type en adressant une requête GET au point d’entrée `authoring/testing/template/sample/` et en fournissant l’identifiant de destination de la configuration de destination en fonction de laquelle vous créez votre modèle.

>[!TIP]
>
>* L’identifiant de destination que vous devez utiliser ici est `instanceId`, qui correspond à une configuration de destination, créée à l’aide du point d’entrée `/destinations`. Pour en savoir plus, consultez [Récupération d’une configuration de destination](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**Format d’API**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | Identifiant de la configuration de destination pour laquelle vous générez un modèle de transformation de message. |

**Requête**

La requête suivante génère un nouveau modèle d’audience configuré en fonction des paramètres fournis dans la payload.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec un modèle type que vous pouvez modifier pour correspondre au format de données attendu.

Si l’identifiant de destination que vous fournissez correspond à une configuration de destination avec [agrégation des meilleurs efforts](../../functionality/destination-configuration/aggregation-policy.md) et `maxUsersPerRequest=1` dans la politique d’agrégation, la requête renvoie un modèle type similaire à celui-ci :

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Si l’identifiant de destination que vous fournissez correspond à un modèle de serveur de destination avec [agrégation configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) ou [agrégation des meilleurs efforts](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) et que `maxUsersPerRequest` est supérieur à un, la requête renvoie un modèle type similaire à celui-ci :

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering audiences by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment générer un modèle de transformation de message à l’aide du point d’entrée `/authoring/testing/template/sample` de l’API. Vous pouvez désormais utiliser le [point d’entrée de l’API du modèle de rendu](render-template-api.md) pour générer les profils exportés en fonction du modèle et les comparer au format de données attendu de la destination.
