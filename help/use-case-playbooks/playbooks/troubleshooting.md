---
solution: Experience Platform
title: Résolution des problèmes liés aux playbooks
description: Prenez connaissance des problèmes courants liés aux playbooks et apportez une solution
badgeBeta: label="Version Beta" type="Informative"
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 5226a3f9a6da22c2c199f8efffd71360af034dcc
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 100%

---


# (Version Beta) Dépannage et limites connues

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta et nʼest pas disponible pour tous les utilisateurs et utilisatrices. La documentation et les fonctionnalités peuvent changer.

Pour la version Beta de la section [!UICONTROL Cas d’utilisation des playbooks], notez la présence de conseils de dépannage et de limites connues.

## Limites connues {#known-limitations}

Lorsque vous créez une instance d’un playbook, de nouvelles ressources sont générées. Toutefois, pour les schémas générés, si un schéma est généré dans une instance d’un playbook et que vous le modifiez, un autre schéma *ne sera pas* généré si vous activez une autre instance du playbook. Au lieu de cela, vous continuerez à utiliser le schéma que vous avez modifié dans la nouvelle instance.
