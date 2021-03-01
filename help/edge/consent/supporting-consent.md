---
title: Prise en charge des préférences de consentement des clients à l’aide du SDK Web Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement avec le Adobe Experience Platform Web SDK.
keywords: consentement ; defaultConsent ; consentement par défaut ; setConsent ; mélange de confidentialité des Profils ; mélange de confidentialité des Événements d’expérience ; mélange de confidentialité ;
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 57%

---


# Prise en charge des préférences de consentement du client

Pour respecter la confidentialité des utilisateurs, vous pouvez leur demander leur consentement avant d’autoriser le SDK à utiliser des données spécifiques à ceux-ci à certains usages. Actuellement, le SDK permet aux utilisateurs de donner ou de refuser leur consentement uniquement pour tous les usages, mais Adobe espère prochainement offrir un contrôle plus précis sur des usages spécifiques.

Si l’utilisateur choisit de donner son consentement pour tous les usages, le SDK est autorisé à effectuer les tâches suivantes :

* envoyer des données vers et depuis les serveurs d’Adobe ;
* Lisez et écrivez des cookies ou des éléments d’enregistrement Web.

Si l’utilisateur choisit de refuser son consentement pour tous les usages, le SDK n’effectue aucune de ces tâches.

## Configuration du consentement

Par défaut, le consentement de l’utilisateur est donné pour tous les usages. Pour empêcher le SDK d’exécuter les tâches ci-dessus jusqu’à ce que l’utilisateur donne son consentement, transmettez `"defaultConsent": "pending"` pendant la configuration du SDK de la manière suivante :

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Lorsque le consentement par défaut pour un usage général est défini sur En attente, toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur (par exemple, la commande`event`) entraîne la mise en file d’attente de la commande dans le SDK. Ces commandes ne sont pas traitées tant que vous n’avez pas communiqué les préférences de consentement de l’utilisateur au SDK.

À ce stade, vous préférerez peut-être demander à l’utilisateur de donner son consentement à un emplacement dans l’interface utilisateur. Une fois les préférences de l’utilisateur collectées, communiquez-les au SDK.

## Communication des préférences de consentement via Adobe Standard

Si l’utilisateur accorde son consentement, exécutez la commande `setConsent` en définissant l’option `general` sur `in` de la manière suivante :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

L’utilisateur ayant donné son consentement, le SDK exécute toutes les commandes précédemment mises en file d’attente. Les prochaines commandes qui dépendent du consentement de l’utilisateur ne seront pas mises en file d’attente et seront exécutées rapidement.

Si l’utilisateur choisit de ne pas donner son consentement, exécutez la commande `setConsent` en définissant l’option `general` sur `out` de la manière suivante :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>Lorsque l’utilisateur n’a pas donné son consentement, le SDK ne vous permet pas de définir le consentement des utilisateurs sur `in`.

L’utilisateur ayant choisi de ne pas donner son consentement, les promesses qui ont été renvoyées à partir de commandes précédemment mises en file d’attente sont rejetées. Les prochaines commandes qui dépendent du consentement de l’utilisateur retournent les promesses également rejetées. Pour plus d’informations sur la gestion ou la suppression des erreurs, reportez-vous à la section [Exécution des commandes](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Actuellement, le SDK ne prend en charge que l’usage `general`. Bien que nous prévoyions de créer un ensemble plus riche d’usages ou de catégories qui devront correspondre aux différentes capacités et offres de produits Adobe, l’implémentation actuelle s’effectue sur la base du « tout ou rien ».  Ceci s’applique uniquement à Adobe Experience Platform [!DNL Web SDK] et NON à d’autres bibliothèques JavaScript d’Adobe.

## Communiquer les préférences de consentement au moyen de la norme TCF de l&#39;IAB

Le SDK prend en charge l’enregistrement des préférences de consentement d’un utilisateur fournies par le biais de la norme Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF). La chaîne de consentement peut être définie à l’aide de la même commande `setConsent` que ci-dessus :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Lorsque le consentement est défini de cette manière, le Profil client en temps réel est mis à jour avec les informations de consentement. Pour que cela fonctionne, le schéma XDM du profil doit contenir le [mélange de confidentialité du Profil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Lors de l’envoi de événements, les informations de consentement IAB doivent être ajoutées manuellement à l’objet XDM du événement. Le SDK n’inclut pas automatiquement les informations de consentement dans les événements. Pour envoyer les informations de consentement dans les événements, le [Mélange de confidentialité du Événement d’expérience](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) doit être ajouté au schéma du Événement d’expérience.

## Envoi des deux normes dans une seule requête

Le SDK prend également en charge l’envoi de plusieurs objets de consentement dans une requête.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistance des préférences de consentement

Après avoir communiqué les préférences de l’utilisateur au SDK à l’aide de la commande `setConsent`, le SDK les conserve dans un cookie. La prochaine fois que l’utilisateur charge votre site Web dans le navigateur, le SDK récupérera et utilisera ces préférences persistantes pour déterminer si des événements peuvent être envoyés à l’Adobe ou non. Il n’est pas nécessaire d’exécuter de nouveau la commande `setConsent`, sauf pour communiquer un changement dans les préférences de l’utilisateur, ce que vous pouvez faire à tout moment.

## Synchronisation des identités lors de la définition du consentement

Lorsque le consentement par défaut est en attente, `setConsent` peut être la première requête à être envoyée et à établir l&#39;identité. C’est pourquoi il peut s’avérer important de synchroniser les identités lors de la première requête. La carte d&#39;identité peut être ajoutée à la commande `setConsent`, tout comme dans la commande `sendEvent`. Voir [Récupération de l’ID d’Experience Cloud](../identity/overview.md).

