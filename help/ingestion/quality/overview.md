---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualité d'assimilation des données
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca

---


# Qualité des données dans Adobe Experience Platform

Adobe Experience Platform fournit des garanties bien définies d’exhaustivité, d’exactitude et de cohérence pour toutes les données transférées par lot ou par flux continu. Le suivant présente un résumé des contrôles et des comportements de validation pris en charge pour l’assimilation par lot et en flux continu dans la plateforme d’expérience.

## Vérifications prises en charge

|   | Ingestion par lot | Ingestion en flux continu |
| ------ | --------------- | ------------------- |
| Vérification du type de données | Oui | Oui |
| Vérification de l&#39;énumération | Oui | Oui |
| Contrôle de plage (min, max.) | Oui | Oui |
| Vérification de champ obligatoire | Oui | Oui |
| Vérification de motif | Non | Oui |
| Vérification du format | Non | Oui |

## Comportements de validation pris en charge

L’assimilation par lot et par flux continu empêche les données défectueuses de se rendre en aval en déplaçant les données incorrectes pour les récupérer et   dans Data Lake. L’assimilation de données fournit les validations suivantes pour l’assimilation par lot et en flux continu.

### Importation par lot

Les validations suivantes sont effectuées pour l’assimilation par lot :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Assurez-vous que le  de **n’est pas** vide et qu’il contient une référence au del’ de, comme suit : `"meta:immutableTags": ["union"]` |
| `identityField` | Vérifie que tous les descripteurs d’identité valides sont définis. |
| `createdUser` | Garantit que l’utilisateur qui a assimilé le lot est autorisé à assimiler le lot. |

### Extraction en flux continu

Les validations suivantes sont effectuées pour l’assimilation en flux continu :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Assurez-vous que le  de **n’est pas** vide et qu’il contient une référence au del’ de, comme suit : `"meta:immutableTags": ["union"]` |
| `identityField` | Vérifie que tous les descripteurs d’identité valides sont définis. |
| JSON | Vérifie que le fichier JSON est valide. |
| Organisation IMS | S&#39;assure que l&#39;organisation IMS répertoriée est une organisation valide. |
| Nom de la source | Vérifie que le nom de la source de données est spécifié. |
| Jeu de données | Vérifie que le jeu de données est spécifié, activé et n’a pas été supprimé. |
| En-tête | Vérifie que l’en-tête est spécifié et valide. |

Pour plus d’informations sur la manière dont Platform surveille et valide les données, consultez la documentation [sur les flux de données de](./monitor-data-flows.md)surveillance.
