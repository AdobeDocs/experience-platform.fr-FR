---
title: Guide de dépannage d’Adobe Experience Platform Assurance
description: Ce document présente les solutions aux problèmes courants rencontrés lors de l’utilisation d’Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
TQID: https://experienceleague.adobe.com/aePE9uZ-W7DVgPw-g-Wg7oLpOoDhaQEYcIX0RKgxXak
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 538
ht-degree: 5%

---

# Résolution des problèmes d’Adobe Experience Platform Assurance

Si vous rencontrez des problèmes pour faire fonctionner Assurance, consultez les suggestions dans les rubriques de problèmes suivantes pour résoudre les problèmes courants.

Pour faciliter l’implémentation et détecter tout problème potentiel, assurez-vous que la journalisation de SDK est activée conformément à l’option [Activer la journalisation du débogage](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) de la section Prise en main .

Vous pouvez modifier les niveaux de journal SDK à l’aide de l’API [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel).

## Problèmes sur l’appareil et l’application

### Le code QR n’ouvre pas l’application

* Accédez directement au lien . Copiez le lien de **Détails de la session**. Collez-le dans la barre d’adresse du navigateur de l’appareil pour l’ouvrir. S’il ne s’ouvre pas, consultez la section [L’application n’ouvre pas le lien](#app-does-not-open-link).
* Utilisez un autre lecteur de QR. Pour iOS 11 ou version ultérieure, utilisez l’application Photo pour lire le code QR.

### L’application n’ouvre pas le lien

* Vérifiez que l’implémentation du lien profond est correctement configurée dans l’application.
   * **Android:** Liens Profonds (Liens D’Application)
      * [Créer des liens profonds vers App Context](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** schéma d&#39;URL personnalisé ou liens universels
      * [Définition d’un schéma d’URL personnalisé pour votre application](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Prise en charge des liens universels dans votre application](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Pour Android, il n’est pas nécessaire d’appeler explicitement l’API `startSession`. Pour iOS, utilisez l’API comme décrit dans [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### La superposition d’authentification apparaît, mais l’application ne parvient pas à se connecter

* Assurez la connectivité Internet de l’appareil via le navigateur web de l’appareil.
* Si l’application ne s’est jamais connectée correctement au service Assurance, assurez-vous qu’elle est correctement configurée pour Assurance. Voir les instructions d’installation de la bibliothèque SDK [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md).
* Vérifiez que la session correspond au lien et qu’elle est saisie correctement pour la session prévue. Voir [ Message du journal « Les informations d’ID d’organisation ne sont pas disponibles »](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (cela est rare et pertinent uniquement si vous avez accès à plusieurs instances d’organisation).

### Débogage d’Adobe Analytics

**Statut de post-traitement - Aucun indicateur de débogage**

Dans votre vue d’événements Analytics, si les événements échouent avec le statut post-traité « Aucun indicateur de débogage », votre version actuelle d’Adobe Analytics ou d’Assurance SDK peut ne pas prendre en charge la fonctionnalité de débogage Analytics.
Veuillez mettre à niveau les extensions Adobe Analytics et Assurance SDK vers les versions les plus récentes pour résoudre ce problème.

| Exigences de version minimale | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Compatibilité de React Native MobileCore et AEPAsassurance

| Version AEP Assurance | Version principale mobile | Instructions d’installation |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Si vous utilisez `react-native-acpcore` avec Assurance, la création de l’application React Native peut échouer avec l’un des messages d’erreur suivants :

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

or

```
AppDelegate: AEPAssurance.h file not found
```

**Solution**

Si cela se produit, rétrogradez votre `react-native-aepassurance` à l’aide de la commande npm suivante :

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Cette erreur se produit, car l’extension `react-native-acpcore` est **uniquement** compatible avec les versions 2.x.x et `react-native-aepassurance` ultérieures.
