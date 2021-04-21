---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; segment ; adhésion à un segment ; adhésion à un segment ; conception de Schéma ; carte ; carte ;
solution: Experience Platform
title: Mélange de détails d'adhésion de segment
topic-legacy: overview
description: Ce document présente un aperçu du mixin Détails de l’appartenance au segment.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# [!UICONTROL Segmenter les ] détails de l&#39;adhésion mixin

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

[!UICONTROL Appartenance à un segment ] Détail d&#39;un mixin standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit un champ de mappage unique qui capture les informations concernant l’appartenance au segment, y compris les segments auxquels appartient la personne, l’heure de la dernière qualification et le moment où l’appartenance est valide jusqu’à la date de validité de l’adhésion.

>[!WARNING]
>
>Bien que le champ `segmentMembership` doive être ajouté manuellement à votre schéma de profil à l&#39;aide de ce mixin, vous ne devez pas essayer de renseigner ou de mettre à jour ce champ manuellement. Le système met automatiquement à jour la carte `segmentMembership` pour chaque profil au fur et à mesure que les tâches de segmentation sont exécutées.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `segmentMembership` | Carte | Objet map qui décrit les appartenances aux segments de la personne. La structure de cet objet est décrite en détail ci-dessous. |

Voici un exemple de mappage `segmentMembership` que le système a renseigné pour un profil particulier. Les adhésions aux segments sont triées par espace de nommage, comme indiqué par les clés de niveau racine de l’objet. En retour, les clés individuelles sous chaque espace de nommage représentent les ID des segments dont le profil est membre. Chaque objet de segment contient plusieurs sous-champs qui fournissent des détails supplémentaires sur l’appartenance :

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `xdm:version` | Version du segment pour lequel ce profil s’est qualifié. |
| `xdm:lastQualificationTime` | Horodatage de la dernière qualification de ce profil pour le segment. |
| `xdm:validUntil` | Horodatage indiquant à quel moment l’appartenance au segment ne doit plus être considérée comme valide. |
| `xdm:status` | Indique si l’appartenance au segment a été réalisée dans le cadre de la demande en cours. Les valeurs suivantes sont acceptées : <ul><li>`existing`: Le profil faisait déjà partie du segment avant la demande et continue à en faire partie.</li><li>`realized`: Le profil entre le segment dans le cadre de la demande en cours.</li><li>`exited`: Le profil quitte le segment dans le cadre de la demande en cours.</li></ul> |
| `xdm:payload` | Certains abonnements de segment incluent une charge utile qui décrit les valeurs supplémentaires directement liées à l’appartenance. Une seule charge utile d’un type donné peut être fournie pour chaque abonnement. `xdm:payloadType` indique le type de charge utile (`boolean`,  `number`,  `propensity` ou  `string`), tandis que sa propriété frère fournit la valeur du type de charge utile. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
