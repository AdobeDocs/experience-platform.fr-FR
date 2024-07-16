---
title: Guide de dépannage de Adobe Experience Platform Assurance
description: Ce document décrit les solutions aux problèmes courants lors de l’utilisation de Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Résolution des problèmes de Adobe Experience Platform Assurance

Si vous rencontrez des difficultés à obtenir le bon fonctionnement d’Assurance, reportez-vous à des suggestions sous les rubriques de problème suivantes pour résoudre les problèmes courants.

Pour permettre une mise en oeuvre plus fluide et découvrir les problèmes potentiels, assurez-vous que la journalisation du SDK est activée par [Activer la journalisation de débogage](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) dans la section Prise en main.

Vous pouvez modifier les niveaux de journal du SDK à l’aide de l’API [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel).

## Problèmes liés à l’application sur l’appareil

### Le code QR n’ouvre pas l’application

* Accédez directement au lien. Copiez le lien de **Détails de la session**. Collez-le dans la barre d’adresse du navigateur de l’appareil pour l’ouvrir. S’il ne s’ouvre pas, reportez-vous à la section [L’application n’ouvrira pas le lien](#app-does-not-open-link).
* Utilisez un autre lecteur de QR. Pour iOS 11 ou version ultérieure, utilisez l’application photo pour lire le code QR.

### L’application n’ouvre pas le lien

* Vérifiez que la mise en oeuvre du lien profond est correctement configurée dans l’application.
   * **Android :** liens profonds (liens d’application)
      * [Création de liens profonds vers le contexte de l’application](https://developer.android.com/training/app-links/deep-linking)
   * **iOS :** schéma d’URL personnalisée ou liens universels
      * [Définition d’un schéma d’URL personnalisé pour votre application](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Prise en charge des liens universels dans votre application](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Pour Android, l’API `startSession` n’a pas besoin d’être appelée explicitement. Pour iOS, utilisez l’API comme décrit dans [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### La superposition d’authentification s’affiche, mais l’application ne parvient pas à se connecter.

* Assurez la connectivité Internet de l’appareil par le biais du navigateur Web de l’appareil.
* Si l’application n’a jamais réussi à se connecter au service Assurance, assurez-vous qu’elle est correctement configurée pour Assurance. Voir les instructions d’installation de la bibliothèque SDK [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md).
* Vérifiez que la session correspond au lien et qu’elle est saisie correctement pour la session attendue. Voir [Message du journal &quot;Les informations OrgID ne sont pas disponibles&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (ce qui est rare et pertinent uniquement si vous avez accès à plusieurs instances ORG).

### Débogage Adobe Analytics

**État de traitement Post - Aucun indicateur de débogage**

Dans la vue Événements Analytics, si les événements échouent avec l’état &quot;Aucun indicateur de débogage&quot; traité par Post, votre version actuelle du SDK Adobe Analytics ou Assurance peut ne pas prendre en charge la fonction de débogage Analytics.
Mettez à niveau les extensions du SDK Adobe Analytics et Assurance vers les versions les plus récentes pour résoudre ce problème.

| Exigences de version minimale | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Compatibilité de React Native MobileCore et AEPAs

| Version d’assurance AEP | Version principale mobile | Instruction d’installation |
| --------------------- | ------------------- | ------------------- |
| response-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Si vous utilisez `react-native-acpcore` avec Assurance, la compilation de l’application React Native peut échouer avec l’un des messages d’erreur suivants :

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

ou

```
AppDelegate: AEPAssurance.h file not found
```

**Solution**

Si cela se produit, veuillez rétrograder votre `react-native-aepassurance` à l’aide de la commande npm suivante :

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Cette erreur se produit car l’extension `react-native-acpcore` est **uniquement** compatible avec `react-native-aepassurance` versions 2.x.x et antérieures.
