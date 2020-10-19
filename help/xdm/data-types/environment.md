---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;environment;datatype;data-type;data type;
solution: Experience Platform
title: Type de données d'Environnement
topic: overview
description: Ce document présente un aperçu du type de données XDM Environnement.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 15%

---


# [!UICONTROL Type de données Environnement]

[!UICONTROL L&#39;Environnement] est un type de données XDM standard qui décrit l&#39;environnement environnant d&#39;un événement observé, en détaillant en particulier les informations transitoires telles que les versions réseau et logiciel.

>[!IMPORTANT]
>
>Toutes les valeurs doivent être alignées avec la base de données [DeviceAtlas](https://deviceatlas.com) , sous licence par Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc` | Objet | Objet qui contient un seul champ `language`, qui indique la langue de l’environnement pour représenter les préférences linguistiques, géographiques ou culturelles de l’utilisateur pour la présentation des données. Languages are specified in language code as defined in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Détails du navigateur](./browser-details.md) | Décrit les détails propres au navigateur de l’environnement, tels que le nom du navigateur, la version, la version JavaScript, la chaîne d’agent utilisateur et le langage d’acceptation. |
| `ISP` | Chaîne | Nom du prestataire Internet de l’utilisateur. |
| `carrier` | Chaîne | Nom de l’opérateur de réseau mobile ou MNO (également appelé prestataire sans fil, opérateur de téléphonie mobile, société cellulaire ou opérateur de réseau mobile) qui vend et fournit des services de communication à l’utilisateur. |
| `colorDepth` | Entier | Nombre de bits utilisés pour chaque composante de couleur d’un pixel unique. |
| `connectionType` | Chaîne | Type de connexion Internet. Les valeurs acceptées sont les suivantes : <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Chaîne | Domaine du fournisseur de services Internet de l’utilisateur. |
| `ipV4` | Chaîne | Libellé numérique attribué à un périphérique participant à un réseau informatique qui utilise le protocole Internet pour la communication (32 bits). |
| `ipV6` | Chaîne | Libellé numérique attribué à un périphérique participant à un réseau informatique qui utilise le protocole Internet pour la communication (128 bits). |
| `operatingSystem` | Chaîne | Nom du système d’exploitation utilisé lors de l’observation. The attribute should not contain any version information such as `10.5.3`, but instead contain &quot;edition&quot; designations such as `Ultimate` or `Professional`. |
| `operatingSystemVendor` | Chaîne | Nom du fournisseur du système d’exploitation utilisé lors de l’observation. |
| `operatingSystemVersion` | Chaîne | Identificateur de la version complète du système d’exploitation utilisé lors de l’observation. Les versions sont généralement composées numériquement, mais elles peuvent être dans un format défini par le fournisseur. |
| `type` | Chaîne | Type de l’environnement d’application. Consultez l’ [annexe](#type) pour connaître les valeurs acceptées. |
| `viewportHeight` | Entier | Taille verticale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement de vue Web, il s’agit de la hauteur de fenêtre d’affichage du navigateur. |
| `viewPortWidth` | Entier | Taille horizontale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement de vue Web, il s’agit de la largeur de fenêtre d’affichage du navigateur. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device] .

## Valeurs acceptées pour le type {#type}

Le tableau suivant présente les valeurs acceptées pour `type` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `browser` | Browser |
| `application` | Application |
| `iot` | Internet des choses |
| `external` | Système externe |
| `widget` | Extension d’application |