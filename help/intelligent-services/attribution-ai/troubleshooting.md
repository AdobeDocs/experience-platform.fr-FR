---
keywords: Experience Platform;prise en main;ia dédiée à l’attribution;rubriques les plus consultées;entrée ia dédiée à l’attribution;sortie ia dédiée à l’attribution;dépannage ia dédiée à l’attribution;erreurs ia dédiée à l’attribution
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Dépannage des erreurs liées à l’IA dédiée à l’attribution
description: Trouvez des réponses aux erreurs courantes liées à l’IA dédiée à l’attribution.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
TQID: https://experienceleague.adobe.com/USuhMP2k6AWQKAh27k4KPSQ99WDws5VLydTy5w1WfKc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: fdddec33-c9cb-4459-b8b6-2664395a6f10
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 98%

---

# Dépannage des erreurs liées à l’IA dédiée à l’attribution

Ce document répond aux questions les plus fréquemment posées sur l’IA dédiée à l’attribution.

## Impossible d’accéder à l’IA dédiée à l’attribution dans Chrome en navigation privée

Les erreurs de chargement en mode navigation privée de Google Chrome sont présentes en raison des mises à jour des paramètres de sécurité du mode navigation privée de Google Chrome. Le problème est en cours de traitement avec Chrome pour faire d’experience.adobe.com un domaine de confiance.

![Image d’erreur](./images/faq/error.PNG){width=500}

### Correctif recommandé

Pour contourner ce problème, vous devez ajouter experience.adobe.com en tant que site pouvant toujours utiliser des cookies. Commencez par accéder à **chrome://settings/cookies**. Faites ensuite défiler l’écran jusqu’à la section **Comportements personnalisés**, puis sélectionnez le bouton **Ajouter** en regard de « Sites autorisés à utiliser des cookies ». Dans la fenêtre contextuelle qui s’affiche, effectuez un copier-coller de `[*.]experience.adobe.com` puis cochez la case **Inclure les cookies tiers de ce site**. Une fois l’opération terminée, sélectionnez **Ajouter** et chargez à nouveau l’IA dédiée à l’attribution en navigation privée.

![Correctif recommandé](./images/faq/cookies2.gif)
