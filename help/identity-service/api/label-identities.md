---
keywords: Experience Platform ; accueil ; rubriques populaires ; identités des étiquettes
solution: Experience Platform
title: Étiquetage d’un champ comme identité
topic: api guide
description: Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Identity Service interprète comme identité les valeurs fournies dans un champ d’identité. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 89%

---


# Étiquetage d’un champ comme identité

Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Une valeur fournie dans un champ d&#39;identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.

Pour étiqueter un champ en tant qu’identité, vous devrez respecter les critères suivants :

- Vous ne pouvez utiliser que les champs de type chaîne en tant qu’identité.
- Les identités ne sont reconnues que dans les données d’enregistrement et de séries temporelles.
- Seuls les champs PII doivent être marqués comme identité. Choisir un champ représentant des données plus génériques entraînerait des relations moins précises et des erreurs potentielles pour accéder aux identités associées du graphique d’identités.

Pour obtenir des instructions sur la manière dont utiliser l’API Schema Registry pour étiqueter un champ en tant qu’identité, consultez la section [Création d’un descripteur](../../xdm/api/descriptors.md).

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier les identités d’un cluster](./list-cluster-identites.md)