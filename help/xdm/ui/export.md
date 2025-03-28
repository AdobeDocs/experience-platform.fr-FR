---
solution: Experience Platform
title: Exportation des schémas XDM dans l’interface utilisateur
description: Découvrez comment exporter un schéma existant vers un environnement de test ou une organisation différente dans l’interface utilisateur de Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 11%

---

# Exporter des schémas XDM dans l’interface d’utilisation {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Copier la structure JSON"
>abstract="Générez un payload d’export pour le schéma de votre choix en copiant la structure JSON dans le presse-papiers. Utilisez cette fonction pour exporter les détails de n’importe quel schéma dans la bibliothèque de schémas. Ce fichier JSON exporté peut ensuite être utilisé pour importer le schéma et toutes les ressources associées dans une autre organisation ou un autre sandbox. Cela rend le partage et la réutilisation des schémas entre différents environnements simples et efficaces."

Toutes les ressources de la bibliothèque de schémas sont contenues dans un environnement de test spécifique au sein d’une organisation. Dans certains cas, vous souhaiterez peut-être partager des ressources de modèle de données d’expérience (XDM) entre des environnements de test et des organisations.

Pour répondre à ce besoin, l’espace de travail [!UICONTROL Schémas] de l’interface utilisateur de Adobe Experience Platform vous permet de générer une charge d’exportation pour n’importe quel schéma dans la bibliothèque de schémas. Cette payload peut ensuite être utilisée dans un appel à l’API Schema Registry pour importer le schéma (et toutes les ressources dépendantes) dans un environnement de test et une organisation cible.

>[!NOTE]
>
>Vous pouvez également utiliser l’API Schema Registry pour exporter d’autres ressources en plus des schémas, notamment des classes, des groupes de champs de schéma et des types de données. Pour plus d’informations, consultez le [guide de point de terminaison d’exportation](../api/export.md) .

## Conditions préalables

Bien que l’interface utilisateur de Platform vous permette d’exporter des ressources XDM, vous devez utiliser l’API Schema Registry pour importer ces ressources dans d’autres environnements de test ou organisations afin de terminer le processus. Pour obtenir des informations importantes sur les en-têtes d’authentification requis avant de suivre ce guide, reportez-vous au guide de [prise en main de l’API Schema Registry](../api/getting-started.md).

## Génération d’une payload d’exportation {#generate-export-payload}

Les payloads d’exportation peuvent être générés dans l’interface utilisateur de Platform à partir du panneau des détails de l’onglet [!UICONTROL Parcourir] ou directement à partir du canevas du schéma dans l’éditeur de schémas.

Pour générer une payload d’exportation, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Dans l’espace de travail [!UICONTROL Schémas], sélectionnez la ligne du schéma que vous souhaitez exporter afin d’afficher les détails du schéma dans la barre latérale droite.

>[!TIP]
>
>Consultez le guide sur l’ [exploration des ressources XDM](./explore.md) pour plus d’informations sur la manière de trouver la ressource XDM que vous recherchez.

Sélectionnez ensuite l’icône **[!UICONTROL Copier JSON]** (![Copier l’icône](/help/images/icons/copy.png)) dans les options disponibles.

![ L’espace de travail des schémas avec une ligne de schéma et [!UICONTROL Copier vers JSON] mis en surbrillance.](../images/ui/export/copy-json.png)

Cette opération copie une charge utile JSON dans le presse-papiers, générée en fonction de la structure du schéma. Pour le schéma &quot;[!DNL Loyalty Members]&quot; illustré ci-dessus, le fichier JSON suivant est généré :

+++Sélectionner pour développer un exemple de payload JSON

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

+++

La charge utile peut également être copiée en sélectionnant [!UICONTROL Plus] en haut à droite de l’éditeur de schémas. Un menu déroulant propose deux options, [!UICONTROL Copier la structure JSON] et [!UICONTROL Supprimer le schéma].

>[!NOTE]
>
>Un schéma ne peut pas être supprimé s’il est activé pour Profile ou s’il comporte des jeux de données associés.

![ L’éditeur de schémas avec [!UICONTROL Plus] et [!UICONTROL Copier vers JSON] surligné.](../images/ui/export/schema-editor-copy-json.png)

La charge utile prend la forme d’un tableau, chaque élément de tableau étant un objet qui représente une ressource XDM personnalisée à exporter. Dans l’exemple ci-dessus, le groupe de champs personnalisés &quot;[!DNL Loyalty details]&quot; et le schéma &quot;[!DNL Loyalty Members]&quot; sont inclus. Les ressources de base utilisées par le schéma ne sont pas incluses dans l’exportation, car elles sont disponibles dans tous les environnements de test et toutes les organisations.

Notez que chaque instance de l’ID de tenant de votre organisation apparaît sous la forme `<XDM_TENANTID_PLACEHOLDER>` dans la payload. Ces espaces réservés seront automatiquement remplacés par la valeur d’identifiant du client appropriée en fonction de l’endroit où vous importez le schéma à l’étape suivante.

## Importer la ressource à l’aide de l’API {#import-resource-with-api}

Une fois que vous avez copié le fichier JSON d’exportation pour le schéma, vous pouvez l’utiliser comme charge utile pour une requête de POST sur le point de terminaison `/rpc/import` de l’API Schema Registry. Pour plus d’informations sur la configuration de l’appel pour envoyer le schéma à l’organisation et à l’environnement de test désirés, consultez le [guide de point de terminaison d’importation](../api/import.md) .

## Étapes suivantes

En suivant ce guide, vous avez correctement exporté un schéma XDM vers une autre organisation ou un autre environnement de test. Pour plus d’informations sur les fonctionnalités de l’interface utilisateur [!UICONTROL Schemas], reportez-vous à la [[!UICONTROL présentation de l’interface utilisateur Schemas]](./overview.md).
