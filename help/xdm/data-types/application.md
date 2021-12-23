---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;application;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de l’application
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Application Experience Data Model).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 64e76c456ac5f59a2a1996e58eda405f1b27efa8
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 5%

---

# [!UICONTROL Application] type de données

[!UICONTROL Application] est un type de données XDM (Experience Data Model) standard qui décrit les détails liés aux interactions générées par une application. Une application fait référence à une expérience logicielle, telle qu’une application mobile ou de bureau, qui peut être installée, exécutée, fermée ou désinstallée par un utilisateur final. Les propriétés de ce type de données ne sont pas destinées à décrire des agents tels que des chatbots, des modules externes basés sur un navigateur ou d’autres expériences qui ne s’appliquent pas aux applications.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Mesure]](./measure.md) | Décrit les détails de la fin d’une application. |
| `crashes` | [[!UICONTROL Mesure]](./measure.md) | Cette propriété se déclenche lorsque l’application ne se ferme pas comme prévu. |
| `featureUsages` | [[!UICONTROL Mesure]](./measure.md) | Décrit toutes les données provenant de l’activation d’une fonction d’application qui sont mesurées. |
| `firstLaunches` | [[!UICONTROL Mesure]](./measure.md) | Contient des données au premier lancement. Cette propriété est déclenchée au premier lancement après une installation. |
| `installs` | [[!UICONTROL Mesure]](./measure.md) | Enregistre l’installation d’une application sur un périphérique lorsqu’un événement d’installation spécifique est disponible. |
| `launches` | [[!UICONTROL Mesure]](./measure.md) | Décrit une valeur associée au lancement d’une application. Elle est déclenchée à chaque exécution, notamment les blocages, les installations et la reprise en arrière-plan lorsque le délai d’expiration de la session a été dépassé. |
| `upgrades` | [[!UICONTROL Mesure]](./measure.md) | Contient des données sur la mise à niveau d’une application qui a été installée précédemment. Elle est déclenchée au premier lancement après une mise à niveau. |
| `id` | Chaîne | Identifiant unique de l’application. |
| `name` | Chaîne | Nom de l’application  |
| `userPerspective` | Chaîne | La perspective ou la relation physique entre l’utilisateur et l’application ou la marque au moment où un événement s’est produit. La compréhension de la perspective de l’utilisateur par rapport à l’application permet de générer des sessions avec précision, car la plupart du temps vous ne souhaitez pas inclure `background` et `detached` dans le cadre d’une &quot;principale&quot; session. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération répertoriées ci-dessous. <li> `foreground`: L’utilisateur et l’application interagissent directement les uns avec les autres. </li> <li> `background`: L’application et l’utilisateur interagissent indirectement. Par exemple, l’application peut mesurer une valeur et l’actualiser lorsque l’écran est verrouillé ou qu’une autre application est utilisée en premier plan.  </li> <li> `detached`: Désolidarisé signifie que l’événement était lié à l’application, mais ne provenait pas directement de l’application, comme l’envoi d’un email ou d’une notification push depuis un système externe. |
| `version` | Chaîne | Version de l’application. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
