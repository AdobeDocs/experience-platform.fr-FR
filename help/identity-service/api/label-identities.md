---
keywords: Experience Platform;accueil;rubriques populaires;identités de libellés
solution: Experience Platform
title: Étiqueter un champ en tant qu’identité
description: Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Le service d’identités interprète comme identité les valeurs fournies dans un champ d’identité. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
TQID: https://experienceleague.adobe.com/j8K5cX4bRdHe9Aip7UwBsh2UXRMfYE8OeB5qXVol7ms
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 196
ht-degree: 73%

---

# Étiqueter un champ comme identité

Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Une valeur fournie dans un champ d’identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.

Pour étiqueter un champ en tant qu’identité, vous devrez respecter les critères suivants :

- Vous ne pouvez utiliser que les champs de type chaîne en tant qu’identité.
- Les identités ne sont reconnues que dans les données d’enregistrement et de séries temporelles.
- Seuls les champs PII doivent être marqués comme identité. Choisir un champ représentant des données plus génériques entraînerait des relations moins précises et des erreurs potentielles pour accéder aux identités associées du graphique d’identités.

Pour savoir comment utiliser l’API Schema Registry pour étiqueter un champ en tant qu’identité, consultez le [guide de point d’entrée des descripteurs](../../xdm/api/descriptors.md#create).

## Étapes suivantes

Passez au tutoriel suivant pour [répertorier les identités d’un cluster](./list-cluster-identites.md)
