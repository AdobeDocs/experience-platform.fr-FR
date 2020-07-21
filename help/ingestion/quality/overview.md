---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualité d’ingestion des données
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 86%

---


# Qualité des données dans Adobe Experience Platform

Adobe Experience Platform fournit des garanties bien définies d’exhaustivité, d’exactitude et de cohérence pour toute donnée transférée par ingestion par lots ou par flux. Le document suivant présente un résumé des contrôles et des comportements de validation pris en charge pour l’ingestion par lots et par flux dans [!DNL Experience Platform].

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

Both batch and streaming ingestion prevent failed data from going downstream by moving bad data for retrieval and analysis in [!DNL Data Lake]. L’ingestion de données fournit les validations suivantes pour l’ingestion par lots et par flux.

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
| Organisation IMS | Vérifie que l’organisation IMS répertoriée est une organisation valide. |
| Nom de source | Vérifie que le nom de la source de données est spécifié. |
| Jeu de données | Vérifie que le jeu de données est spécifié, activé et n’a pas été supprimé. |
| En-tête | Vérifie que l’en-tête est spécifié et valide. |

More information about how [!DNL Platform] monitors and validates data can be found in the [monitoring data flows documentation](./monitor-data-flows.md).
