---
title: Prise en charge des préférences de consentement des clients à l’aide du SDK Web Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement avec le Adobe Experience Platform Web SDK.
keywords: consentement ; defaultConsent ; consentement par défaut ; setConsent ; mélange de confidentialité des Profils ; mélange de confidentialité des Événements d’expérience ; mélange de confidentialité ;
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 33%

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

Lorsque le consentement par défaut pour un usage général est défini sur En attente, toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur (par exemple, la commande`sendEvent`) entraîne la mise en file d’attente de la commande dans le SDK. Ces commandes ne sont pas traitées tant que vous n’avez pas communiqué les préférences de consentement de l’utilisateur au SDK.

>[!NOTE]
>
>Les commandes sont placées en file d&#39;attente uniquement en mémoire. Ils ne sont pas enregistrés lors des chargements de pages.

Si vous ne souhaitez pas collecter les événements qui se sont produits avant que les préférences d’inclusion de l’utilisateur ne soient définies, vous pouvez transmettre `"defaultConsent": "out"` pendant la configuration du SDK. Toute tentative d’exécution de commandes qui dépendent des préférences d’inclusion de l’utilisateur n’aura aucun effet tant que vous n’aurez pas communiqué les préférences d’inclusion de l’utilisateur au SDK.

>[!NOTE]
>
>Actuellement, le SDK ne prend en charge qu’un seul objectif tout ou rien. Bien que nous prévoyions de créer un ensemble plus riche d’usages ou de catégories qui devront correspondre aux différentes capacités et offres de produits Adobe, l’implémentation actuelle s’effectue sur la base du « tout ou rien ».  Ceci s’applique uniquement à Adobe Experience Platform [!DNL Web SDK] et NON à d’autres bibliothèques JavaScript d’Adobe.

À ce stade, vous préférerez peut-être demander à l’utilisateur de donner son consentement à un emplacement dans l’interface utilisateur. Une fois les préférences de l’utilisateur collectées, communiquez-les au SDK.

## Communication des préférences de consentement via la norme Adobe Experience Platform

Le SDK prend en charge les versions 1.0 et 2.0 de la norme de consentement Adobe Experience Platform. À l&#39;heure actuelle, les normes 1.0 et 2.0 n&#39;appuient que l&#39;application automatique d&#39;une préférence de consentement pour tout ou rien. La norme 1.0 est progressivement abandonnée en faveur de la norme 2.0. La norme 2.0 vous permet d’ajouter des préférences de consentement supplémentaires qui peuvent être utilisées pour appliquer manuellement les préférences de consentement.

### Utilisation de la version Adobe standard 2.0

Si vous utilisez Adobe Experience Platform, vous devrez inclure un mixin de confidentialité dans votre schéma de profil. Voir [Gouvernance, confidentialité et sécurité dans Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) pour plus d’informations sur la version standard de l’Adobe 2.0. Vous pouvez ajouter des données dans l’objet de valeur ci-dessous correspondant au schéma du champ `consents` du mixin du profil Consommations et préférences.

Si l’utilisateur accepte, exécutez la commande `setConsent` avec la préférence de collecte définie sur `y` comme suit :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        }
      }
    }]
});
```

Si l’utilisateur choisit de opt-out, exécutez la commande `setConsent` avec la préférence de collecte définie sur `n` comme suit :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        }
      }
    }]
});
```

>[!NOTE]
>
>Une fois qu’un utilisateur s’est désabonné, le SDK ne vous permet pas de définir le consentement des utilisateurs pour la collecte sur `y`.

### Utilisation de l’Adobe version 1.0 standard

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

## Envoi de plusieurs normes dans une seule requête

Le SDK prend également en charge l’envoi de plusieurs objets de consentement dans une requête.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        }
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

Après avoir communiqué les préférences de l’utilisateur au SDK à l’aide de la commande `setConsent`, le SDK les conserve dans un cookie. La prochaine fois que l’utilisateur charge votre site Web dans le navigateur, le SDK récupérera et utilisera ces préférences persistantes pour déterminer si des événements peuvent être envoyés à l’Adobe ou non.

Vous devez stocker les préférences de l&#39;utilisateur indépendamment pour pouvoir afficher la boîte de dialogue de consentement avec les préférences actuelles. Il n’existe aucun moyen de récupérer les préférences de l’utilisateur à partir du SDK. Pour vous assurer que les préférences utilisateur restent synchronisées avec le SDK, vous pouvez appeler la commande `setConsent` à chaque chargement de page. Le SDK effectue un appel serveur uniquement si les préférences ont changé.

## Synchronisation des identités lors de la définition du consentement

Lorsque le consentement par défaut est en attente ou en attente, `setConsent` peut être la première demande qui sort et établit l&#39;identité. C’est pourquoi il peut s’avérer important de synchroniser les identités lors de la première requête. La carte d&#39;identité peut être ajoutée à la commande `setConsent`, tout comme dans la commande `sendEvent`. Voir [Récupération de l’ID d’Experience Cloud](../identity/overview.md).

