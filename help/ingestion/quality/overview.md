---
keywords: Experience Platform;accueil;rubriques populaires;Qualité des données;qualité;Qualité;Validation prise en charge;Validation;validation prise en charge;
solution: Experience Platform
title: Qualité des données
description: Le document suivant présente un résumé des contrôles et des comportements de validation pris en charge pour l’ingestion par lots et par flux dans Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 73%

---

# Qualité des données dans Adobe Experience Platform

Adobe Experience Platform fournit des garanties bien définies d’exhaustivité, d’exactitude et de cohérence pour toute donnée chargée par ingestion par lots ou par flux. Le document suivant présente un résumé des contrôles et des comportements de validation pris en charge pour l’ingestion par lots et par flux dans [!DNL Experience Platform].

## Vérifications prises en charge

|   | Ingestion par lots | Ingestion par flux |
| ------ | --------------- | ------------------- |
| Vérification du type de données | Oui | Oui |
| Vérification de l’énumération | Oui | Oui |
| Contrôle de plage (min, max) | Oui | Oui |
| Vérification de champ obligatoire | Oui | Oui |
| Vérification du modèle | Non | Oui |
| Vérification du format | Non | Oui |

## Comportements de validation pris en charge

L’ingestion par lots et en flux continu empêche les données en échec de descendre en déplaçant les données incorrectes pour récupération et analyse en [!DNL Data Lake]. L’ingestion de données fournit les validations suivantes pour l’ingestion par lots et par flux.

### Ingestion par lots

Les validations suivantes sont effectuées pour l’ingestion par lots :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Vérifie que le schéma n’est **pas** vide et contient une référence au schéma d’union, comme ci-dessous : `"meta:immutableTags": ["union"]` |
| `identityField` | Vérifie que tous les descripteurs d’identité valides sont définis. |
| `createdUser` | Vérifie que l’utilisateur qui a ingéré le lot est autorisé à ingérer le lot. |

### Ingestion par flux

Les validations suivantes sont effectuées pour l’ingestion par flux :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Vérifie que le schéma n’est **pas** vide et contient une référence au schéma d’union, comme ci-dessous : `"meta:immutableTags": ["union"]` |
| `identityField` | Vérifie que tous les descripteurs d’identité valides sont définis. |
| JSON | Vérifie que le fichier JSON est valide. |
| Organisation | S’assure que l’organisation répertoriée est une organisation valide. |
| Nom de source | Vérifie que le nom de la source de données est spécifié. |
| Jeu de données | Vérifie que le jeu de données est spécifié, activé et n’a pas été supprimé. |
| En-tête | Vérifie que l’en-tête est spécifié et valide. |

Vous trouverez plus d’informations sur la manière dont [!DNL Experience Platform] surveille et valide les données dans la documentation [surveillance des flux de données](./monitor-data-ingestion.md).

## Validation de la valeur d’identité

Le tableau suivant décrit les règles à suivre pour garantir la validation de votre valeur d’identité.

| Espace de noms | Règle de validation | Comportement du système en cas de violation de règle |
| --- | --- | --- |
| ECID | <ul><li>La valeur d’identité d’un ECID doit comporter exactement 38 caractères.</li><li>La valeur d’identité d’un ECID ne doit être composée que de chiffres.</li></ul> | <ul><li>Si la valeur d’identité d’un ECID ne comporte pas exactement 38 caractères, l’enregistrement est ignoré.</li><li>Si la valeur d’identité d’un ECID contient des caractères non numériques, l’enregistrement est ignoré.</li></ul> |
| Non-ECID | La valeur d’identité ne peut pas dépasser 1 024 caractères. | Le cas échéant, l’enregistrement est ignoré. |

Pour plus d’informations sur les mécanismes de sécurisation [!DNL Identity Service], consultez la présentation des [[!DNL Identity Service] mécanismes de sécurisation](../../identity-service/guardrails.md).
