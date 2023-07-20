---
keywords: Experience Platform;prise en main;ia dédiée aux clients;rubriques populaires;entrée ia dédiée aux clients;sortie ia dédiée aux clients;dépannage ia dédiée aux clients;erreurs ia dédiée aux clients
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Dépannage des erreurs de l’IA dédiée aux clients
description: Trouvez des réponses aux erreurs courantes de l’IA dédiée aux clients.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 100%

---

# Dépannage des erreurs de l’IA dédiée aux clients

L’IA dédiée aux clients affiche des erreurs lorsque l’entraînement, la notation et la configuration des modèles échouent. Dans la section **[!UICONTROL Instances de service]**, une colonne pour le **[!UICONTROL STATUT DE LA DERNIÈRE EXÉCUTION]** affiche l’un des messages suivants : **[!UICONTROL Succès]**, **[!UICONTROL Problème de formation]**, et **[!UICONTROL Échec]**.

![statut de la dernière exécution](./images/errors/last-run-status.png)

Dans le cas où **[!UICONTROL Échec]** ou **[!UICONTROL Problème d’entraînement]** s’affiche, vous pouvez sélectionner le statut d’exécution pour ouvrir un panneau latéral. Le panneau latéral contient le **[!UICONTROL statut de votre dernière exécution]** et les **[!UICONTROL détails de la dernière exécution]**. Les **[!UICONTROL détails de la dernière exécution]** contiennent des informations sur les raisons de l’échec de l’exécution. Dans le cas où l’IA dédiée aux clients ne peut pas fournir de détails sur votre erreur, contactez l’assistance avec le code d’erreur fourni.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Impossible d’accéder à l’IA dédiée aux clients dans Chrome en navigation privée

Les erreurs de chargement en mode navigation privée de Google Chrome sont présentes en raison des mises à jour des paramètres de sécurité du mode navigation privée de Google Chrome. Le problème est en cours de traitement avec Chrome pour faire d’experience.adobe.com un domaine de confiance.

<img src="./images/errors/error.PNG" width="500" /><br />

### Correctif recommandé

Pour contourner ce problème, vous devez ajouter experience.adobe.com en tant que site pouvant toujours utiliser des cookies. Commencez par accéder à **chrome://settings/cookies**. Faites ensuite défiler l’écran jusqu’à la section **Comportements personnalisés**, puis sélectionnez le bouton **Ajouter** en regard de « Sites autorisés à utiliser des cookies ». Dans la fenêtre contextuelle qui s’affiche, effectuez un copier-coller de `[*.]experience.adobe.com` puis cochez la case **Inclure les cookies tiers de ce site**. Une fois l’opération terminée, sélectionnez **Ajouter** et chargez à nouveau l’IA dédiée aux clients en navigation privée.

![correctif recommandé](./images/errors/cookies2.gif)

## La qualité du modèle est médiocre.

Si vous recevez l’erreur « [!UICONTROL La qualité du modèle est médiocre. Nous vous recommandons de créer une application avec la configuration modifiée.] ». Suivez les étapes recommandées ci-dessous pour résoudre les problèmes.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correctif recommandé

« La qualité du modèle est médiocre » signifie que la précision du modèle n’est pas comprise dans une plage acceptable. L’IA dédiée aux clients n’a pas pu créer de modèle fiable et l’AUC (aire sous la courbe ROC) est inférieure à 0,65 après l’entraînement. Pour corriger l’erreur, il est recommandé de modifier l’un des paramètres de configuration et de relancer l’entraînement.

Commencez par vérifier l’exactitude de vos données. Il est important que vos données contiennent les champs nécessaires à votre résultat prédictif.

- Vérifiez si votre jeu de données comporte les dates les plus récentes. L’IA dédiée aux clients suppose toujours que les données sont à jour lorsque le modèle est déclenché.
- Recherchez les données manquantes dans la fenêtre de prédiction et d’éligibilité que vous avez définie. Vos données doivent être complètes sans oubli. Assurez-vous également que votre jeu de données respecte les [exigences en matière de données historiques de l’IA dédiée aux clients](./data-requirements.md#data-requirements).
- Recherchez les données manquantes dans les propriétés de champ de schéma dans le commerce, l’application, le web et la recherche.

Si vos données ne semblent pas poser problème, essayez de modifier la condition de la population d’éligibilité pour restreindre le modèle à certains profils (par exemple, `_experience.analytics.customDimensions.eVars.eVar142` existe dans les 56 derniers jours). Cela limite la population et la taille des données utilisées dans la fenêtre d’entraînement.

Si limiter la population d’éligibilité n’a pas fonctionné ou si cela n’est pas possible, modifiez votre fenêtre de prédiction.

- Essayez de passer votre fenêtre de prédiction à 7 jours et vérifiez si l’erreur se produit toujours. Si l’erreur ne se produit plus, cela indique que vous ne disposez peut-être pas de suffisamment de données pour la fenêtre de prédiction que vous avez définie.
