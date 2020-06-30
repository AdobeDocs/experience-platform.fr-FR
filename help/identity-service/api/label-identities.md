---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Attribuer une étiquette à un champ en tant qu’identité
topic: api guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---


# Attribuer une étiquette à un champ en tant qu’identité

Les champs qui contiennent des informations d’identification personnelle peuvent être étiquetés comme champs d’identité. Une valeur fournie dans un champ d&#39;identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de nommage de l’identité est spécifié dans le cadre de l’étiquetage du champ.

Les critères suivants doivent être respectés pour qu’un champ soit étiqueté comme identité :

- Seuls les champs de type chaîne peuvent être utilisés pour l&#39;identité
- Les identités ne sont reconnues que dans les données d&#39;enregistrement et de série chronologique.
- Seuls les champs d’identification personnelle doivent être marqués comme identité. Le choix d’un champ représentant des données plus génériques se traduirait par des relations moins précises et des erreurs potentielles d’accès aux identités liées à partir du graphique d’identité.

Pour obtenir des instructions sur l&#39;utilisation de l&#39;API Schéma Registry pour étiqueter un champ comme identité, consultez la page [Création d&#39;un descripteur](../../xdm/api/descriptors.md).

## Étapes suivantes

Accédez au didacticiel suivant pour [liste des identités de grappe](./list-cluster-identites.md)