---
keywords: Experience Platform;prise en main;service clientèle;rubriques les plus consultées;entrée de l’assistance client;sortie de l’assistance client;dépannage des problèmes client;erreurs de l’assistance client
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Dépannage des erreurs de Customer AI
topic-legacy: Getting started
description: Trouvez des réponses aux erreurs courantes de Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Dépannage des erreurs de Customer AI

Customer AI affiche des erreurs lorsque la formation, la notation et la configuration des modèles échouent. Dans la section **[!UICONTROL Instances de service]** , une colonne pour **[!UICONTROL DERNIER ÉTAT D’EXÉCUTION]** affiche l’un des messages suivants : **[!UICONTROL Succès]**, **[!UICONTROL Problème d’entraînement]** et **[!UICONTROL Échec]**.

![état de la dernière exécution](./images/errors/last-run-status.png)

Dans le cas où **[!UICONTROL Échec]** ou **[!UICONTROL Problème d’entraînement]** s’affiche, vous pouvez sélectionner l’état d’exécution pour ouvrir un panneau latéral. Le panneau latéral contient vos **[!UICONTROL états Dernière exécution]** et **[!UICONTROL détails de la dernière exécution]**. **[!UICONTROL Les]** détails de la dernière exécution contiennent des informations sur les raisons de l’échec de l’exécution. Dans le cas où Customer AI ne peut pas fournir de détails sur votre erreur, contactez l’assistance avec le code d’erreur fourni.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## La qualité du modèle est médiocre

Si vous recevez l’erreur &quot;[!UICONTROL La qualité du modèle est médiocre. Nous vous recommandons de créer une application avec la configuration modifiée ]&quot;. Suivez les étapes recommandées ci-dessous pour résoudre les problèmes.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correctif recommandé

&quot;La qualité du modèle est médiocre&quot; signifie que la précision du modèle n’est pas comprise dans une plage acceptable. Customer AI n’a pas pu créer de modèle fiable et AUC (zone sous la courbe de ROC) &lt; 0,65 après la formation. Pour corriger l’erreur, il est recommandé de modifier l’un des paramètres de configuration et de relancer l’entraînement.

Commencez par vérifier l’exactitude de vos données. Il est important que vos données contiennent les champs nécessaires à votre résultat prédictif.

- Vérifiez si votre jeu de données comporte les dates les plus récentes. Customer AI suppose toujours que les données sont à jour lorsque le modèle est déclenché.
- Recherchez les données manquantes dans la fenêtre de prédiction et d’éligibilité que vous avez définie. Vos données doivent être complètes sans intervalle. Assurez-vous également que votre jeu de données respecte les [exigences de données historiques de Customer AI](./input-output.md#data-requirements).
- Recherchez les données manquantes dans les propriétés de champ de schéma dans le commerce, l’application, le web et la recherche.

Si vos données ne semblent pas poser problème, essayez de modifier la condition de population éligible pour limiter le modèle à certains profils (par exemple, il existe `_experience.analytics.customDimensions.eVars.eVar142` dans les 56 derniers jours). Cela limite la population et la taille des données utilisées dans la fenêtre d&#39;apprentissage.

Si la limitation de la population éligible n’a pas fonctionné ou n’est pas possible, modifiez votre fenêtre de prédiction.

- Essayez de passer votre fenêtre de prédiction à 7 jours et vérifiez si l’erreur se produit toujours. Si l’erreur ne se produit plus, cela indique que vous ne disposez peut-être pas de suffisamment de données pour la fenêtre de prédiction définie.
