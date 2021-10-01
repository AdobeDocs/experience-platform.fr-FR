---
solution: Experience Platform
title: Exportation des schémas XDM dans l’interface utilisateur
description: Découvrez comment exporter un schéma existant vers un autre environnement de test ou organisation IMS dans l’interface utilisateur de Adobe Experience Platform.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Exportation des schémas XDM dans l’interface utilisateur

Toutes les ressources de la bibliothèque de schémas sont contenues dans un environnement de test spécifique au sein d’une organisation IMS. Dans certains cas, vous souhaiterez peut-être partager des ressources du modèle de données d’expérience (XDM) entre les environnements de test et les organisations IMS.

Pour répondre à ce besoin, l’espace de travail [!UICONTROL Schémas] de l’interface utilisateur de Adobe Experience Platform vous permet de générer une payload d’exportation pour n’importe quel schéma dans la bibliothèque de schémas. Cette payload peut ensuite être utilisée dans un appel à l’API Schema Registry pour importer le schéma (et toutes les ressources dépendantes) dans un environnement de test cible et une organisation IMS.

>[!NOTE]
>
>Vous pouvez également utiliser l’API Schema Registry pour exporter d’autres ressources en plus des schémas, notamment des classes, des groupes de champs de schéma et des types de données. Pour plus d’informations, consultez le guide sur les [points de terminaison export/import](../api/export-import.md) .

## Conditions préalables

Bien que l’interface utilisateur de Platform vous permette d’exporter des ressources XDM, vous devez utiliser l’API Schema Registry pour importer ces ressources dans d’autres environnements de test ou organisations IMS afin de terminer le workflow. Consultez le guide de [prise en main de l’API Schema Registry](../api/getting-started.md) pour obtenir des informations importantes sur les en-têtes d’authentification requis avant de suivre ce guide.

## Génération d’une payload d’exportation

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Dans l’espace de travail [!UICONTROL Schémas], recherchez le schéma que vous souhaitez exporter et ouvrez-le dans la balise [!DNL Schema Editor].

>[!TIP]
>
>Pour plus d’informations sur la manière de trouver la ressource XDM que vous recherchez, consultez le guide sur l’ [exploration des ressources XDM](./explore.md) .

Une fois le schéma ouvert, sélectionnez l’icône **[!UICONTROL Copier JSON]** (![Copier l’icône](../images/ui/export/icon.png)) en haut à droite du canevas.

![](../images/ui/export/copy-json.png)

Cette opération copie une charge utile JSON dans le presse-papiers, générée en fonction de la structure du schéma. Pour le schéma &quot;[!DNL Loyalty Members]&quot; illustré ci-dessus, le fichier JSON suivant est généré :

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

La charge utile prend la forme d’un tableau, chaque élément de tableau étant un objet qui représente une ressource XDM personnalisée à exporter. Dans l’exemple ci-dessus, le groupe de champs personnalisé &quot;[!DNL Loyalty details]&quot; et le schéma &quot;[!DNL Loyalty Members]&quot; sont inclus. Les ressources de base utilisées par le schéma ne sont pas incluses dans l’exportation, car elles sont disponibles dans tous les environnements de test et toutes les organisations IMS.

Notez que chaque instance de l’ID de tenant de votre organisation s’affiche sous la forme `<XDM_TENANTID_PLACEHOLDER>` dans la payload. Ces espaces réservés seront automatiquement remplacés par la valeur d’identifiant du client appropriée en fonction de l’endroit où vous importez le schéma à l’étape suivante.

## Importer la ressource à l’aide de l’API

Une fois que vous avez copié le fichier JSON d’exportation pour le schéma, vous pouvez l’utiliser comme charge utile pour une requête de POST au point de terminaison `/import` dans l’API Schema Registry. Voir la section sur l’[importation d’une ressource XDM dans l’API](../api/export-import.md#import) pour plus d’informations sur la configuration de l’appel pour envoyer le schéma à l’organisation IMS et à l’environnement de test de votre choix.

## Étapes suivantes

En suivant ce guide, vous avez correctement exporté un schéma XDM vers une organisation IMS ou un environnement de test différent. Pour plus d’informations sur les fonctionnalités de l’interface utilisateur des [!UICONTROL schémas], consultez la [[!UICONTROL présentation de l’interface utilisateur des ]](./overview.md).
