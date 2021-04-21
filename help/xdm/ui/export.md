---
solution: Experience Platform
title: Exportation de Schémas XDM dans l’interface utilisateur
description: Découvrez comment exporter un schéma existant vers un autre sandbox ou une organisation IMS dans l’interface utilisateur de Adobe Experience Platform.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Exportation de schémas XDM dans l’interface utilisateur

Toutes les ressources de la bibliothèque de Schémas sont contenues dans un sandbox spécifique au sein d’une organisation IMS. Dans certains cas, vous pouvez partager des ressources de modèle de données d’expérience (XDM) entre des sandbox et des organisations IMS.

Pour répondre à ce besoin, l’espace de travail [!UICONTROL Schémas] de l’interface utilisateur de Adobe Experience Platform vous permet de générer une charge utile d’exportation pour tout schéma de la bibliothèque de Schémas. Cette charge utile peut ensuite être utilisée dans un appel à l&#39;API de registre de Schéma pour importer le schéma (et toutes les ressources dépendantes) dans un sandbox de cible et une organisation IMS.

>[!NOTE]
>
>Vous pouvez également utiliser l&#39;API Schéma Registry pour exporter d&#39;autres ressources en plus des schémas, notamment des classes, des mixins et des types de données. Pour plus d&#39;informations, consultez le guide des [points de terminaison export/import](../api/export-import.md).

## Conditions préalables

Bien que l’interface utilisateur de la plate-forme vous permette d’exporter des ressources XDM, vous devez utiliser l’API Schéma Registry pour importer ces ressources dans d’autres sandbox ou des organisations IMS afin de terminer le processus. Pour obtenir des informations importantes sur les en-têtes d&#39;authentification requis avant de suivre ce guide, reportez-vous au guide [Prise en main de l&#39;API de registre des Schémas](../api/getting-started.md).

## Générer une charge utile d’exportation

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Dans l&#39;espace de travail [!UICONTROL Schémas], recherchez le schéma à exporter et ouvrez-le dans [!DNL Schema Editor].

>[!TIP]
>
>Consultez le guide sur [l&#39;exploration des ressources XDM](./explore.md) pour plus d&#39;informations sur la manière de trouver la ressource XDM que vous recherchez.

Une fois le schéma ouvert, sélectionnez l’icône **[!UICONTROL Copier JSON]** (![Copier l’icône](../images/ui/export/icon.png)) dans le coin supérieur droit de la trame.

![](../images/ui/export/copy-json.png)

Cette opération copie une charge JSON dans le Presse-papiers, générée en fonction de la structure du schéma. Pour le schéma &quot;[!DNL Loyalty Members]&quot; illustré ci-dessus, le fichier JSON suivant est généré :

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

La charge utile prend la forme d&#39;un tableau, chaque élément de tableau étant un objet qui représente une ressource XDM personnalisée à exporter. Dans l’exemple ci-dessus, le mixin personnalisé &quot;[!DNL Loyalty details]&quot; et le schéma &quot;[!DNL Loyalty Members]&quot; sont inclus. Les ressources de base utilisées par le schéma ne sont pas incluses dans l&#39;exportation, car elles sont disponibles dans tous les sandbox et les organismes IMS.

Notez que chaque instance de l’ID de client de votre organisation s’affiche sous la forme `<XDM_TENANTID_PLACEHOLDER>` dans la charge utile. Ces espaces réservés seront automatiquement remplacés par la valeur d&#39;ID de locataire appropriée en fonction de l&#39;endroit où vous importez le schéma à l&#39;étape suivante.

## Importer la ressource à l&#39;aide de l&#39;API

Une fois que vous avez copié le fichier JSON d’exportation pour le schéma, vous pouvez l’utiliser comme charge utile pour une demande de POST au point de terminaison `/import` de l’API de registre de Schéma. Voir la section sur l&#39;[importation d&#39;une ressource XDM dans l&#39;API](../api/export-import.md#import) pour plus d&#39;informations sur la configuration de l&#39;appel pour envoyer le schéma à l&#39;organisation IMS et au sandbox de votre choix.

## Étapes suivantes

En suivant ce guide, vous avez exporté un schéma XDM vers une autre organisation IMS ou un autre sandbox. Pour plus d&#39;informations sur les fonctionnalités de l&#39;interface utilisateur [!UICONTROL Schémas], consultez la section [[!UICONTROL Schémas] présentation de l&#39;interface utilisateur](./overview.md).
