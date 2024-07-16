---
keywords: Experience Platform;accueil;rubriques populaires;
title: Guide de dépannage de la préparation des données
description: Ce document fournit des réponses aux questions fréquentes sur la préparation des données Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 100%

---

# Guide de dépannage de [!DNL Data Prep]

Ce document fournit des réponses aux questions fréquentes sur la [!DNL Data Prep] Adobe Experience Platform ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou pour obtenir des informations de dépannage concernant les API de Platform en général, reportez-vous au [guide de dépannage des API d’Adobe Experience Platform](../landing/troubleshooting.md).

## FAQ

Vous trouverez ci-dessous une liste des questions fréquentes sur [!DNL Data Prep] et leurs réponses.

### Comment les erreurs de transformation sont-elles résolues ?

[!DNL Data Prep] localise toutes les erreurs de transformation dans la colonne dans laquelle elles se sont produites. Par conséquent, cette colonne devient nulle et le reste de la ligne continue à être traité. Ces problèmes de transformation sont consignés comme **Avertissements**. Il est recommandé de consulter régulièrement les avertissements et d’ajuster la logique de transformation pour tenir compte des problèmes de transformation. Cela augmentera la qualité des données ingérées dans Experience Platform.

Si les colonnes marquées comme **Obligatoires** deviennent nulles en raison de problèmes de transformation, la ligne ne sera pas ingérée. Lorsque l’ingestion de données partielle est activée, vous pouvez définir le seuil de ces rejets avant que le flux entier échoue. Si l’attribut devenu nul n’a eu aucune incidence sur les validations au niveau du schéma, la ligne continuera à être ingérée.

Toutes les lignes non valides, même sans erreur de transformation, seront également rejetées. Par exemple, un flux d’ingestion de données peut avoir un mappage passthrough (sans logique de transformation) vers un champ obligatoire et il n’y a pas de valeur entrante pour cet attribut. Cette ligne sera rejetée.

### Comment échapper des caractères spéciaux dans un champ ?

Vous pouvez échapper les caractères spéciaux d’un champ à l’aide de `${...}`. Toutefois, les fichiers JSON qui contiennent des champs avec un point (`.`) ne sont pas pris en charge par ce mécanisme. Lors de l’interaction avec des hiérarchies, si un attribut enfant comporte un point (`.`), vous devez utiliser une barre oblique inverse (`\`) pour échapper les caractères spéciaux. Par exemple, `address` est un objet qui contient l’attribut `street.name`. Il peut donc être appelé `address.street\.name` au lieu de `address.street.name`.

### Quelle est la longueur maximale des champs calculés ?

La longueur maximale des champs calculés est de 4 096 caractères.