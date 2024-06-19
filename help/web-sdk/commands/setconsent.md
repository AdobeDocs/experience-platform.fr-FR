---
title: setConsent
description: Utilisé sur chaque page pour suivre les préférences de consentement de vos utilisateurs.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 3%

---


# `setConsent`

La variable `setConsent` indique au SDK Web s’il doit envoyer des données (inclusion), ignorer des données (exclusion) ou utiliser [`defaultConsent`](configure/defaultconsent.md) (consentement inconnu).

Le SDK Web prend en charge les normes suivantes :

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: les normes 1.0 et 2.0 sont prises en charge.
* **[Structure de transparence et de consentement de l’IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: si vous utilisez cette norme, le profil client en temps réel du visiteur est mis à jour avec les informations de consentement si votre mise en oeuvre est correctement configurée :
   1. Le schéma de profil individuel XDM contient la variable [Groupe de champs de consentement du TCF 2.0 de l’IAB](/help/xdm/field-groups/profile/iab.md).
   1. Le schéma Événement d’expérience contient la variable [Groupe de champs de consentement du TCF 2.0 de l’IAB](/help/xdm/field-groups/event/iab.md).
   1. Vous incluez les informations de consentement IAB dans l’événement [Objet XDM](sendevent/xdm.md). Le SDK Web n’inclut pas automatiquement les informations de consentement lors de l’envoi de données d’événement.

Après avoir utilisé cette commande, le SDK Web écrit les préférences de l’utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur, le SDK récupère ces préférences persistantes pour déterminer si des événements peuvent être envoyés à Adobe.

Adobe vous recommande de stocker les préférences de boîte de dialogue de consentement séparément de celles du consentement du SDK Web. Le SDK Web ne permet pas de récupérer le consentement. Pour vous assurer que les préférences de l’utilisateur restent synchronisées avec le SDK, vous pouvez appeler la fonction `setConsent` à chaque chargement de page. Le SDK Web effectue uniquement un appel au serveur lorsque le consentement est modifié.

## Utilisation `defaultConsent` ensemble avec `setConsent` {#using-consent}

Le SDK Web propose deux commandes de configuration de consentement complémentaires :

* [`defaultConsent`](configure/defaultconsent.md): cette commande est destinée à capturer les préférences de consentement des clients Adobe utilisant le SDK Web.
* [`setConsent`](setconsent.md): cette commande est destinée à capturer les préférences de consentement des visiteurs de votre site.

Lorsqu’ils sont utilisés ensemble, ces paramètres peuvent donner lieu à différents résultats de collecte de données et de définition des cookies, selon leurs valeurs configurées.

Consultez le tableau ci-dessous pour savoir quand se produit la collecte de données et quand les cookies sont définis, en fonction des paramètres de consentement.

| defaultConsent | setConsent | Collecte de données | Le SDK Web définit les cookies de navigateur. |
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

Les cookies suivants sont définis lorsque la configuration du consentement permet :

| Nom | Âge max. | Description |
|---|---|---|
| **AMCV_##@AdobeOrg** | 34128000 (395 jours) | Présenter quand [`idMigrationEnabled`](configure/idmigrationenabled.md) est activée. Cela s’avère utile lors de la transition vers le SDK Web alors que certaines parties du site utilisent toujours `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 jours) | Présent si la synchronisation des identifiants est activée. L’Audience Manager définit ce cookie afin d’affecter un identifiant unique à un visiteur du site. Le cookie demdex permet à Audience Manager d’exécuter des fonctions de base, telles que l’identification des visiteurs, la synchronisation des identifiants, la segmentation, la modélisation, la création de rapports, etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutes) | Stocke la région de l’Edge Network qui sert les requêtes de l’utilisateur actuel. La région est utilisée dans le chemin de l’URL afin que l’Edge Network puisse acheminer la requête vers la région appropriée. Si un utilisateur se connecte à une autre adresse IP ou lors d’une autre session, la demande est de nouveau acheminée vers la région la plus proche. |
| **kndct_orgid_identity** | 34128000 (395 jours) | Stocke l’ECID, ainsi que d’autres informations relatives à l’ECID. |
| **kndctr_orgid_consent** | 15552000 (180 jours) | Stocke les préférences de consentement des utilisateurs pour le site web. |
| **s_ecid** | 63115200 (2 ans) | Contient une copie de l’ID Experience Cloud ([!DNL ECID]) ou MID. Le MID est stocké dans une paire clé-valeur qui suit la syntaxe suivante, `s_ecid=MCMID\|<ECID>`. |

## Définition du consentement à l’aide de l’extension de balise SDK Web

La définition du consentement est effectuée en tant qu’action dans une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Définition du consentement]**.
1. Définissez les champs de votre choix à droite, y compris **[!UICONTROL Standard]** et **[!UICONTROL Consentement général]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

Vous pouvez inclure plusieurs objets de consentement dans cette action.

## Définition du consentement à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `setConsent` lors de l’appel de votre instance configurée du SDK Web. Vous pouvez inclure les objets suivants dans cette commande :

* **`consent[]`**: un tableau de `consent` objets. L’objet de consentement est formaté différemment selon la norme et la version que vous choisissez. Consultez les onglets ci-dessous pour obtenir des exemples de chaque objet de consentement, selon la norme de consentement.
* **`identityMap`**: objet contrôlant la manière dont un ECID est généré et les informations de consentement des identifiants sont liées. Adobe recommande d’inclure cet objet lors de la `setConsent` est exécuté avant d’autres commandes, telles que [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: objet qui contient [remplacements de la configuration du flux de données](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 standard `consent` objet

Si vous utilisez Adobe Experience Platform, vous devez inclure un groupe de champs de schéma de confidentialité dans votre schéma de profil. Voir [Gouvernance, confidentialité et sécurité dans Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) pour plus d’informations sur la norme Adobe 2.0. Vous pouvez ajouter des données dans l’objet de valeur ci-dessous correspondant au schéma de la variable `consents` du champ [!UICONTROL Consentements et préférences] groupe de champs de profil.

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 2.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme Adobe 2.0.
* **`value`**: objet contenant des valeurs de consentement.
   * **`value.collect.val`**: valeur de consentement. Définissez cette variable sur `"y"` lorsque les utilisateurs souscrivent et à `"n"` lorsque les utilisateurs se désabonnent.
   * **`value.metadata.time`**: horodatage de la dernière mise à jour des paramètres de consentement des utilisateurs.

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

### Norme IAB TCF 2.0 `consent` objet

Pour enregistrer les préférences de consentement de l’utilisateur fournies par le biais de la norme Transparency and Consent Framework (TCF) de l’Interactive Advertising Bureau Europe (IAB), définissez la chaîne de consentement comme illustré ci-dessous.

Lorsque le consentement est défini de cette manière, le profil client en temps réel est mis à jour avec les informations de consentement. Pour que cela fonctionne, le schéma XDM du profil doit contenir le [Groupe de champs de schéma Confidentialité du profil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Lors de l’envoi d’événements, les informations de consentement de l’IAB doivent être ajoutées manuellement à l’objet XDM d’événement. Le SDK Web n’inclut pas automatiquement les informations de consentement dans les événements.

Pour envoyer les informations de consentement dans les événements, vous devez ajouter le groupe de champs Confidentialité des événements d’expérience à votre [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schéma. Voir la section sur [mise à jour du schéma ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) dans le guide de préparation des jeux de données pour connaître les étapes de configuration.

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"IAB TCF"` pour la norme IAB TCF 2.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme IAB TCF 2.0.
* **`value`**: chaîne contenant la valeur de consentement.
* **`gdprApplies`**: valeur booléenne qui détermine si le RGPD s’applique à cette valeur de consentement. Sa valeur par défaut est `true`.
* **`gdprContainsPersonalData`**: valeur booléenne qui détermine si les données d’événement associées à cet utilisateur contiennent des données personnelles. Sa valeur par défaut est `false`.

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

### Adobe 1.0 standard `consent` objet

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 1.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"1.0"` pour la norme Adobe 1.0.
* **`value.general`**: valeur de consentement. Définissez cette variable sur `"in"` lorsque les utilisateurs souscrivent et à `"out"` lorsque les utilisateurs se désabonnent.

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

### Envoi de plusieurs normes dans une même requête {#multiple-standards}

Le SDK Web prend également en charge l’envoi de plusieurs objets de consentement dans une requête, comme illustré dans l’exemple ci-dessous.

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

Après avoir communiqué les préférences de l’utilisateur au SDK Web à l’aide de la variable `setConsent` , le SDK conserve les préférences de l’utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur, le SDK Web récupère et utilise ces préférences persistantes pour déterminer si des événements peuvent être envoyés à Adobe.

Vous devrez stocker les préférences de l’utilisateur indépendamment pour pouvoir afficher la boîte de dialogue de consentement avec les préférences actuelles. Il n’est pas possible de récupérer les préférences de l’utilisateur à partir du SDK Web. Pour vous assurer que les préférences de l’utilisateur restent synchronisées avec le SDK, vous pouvez appeler la fonction `setConsent` à chaque chargement de page. Le SDK Web effectue un appel au serveur uniquement si les préférences ont changé.

## Synchronisation des identités lors de la définition du consentement {#sync-identities}

Lorsque le consentement par défaut (défini par l’intermédiaire de la variable [defaultConsent](configure/defaultconsent.md) ) est défini sur `pending` ou `out`, la variable `setConsent` peut être la première requête qui établit l’identité. Il peut donc être important de synchroniser les identités lors de la première requête. Vous pouvez ajouter la carte d’identité à la variable `setConsent` comme sur la commande `sendEvent` . Voir [utilisation d’identityMap](../identity/overview.md#using-identitymap) pour obtenir un exemple d’inclusion de identity map dans votre commande.
