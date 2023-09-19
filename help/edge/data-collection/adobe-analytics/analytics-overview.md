---
title: Utiliser Adobe Analytics avec le SDK Web Platform
description: Découvrez comment envoyer des données à Adobe Analytics avec le SDK Web de Adobe Experience Platform.
keywords: adobe analytics;analytics;données mappées;variables mappées;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 39%

---

# Utiliser Adobe Analytics avec le SDK Web Platform

Adobe Experience Platform [!DNL Web SDK] peut envoyer des données à Adobe Analytics. Cela fonctionne en convertissant `xdm` dans un format utilisable par Adobe Analytics.

## Configuration

Adobe Analytics récupère automatiquement les données que vous envoyez si une suite de rapports est mappée dans l’interface utilisateur de configuration du client. Ici, vous pouvez mapper un ou plusieurs rapports à une configuration donnée. Une fois qu’une suite de rapports est mappée, les données commencent automatiquement à circuler.

## Groupe de champs XDM

Pour faciliter la capture des mesures Adobe Analytics les plus courantes, nous fournissons un groupe de champs Analytics que vous pouvez utiliser. Pour plus d’informations sur ce schéma, consultez la documentation de la [Groupe de champs de l’extension complète Adobe Analytics ExperienceEvent](../../../xdm/field-groups/event/analytics-full-extension.md)

## Données mappées automatiquement

Adobe Experience Platform [!DNL Edge Network] mappe automatiquement de nombreuses variables XDM. La liste complète de ces variables est répertoriée. [here](automatically-mapped-vars.md).

## Données mappées manuellement

Toute donnée qui n’est pas automatiquement mappée par la variable [!DNL Edge Network] sont accessibles via les règles de traitement. Les données sont aplaties à l’aide d’une notation par points et disponibles en tant que contextData.

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

![Interface des règles de traitement](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>Avec la collection Edge Network, tous les événements sont envoyés à Analytics ainsi qu’à tous les autres services que vous avez configurés pour votre flux de données. Par exemple, si Analytics et Target sont tous deux configurés en tant que services et que vous effectuez des appels distincts pour la personnalisation et pour Analytics, les deux événements seront envoyés à Analytics ainsi qu’à Target. Ces événements seront enregistrés dans les rapports Analytics et peuvent affecter des mesures telles que le taux de rebond.
