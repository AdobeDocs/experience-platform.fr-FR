---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Attribuer une étiquette à un champ en tant qu’identité
topic: api guide
translation-type: tm+mt
source-git-commit: 40ce232e39f62f1ee478ef05229dd2fc125ee4c0

---


# Attribuer une étiquette à un champ en tant qu’identité

Les champs contenant des informations d’identification personnelle peuvent être étiquetés comme champs d’identité. Une valeur fournie dans un champ d’identité est interprétée comme une identité par Identity Service. Le  de l’identité est spécifié dans le cadre de l’étiquetage du champ.

Les critères suivants doivent être satisfaits pour qu’un champ soit étiqueté comme identité :

- Seuls les champs de type chaîne peuvent être utilisés pour l’identité
- Les identités ne sont reconnues que dans les données d’enregistrement et de série chronologique.
- Seuls les champs d’informations d’identification personnelle doivent être marqués comme une identité. Le choix d’un champ représentant des données plus génériques se traduirait par des relations moins précises et par des erreurs potentielles d’accès aux identités liées à partir du graphique d’identité.

Pour savoir comment utiliser l’API de Registre  pour étiqueter un champ comme identité, consultez [Création d’un descripteur](../../xdm/api/descriptors.md).

## Étapes suivantes

Passez au didacticiel suivant pour [des identités de la grappe](./list-cluster-identites.md)