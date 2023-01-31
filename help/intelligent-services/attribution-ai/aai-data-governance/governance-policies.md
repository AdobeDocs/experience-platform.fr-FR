---
keywords: Experience Platform;guide de l’utilisateur;accès à l’attribution;rubriques populaires;contrôles d’accès;créer un modèle ;
feature: Attribution AI
title: Stratégies de gouvernance pour Attribution AI
description: Adobe Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance les données d’expérience collectées.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# Politiques de gouvernance

Une fois que vous avez parcouru le workflow pour créer un modèle et envoyer la configuration du modèle, la variable [application des stratégies](../../../data-governance/enforcement/auto-enforcement.md) vérifie s’il existe des violations. Si une violation de stratégie se produit, une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs stratégies ont été violées. Cela permet de vous assurer que vos opérations de données et vos actions marketing dans Platform sont conformes aux politiques d’utilisation des données.

## Fenêtre contextuelle de violation de politique

[Une fenêtre contextuelle affichant des informations sur la violation de politique](../../attribution-ai/images/data-governance/policy-violation-popover-aai.png).

La fenêtre contextuelle fournit des informations spécifiques sur la violation. Vous pouvez résoudre ces violations par le biais de paramètres de stratégie et d’autres mesures qui ne sont pas directement liés au workflow de configuration. Par exemple, vous pouvez modifier les étiquettes afin que certains champs soient autorisés à être utilisés à des fins de science des données. Vous pouvez également modifier la configuration de modèle elle-même afin qu’elle n’utilise rien avec un libellé. Consultez la documentation pour en savoir plus sur la configuration des stratégies.