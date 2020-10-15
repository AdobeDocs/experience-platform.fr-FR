---
title: Envoi de données à Adobe Analytics
seo-title: Envoi de données à Adobe Analytics avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment envoyer des données à Adobe Analytics avec le SDK Web d’Experience Platform
seo-description: Découvrez comment envoyer des données à Adobe Analytics avec le SDK Web d’Experience Platform
keywords: adobe analytics;analytics;mapped data;mapped vars;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 84%

---


# Envoi de données à Adobe Analytics

The Adobe Experience Platform [!DNL Web SDK] can send data to Adobe Analytics. Cela fonctionne en convertissant `xdm` dans un format utilisable par Adobe Analytics.

## Configuration

Adobe Analytics récupère automatiquement les données que vous envoyez si une suite de rapports est mappée dans l’interface utilisateur de configuration du client. Ici, vous pouvez mapper un ou plusieurs rapports à une configuration donnée. Une fois qu’une suite de rapports est mappée, les données commencent automatiquement à circuler.

## Données mappées automatiquement

The Adobe Experience Platform [!DNL Edge Network] automatically maps many XDM variables automatically. La liste complète des variables mappées automatiquement se trouve [ici](automatically-mapped-vars.md).

## Données mappées manuellement

Toutes les données collectées par le réseau Edge sont accessibles via des règles de traitement. Les données sont aplaties à l’aide d’une notation par points et disponibles en tant que contextData.

Si vous aviez un schéma qui ressemblait à celui-ci.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Il s’agirait alors des clés de données contextuelles mises à votre disposition.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

Voici un exemple de règle de traitement qui utiliserait ces données.

![Interface des règles de traitement](../../../assets/edge_analytics_processing_rules.png)
