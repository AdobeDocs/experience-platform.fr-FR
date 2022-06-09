---
keywords: Experience Platform;accueil;rubriques populaires;
title: Guide de dépannage de Data Prep
topic-legacy: troubleshooting
description: Ce document répond aux questions les plus fréquemment posées sur Adobe Experience Platform Data Prep.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# Guide de dépannage du [!DNL Data Prep]

Ce document répond aux questions les plus fréquemment posées sur Adobe Experience Platform [!DNL Data Prep], ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou information de dépannage concernant les API de Platform en général, reportez-vous à la section [Guide de dépannage des API Adobe Experience Platform](../landing/troubleshooting.md).

## FAQ

Vous trouverez ci-dessous une liste des questions fréquentes sur [!DNL Data Prep] et leurs réponses.

### Comment les erreurs de transformation sont-elles résolues ?

[!DNL Data Prep] localise toutes les erreurs de transformation dans la colonne dans laquelle elles se sont produites. Par conséquent, cette colonne est annulée et le reste de la ligne continuera à être traité. Ces problèmes de transformation sont consignés comme **Avertissements**. Il est recommandé de consulter régulièrement les avertissements et d’ajuster la logique de transformation pour tenir compte des problèmes de transformation. Cela augmentera la qualité des données ingérées dans Experience Platform.

Si les colonnes marquées comme **Obligatoire** sont nullifiés en raison de problèmes de transformation, la ligne ne sera pas ingérée. Lorsque l’ingestion de données partielle est activée, vous pouvez définir le seuil de ces rejets avant que le flux entier ne s’arrête. Si l’attribut nullified n’a eu aucune incidence sur les validations au niveau du schéma, la ligne continuera à être ingérée.

Toutes les lignes non valides, même sans erreur de transformation, seront également rejetées. Par exemple, un flux d’ingestion de données peut avoir un mappage de transfert (sans logique de transformation) vers un champ obligatoire et il n’y a pas de valeur entrante pour cet attribut. Cette ligne sera rejetée.