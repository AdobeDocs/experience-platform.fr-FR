---
title: edgeDomain
description: Déterminez le domaine vers lequel vous souhaitez envoyer des données.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
TQID: https://experienceleague.adobe.com/AGtfo51srVVyouLSiLya2Ie5-P6V50vl9Xxxwi0iQ-s
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2: id: bdea9bc8-5600-45db-b85e-d74bb59dfcff
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 5%

---

# `edgeDomain`

La propriété `edgeDomain` vous permet de modifier le domaine dans lequel le SDK Web envoie des données. L’utilisation d’un domaine personnalisé peut contribuer à réduire l’impact des bloqueurs d’annonces publicitaires.

>[!NOTE]
>
>Cette propriété ne modifie pas l’emplacement de définition des cookies. Le SDK Web définit toujours des [cookies propriétaires](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr), quel que soit l’endroit où il envoie finalement les données.

La valeur que vous utilisez pour `edgeDomain` dépend de votre participation au programme de certificat géré par Adobe [](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) :

**Si votre entreprise participe au programme de certificat géré par Adobe**, définissez la valeur sur le domaine propriétaire sélectionné lors de la configuration du certificat. En règle générale, cette valeur est un sous-domaine détenu par votre organisation. Par exemple : `data.example.com`. Les enregistrements CNAME de votre organisation transfèrent ces données vers Adobe.

**Si votre organisation ne participe pas au programme de certificat**, définissez la valeur sur un sous-domaine de `data.adobedc.net`. Adobe recommande d’utiliser l’ID de société IMS attribué par Adobe à votre organisation par souci de cohérence. Par exemple : `example.data.adobedc.net`. Procédez comme suit pour déterminer votre ID d’entreprise IMS :

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. N’importe où dans l’interface d’Experience Cloud, appuyez sur `[Cmd]` + `[I]` (macOS) ou `[Ctrl]` + `[I]` (Windows).
1. Un **[!UICONTROL Débogueur de données utilisateur]** s’affiche. Sélectionnez l’onglet **[!UICONTROL Organisations affectées]**.
1. Développez l’organisation IMS souhaitée.
1. Recherchez le champ **[!UICONTROL Client]**. Cette valeur est le sous-domaine de `data.adobedc.net` recommandé à utiliser.

Définissez la chaîne de `edgeDomain` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, elle est définie par défaut sur `edge.adobedc.net`. Bien que la valeur par défaut soit acceptable, Adobe considère qu’il est recommandé de définir une valeur spécifique à l’organisation.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Domaine Edge utilisant l’extension de balise Web SDK

L’extension de balise équivalente à cette propriété est le champ **[!UICONTROL domaine]** sous [paramètres de configuration de l’instance SDK](/help/tags/extensions/client/web-sdk/configure/general.md) lors de la configuration de l’extension.
