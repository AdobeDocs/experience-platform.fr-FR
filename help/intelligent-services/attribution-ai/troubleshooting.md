---
keywords: Experience Platform;prise en main;accès d’attribution;rubriques populaires;entrée d’attribution;sortie d’attribution ai;résolution des problèmes d’attribution;erreurs d’attribution ai
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Dépannage des erreurs Attribution AI
description: Trouvez des réponses aux erreurs courantes dans Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 61%

---

# Dépannage des erreurs Attribution AI

Ce document répond aux questions les plus fréquemment posées sur Attribution AI.

## Impossible d’accéder à Attribution AI dans Chrome incognito

Les erreurs de chargement en mode navigation privée de Google Chrome sont présentes en raison des mises à jour des paramètres de sécurité du mode navigation privée de Google Chrome. Le problème est en cours de traitement avec Chrome pour faire d’experience.adobe.com un domaine de confiance.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correctif recommandé

Pour contourner ce problème, vous devez ajouter experience.adobe.com en tant que site pouvant toujours utiliser des cookies. Commencez par accéder à **chrome://settings/cookies**. Faites ensuite défiler l’écran jusqu’à la section **Comportements personnalisés**, puis sélectionnez le bouton **Ajouter** en regard de « Sites autorisés à utiliser des cookies ». Dans la fenêtre contextuelle qui s’affiche, effectuez un copier-coller de `[*.]experience.adobe.com` puis cochez la case **Inclure les cookies tiers de ce site**. Une fois l’opération terminée, sélectionnez **Ajouter** et rechargez Attribution AI dans incognito.

![correctif recommandé](./images/faq/cookies2.gif)
