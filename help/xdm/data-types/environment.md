---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; environnement ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d'Environnement
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM Environnement.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 14%

---

# [!UICONTROL Type de données ] Environment

 Environment est un type de données XDM standard qui décrit l&#39;environnement environnant d&#39;un événement observé, en détaillant en particulier les informations transitoires telles que les versions réseau et logicielles.

>[!IMPORTANT]
>
>Toutes les valeurs doivent être alignées avec la base de données [DeviceAtlas](https://deviceatlas.com), sous licence par Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc` | Objet | Objet contenant un seul champ, `language`, qui indique la langue de l&#39;environnement pour représenter les préférences linguistiques, géographiques ou culturelles de l&#39;utilisateur pour la présentation des données. Les langues sont spécifiées dans le code de langue tel que défini dans [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Détails du navigateur](./browser-details.md) | Décrit les détails propres au navigateur de l’environnement, tels que le nom du navigateur, la version, la version JavaScript, la chaîne d’agent utilisateur et le langage d’acceptation. |
| `ISP` | Chaîne | Nom du prestataire Internet de l’utilisateur. |
| `carrier` | Chaîne | Nom de l’opérateur de réseau mobile ou MNO (également appelé prestataire sans fil, opérateur de téléphonie mobile, société cellulaire ou opérateur de réseau mobile) qui vend et fournit des services de communication à l’utilisateur. |
| `colorDepth` | Entier | Nombre de bits utilisés pour chaque composante de couleur d’un pixel unique. |
| `connectionType` | Chaîne | Type de connexion Internet. Les valeurs acceptées sont les suivantes : <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Chaîne | Domaine du fournisseur de services Internet de l’utilisateur. |
| `ipV4` | Chaîne | Libellé numérique attribué à un périphérique participant à un réseau informatique qui utilise le protocole Internet pour la communication (32 bits). |
| `ipV6` | Chaîne | Libellé numérique attribué à un périphérique participant à un réseau informatique qui utilise le protocole Internet pour la communication (128 bits). |
| `operatingSystem` | Chaîne | Nom du système d’exploitation utilisé lors de l’observation. L&#39;attribut ne doit pas contenir d&#39;informations de version telles que `10.5.3`, mais doit plutôt contenir des désignations d&#39;&quot;édition&quot; telles que `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | Chaîne | Nom du fournisseur du système d’exploitation utilisé lors de l’observation. |
| `operatingSystemVersion` | Chaîne | Identificateur de la version complète du système d’exploitation utilisé lors de l’observation. Les versions sont généralement composées numériquement, mais elles peuvent être dans un format défini par le fournisseur. |
| `type` | Chaîne | Type de l’environnement d’application. Voir l&#39;[annexe](#type) pour connaître les valeurs acceptées. |
| `viewportHeight` | Entier | Taille verticale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement de vue Web, il s’agit de la hauteur de fenêtre d’affichage du navigateur. |
| `viewPortWidth` | Entier | Taille horizontale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement de vue Web, il s’agit de la largeur de fenêtre d’affichage du navigateur. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device].

## Valeurs acceptées pour le type {#type}

Le tableau suivant décrit les valeurs acceptées pour `type` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `browser` | Browser |
| `application` | Application |
| `iot` | Internet des choses |
| `external` | Système externe |
| `widget` | Extension d’application |
