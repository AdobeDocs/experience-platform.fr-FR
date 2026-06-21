---
keywords: Experience Platform;accueil;rubriques populaires;identités de libellés
title: Étiqueter un champ comme identité dans l’interface utilisateur
description: Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Le service d’identités interprète comme identité les valeurs fournies dans un champ d’identité. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.
hide: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
TQID: https://experienceleague.adobe.com/xtQvYLF9RdLjBfY56bQj5UHdAzn9Kb-pCe0fvXIufmc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 70%

---

# Étiqueter un champ comme identité dans l’interface utilisateur

Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Une valeur fournie dans un champ d’identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.

Pour étiqueter un champ en tant qu’identité, vous devrez respecter les critères suivants :

* Vous ne pouvez utiliser que les champs de type chaîne en tant qu’identité.
* Les identités ne sont reconnues que dans les données d’enregistrement et de séries temporelles.
* Seuls les champs PII doivent être marqués comme identité. Choisir un champ représentant des données plus génériques entraînerait des relations moins précises et des erreurs potentielles pour accéder aux identités associées du graphique d’identités.

Pour obtenir des instructions sur la manière d’étiqueter les champs d’identité dans l’interface utilisateur, consultez le guide sur la [définition de champs d’identité dans l’interface utilisateur](../xdm/ui/fields/identity.md).

## Étapes suivantes

Pour plus d’informations sur [!DNL Identity Service], consultez la présentation [[!DNL Identity Service] ](./home.md).
