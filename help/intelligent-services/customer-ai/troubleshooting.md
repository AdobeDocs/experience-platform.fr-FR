---
keywords: Experience Platform;prise en main;service clientèle;rubriques les plus consultées;entrée de l’assistance client;sortie de l’assistance client;dépannage des problèmes client;erreurs de l’assistance client
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Dépannage des erreurs de Customer AI
topic-legacy: Getting started
description: Trouvez des réponses aux erreurs courantes de Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Dépannage des erreurs de Customer AI

Customer AI affiche des erreurs lorsque la formation, la notation et la configuration des modèles échouent. Dans le **[!UICONTROL Instances de service]** , une colonne pour **[!UICONTROL DERNIÈRE EXÉCUTION]** affiche l’un des messages suivants : **[!UICONTROL Succès]**, **[!UICONTROL Problème de formation]**, et **[!UICONTROL En échec]**.

![état de la dernière exécution](./images/errors/last-run-status.png)

Dans le cas où **[!UICONTROL En échec]** ou **[!UICONTROL Problème de formation]** s’affiche, vous pouvez sélectionner l’état d’exécution pour ouvrir un panneau latéral. Le panneau latéral contient votre **[!UICONTROL État de la dernière exécution]** et **[!UICONTROL Détails de la dernière exécution]**. **[!UICONTROL Détails de la dernière exécution]** contient des informations sur les raisons de l’échec de l’exécution. Dans le cas où Customer AI ne peut pas fournir de détails sur votre erreur, contactez l’assistance avec le code d’erreur fourni.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Impossible d’accéder à Customer AI dans Chrome incognito

Les erreurs de chargement en mode incognito de Google Chrome sont présentes en raison des mises à jour apportées aux paramètres de sécurité du mode incognito de Google. Le problème est en cours de traitement avec Chrome pour faire d’experience.adobe.com un domaine de confiance.

<img src="./images/errors/error.PNG" width="500" /><br />

### Correctif recommandé

Pour résoudre ce problème, vous devez ajouter experience.adobe.com en tant que site pouvant toujours utiliser des cookies. Commencez par accéder à **chrome://settings/cookies**. Faites ensuite défiler l’écran jusqu’à la **Comportements personnalisés** , puis sélectionnez **Ajouter** en regard de &quot;sites pouvant toujours utiliser des cookies&quot;. Dans la fenêtre contextuelle qui s’affiche, effectuez un copier-coller `[*.]experience.adobe.com` sélectionnez ensuite le **Inclusion de cookies tiers** sur ce site. Une fois l’opération terminée, sélectionnez **Ajouter** et rechargez Customer AI dans incognito.

![correctif recommandé](./images/errors/cookies2.gif)

## La qualité du modèle est médiocre

Si vous recevez l’erreur &quot;[!UICONTROL La qualité du modèle est médiocre. Nous vous recommandons de créer une application avec la configuration modifiée.]&quot;. Suivez les étapes recommandées ci-dessous pour résoudre les problèmes.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correctif recommandé

&quot;La qualité du modèle est médiocre&quot; signifie que la précision du modèle n’est pas comprise dans une plage acceptable. Customer AI n’a pas pu créer de modèle fiable et AUC (zone sous la courbe de ROC) &lt; 0,65 après la formation. Pour corriger l’erreur, il est recommandé de modifier l’un des paramètres de configuration et de relancer l’entraînement.

Commencez par vérifier l’exactitude de vos données. Il est important que vos données contiennent les champs nécessaires à votre résultat prédictif.

- Vérifiez si votre jeu de données comporte les dates les plus récentes. Customer AI suppose toujours que les données sont à jour lorsque le modèle est déclenché.
- Recherchez les données manquantes dans la fenêtre de prédiction et d’éligibilité que vous avez définie. Vos données doivent être complètes sans intervalle. Assurez-vous également que votre jeu de données respecte la variable [Exigences en matière de données historiques Customer AI](./input-output.md#data-requirements).
- Recherchez les données manquantes dans les propriétés de champ de schéma dans le commerce, l’application, le web et la recherche.

Si vos données ne semblent pas poser problème, essayez de modifier la condition d&#39;éligibilité de la population pour restreindre le modèle à certains profils (par exemple, `_experience.analytics.customDimensions.eVars.eVar142` existe dans les 56 derniers jours). Cela limite la population et la taille des données utilisées dans la fenêtre d&#39;apprentissage.

Si la limitation de la population éligible n’a pas fonctionné ou n’est pas possible, modifiez votre fenêtre de prédiction.

- Essayez de passer votre fenêtre de prédiction à 7 jours et vérifiez si l’erreur se produit toujours. Si l’erreur ne se produit plus, cela indique que vous ne disposez peut-être pas de suffisamment de données pour la fenêtre de prédiction définie.
