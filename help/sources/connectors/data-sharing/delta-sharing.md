---
title: Partage Delta
description: Découvrez comment utiliser la source de partage Delta sur Adobe Experience Platform.
badge: Beta
exl-id: 69c4e250-aa9b-4db1-b44b-6056bdddb637
source-git-commit: d820a764b7adc6001992964e4245396161325937
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---

# [!DNL Delta Sharing]

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta **limitée** et ne sera disponible que jusqu’au 15 juillet 2026. Contactez votre équipe de compte Adobe pour demander l’accès à la version bêta.

Avec le connecteur source [!DNL Delta Sharing], vous pouvez vous connecter en toute sécurité à votre source [!DNL Databricks Delta Sharing] et créer des jeux de données virtuels dans Adobe Experience Platform. Vous pouvez ainsi interroger et utiliser des tables externes par le biais des services Experience Platform, tout en représentant les données partagées au moyen de schémas relationnels, sans ingérer physiquement les données dans Platform. En utilisant [!DNL Delta Sharing], vous pouvez réduire le stockage des données en double, réduire les coûts de stockage et simplifier la gestion des données.

## Conditions préalables {#prerequisites}

Avant de vous connecter à une source de [!DNL Databricks Delta Sharing] à partir de Adobe Experience Platform, assurez-vous que les conditions suivantes sont remplies.

>[!IMPORTANT]
>
>[!DNL Delta Sharing] n’ingère ni ne copie physiquement les données sources dans Experience Platform. Au lieu de cela, les données partagées sont représentées dans Experience Platform sous la forme de jeux de données virtuels. Assurez-vous que les tables partagées que vous souhaitez utiliser sont disponibles par le biais du partage Delta et qu’elles peuvent être représentées par des schémas relationnels dans Experience Platform.

### Conditions préalables requises pour le fournisseur de [!DNL Databricks]

Du côté du fournisseur, assurez-vous que vous disposez des éléments suivants :

- **Le [!DNL Delta Sharing] externe est activé** : le [!DNL Delta Sharing] externe doit être activé pour votre compte/espace de travail [!DNL Databricks] et une TTL de jeton par défaut doit être configurée.
- **Tables delta éligibles** : les tables que vous envisagez de partager doivent :
   - Soyez **tables delta**.
   - être configuré sur un stockage qui prend en charge les [!DNL Delta Sharing] ouverts (stockage externe ou configuration prise en charge par le [!DNL Databricks]).
   - Les filtres de ligne ou les masques de colonne ne sont pas appliqués **&#x200B;**&#x200B;[!DNL Databricks] ne permet pas le partage de tels tableaux).

#### Configuration des destinataires et des partages

Un administrateur [!DNL Databricks] doit effectuer les étapes suivantes :

1. Créez un **partage** et ajoutez des tableaux :

   ```sql
   CREATE SHARE IF NOT EXISTS my_first_share
     COMMENT 'Share for Adobe Experience Platform';
   
   ALTER SHARE my_first_share
     ADD TABLE {CATALOG}.{SCHEMA}.{TABLE};
   ```

2. Créez un destinataire pour Experience Platform et accordez le partage :

   ```sql
   CREATE RECIPIENT IF NOT EXISTS plat_recipient
     COMMENT 'Recipient for Platform Delta Sharing source';
   GRANT SELECT ON SHARE my_first_share TO RECIPIENT plat_recipient;
   ```

Téléchargez le fichier d’informations d’identification [!DNL Delta Sharing] (.share) pour ce destinataire. Ce fichier contient les quatre valeurs que vous utiliserez dans l’interface utilisateur d’Experience Platform.

+++Sélectionner pour afficher un exemple de fichier `.share`

```json
{
  "shareCredentialsVersion": 1,
  "endpoint": "https://{WORKSPACE}.azuredatabricks.net/api/2.0/delta-sharing/metastores/{ID}",
  "bearerToken": "dapi1234567890abcdef1234567890abcdef-1234567890abcdef",
  "expirationTime": "2026-03-31T23:59:59Z"
}
```

+++

#### Configuration du réseau et du pare-feu

Si vos comptes de stockage dans le cloud, tels que [!DNL Azure Data Lake Storage Gen2], [!DNL Amazon S3] [!DNL Google Cloud Storage], sont protégés par des règles de pare-feu, assurez-vous qu’Experience Platform peut accéder aux [!DNL Delta Sharing resource, including] requises :

- Point d’entrée [!DNL Delta Sharing] à partir du fichier `.share`.
- Chemins de stockage sous-jacents pour les tables partagées.

### Conditions préalables d’Experience Platform

#### Environnement pris en charge

- Votre organisation Experience Platform doit être hébergée dans une région Azure prise en charge.
- La fonctionnalité de source [!DNL Delta Sharing] doit être activée pour votre organisation. Si la vignette « Partage de données → Partage de briques de données dans le catalogue des sources » n’apparaît pas, contactez le support technique d’Adobe ou votre représentant Adobe.

En outre, l’utilisateur qui crée la connexion doit disposer des autorisations suivantes dans le sandbox cible :

- Accès aux sources et autorisation de créer des connexions source/flux de données.
- Autorisation de créer des schémas et des jeux de données, y compris des jeux de données virtuels.

#### Attentes en matière de gouvernance

- Les connexions [!DNL Delta Sharing] créent des jeux de données virtuels dans le catalogue. Ces jeux de données sont en lecture seule et sont représentés sous la forme de jeux de données virtuels dans Experience Platform.
- Aucune ligne n’est ingérée dans Experience Platform. Seules les métadonnées telles que les détails de schéma, de parenté et de connexion sont stockées.
- Des étiquettes et des politiques de gouvernance standard peuvent être appliquées au schéma virtuel, mais les tâches de confidentialité/conservation ne modifient pas les données sources.

### Collecter les informations d’identification requises {#gather-required-credentials}

Vous devez fournir des valeurs pour les informations d’identification suivantes afin d’authentifier et d’utiliser la source [!DNL Delta Sharing] :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Point d’entrée | Le point d’entrée est l’URL de base du serveur [!DNL Delta Sharing] qui héberge les tables partagées. Généré par [!DNL Databricks] lorsque le [!DNL Delta Sharing] externe est activé, ce point d’entrée apparaît dans le fichier d’informations d’identification `.share` du destinataire et est utilisé par Experience Platform pour énumérer les partages, parcourir les schémas et les tableaux, et récupérer les aperçus des métadonnées et des données. | `https://adb-1234567890123.4.azuredatabricks.net/api/2.0/delta-sharing/metastores/0a1b2c3d-4e5f-6789-abcd-0123456789ef` |
| Jeton porteur | Le jeton porteur est un jeton d’accès [!DNL Delta Sharing] en lecture seule associé à un destinataire spécifique dans [!DNL Databricks]. Il authentifie Experience Platform en tant que destinataire auprès du serveur [!DNL Delta Sharing] en étant inclus en tant qu’en-tête d’autorisation dans chaque requête (`Authorization: Bearer {BEARER_TOKEN}`). | `dapi1a2b3c4d5e6f7g8h9i0jklmnopqrstuvwx` |
| Partager la version des informations d’identification | La version des informations d’identification du partage correspond à `shareCredentialsVersion` dans le fichier `.share`. Il s’agit de la version du schéma du fichier d’informations d’identification, et non de la version du jeton. Experience Platform l’utilise pour comprendre comment interpréter les champs du profil. Pour les profils [!DNL Databricks Delta Sharing] d’aujourd’hui, la valeur est 1. | `1` |
| Délai d’expiration | L’heure d’expiration est un horodatage facultatif spécifiant le moment d’expiration du jeton porteur. La date d’expiration doit être un horodatage UTC ISO-8601 valide. | `2026-03-31T23:59:59Z` |

{style="table-layout:auto"}

## Types de données de champs XDM autorisés {#allowed-xdm-field-data-types}

Lors du mappage de tables partagées à des schémas Experience Platform, seuls les types de données de champ XDM suivants sont autorisés :

- **Primitives de base :** chaîne, nombre, entier, booléen
- **Sous-types via des contraintes :** octet, court, entier (32 bits), long
- **Temporel:** Date, DateTime
- **Structure:** Tableau, Objet
- **Variantes de chaîne contraintes :** Énumération / Liste suggérée (meta:enum)

## Connexion à [!DNL Databricks Delta Sharing] dans l’interface utilisateur

Lisez le [[!DNL Databricks Delta Sharing &#x200B;]  guide de l’interface utilisateur &#x200B;](../../tutorials/ui/create/data-sharing/delta-sharing.md) pour savoir comment ingérer des données dans Experience Platform avec la source [!DNL Delta Sharing].