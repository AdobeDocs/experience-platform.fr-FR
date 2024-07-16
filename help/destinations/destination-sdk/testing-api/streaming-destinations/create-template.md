---
description: Découvrez comment utiliser l’API de test de destination pour tester votre modèle de transformation de message de destination de diffusion en streaming avant de publier la destination.
title: Création et test d’un modèle de transformation de message
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 100%

---


# Création et test d’un modèle de transformation de message {#create-template}

## Vue d’ensemble {#overview}

Dans le cadre de Destination SDK, Adobe fournit des outils de développement pour vous aider à configurer et tester la destination. Cette page décrit comment créer et tester un modèle de transformation de messages. Pour en savoir plus sur la manière de tester la destination, consultez la documentation [Tester la configuration de destination](streaming-destination-testing-overview.md).

Pour **créer et tester un modèle de transformation de message** entre le schéma cible d’Adobe Experience Platform et le format de message pris en charge par la destination, utilisez la méthode *Outil de création de modèles* décrite plus en détail ci-après.  Consultez le[Document du format du message](../../functionality/destination-server/message-format.md#using-templating) pour en savoir plus sur la transformation des données entre le schéma source et le schéma cible.

L’illustration ci-dessous montre comment la création et le test d’un modèle de transformation de message s’intègrent dans le [workflow de configuration de la destination](../../guides/configure-destination-instructions.md) de Destination SDK :

![Graphique indiquant la place de l’étape de création de modèles dans le workflow de configuration de destination](../../assets/testing-api/create-template-step.png)

## Pourquoi créer et tester un modèle de transformation de messages {#why-create-message-transformation-template}

L’une des premières étapes de la création de la destination dans Destination SDK consiste à réfléchir à la manière dont le format de données pour l’appartenance à une audience, les identités et les attributs de profil est transformé au moment de l’exportation d’Adobe Experience Platform vers la destination. Pour plus d’informations sur la transformation entre le schéma XDM d’Adobe et votre schéma de destination, consultez le [Document du format du message](../../functionality/destination-server/message-format.md#using-templating).

Pour que la transformation réussisse, vous devez fournir un modèle de transformation semblable au modèle suivant : [Création d’un modèle qui envoie des segments, des identités et des attributs de profil](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe fournit un outil de modèle qui vous permet de créer et de tester le modèle de message transformant les données du format XDM d’Adobe en un format pris en charge par la destination. L’outil comporte deux points d’entrée API que vous pouvez utiliser :

* Utilisez l’*l’API du modèle type* pour obtenir un modèle type.
* Utilisez l’*API du modèle de rendu* pour obtenir l’exemple du modèle de rendu afin de comparer le résultat au format de données attendu de la destination. Après avoir comparé les données exportées au format de données attendu par la destination, vous pouvez modifier le modèle. Ainsi, les données exportées que vous générez correspondent au format de données attendu par la destination.

## Étapes à suivre avant de créer le modèle {#prerequisites}

Avant de pouvoir créer le modèle, procédez comme suit :

1. [Créez une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md). Le modèle que vous allez générer est différent en fonction de la valeur fournie pour le paramètre `maxUsersPerRequest`.
   * Utilisez `maxUsersPerRequest=1` si vous souhaitez inclure un seul profil dans un appel API à la destination, ainsi que ses qualifications d’audience, ses identités et ses attributs de profil.
   * Utilisez `maxUsersPerRequest` avec une valeur supérieure à un si vous souhaitez inclure plusieurs profils dans un appel API à la destination, ainsi que leurs qualifications d’audience, leurs identités et leurs attributs de profil.
2. [Créez une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) et ajoutez l’identifiant de la configuration du serveur de destination dans `destinationDelivery.destinationServerId`.
3. [Obtenez l’identifiant de la configuration de destination](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) que vous venez de créer, afin de l’utiliser dans l’outil de création de modèles.
4. Identifiez [les fonctions et filtres que vous pouvez utiliser](../../functionality/destination-server/supported-functions.md) dans le modèle de transformation des messages.

## Utilisation de l’exemple d’API de modèle et de l’API de modèle de rendu pour créer un modèle pour la destination {#iterative-process}

>[!TIP]
>
>Avant de concevoir et de modifier votre modèle de transformation des messages, vous pouvez commencer par appeler le [point d’entrée de l’API du modèle de rendu](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) avec un modèle simple qui exporte vos profils bruts sans appliquer de transformations. La syntaxe du modèle simple est la suivante : <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Le processus d’obtention et de test du modèle se répète. Répétez les étapes ci-dessous jusqu’à ce que les profils exportés correspondent au format de données attendu de la destination.

1. Tout d’abord, [obtenez un modèle type](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. Utilisez le modèle type comme point de départ pour créer votre propre version préliminaire.
3. Appelez le [point d’entrée de l’API du modèle de rendu](../../testing-api/streaming-destinations/create-template.md#render-template-api) avec votre propre modèle. Adobe génère des profils types en fonction de votre schéma et renvoie le résultat ou les erreurs rencontrées.
4. Comparez les données exportées au format de données attendu par la destination. Si nécessaire, modifiez le modèle.
5. Répétez ce processus ci-dessous jusqu’à ce que les profils exportés correspondent au format de données attendu de la destination.

## Obtention d’un modèle type à l’aide de l’exemple d’API de modèle {#sample-template-api}

>[!NOTE]
>
>Pour consulter la documentation de référence complète sur l’API, consultez la documentation [Obtention d’un exemple d’opération d’API de modèle](../../testing-api/streaming-destinations/sample-template-api.md).

Ajoutez un identifiant de destination à l’appel, comme illustré ci-dessous, pour que la réponse renvoie un modèle type correspondant à l’identifiant de destination.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Si l’identifiant de destination que vous fournissez correspond à une configuration de destination avec [agrégation des meilleurs efforts](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) et `maxUsersPerRequest=1` dans la politique d’agrégation, la requête renvoie un modèle type similaire à celui-ci :

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

## Caractère d’échappement dans votre modèle {#character-escape-template}

Avant d’utiliser le modèle pour effectuer le rendu des profils qui correspondent au format attendu de la destination, vous devez insérer un caractère d’échappement dans le modèle, comme indiqué dans l’enregistrement d’écran ci-dessous.

![Vidéo montrant comment insérer un caractère d’échappement dans un modèle à l’aide d’un outil d’échappement de caractères en ligne](../../assets/testing-api/escape-characters.gif)

Vous pouvez utiliser un outil d’échappement de caractères en ligne. La méthode [Formateur d’échappement JSON](https://jsonformatter.org/json-escape) est utilisée dans la démo ci-dessus.

## API du modèle de rendu {#render-template-api}

Après avoir créé un modèle de transformation de message à l’aide de l’[API du modèle type](create-template.md#sample-template-api), vous pouvez [effectuer le rendu du modèle](render-template-api.md) pour générer les données exportées en fonction de celle-ci. Cela vous permet de vérifier si les profils qu’Adobe Experience Platform exporterait vers la destination correspondent au format prévu de la destination.

Consultez la référence d’API pour obtenir des exemples d’appels que vous pouvez effectuer :

* [Rendu d’un modèle sans profils envoyés dans le corps](render-template-api.md#multiple-profiles-no-body)
* [Rendu d’un modèle avec des profils envoyés dans le corps](render-template-api.md#multiple-profiles-with-body)

Modifiez le modèle et effectuez des appels vers le point d’entrée de l’API du modèle de rendu jusqu’à ce que les profils exportés correspondent au format de données attendu de la destination.

## Ajoutez votre modèle avec caractères d’échappement à la configuration du serveur de destination

Une fois que votre modèle de transformation de messages vous satisfait, ajoutez-le à la [configuration du serveur de destination](../../authoring-api/destination-server/create-destination-server.md), dans `httpTemplate.requestBody.value`.
