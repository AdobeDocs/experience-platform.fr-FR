---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualité d'assimilation des données
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 6%

---


# Qualité des données dans Adobe Experience Platform

Adobe Experience Platform fournit des garanties bien définies d’exhaustivité, d’exactitude et de cohérence pour toutes les données transférées par lots ou en flux continu. Le document suivant fournit un résumé des contrôles et des comportements de validation pris en charge pour l’assimilation par lots et en flux continu dans la plate-forme d’expérience.

## Vérifications prises en charge

|   | Ingestion par lots | Ingestion en flux continu |
| ------ | --------------- | ------------------- |
| Vérification du type de données | Oui | Oui |
| Vérification de l&#39;énumération | Oui | Oui |
| Contrôle de plage (min, max.) | Oui | Oui |
| Vérification du champ obligatoire | Oui | Oui |
| Vérification du modèle | Non | Oui |
| Vérification du format | Non | Oui |

## Comportements de validation pris en charge

L’assimilation par lot et l’assimilation en flux continu empêchent les données défectueuses de se rendre en aval en déplaçant les données erronées en vue de leur récupération et de leur analyse dans Data Lake. L’assimilation de données fournit les validations suivantes pour l’assimilation par lots et en flux continu.

### Importation par lot

Les validations suivantes sont effectuées pour l’assimilation par lot :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Veille à ce que le schéma **ne soit pas** vide et qu’il contienne une référence au schéma d’union, comme suit : `"meta:immutableTags": ["union"]` |
| `identityField` | Veille à ce que tous les descripteurs d’identité valides soient définis. |
| `createdUser` | Veille à ce que l’utilisateur qui a assimilé le lot soit autorisé à assimiler le lot. |

### Extraction en flux continu

Les validations suivantes sont effectuées pour l’assimilation en flux continu :

| Zone de validation | Description |
| --------------- | ----------- |
| Schéma | Veille à ce que le schéma **ne soit pas** vide et qu’il contienne une référence au schéma d’union, comme suit : `"meta:immutableTags": ["union"]` |
| `identityField` | Veille à ce que tous les descripteurs d’identité valides soient définis. |
| JSON | Vérifie que le fichier JSON est valide. |
| Organisation IMS | S&#39;assure que l&#39;organisation IMS répertoriée est une organisation valide. |
| Nom de la source | Veille à ce que le nom de la source de données soit spécifié. |
| Jeu de données | Vérifie que le jeu de données est spécifié, activé et n&#39;a pas été supprimé. |
| En-tête | Vérifie que l’en-tête est spécifié et valide. |

Pour plus d’informations sur la façon dont Platform surveille et valide les données, consultez la documentation [sur les flux de données de](./monitor-data-flows.md)surveillance.
