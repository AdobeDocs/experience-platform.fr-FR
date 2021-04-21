---
keywords: Experience Platform ; accueil ; rubriques populaires ; Qualité des données ; Qualité ; Qualité ; Validation prise en charge ; Validation ; Validation prise en charge ;
solution: Experience Platform
title: Qualité des données
topic-legacy: overview
description: Le document suivant fournit un résumé des contrôles et des comportements de validation pris en charge pour l’assimilation par lots et en flux continu dans Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 76%

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

L’assimilation par lot et en flux continu empêche les données en panne de se rendre en aval en déplaçant les données incorrectes pour récupération et analyse dans [!DNL Data Lake]. L’ingestion de données fournit les validations suivantes pour l’ingestion par lots et par flux.

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

Pour plus d&#39;informations sur la façon dont [!DNL Platform] surveille et valide les données, consultez la [documentation sur les flux de données de surveillance](./monitor-data-ingestion.md).
