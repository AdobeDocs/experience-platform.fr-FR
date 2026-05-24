---
title: setConsent
description: Utilisé sur chaque page pour suivre les préférences de consentement de vos utilisateurs.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
TQID: https://experienceleague.adobe.com/kQQB8KbJRWZvviQB-8hQ5dsdBio411lMiKugggJRDRQ
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1066
ht-degree: 0%

---

# `setConsent`

La commande `setConsent` indique à Web SDK s’il doit envoyer des données (opt-in), les ignorer (opt-out) ou les utiliser [`defaultConsent`](configure/defaultconsent.md) (consentement inconnu).

Web SDK prend en charge les normes suivantes :

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)** : les normes 1.0 et 2.0 sont prises en charge.
* **[Transparence et cadre de consentement IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)** : si vous utilisez cette norme, le profil client en temps réel du visiteur est mis à jour avec les informations de consentement si votre implémentation est correctement configurée :
   1. Le schéma de profil individuel XDM contient le groupe de champs de consentement [IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Le schéma Événement d’expérience contient le groupe de champs de consentement [IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Vous incluez les informations de consentement IAB dans l’événement [objet XDM](sendevent/xdm.md). Le SDK Web n’inclut pas automatiquement les informations de consentement lors de l’envoi des données d’événement.

Lors de l’utilisation de cette commande, le SDK Web écrit les préférences de l’utilisateur dans le cookie [`kndctr_<orgId>_consent`](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk). Ce cookie est défini quelles que soient les préférences de consentement du visiteur, car il stocke ses préférences de consentement. La prochaine fois que l’utilisateur charge votre site web dans le navigateur , le SDK récupère ces préférences persistantes afin de déterminer si des événements peuvent être envoyés à Adobe.

Adobe vous recommande de stocker les préférences de boîte de dialogue de consentement séparément du consentement de Web SDK. Le SDK Web ne permet pas de récupérer le consentement. Pour vous assurer que les préférences utilisateur restent synchronisées avec le SDK, vous pouvez appeler la commande `setConsent` à chaque chargement de page. Web SDK effectue uniquement un appel au serveur lorsque le consentement est modifié.

## Considérations relatives à la synchronisation des identités {#identity-considerations}

La commande `setConsent` utilise uniquement le `ECID` du mappage d’identités, car elle fonctionne au niveau de l’appareil. Les autres identités du mappage d’identités ne sont pas prises en compte par la commande `setConsent`.

## Utilisation de `defaultConsent` avec `setConsent` {#using-consent}

Utilisés conjointement, `defaultConsent` et `setConsent` produisent différents résultats de collecte de données, de configuration des cookies et d’identité en fonction de leurs valeurs configurées. Voir [Consentement et identité dans la collecte de données](/help/collection/identity/consent.md#how-consent-affects-identity) pour obtenir un tableau d’interaction complet.

## Utilisation de la commande `setConsent`

Exécutez la commande `setConsent` lors de l’appel de votre instance configurée de Web SDK. Vous pouvez inclure les objets suivants dans cette commande :

* **`consent[]`** : tableau d’objets `consent`. L’objet de consentement est formaté différemment selon la norme et la version que vous choisissez. Consultez les onglets ci-dessous pour obtenir des exemples de chaque objet de consentement, en fonction de la norme de consentement.
* **`identityMap`** : objet contrôlant la manière dont un ECID est généré et les ID auxquels les informations de consentement sont liées. Adobe recommande d’inclure cet objet lorsque `setConsent` est exécuté avant d’autres commandes, telles que [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`** : objet contenant des remplacements de configuration de train de données [datastream](configure/edgeconfigoverrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Objet `consent` standard Adobe 2.0

Si vous envoyez des données à Adobe Experience Platform, vous souhaiterez inclure un groupe de champs de schéma de confidentialité dans votre schéma de profil. Voir [Gouvernance, confidentialité et sécurité dans Adobe Experience Platform](/help/landing/governance-privacy-security/overview.md) pour plus d’informations sur la norme Adobe 2.0. Vous pouvez ajouter des données à l’intérieur de l’objet de valeur sous correspondant au schéma du champ de `consents` du groupe de champs de profil de [!UICONTROL Consents and Preferences].

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

Pour envoyer les informations de consentement dans les événements, vous devez ajouter le groupe de champs Confidentialité des événements d’expérience à votre schéma de [!DNL XDM ExperienceEvent] activé pour [!DNL Profile]. Voir la section [mise à jour du schéma ExperienceEvent](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) dans le guide de préparation des jeux de données pour savoir comment configurer cela.

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

L’API IAB TCF 2.0 fournit un événement pour le moment où le consentement est mis à jour par le client. Cela se produit lorsque le client définit initialement ses préférences et lorsqu’il les met à jour. Vous pouvez ajouter un écouteur d’événement pour exécuter la commande `setConsent` :

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Le bloc de code ci-dessus écoute l’événement de `useractioncomplete`, puis définit le consentement en transmettant la chaîne de consentement et l’indicateur de `gdprApplies`. Si vous disposez d’identités personnalisées pour vos clients, veillez à renseigner la variable `identityMap` .

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
                time: "YYYY-03-17T15:48:42-07:00"
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

Après avoir communiqué les préférences utilisateur à Web SDK à l’aide de la commande `setConsent`, SDK conserve les préférences utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur , Web SDK récupère et utilise ces préférences persistantes pour déterminer si des événements peuvent être envoyés ou non à Adobe.

Stockez les préférences de l’utilisateur indépendamment afin de pouvoir afficher la boîte de dialogue de consentement avec les préférences actuelles. Il n’existe aucun moyen de récupérer les préférences utilisateur à partir de Web SDK. Pour vous assurer que les préférences utilisateur restent synchronisées avec le SDK, vous pouvez appeler la commande `setConsent` à chaque chargement de page. Web SDK effectue uniquement un appel au serveur si les préférences changent.

## Définir le consentement à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
