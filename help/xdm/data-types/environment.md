---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;environnement;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’environnement
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM d’environnement.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 18%

---

# [!UICONTROL Environnement] type de données

[!UICONTROL Environnement] est un type de données XDM standard qui décrit l’environnement environnant d’un événement observé, en détaillant spécifiquement les informations transitoires telles que les versions réseau et logicielle.

>[!IMPORTANT]
>
>Toutes les valeurs doivent être alignées sur la variable [DeviceAtlas](https://deviceatlas.com) base de données, sous licence par Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc` | Objet | Un objet contenant un seul champ, `language`, qui indique la langue de l’environnement pour représenter les préférences linguistiques, géographiques ou culturelles de l’utilisateur pour la présentation des données. Les langues sont spécifiées dans le code de langue comme défini dans [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Informations sur le navigateur](./browser-details.md) | Décrit les détails spécifiques au navigateur de l’environnement, tels que le nom du navigateur, la version, la version JavaScript, la chaîne de l’agent utilisateur et le langage d’acceptation. |
| `ISP` | Chaîne | Nom du fournisseur d’accès Internet de l’utilisateur. |
| `carrier` | Chaîne | Nom de l’opérateur de réseau mobile ou MNO (également appelé fournisseur de service sans fil, opérateur de réseau sans fil, entreprise de téléphonie mobile ou opérateur de réseau mobile) qui vend et fournit des services de communication à l’utilisateur. |
| `colorDepth` | Nombre entier | Nombre de bits utilisés pour chaque composant de couleur d’un seul pixel. |
| `connectionType` | Chaîne | Type de connexion Internet. Les valeurs acceptées sont les suivantes : <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Chaîne | Domaine du FAI de l’utilisateur. |
| `ipV4` | Chaîne | Libellé numérique attribué à un appareil appartenant à un réseau informatique qui utilise le protocole Internet pour la communication (32 bits). |
| `ipV6` | Chaîne | Libellé numérique attribué à un appareil appartenant à un réseau informatique qui utilise le protocole Internet pour la communication (128 bits). |
| `operatingSystem` | Chaîne | Nom du système d’exploitation utilisé lors de l’observation. L’attribut ne doit contenir aucune information de version, telle que `10.5.3`, mais contiennent à la place des désignations &quot;edition&quot; telles que `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | Chaîne | Nom du fournisseur du système d’exploitation utilisé lors de l’observation. |
| `operatingSystemVersion` | Chaîne | Identificateur de la version complète du système d’exploitation utilisé lors de l’observation. Les versions sont généralement composées numériquement, mais peuvent être dans un format défini par le fournisseur. |
| `type` | Chaîne | Type de l’environnement de l’application. Voir [annexe](#type) pour les valeurs acceptées. |
| `viewportHeight` | Nombre entier | Taille verticale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage Web, il s’agit de la hauteur de la fenêtre d’affichage du navigateur. |
| `viewPortWidth` | Nombre entier | Taille horizontale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage Web, il s’agit de la largeur de la fenêtre d’affichage du navigateur. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur la variable [!UICONTROL Appareil] type de données.

## Valeurs acceptées pour le type {#type}

Le tableau suivant décrit les valeurs acceptées pour `type` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `browser` | Navigateur |
| `application` | Application |
| `iot` | Internet des choses |
| `external` | Système externe |
| `widget` | Extension d’application |
