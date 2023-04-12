---
keywords: Experience Platform;accueil;rubriques populaires;Qualité des données;Qualité;Qualité;Validation prise en charge;Validation;Validation prise en charge ;
solution: Experience Platform
title: Qualité des données
description: Le document suivant résume les comportements de vérification et de validation pris en charge pour l’ingestion par lots et par flux dans Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 54%

---

# Qualité des données dans Adobe Experience Platform

Adobe Experience Platform fournit des garanties bien définies d’exhaustivité, d’exactitude et de cohérence pour toute donnée transférée par ingestion par lots ou par flux. Le document suivant présente un résumé des contrôles et des comportements de validation pris en charge pour l’ingestion par lots et par flux dans [!DNL Experience Platform].

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

L’ingestion par lots et par flux empêche les données en échec de se rendre en aval en déplaçant les données incorrectes pour récupération et analyse dans [!DNL Data Lake]. L’ingestion de données fournit les validations suivantes pour l’ingestion par lots et par flux.

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
| Organisation | Vérifie que l’organisation répertoriée est une organisation valide. |
| Nom de source | Vérifie que le nom de la source de données est spécifié. |
| Jeu de données | Vérifie que le jeu de données est spécifié, activé et n’a pas été supprimé. |
| En-tête | Vérifie que l’en-tête est spécifié et valide. |

Informations supplémentaires sur la manière dont [!DNL Platform] Les analyses et les validations des données sont disponibles dans la variable [documentation sur la surveillance des flux de données](./monitor-data-ingestion.md).

## Validation de la valeur d’identité

Le tableau suivant décrit les règles existantes que vous devez suivre pour garantir une validation réussie de votre valeur d’identité.

| Espace de noms | Règle de validation | Comportement du système en cas de violation de la règle |
| --- | --- | --- |
| ECID | <ul><li>La valeur d’identité d’un ECID doit comporter exactement 38 caractères.</li><li>La valeur d’identité d’un ECID ne doit être composée que de nombres.</li></ul> | <ul><li>Si la valeur d’identité d’ECID ne comporte pas exactement 38 caractères, l’enregistrement est ignoré.</li><li>Si la valeur d’identité d’ECID contient des caractères non numériques, l’enregistrement est ignoré.</li></ul> |
| Non ECID | La valeur d’identité ne peut pas dépasser 1 024 caractères. | Si la valeur d’identité dépasse 1 024 caractères, l’enregistrement est ignoré. |

Pour plus d’informations sur [!DNL Identity Service] barrières de sécurité, voir [[!DNL Identity Service] Présentation des barrières de sécurité](../../identity-service/guardrails.md).
