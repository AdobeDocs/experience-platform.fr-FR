---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;environnement;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’environnement
description: Découvrez le type de données XDM d’environnement.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 19%

---

# Type de données [!UICONTROL Environment]

[!UICONTROL Environnement] est un type de données XDM standard qui décrit l’environnement environnant d’un événement observé, en particulier les informations transitoires telles que les versions réseau et logicielle.

>[!IMPORTANT]
>
>Toutes les valeurs doivent être alignées avec la base de données [DeviceAtlas](https://deviceatlas.com), sous licence par Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc` | Objet | Objet contenant un seul champ, `language`, qui indique la langue de l’environnement pour représenter les préférences linguistiques, géographiques ou culturelles de l’utilisateur pour la présentation des données. Les langues sont spécifiées dans le code de langue comme défini dans [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Détails du navigateur](./browser-details.md) | Décrit les détails spécifiques au navigateur de l’environnement, tels que le nom du navigateur, la version, la version JavaScript, la chaîne de l’agent utilisateur et la langue d’acceptation. |
| `ISP` | Chaîne | Nom du fournisseur de services Internet de l’utilisateur. |
| `carrier` | Chaîne | Nom de l’opérateur de réseau mobile ou MNO (également appelé fournisseur de service sans fil, opérateur de réseau sans fil, entreprise de téléphonie mobile ou opérateur de réseau mobile) qui vend et fournit des services de communication à l’utilisateur. |
| `colorDepth` | Nombre entier | Nombre de bits utilisés pour chaque composant de couleur d’un seul pixel. |
| `connectionType` | Chaîne | Type de connexion Internet. Les valeurs acceptées sont les suivantes : <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Chaîne | Domaine du FAI de l’utilisateur. |
| `ipV4` | Chaîne | Libellé numérique attribué à un appareil appartenant à un réseau informatique qui utilise le protocole Internet pour la communication (32 bits). |
| `ipV6` | Chaîne | Libellé numérique attribué à un appareil appartenant à un réseau informatique qui utilise le protocole Internet pour la communication (128 bits). |
| `operatingSystem` | Chaîne | Nom du système d’exploitation utilisé lors de l’observation. L’attribut ne doit pas contenir d’informations de version telles que `10.5.3`, mais contenir des désignations &quot;d’édition&quot; telles que `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | Chaîne | Nom du fournisseur du système d’exploitation utilisé lors de l’observation. |
| `operatingSystemVersion` | Chaîne | Identificateur de la version complète du système d’exploitation utilisé lors de l’observation. Les versions sont généralement composées numériquement, mais peuvent être dans un format défini par le fournisseur. |
| `type` | Chaîne | Type de l’environnement de l’application. Pour connaître les valeurs acceptées, reportez-vous à l’ [annexe](#type) . |
| `viewportHeight` | Nombre entier | Taille verticale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage Web, il s’agit de la hauteur de la fenêtre d’affichage du navigateur. |
| `viewPortWidth` | Nombre entier | Taille horizontale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage Web, il s’agit de la largeur de la fenêtre d’affichage du navigateur. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device].

## Valeurs acceptées pour le type {#type}

Le tableau suivant décrit les valeurs acceptées pour `type` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `browser` | Navigateur |
| `application` | Application |
| `iot` | Internet des choses |
| `external` | Système externe |
| `widget` | Extension d’application |
