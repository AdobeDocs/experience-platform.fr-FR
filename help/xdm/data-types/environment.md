---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;environnement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d’environnement
description: En savoir plus sur le type de données XDM de l’environnement.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 19%

---

# Type de données [!UICONTROL Environment]

[!UICONTROL Environnement] est un type de données XDM standard qui décrit l’environnement d’un événement observé, en détaillant spécifiquement les informations éphémères telles que les versions logicielles et réseau.

>[!IMPORTANT]
>
>Toutes les valeurs doivent être alignées sur la base de données [DeviceAtlas](https://deviceatlas.com), sous licence par Adobe.

![](../images/data-types/environment.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc` | Objet | Objet contenant un seul champ, `language`, qui indique la langue de l’environnement pour représenter les préférences linguistiques, géographiques ou culturelles de l’utilisateur pour la présentation des données. Les langues sont spécifiées dans le code de langue comme défini dans [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Informations sur le navigateur](./browser-details.md) | Décrit les détails spécifiques au navigateur de l’environnement, tels que le nom du navigateur, la version, la version de JavaScript, la chaîne de l’agent utilisateur et la langue acceptée. |
| `ISP` | Chaîne | Nom du fournisseur de services Internet de l’utilisateur. |
| `carrier` | Chaîne | Nom de l’opérateur de réseau mobile (également appelé fournisseur de services sans fil, opérateur de réseau sans fil, société de téléphonie cellulaire ou opérateur de réseau mobile) qui vend et fournit des services de communication à l’utilisateur. |
| `colorDepth` | Nombre entier | Nombre de bits utilisés pour chaque composant de couleur d’un seul pixel. |
| `connectionType` | Chaîne | Type de connexion Internet. Les valeurs acceptées sont les suivantes : <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Chaîne | Domaine du FAI de l’utilisateur. |
| `ipV4` | Chaîne | Étiquette numérique attribuée à un appareil faisant partie d’un réseau informatique qui utilise le protocole Internet pour communiquer (32 bits). |
| `ipV6` | Chaîne | Étiquette numérique attribuée à un appareil faisant partie d’un réseau informatique qui utilise le protocole IP pour communiquer (128 bits). |
| `operatingSystem` | Chaîne | Nom du système d’exploitation utilisé lors de l’observation. L’attribut ne doit pas contenir d’informations de version telles que `10.5.3`, mais plutôt des désignations d’« édition » telles que `Ultimate` ou `Professional`. |
| `operatingSystemVendor` | Chaîne | Nom du fournisseur du système d’exploitation utilisé lors de l’observation. |
| `operatingSystemVersion` | Chaîne | Identificateur de la version complète du système d’exploitation utilisé lors de l’observation. Les versions sont généralement composées numériquement, mais peuvent se trouver dans un format défini par le fournisseur. |
| `type` | Chaîne | Type de l’environnement d’application. Voir l’[annexe](#type) pour connaître les valeurs acceptées. |
| `viewportHeight` | Nombre entier | Taille verticale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage web, il s’agit de la hauteur de la fenêtre d’affichage du navigateur. |
| `viewPortWidth` | Nombre entier | Taille horizontale en pixels de la fenêtre dans laquelle l’expérience s’affichait. Pour un événement d’affichage web, il s’agit de la largeur de la fenêtre d’affichage du navigateur. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Appareil].

## Valeurs acceptées pour le type {#type}

Le tableau suivant décrit les valeurs acceptées pour les `type` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `browser` | Navigateur |
| `application` | Application |
| `iot` | Internet des objets |
| `external` | Système externe |
| `widget` | Extension d’application |
