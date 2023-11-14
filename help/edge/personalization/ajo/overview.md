---
title: Utilisation de Adobe Journey Optimizer avec le SDK Web Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide de Adobe Journey Optimizer
keywords: ajo;ajo web;adobe parcours optimizer;renderDecisions;surfaces;décisions;propositions;portée;schéma
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 4%

---

# Utilisation [!DNL Adobe Journey Optimizer] avec la propriété [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans [!DNL Adobe Journey Optimizer] au canal web. Vous pouvez utiliser un éditeur WYSIWYG, [!DNL Adobe Journey Optimizer] [Interface utilisateur de Campaign web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), pour créer, activer et diffuser vos [!DNL Journey Optimizer Web] campagnes et expériences de personnalisation.

>[!IMPORTANT]
>
>Lisez la section [Documentation sur le canal web Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=fr) pour plus d’informations sur la prise en main de [!DNL Journey Optimizer Web] création d’expériences et création de rapports.

## Terminologie {#terminology}

**[!UICONTROL Surface]**: une surface web est une propriété web identifiée par une URL dans laquelle la propriété [!DNL Adobe Journey Optimizer] le contenu de l’expérience sera diffusé.

**[!UICONTROL Propositions]**: dans [!DNL Adobe Journey Optimizer], les propositions correspondent à l’expérience sélectionnée dans un [!DNL Journey Optimizer Campaign].

## Activation [!DNL Adobe Journey Optimizer] {#enable-ajo}

Pour commencer à [!DNL Adobe Journey Optimizer], suivez les étapes ci-dessous.

1. Accédez au [conditions préalables](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) de la [!DNL Adobe Journey Optimizer] [Guide des expériences web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), en particulier :
   * Configurer [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Activer [!DNL Adobe Journey Optimizer] dans votre [datastream](../../../datastreams/overview.md).
   * Activez la variable [!UICONTROL Stratégie de fusion Active-On-Edge] .

2. Ajoutez la variable `renderDecisions` à vos événements. Définir `renderDecisions` to `true` pour le rendu automatique des propositions de contenu Journey Optimizer diffusées sur les surfaces de votre page web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Vous pouvez éventuellement spécifier des surfaces supplémentaires dans vos événements. Par défaut, le SDK Web génère automatiquement la surface web de la page web actuelle et l’inclut dans la requête au réseau Edge. Si nécessaire, d’autres surfaces peuvent être incluses dans la requête en les spécifiant dans la variable `personalization.surfaces` de l’ `sendEvent` ou dans la **[!UICONTROL Surfaces]** [[!UICONTROL Envoyer un événement] action](../../../tags/extensions/client/web-sdk/action-types.md#send-event) configuration de l’extension SDK Web.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Les surfaces d’événement sont incluses dans `query.personalization.surfaces` champ de requête :

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Comme pour d’autres fonctions de personnalisation, vous pouvez ajouter une **[prémasquage du fragment de code](../manage-flicker.md)** pour masquer certaines parties de la page lors de la récupération d’expériences.

## Création d’expériences web Adobe Journey Optimizer {#create-ajo-web-experiences}

Suivez la [création de campagnes web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) des instructions de la fonction [!DNL Adobe Journey Optimizer] [Guide des expériences web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) pour créer [!DNL Journey Optimizer Web] campagnes et expériences.

## Rendu du contenu personnalisé {#rendering-personalized-content}

Consultez la documentation relative à [rendu du contenu de personnalisation](../rendering-personalization-content.md) pour plus d’informations.

Les propositions Adobe Journey Optimizer pour les surfaces web sont traitées de la même manière que les `__view__` propositions de portée de décision. Plus précisément, lorsque `renderDecisions` est définie sur `true` dans le `sendEvent` Ces fichiers seront automatiquement rendus par le SDK Web.

Exemple de proposition de contenu Journey Optimizer :

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Débogage {#debugging}

Pour déboguer les implémentations de personnalisation de Adobe Journey Optimizer, utilisez [[!DNL Web SDK] débogage](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] des traces de débogage sont disponibles lors de la résolution des problèmes à l’aide de [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Recherchez des événements avec la variable `AJO:` préfixe.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
