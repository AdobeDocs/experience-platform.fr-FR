---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; application ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d’application
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Application Experience Data Model).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 4%

---

# [!UICONTROL Type ] ApplicationData

 Application est un type de données standard de modèle de données d’expérience (XDM) qui décrit les détails relatifs aux interactions générées par l’application. Une application fait référence à une expérience logicielle, telle qu’une application mobile ou de bureau, qui peut être installée, exécutée, fermée ou désinstallée par un utilisateur final. Les propriétés de ce type de données ne sont pas destinées à décrire des agents tels que des chatbots, des modules externes basés sur un navigateur ou d’autres expériences qui ne s’appliquent pas aux applications.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Mesure]](./measure.md) | Décrit les détails de la résiliation d’une demande. |
| `crashes` | [[!UICONTROL Mesure]](./measure.md) | Cette propriété se déclenche lorsque l’application ne se ferme pas comme prévu. |
| `featureUsages` | [[!UICONTROL Mesure]](./measure.md) | Décrit toutes les données provenant de l’activation d’une fonction d’application qui sont mesurées. |
| `firstLaunches` | [[!UICONTROL Mesure]](./measure.md) | Contient des données au premier lancement. Cette propriété est déclenchée au premier lancement après une installation. |
| `installs` | [[!UICONTROL Mesure]](./measure.md) | Enregistre l’installation d’une application sur un périphérique lorsqu’un événement d’installation spécifique est disponible. |
| `launches` | [[!UICONTROL Mesure]](./measure.md) | Décrit une valeur associée au lancement d’une application. Cette opération est déclenchée à chaque exécution, y compris les blocages, les installations et la reprise en arrière-plan lorsque le délai d’expiration de la session est dépassé. |
| `upgrades` | [[!UICONTROL Mesure]](./measure.md) | Contient des données sur la mise à niveau d’une application qui a été installée précédemment. Ceci est déclenché au premier lancement après une mise à niveau. |
| `id` | Chaîne | Identificateur unique de l’application. |
| `name` | Chaîne | Nom de l’application  |
| `userPerspective` | Chaîne | La perspective ou la relation physique entre l’utilisateur et l’application ou la marque au moment où un événement s’est produit. Comprendre le point de vue de l’utilisateur par rapport à l’application permet de générer des sessions avec précision car la plupart du temps, vous ne souhaitez pas inclure les événements `background` et `detached` dans une session &quot;principale&quot;. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération répertoriées ci-dessous. <li> `foreground`: L’utilisateur et l’application interagissent directement entre eux. </li> <li> `background`: L’application et l’utilisateur interagissent indirectement entre eux. Par exemple, l’application peut mesurer une valeur et l’actualiser pendant que l’écran est verrouillé ou qu’une autre application est utilisée au premier plan.  </li> <li> `detached`: Détaché signifie que le événement était lié à l’application mais ne provenait pas directement de l’application, comme l’envoi d’un courrier électronique ou d’une notification Push depuis un système externe. |
| `version` | Chaîne | Version de l’application. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
