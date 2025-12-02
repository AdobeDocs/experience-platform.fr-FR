---
title: edgeDomain
description: Déterminez le domaine racine auquel vous souhaitez envoyer des données.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# `edgeDomain`

La propriété `edgeDomain` vous permet de modifier le domaine dans lequel le SDK Web envoie des données. Cette propriété est fréquemment utilisée par les organisations qui utilisent des [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr). Les données sont envoyées au domaine de l’organisation, puis un enregistrement CNAME les transfère à Adobe.

La valeur que vous utilisez pour `edgeDomain` dépend de votre participation au programme de certificat géré par Adobe [&#128279;](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/adobe-managed-cert) :

**Si votre entreprise participe au programme de certificat géré par Adobe**, définissez la valeur sur le domaine propriétaire sélectionné lors de la configuration du certificat. En règle générale, cette valeur est un sous-domaine détenu par votre organisation. Par exemple : `data.example.com`. Les enregistrements CNAME de votre organisation redirigent ces données vers Adobe.

**Si vous ne participez pas au programme de certificat**, définissez la valeur sur un sous-domaine de `data.adobedc.net`. Adobe recommande d’utiliser l’identifiant de société de votre organisation par souci de cohérence. Par exemple : `example.data.adobedc.net`. Procédez comme suit pour déterminer l’ID de votre société :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. N’importe où dans l’interface d’Experience Cloud, appuyez sur `[Cmd]` + `[I]` (iOS) ou `[Ctrl]` + `[I]` (Windows).
1. Une **[!UICONTROL User data debugger]** s’affiche. Sélectionnez l’onglet **[!UICONTROL Assigned orgs]** .
1. Développez l’organisation IMS souhaitée.
1. Recherchez le champ **[!UICONTROL Tenant]** . Cette valeur est le sous-domaine de `data.adobedc.net` recommandé à utiliser.

Définissez la chaîne de `edgeDomain` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `edge.adobedc.net`. Bien que la valeur par défaut soit acceptable, Adobe considère qu’il est recommandé de définir une valeur spécifique à l’organisation.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Domaine Edge utilisant l’extension de balise Web SDK

L’extension de balise équivalente à cette propriété est le champ **[!UICONTROL Edge domain]** sous [Paramètres de configuration de l’instance SDK](/help/tags/extensions/client/web-sdk/configure/general.md) lors de la configuration de l’extension.
