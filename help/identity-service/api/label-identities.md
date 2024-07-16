---
keywords: Experience Platform;accueil;rubriques populaires;identités des étiquettes
solution: Experience Platform
title: Étiquetage d’un champ comme identité
description: Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Le service d’identités interprète comme identité les valeurs fournies dans un champ d’identité. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 73%

---

# Étiquetage d’un champ comme identité

Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Une valeur fournie dans un champ d’identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.

Pour étiqueter un champ en tant qu’identité, vous devrez respecter les critères suivants :

- Vous ne pouvez utiliser que les champs de type chaîne en tant qu’identité.
- Les identités ne sont reconnues que dans les données d’enregistrement et de séries temporelles.
- Seuls les champs PII doivent être marqués comme identité. Choisir un champ représentant des données plus génériques entraînerait des relations moins précises et des erreurs potentielles pour accéder aux identités associées du graphique d’identités.

Pour plus d’informations sur l’utilisation de l’API Schema Registry pour étiqueter un champ en tant qu’identité, consultez le [guide de point de terminaison des descripteurs](../../xdm/api/descriptors.md#create).

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier les identités d’un cluster](./list-cluster-identites.md)
