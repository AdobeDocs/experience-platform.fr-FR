---
solution: Experience Platform
title: Groupe de champs de schéma Détails de l’appartenance à un segment
description: Découvrez le groupe de champs Détails de l’appartenance au segment .
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 20%

---


# [!UICONTROL Détails de l’adhésion au segment] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Segment Membership Details] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un champ map unique qui capture les informations concernant l’appartenance au segment, y compris les segments auxquels appartient l’individu, l’heure de la dernière qualification et le moment où l’appartenance est valide jusqu’à ce que le groupe de champs fournisse des informations.

>[!WARNING]
>
>Bien que le champ `segmentMembership` doive être ajouté manuellement à votre schéma de profil à l’aide de ce groupe de champs, vous ne devez pas essayer de renseigner ou de mettre à jour ce champ manuellement. Le système met automatiquement à jour la carte `segmentMembership` pour chaque profil lors de l’exécution des tâches de segmentation.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `segmentMembership` | Carte | Objet map qui décrit les appartenances à un segment de l’individu. La structure de cet objet est décrite en détail ci-dessous. |

{style="table-layout:auto"}

Voici un exemple de mappage `segmentMembership` que le système a renseigné pour un profil particulier. Les appartenances aux segments sont triées par espace de noms, comme indiqué par les clés au niveau racine de l’objet. En retour, les clés individuelles sous chaque espace de noms représentent les identifiants des segments dont le profil est membre. Chaque objet de segment contient plusieurs sous-champs qui fournissent des détails supplémentaires sur l’appartenance :

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
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
| `xdm:lastQualificationTime` | Date et heure de la dernière qualification de ce profil pour le segment. |
| `xdm:validUntil` | Horodatage indiquant le moment où l’appartenance au segment ne doit plus être considérée comme valide. Pour les audiences externes, si ce champ n’est pas défini, l’appartenance au segment sera conservée uniquement pendant 30 jours à partir du `lastQualificationTime`. |
| `xdm:status` | Un champ de chaîne qui indique si l’appartenance à un segment a été réalisée dans le cadre de la requête actuelle. Les valeurs suivantes sont acceptées : <ul><li>`realized` : le profil est admissible pour le segment.</li><li>`exited` : le profil quitte le segment dans le cadre de la requête actuelle.</li></ul> |
| `xdm:payload` | Certaines adhésions aux segments incluent une payload qui décrit les valeurs supplémentaires directement liées à l’appartenance. Un seul payload d’un type donné peut être fourni pour chaque appartenance. `xdm:payloadType` indique le type de payload (`boolean`, `number`, `propensity` ou `string`), tandis que sa propriété frère fournit la valeur du type de payload. |

{style="table-layout:auto"}

>[!NOTE]
>
>Toute appartenance à un segment qui a l’état `exited` pendant plus de 30 jours, sur la base de `lastQualificationTime`, sera sujette à suppression.

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
