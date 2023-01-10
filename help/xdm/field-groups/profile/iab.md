---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schéma;conception de schéma;groupe de champs;iab;tcf;consentement
solution: Experience Platform
title: Groupe de champs de consentement du TCF 2.0 de l’IAB pour les schémas de profil
description: Ce document fournit un aperçu du groupe de champs de schéma de consentement IAB TCF 2.0 pour la classe XDM Individual Profile.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---

# [!UICONTROL Consentement IAB TCF 2.0] groupe de champs pour les schémas de profil

>[!NOTE]
>
>Ce document couvre les [!UICONTROL Consentement IAB TCF 2.0] groupe de champs de schéma pour la classe XDM Individual Profile. Pour le groupe de champs destiné à la classe XDM ExperienceEvent, reportez-vous aux sections suivantes : [document](../event/iab.md) au lieu de .

[!UICONTROL Consentement IAB TCF 2.0] est un groupe de champs de schéma standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) utilisé pour capturer une série horodatée de chaînes de consentement IAB, afin de suivre les modèles de changement de consentement au fil du temps.

![](../../images/field-groups/iab-profile.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `identityPrivacyInfo` | Carte | Objet de type map qui associe les valeurs d’identité individuelles d’un client à différentes chaînes de consentement TCF. Vous trouverez ci-dessous un exemple de la structure de cet objet. |

{style=&quot;table-layout:auto&quot;}

Le fichier JSON suivant illustre la structure de la variable `identityPrivacyInfo` carte.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Comme le montre l’exemple, chaque clé de niveau racine de `xdm:identityPrivacyInfo` correspond à un espace de noms d’identité reconnu par Identity Service. De même, chaque propriété d’espace de noms doit comporter au moins une sous-propriété dont la clé correspond à la valeur d’identité correspondante du client pour cet espace de noms. Dans cet exemple, le client est identifié avec un identifiant Experience Cloud (`ECID`) valeur de `13782522493631189`.

>[!NOTE]
>
>Bien que l’exemple ci-dessus utilise une seule paire espace de noms/valeurs pour représenter l’identité du client, vous pouvez ajouter des clés supplémentaires pour d’autres espaces de noms, et chaque espace de noms peut avoir plusieurs valeurs d’identité, chacune avec son propre jeu de préférences de consentement TCF.

Pour chaque valeur d’identité, une `identityIABConsent` doit être fournie, ce qui fournit la valeur de consentement TCF pour l’identité. La valeur de cette propriété doit être conforme à la propriété [[!UICONTROL Chaîne de consentement] type de données](../../data-types/consent-string.md).

Consultez le guide sur la [Prise en charge du TCF 2.0 de l’IAB dans Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) pour plus d’informations sur le cas d’utilisation de ce groupe de champs. Pour plus d’informations sur le groupe de champs lui-même, consultez le référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
