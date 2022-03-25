---
keywords: Experience Platform;prise en main;accès d’attribution;rubriques populaires;entrée d’attribution;sortie d’attribution ai;résolution des problèmes d’attribution;erreurs d’attribution ai
solution: Intelligent Services, Real-time Customer Data Platform
feature: Attribution AI
title: Dépannage des erreurs Attribution AI
description: Trouvez des réponses aux erreurs courantes dans Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Dépannage des erreurs Attribution AI

Ce document répond aux questions les plus fréquemment posées sur Attribution AI.

## Impossible d’accéder à Attribution AI dans Chrome incognito

Les erreurs de chargement en mode incognito de Google Chrome sont présentes en raison des mises à jour apportées aux paramètres de sécurité du mode incognito de Google. Le problème est en cours de traitement avec Chrome pour faire d’experience.adobe.com un domaine de confiance.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correctif recommandé

Pour résoudre ce problème, vous devez ajouter experience.adobe.com en tant que site pouvant toujours utiliser des cookies. Commencez par accéder à **chrome://settings/cookies**. Faites ensuite défiler l’écran jusqu’à la **Comportements personnalisés** , puis sélectionnez **Ajouter** en regard de &quot;sites pouvant toujours utiliser des cookies&quot;. Dans la fenêtre contextuelle qui s’affiche, effectuez un copier-coller `[*.]experience.adobe.com` sélectionnez ensuite le **Inclusion de cookies tiers** sur ce site. Une fois l’opération terminée, sélectionnez **Ajouter** et rechargez Attribution AI dans incognito.

![correctif recommandé](./images/faq/cookies2.gif)
