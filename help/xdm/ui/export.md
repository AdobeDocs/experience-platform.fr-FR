---
solution: Experience Platform
title: Exporter des schémas XDM dans l’interface utilisateur
description: Découvrez comment exporter un schéma existant vers une autre sandbox ou organisation dans l’interface utilisateur de Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 11%

---

# Exporter des schémas XDM dans l’interface d’utilisation {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Copier la structure JSON"
>abstract="Générez un payload d’export pour le schéma de votre choix en copiant la structure JSON dans le presse-papiers. Utilisez cette fonction pour exporter les détails de n’importe quel schéma dans la bibliothèque de schémas. Ce fichier JSON exporté peut ensuite être utilisé pour importer le schéma et toutes les ressources associées dans une autre organisation ou un autre sandbox. Cela rend le partage et la réutilisation des schémas entre différents environnements simples et efficaces."

Toutes les ressources de la bibliothèque de schémas se trouvent dans un sandbox spécifique au sein d’une organisation. Dans certains cas, vous pouvez partager des ressources de modèle de données d’expérience (XDM) entre des sandbox et des organisations.

Pour répondre à ce besoin, l’espace de travail [!UICONTROL Schemas] de l’interface utilisateur de Adobe Experience Platform vous permet de générer une payload d’exportation pour n’importe quel schéma de la bibliothèque des schémas. Cette payload peut ensuite être utilisée dans un appel à l’API Schema Registry pour importer le schéma (et toutes les ressources dépendantes) dans un sandbox et une organisation cibles.

>[!NOTE]
>
>Vous pouvez également utiliser l’API Schema Registry pour exporter d’autres ressources en plus des schémas, notamment des classes, des groupes de champs de schéma et des types de données. Pour plus d’informations, consultez le [guide du point d’entrée d’exportation](../api/export.md).

## Conditions préalables

Bien que l’interface utilisateur d’Experience Platform vous permette d’exporter des ressources XDM, vous devez utiliser l’API Schema Registry pour importer ces ressources dans d’autres sandbox ou organisations afin de terminer le workflow. Reportez-vous au guide sur la [prise en main de l’API Schema Registry](../api/getting-started.md) pour obtenir des informations importantes sur les en-têtes d’authentification requis avant de suivre ce guide.

## Générer une payload d&#39;export {#generate-export-payload}

Les payloads d’exportation peuvent être générées dans l’interface utilisateur d’Experience Platform à partir du panneau des détails de l’onglet [!UICONTROL Browse] ou directement à partir de la zone de travail du schéma dans l’éditeur de schémas.

Pour générer une payload d’exportation, sélectionnez **[!UICONTROL Schemas]** dans le volet de navigation de gauche. Dans l’espace de travail [!UICONTROL Schemas] , sélectionnez la ligne du schéma à exporter pour afficher les détails du schéma dans la barre latérale droite.

>[!TIP]
>
>Consultez le guide sur l’[exploration des ressources XDM](./explore.md) pour plus d’informations sur la manière de trouver la ressource XDM que vous recherchez.

Sélectionnez ensuite l’icône **[!UICONTROL Copy JSON]** (![Icône Copier](/help/images/icons/copy.png)) dans les options disponibles.

![Espace de travail Schémas avec une ligne de schéma et un [!UICONTROL Copy to JSON] mis en surbrillance.](../images/ui/export/copy-json.png)

Cette opération copie une payload JSON dans le presse-papiers, générée en fonction de la structure du schéma. Pour le schéma « [!DNL Loyalty Members] » illustré ci-dessus, le fichier JSON suivant est généré :

+++Sélectionner cette option pour développer un exemple de payload JSON

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

La payload peut également être copiée en sélectionnant [!UICONTROL More] dans le coin supérieur droit de l’éditeur de schémas. Un menu déroulant fournit deux options, [!UICONTROL Copy JSON structure] et [!UICONTROL Delete schema].

>[!NOTE]
>
>Un schéma ne peut pas être supprimé s’il est activé pour le profil ou s’il est associé à des jeux de données.

![Éditeur de schémas avec [!UICONTROL More] et [!UICONTROL Copy to JSON] mis en surbrillance.](../images/ui/export/schema-editor-copy-json.png)

La payload se présente sous la forme d’un tableau, chaque élément du tableau étant un objet qui représente une ressource XDM personnalisée à exporter. Dans l’exemple ci-dessus, le groupe de champs personnalisés « [!DNL Loyalty details] » et le schéma « [!DNL Loyalty Members] » sont inclus. Toutes les ressources de base utilisées par le schéma ne sont pas incluses dans l’exportation, car ces ressources sont disponibles dans tous les sandbox et toutes les organisations.

Notez que chaque instance de l’identifiant du client de votre organisation apparaît comme `<XDM_TENANTID_PLACEHOLDER>` dans la payload. Ces espaces réservés seront automatiquement remplacés par la valeur d’identifiant client appropriée en fonction de l’endroit où vous importez le schéma à l’étape suivante.

## Importer la ressource à l’aide de l’API {#import-resource-with-api}

Une fois que vous avez copié le fichier JSON d’exportation pour le schéma, vous pouvez l’utiliser comme payload pour une requête POST vers le point d’entrée `/rpc/import` dans l’API Schema Registry. Pour plus d’informations sur la configuration de l’appel pour envoyer le schéma à l’organisation et au sandbox souhaités[ consultez le ](../api/import.md) guide du point d’entrée d’importation .

## Étapes suivantes

En suivant ce guide, vous avez réussi à exporter un schéma XDM vers une autre organisation ou un autre sandbox. Pour plus d’informations sur les fonctionnalités de l’interface utilisateur de [!UICONTROL Schemas], reportez-vous à la présentation de l’interface utilisateur de [[!UICONTROL Schemas] ](./overview.md).
