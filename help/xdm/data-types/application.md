---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;application;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'application
description: Découvrez le type de données Modèle de données d’expérience de l’application (XDM) .
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Type de données [!UICONTROL Application]

[!UICONTROL Application] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails liés aux interactions générées par une application. Une application fait référence à une expérience logicielle, telle qu’une application mobile ou de bureau, qui peut être installée, exécutée, fermée ou désinstallée par un utilisateur final. Les propriétés de ce type de données ne sont pas destinées à décrire des agents tels que des chatbots, des modules externes de navigateur ou d’autres expériences qui ne s’appliquent pas aux applications.

![image de l’application](../images/data-types/application.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Mesure]](./measure.md) | Décrit en détail la fin d’une application. |
| `crashes` | [[!UICONTROL Mesure]](./measure.md) | Cette propriété se déclenche lorsque l’application ne se ferme pas comme prévu. |
| `featureUsages` | [[!UICONTROL Mesure]](./measure.md) | Décrit toutes les données provenant de l’activation d’une fonctionnalité d’application qui sont mesurées. |
| `firstLaunches` | [[!UICONTROL Mesure]](./measure.md) | Contient des données sur le premier lancement. Cette propriété est déclenchée lors du premier lancement qui suit une installation. |
| `installs` | [[!UICONTROL Mesure]](./measure.md) | Enregistre l’installation d’une application sur un appareil lorsqu’un événement d’installation spécifique est disponible. |
| `launches` | [[!UICONTROL Mesure]](./measure.md) | Décrit une valeur associée au lancement d’une application. Cela est déclenché à chaque exécution, y compris les blocages, les installations et la reprise à partir de l’arrière-plan lorsque le délai d’expiration de la session a été dépassé. |
| `upgrades` | [[!UICONTROL Mesure]](./measure.md) | Contient des données sur la mise à niveau d’une application installée précédemment. Elle est déclenchée lors du premier lancement qui suit une mise à niveau. |
| `id` | Chaîne | Identifiant unique de l’application. |
| `name` | Chaîne | Nom de l’application. |
| `userPerspective` | Chaîne | Perspective ou relation physique entre l’utilisateur ou l’utilisatrice et l’application ou la marque au moment où un événement s’est produit. Comprendre le point de vue de l’utilisateur ou de l’utilisatrice par rapport à l’application permet de générer avec précision des sessions, car la plupart du temps, vous ne souhaitez pas inclure d’événements `background` et `detached` dans le cadre d’une session « active ». La valeur de cette propriété doit être égale à l’une des valeurs d’énumération répertoriées ci-dessous. <li> `foreground` : l’utilisateur et l’application interagissent directement entre eux. </li> <li> `background` : l’application et l’utilisateur interagissent indirectement entre eux. Par exemple, l’application peut mesurer une valeur et l’actualiser lorsque l’écran est verrouillé ou qu’une autre application est utilisée au premier plan.  </li> <li> `detached` : détaché signifie que l’événement était associé à l’application, mais ne provenait pas directement de l’application, comme l’envoi d’un e-mail ou d’une notification push depuis un système externe. |
| `version` | Chaîne | Version de l’application. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
