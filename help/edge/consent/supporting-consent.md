---
title: Prise en charge des préférences de consentement du client à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement avec le SDK Web de Adobe Experience Platform.
keywords: consentement;defaultConsent;consentement par défaut;setConsent;groupe de champs Confidentialité du profil;groupe de champs Confidentialité des événements d’expérience;groupe de champs Confidentialité ;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 16c8972333fa67fa2e308445f4ad6282510370d1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 31%

---

# Prise en charge des préférences de consentement du client

Pour respecter la confidentialité des utilisateurs, vous pouvez leur demander leur consentement avant d’autoriser le SDK à utiliser des données spécifiques à ceux-ci à certains usages. Actuellement, le SDK permet aux utilisateurs de donner ou de refuser leur consentement uniquement pour tous les usages, mais Adobe espère prochainement offrir un contrôle plus précis sur des usages spécifiques.

Si l’utilisateur choisit de donner son consentement pour tous les usages, le SDK est autorisé à effectuer les tâches suivantes :

* envoyer des données vers et depuis les serveurs d’Adobe ;
* Lire et écrire des cookies ou des éléments de stockage web.

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
>Les commandes ne sont mises en file d&#39;attente que dans la mémoire. Elles ne sont pas enregistrées lors des chargements de page.

Si vous ne souhaitez pas collecter les événements qui se sont produits avant la définition des préférences d’inclusion de l’utilisateur, vous pouvez transmettre `"defaultConsent": "out"` pendant la configuration du SDK. Toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur n’aura aucun effet tant que vous n’aurez pas communiqué les préférences de consentement de l’utilisateur au SDK.

>[!NOTE]
>
>Actuellement, le SDK ne prend en charge qu’une seule fonction tout ou rien. Bien que nous prévoyions de créer un ensemble plus riche d’usages ou de catégories qui devront correspondre aux différentes capacités et offres de produits Adobe, l’implémentation actuelle s’effectue sur la base du « tout ou rien ».  Cela s’applique uniquement à Adobe Experience Platform [!DNL Web SDK] et PAS d’autres bibliothèques JavaScript d’Adobe.

À ce stade, vous préférerez peut-être demander à l’utilisateur de donner son consentement à un emplacement dans l’interface utilisateur. Une fois les préférences de l’utilisateur collectées, communiquez-les au SDK.

## Communication des préférences de consentement via la norme Adobe Experience Platform

Le SDK prend en charge les versions 1.0 et 2.0 de la norme de consentement Adobe Experience Platform. Actuellement, les normes 1.0 et 2.0 ne prennent en charge que l’application automatique d’une préférence de consentement, totale ou nulle. La norme 1.0 est progressivement abandonnée au profit de la norme 2.0. La version 2.0 vous permet d’ajouter des préférences de consentement supplémentaires qui peuvent être utilisées pour appliquer manuellement les préférences de consentement.

### Utilisation de la version Adobe standard 2.0

Si vous utilisez Adobe Experience Platform, vous devez inclure un groupe de champs de schéma de confidentialité à votre schéma de profil. Voir [Gouvernance, confidentialité et sécurité dans Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) pour plus d’informations sur la version 2.0 standard d’Adobe. Vous pouvez ajouter des données dans l’objet value ci-dessous correspondant au schéma de la variable `consents` du champ [!UICONTROL Consentements et préférences] groupe de champs de profil.

Si l’utilisateur donne son consentement, exécutez la variable `setConsent` avec la préférence Collecter définie sur `y` comme suit :

```javascript
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
    }]
});
```

Le champ d’heure doit indiquer le moment où l’utilisateur a mis à jour pour la dernière fois ses préférences de consentement. Si l’utilisateur choisit de se désinscrire, exécutez la variable `setConsent` avec la préférence Collecter définie sur `n` comme suit :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Utilisation de la version 1.0 standard d’Adobe

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

## Communication des préférences de consentement via la norme IAB TCF

Le SDK prend en charge l’enregistrement des préférences de consentement d’un utilisateur fournies par le biais de la norme IAB (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF). La chaîne de consentement peut être définie via la même `setConsent` comme ci-dessus :

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

Lorsque le consentement est défini de cette manière, Real-time Customer Profile est mis à jour avec les informations de consentement. Pour que cela fonctionne, le schéma XDM du profil doit contenir le [Groupe de champs de schéma Confidentialité du profil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Lors de l’envoi d’événements, les informations de consentement de l’IAB doivent être ajoutées manuellement à l’objet XDM d’événement. Le SDK n’inclut pas automatiquement les informations de consentement dans les événements. Pour envoyer les informations de consentement dans les événements, la variable [Groupe de champs Confidentialité des événements d’expérience](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) doit être ajouté au schéma Experience Event.

## Envoi de plusieurs normes dans une même requête

Le SDK prend également en charge l’envoi de plusieurs objets de consentement dans une requête.

```javascript
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
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistance des préférences de consentement

Après avoir communiqué les préférences de l’utilisateur au SDK à l’aide de la commande `setConsent`, le SDK les conserve dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur, le SDK récupérera et utilisera ces préférences persistantes pour déterminer si des événements peuvent être envoyés à Adobe.

Vous devrez stocker les préférences de l’utilisateur indépendamment pour pouvoir afficher la boîte de dialogue de consentement avec les préférences actuelles. Il n’est pas possible de récupérer les préférences de l’utilisateur à partir du SDK. Pour vous assurer que les préférences de l’utilisateur restent synchronisées avec le SDK, vous pouvez appeler la fonction `setConsent` à chaque chargement de page. Le SDK effectue un appel au serveur uniquement si les préférences ont changé.

## Synchronisation des identités lors de la définition du consentement

Lorsque le consentement par défaut est en attente ou en attente, la variable `setConsent` peut-être la première demande qui établit l’identité. Il peut donc être important de synchroniser les identités lors de la première requête. La carte des identités peut être ajoutée à `setConsent` comme sur la commande `sendEvent` . Voir [Récupération de l’ID d’Experience Cloud](../identity/overview.md)
