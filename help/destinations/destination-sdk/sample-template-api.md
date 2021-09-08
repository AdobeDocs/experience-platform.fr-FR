---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/testing/template/sample` pour obtenir un modèle de transformation de message de test pour votre destination.
title: Obtention d’un exemple d’opération d’API de modèle
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 2%

---

# Obtenir des exemples d’opérations de l’API de modèle {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/testing/template/sample` afin de générer un [modèle de transformation des messages](./message-format.md#using-templating) pour votre destination. Pour une description de la fonctionnalité prise en charge par ce point de terminaison, lisez [create template](./create-template.md).

## Prise en main des exemples d’opérations de l’API de modèle {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Obtenir un exemple de modèle {#generate-sample-template}

Vous pouvez obtenir un exemple de modèle en effectuant une requête de GET sur le point de terminaison `authoring/testing/template/sample/` et en fournissant l’identifiant de destination de la configuration de destination basée sur laquelle vous créez votre modèle.

>[!TIP]
>
>* L’ID de destination que vous devez utiliser ici est `instanceId` qui correspond à une configuration de destination, créée à l’aide du point de terminaison `/destinations` . Reportez-vous à la [référence de l’API de configuration de destination](./destination-configuration-api.md#retrieve-list).


**Format d’API**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | L’identifiant de la configuration de destination pour laquelle vous générez un modèle de transformation de message. |

**Requête**

La requête suivante génère un nouvel exemple de modèle, configuré par les paramètres fournis dans la payload.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec un exemple de modèle que vous pouvez modifier pour correspondre au format de données attendu.

Si l’identifiant de destination que vous fournissez correspond à un modèle de serveur de destination avec `maxUsersPerRequest=1`, la requête renvoie un exemple de modèle similaire à celui-ci :

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
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Si l’identifiant de destination que vous fournissez correspond à un modèle de serveur de destination dont la valeur est `maxUsersPerRequest` supérieure à un, la requête renvoie un exemple de modèle similaire à celui-ci :

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
                {#- Alternative syntax for filtering segments by status: -#}
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

Les points d’entrée de l’API du SDK de destination suivent les principes généraux des messages d’erreur de l’API Experience Platform. Reportez-vous aux sections [Codes d’état d’API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) et [erreurs d’en-tête de requête](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment générer un modèle de transformation de message à l’aide du point de terminaison de l’API `/authoring/testing/template/sample`. Ensuite, vous pouvez utiliser le [point d’entrée de l’API de modèle de rendu](./render-template-api.md) pour générer les profils exportés en fonction du modèle et les comparer au format de données attendu de votre destination.