---
keywords: Experience Platform ; prise en main ; assistance client ; rubriques populaires ; entrée d’assistance client ; sortie d’assistance client ; dépannage client ; erreurs d’assistance client
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Dépannage des erreurs d’IA client
topic-legacy: Getting started
description: Trouvez des réponses aux erreurs courantes dans l’IA du client.
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Dépannage des erreurs d’IA client

L’IA du client affiche des erreurs en cas d’échec de la formation, du score et de la configuration du modèle. Dans la section **[!UICONTROL Instances de service]**, une colonne pour **[!UICONTROL DERNIER ÉTAT D’EXÉCUTION]** affiche l’un des messages suivants : **[!UICONTROL Succès]**, **[!UICONTROL Problème de formation]** et **[!UICONTROL Échec]**.

![état de la dernière exécution](./images/errors/last-run-status.png)

Dans le événement où **[!UICONTROL Échec]** ou **[!UICONTROL Problème de formation]** s’affiche, vous pouvez sélectionner l’état d’exécution pour ouvrir un panneau latéral. Le panneau latéral contient vos **[!UICONTROL Dernière exécution]** et **[!UICONTROL Détails de la dernière exécution]**. **[!UICONTROL Les]** détails de la dernière exécution contiennent des informations sur les raisons de l’échec de l’exécution. Dans le événement où l’API du client n’est pas en mesure de fournir des détails sur votre erreur, contactez l’assistance technique avec le code d’erreur fourni.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## La qualité du modèle est médiocre

Si vous recevez l&#39;erreur &quot;[!UICONTROL La qualité du modèle est médiocre. Nous vous recommandons de créer une nouvelle application avec la configuration modifiée ]&quot;. Suivez les étapes recommandées ci-dessous pour résoudre les problèmes.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correctif recommandé

&quot;La qualité du modèle est médiocre&quot; signifie que la précision du modèle n&#39;est pas comprise dans une plage acceptable. L&#39;IA du client n&#39;a pas pu construire un modèle fiable et l&#39;AUC (zone sous la courbe de ROC) &lt; 0,65 après la formation. Pour corriger l’erreur, il est recommandé de modifier l’un des paramètres de configuration et de réexécuter la formation.

Début en vérifiant l&#39;exactitude de vos données. Il est important que vos données contiennent les champs nécessaires à votre résultat prévisionnel.

- Vérifiez si votre jeu de données contient les dernières dates. L’IA du client suppose toujours que les données sont à jour lorsque le modèle est déclenché.
- Recherchez les données manquantes dans la fenêtre de prédiction et d&#39;éligibilité définie. Vos données doivent être complètes sans espaces. Assurez-vous également que votre jeu de données respecte les [exigences de données historiques d’IA client](./input-output.md#data-requirements).
- Recherchez les données manquantes dans le commerce, l’application, le Web et la recherche, dans les propriétés de vos champs de schéma.

Si vos données ne semblent pas poser problème, essayez de modifier la condition de population d’éligibilité afin de limiter le modèle à certains profils (par exemple, `_experience.analytics.customDimensions.eVars.eVar142` existe au cours des 56 derniers jours). Cela limite la population et la taille des données utilisées dans la fenêtre de formation.

Si la restriction de la population admissible n&#39;a pas fonctionné ou n&#39;est pas possible, changez votre fenêtre de prédiction.

- Essayez de passer à 7 jours la fenêtre de prédiction et voyez si l&#39;erreur continue. Si l’erreur ne se produit plus, cela indique que vous ne disposez peut-être pas de suffisamment de données pour la fenêtre de prédiction définie.

