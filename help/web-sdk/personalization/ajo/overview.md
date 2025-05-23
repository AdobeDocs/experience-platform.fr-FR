---
title: Utilisation de Adobe Journey Optimizer avec Experience Platform Web SDK
description: Découvrez comment effectuer le rendu du contenu personnalisé avec Experience Platform Web SDK à l’aide de Adobe Journey Optimizer
keywords: ajo;ajo web;adobe parcours optimizer;renderDecisions;surfaces;décisions;propositions;portée;schéma
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# Utilisation de [!DNL Adobe Journey Optimizer] avec le [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut diffuser et générer des expériences personnalisées gérées dans [!DNL Adobe Journey Optimizer] au canal web. Vous pouvez utiliser un éditeur WYSIWYG, [!DNL Adobe Journey Optimizer] [canal web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr) ou une interface non visuelle, le [canal d’expérience basé sur le code](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/code-based-experience/get-started-code-based) pour créer, activer et diffuser vos campagnes [!DNL Journey Optimizer Web] et expériences de personnalisation.

>[!IMPORTANT]
>
>Lisez la [Documentation du canal web Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html?lang=fr) pour plus d’informations sur la prise en main de la création et du reporting d’expérience [!DNL Journey Optimizer Web].

## Terminologie {#terminology}

**[!UICONTROL Surface]** : une surface web est une page web ou un emplacement sur une page identifiée par un URI où le contenu de l’expérience [!DNL Adobe Journey Optimizer] sera diffusé.

**[!UICONTROL Propositions]** : dans [!DNL Adobe Journey Optimizer], les propositions sont corrélées à l’expérience sélectionnée dans un [!DNL Journey Optimizer Campaign].

## Activation de [!DNL Adobe Journey Optimizer] {#enable-ajo}

Pour commencer à utiliser [!DNL Adobe Journey Optimizer], procédez comme suit.

1. Parcourez les [conditions préalables](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr#prerequesites) du [!DNL Adobe Journey Optimizer] [Guide des expériences web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr), en particulier :
   * Configurez des [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Activez la [!DNL Adobe Journey Optimizer] dans votre [flux de données](../../../datastreams/overview.md).
   * Activez l’option [!UICONTROL &#x200B; Politique de fusion Active-On-Edge &#x200B;].

2. Ajoutez l’option `renderDecisions` à vos événements. Définissez `renderDecisions` sur `true` pour le rendu automatique des propositions de contenu Journey Optimizer diffusées sur les surfaces de vos pages web.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Vous pouvez éventuellement spécifier des surfaces supplémentaires dans vos événements. Par défaut, le Web SDK génère automatiquement la surface web de la page web active et l’inclut dans la requête envoyée à Edge Network. Si nécessaire, des surfaces supplémentaires peuvent être incluses dans la requête en les spécifiant dans l’option `personalization.surfaces` de la commande `sendEvent` ou dans la configuration correspondante **[!UICONTROL Surfaces]** [[!UICONTROL Événement d’envoi] de l’action](../../../tags/extensions/client/web-sdk/action-types.md#send-event) de l’extension Web SDK.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Les surfaces d’événement sont incluses dans le champ de requête `query.personalization.surfaces` :

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

4. Comme pour d’autres fonctionnalités de personnalisation, vous pouvez ajouter un **[fragment de code de masquage préalable](../manage-flicker.md)** pour ne masquer que certaines parties de la page lors de la récupération d’expériences.

## Création d’expériences web Adobe Journey Optimizer {#create-ajo-web-experiences}

Suivez les instructions [création de campagnes web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr#create-web-campaign) du [!DNL Adobe Journey Optimizer] [Guide des expériences web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr) pour créer des campagnes et des expériences [!DNL Journey Optimizer Web].

## Rendu du contenu personnalisé {#rendering-personalized-content}

Pour plus d’informations, consultez la documentation sur le [rendu de contenu de personnalisation](../rendering-personalization-content.md).

Les propositions Adobe Journey Optimizer pour les surfaces web sont traitées de la même manière que les propositions de portée de décision `__view__`. Plus précisément, lorsque `renderDecisions` option est définie sur `true` dans la commande `sendEvent`, elle est automatiquement rendue par le SDK Web.

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

Pour déboguer les implémentations de la personnalisation Adobe Journey Optimizer, utilisez [débogage Web SDK](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] traces de débogage sont disponibles lors du dépannage à l’aide de [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Recherchez les événements comportant le préfixe `AJO:`.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
