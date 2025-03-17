---
title: setConsent
description: Utilisé sur chaque page pour suivre les préférences de consentement de vos utilisateurs.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 83b4745693749c5f50791d6efeb3a7ba02a4cce5
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 3%

---


# `setConsent`

La commande `setConsent` indique à Web SDK s’il doit envoyer des données (opt-in), les ignorer (opt-out) ou les utiliser [`defaultConsent`](configure/defaultconsent.md) (consentement inconnu).

Web SDK prend en charge les normes suivantes :

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)** : les normes 1.0 et 2.0 sont prises en charge.
* **[Transparence et cadre de consentement IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)** : si vous utilisez cette norme, le profil client en temps réel du visiteur est mis à jour avec les informations de consentement si votre implémentation est correctement configurée :
   1. Le schéma de profil individuel XDM contient le groupe de champs de consentement [IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Le schéma Événement d’expérience contient le groupe de champs de consentement [IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Vous incluez les informations de consentement IAB dans l’événement [objet XDM](sendevent/xdm.md). Le SDK Web n’inclut pas automatiquement les informations de consentement lors de l’envoi des données d’événement.

Après avoir utilisé cette commande, le SDK Web écrit les préférences de l’utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur , le SDK récupère ces préférences persistantes afin de déterminer si des événements peuvent être envoyés à Adobe.

Adobe vous recommande de stocker les préférences de boîte de dialogue de consentement séparément du consentement de Web SDK. Le SDK Web ne permet pas de récupérer le consentement. Pour vous assurer que les préférences utilisateur restent synchronisées avec le SDK, vous pouvez appeler la commande `setConsent` à chaque chargement de page. Web SDK effectue uniquement un appel au serveur lorsque le consentement est modifié.

## Considérations relatives à la synchronisation des identités {#identity-considerations}

La commande `setConsent` utilise uniquement le `ECID` du mappage d’identités, car elle fonctionne au niveau de l’appareil. Les autres identités du mappage d’identités ne sont pas prises en compte par la commande `setConsent`.

## Utilisation de `defaultConsent` avec `setConsent` {#using-consent}

Web SDK propose deux commandes de configuration de consentement complémentaires :

* [`defaultConsent`](configure/defaultconsent.md) : cette commande est destinée à capturer les préférences de consentement des clients Adobe utilisant Web SDK.
* [`setConsent`](setconsent.md) : cette commande est destinée à capturer les préférences de consentement des visiteurs de votre site.

Utilisés conjointement, ces paramètres peuvent donner lieu à différents résultats de collecte de données et de définition de cookies, en fonction de leurs valeurs configurées.

Consultez le tableau ci-dessous pour comprendre à quel moment la collecte de données a lieu et quand les cookies sont définis, en fonction des paramètres de consentement.

| defaultConsent | setConsent | Collecte de données | Web SDK définit les cookies de navigateur |
|---------|----------|---------|---------|
| `in` | `in` | Oui | Oui |
| `in` | `out` | Non | Oui |
| `in` | Non défini | Oui | Oui |
| `pending` | `in` | Oui | Oui |
| `pending` | `out` | Non | Oui |
| `pending` | Non défini | Non | Non |
| `out` | `in` | Oui | Oui |
| `out` | `out` | Non | Oui |
| `out` | Non défini | Non | Non |

Les cookies suivants sont définis lorsque la configuration du consentement le permet :

| Nom | Âge max. | Description |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 jours) | Présent lorsque le [`idMigrationEnabled`](configure/idmigrationenabled.md) est activé. Cela s’avère utile lors de la transition vers Web SDK lorsque certaines parties du site utilisent encore `visitor.js`. |
| **Cookie demdex** | 15552000 (180 jours) | Présent si la synchronisation des identifiants est activée. Audience Manager définit ce cookie pour attribuer un identifiant unique à un visiteur du site. Le cookie demdex aide Audience Manager à effectuer des fonctions de base, telles que l’identification des visiteurs, la synchronisation des identifiants, la segmentation, la modélisation, le compte rendu des performances, etc. |
| **kndctr_orgid_cluster** | 1 800 (30 minutes) | Stocke la région Edge Network qui répond aux demandes de l’utilisateur actuel. La région est utilisée dans le chemin de l’URL afin que l’Edge Network puisse acheminer la requête vers la bonne région. Si un utilisateur se connecte avec une adresse IP différente ou dans une session différente, la requête est à nouveau acheminée vers la région la plus proche. |
| **kndct_orgid_identity** | 34128000 (395 jours) | Stocke l’ECID, ainsi que d’autres informations relatives à l’ECID. |
| **kndctr_orgid_consent** | 15552000 (180 jours) | Stocke la préférence de consentement des utilisateurs pour le site web. |
| **s_ecid** | 63115200 (2 ans) | Contient une copie de l’Experience Cloud ID ([!DNL ECID]) ou du MID. Le MID est stocké dans une paire clé-valeur qui suit la syntaxe suivante, `s_ecid=MCMID\|<ECID>`. |

## Définir le consentement à l’aide de l’extension de balise Web SDK

La définition du consentement est effectuée sous la forme d’une action dans une règle de l’interface des balises de la collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Définir le consentement]**.
1. Définissez les champs souhaités sur la droite, y compris **[!UICONTROL Standard]** et **[!UICONTROL Consentement général]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

Vous pouvez inclure plusieurs objets de consentement dans cette action.

## Définir le consentement à l’aide de la bibliothèque JavaScript de Web SDK

Exécutez la commande `setConsent` lors de l’appel de votre instance configurée de Web SDK. Vous pouvez inclure les objets suivants dans cette commande :

* **`consent[]`** : tableau d’objets `consent`. L’objet de consentement est formaté différemment selon la norme et la version que vous choisissez. Consultez les onglets ci-dessous pour obtenir des exemples de chaque objet de consentement, en fonction de la norme de consentement.
* **`identityMap`** : objet contrôlant la manière dont un ECID est généré et les ID auxquels les informations de consentement sont liées. Adobe recommande d’inclure cet objet lorsque `setConsent` est exécuté avant d’autres commandes, telles que [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`** : objet contenant des remplacements de configuration de train de données [datastream](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Objet `consent` standard Adobe 2.0

Si vous utilisez Adobe Experience Platform, vous devez inclure un groupe de champs de schéma de confidentialité dans votre schéma de profil. Voir [Gouvernance, confidentialité et sécurité dans Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) pour plus d’informations sur la norme Adobe 2.0. Vous pouvez ajouter des données à l’intérieur de l’objet de valeur sous correspondant au schéma du champ de `consents` du groupe de champs de profil [!UICONTROL Consentements et préférences].

* **`standard`** : norme de consentement choisie. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 2.0.
* **`version`** : chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme Adobe 2.0.
* **`value`** : objet contenant des valeurs de consentement.
   * **`value.collect.val`** : valeur de consentement. Définissez ce paramètre sur `"y"` lorsque les utilisateurs souscrivent et sur `"n"` lorsqu’ils se désinscrivent.
   * **`value.metadata.time`** : date et heure de la dernière mise à jour des paramètres de consentement des utilisateurs.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### Objet `consent` standard IAB TCF 2.0

Pour enregistrer les préférences de consentement de l’utilisateur fournies par le biais de la norme Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF), définissez la chaîne de consentement comme illustré ci-dessous.

Lorsque le consentement est défini de cette manière, le profil client en temps réel est mis à jour avec les informations de consentement. Pour que cela fonctionne, le schéma XDM de profil doit contenir le [groupe de champs de schéma de confidentialité du profil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Lors de l’envoi d’événements, les informations de consentement IAB doivent être ajoutées manuellement à l’objet XDM d’événement. Le SDK Web n’inclut pas automatiquement les informations de consentement dans les événements.

Pour envoyer les informations de consentement dans les événements, vous devez ajouter le groupe de champs Confidentialité des événements d’expérience à votre schéma de [!DNL XDM ExperienceEvent] activé pour [!DNL Profile]. Voir la section [mise à jour du schéma ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) dans le guide de préparation des jeux de données pour savoir comment configurer cela.

* **`standard`** : norme de consentement choisie. Définissez cette propriété sur `"IAB TCF"` pour la norme IAB TCF 2.0.
* **`version`** : chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme IAB TCF 2.0.
* **`value`** : chaîne contenant la valeur de consentement.
* **`gdprApplies`** : une valeur booléenne qui détermine si le RGPD s’applique à cette valeur de consentement. Sa valeur par défaut est `true`.
* **`gdprContainsPersonalData`** : valeur booléenne qui détermine si les données d’événement associées à cet utilisateur contiennent des données personnelles. Sa valeur par défaut est `false`.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Objet `consent` standard Adobe 1.0

* **`standard`** : norme de consentement choisie. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 1.0.
* **`version`** : chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"1.0"` pour la norme Adobe 1.0.
* **`value.general`** : valeur de consentement. Définissez ce paramètre sur `"in"` lorsque les utilisateurs souscrivent et sur `"out"` lorsqu’ils se désinscrivent.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### Envoi de plusieurs standards en une seule requête {#multiple-standards}

Web SDK prend également en charge l’envoi de plusieurs objets de consentement dans une requête, comme illustré dans l’exemple ci-dessous.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "2021-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Persistance des préférences de consentement {#persistence}

Après avoir communiqué les préférences utilisateur à Web SDK à l’aide de la commande `setConsent`, SDK conserve les préférences utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur , le Web SDK récupère et utilise ces préférences persistantes pour déterminer si des événements peuvent être envoyés ou non à Adobe.

Vous devez stocker les préférences utilisateur indépendamment pour pouvoir afficher la boîte de dialogue de consentement avec les préférences actuelles. Il n’existe aucun moyen de récupérer les préférences utilisateur à partir de Web SDK. Pour vous assurer que les préférences utilisateur restent synchronisées avec le SDK, vous pouvez appeler la commande `setConsent` à chaque chargement de page. Web SDK n’effectue un appel au serveur que si les préférences ont changé.
