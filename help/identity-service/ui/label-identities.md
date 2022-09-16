---
keywords: Experience Platform;accueil;rubriques populaires;identités des étiquettes
title: Étiquetage d’un champ comme identité dans l’interface utilisateur
description: Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Identity Service interprète comme identité les valeurs fournies dans un champ d’identité. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 67%

---

# Étiquetage d’un champ comme identité dans l’interface utilisateur

Vous pouvez étiqueter des champs contenant des informations d’identification personnelle (PII) en tant que champs d’identité. Une valeur fournie dans un champ d’identité est interprétée comme une identité par [!DNL Identity Service]. L’espace de noms de l’identité est précisé dans le cadre de l’étiquetage du champ.

Pour étiqueter un champ en tant qu’identité, vous devrez respecter les critères suivants :

* Vous ne pouvez utiliser que les champs de type chaîne en tant qu’identité.
* Les identités ne sont reconnues que dans les données d’enregistrement et de séries temporelles.
* Seuls les champs PII doivent être marqués comme identité. Choisir un champ représentant des données plus génériques entraînerait des relations moins précises et des erreurs potentielles pour accéder aux identités associées du graphique d’identités.

Pour plus d’informations sur l’étiquetage des champs d’identité dans l’interface utilisateur, consultez le guide sur [définition des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md).

## Étapes suivantes

Pour plus d’informations sur [!DNL Identity Service], reportez-vous à la section [[!DNL Identity Service] aperçu](../home.md).
