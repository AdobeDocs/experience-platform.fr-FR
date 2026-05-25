---
description: Pour utiliser Destination SDK, une société partenaire doit remplir les conditions préalables répertoriées dans ce document.
title: Conditions préalables à l’intégration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
TQID: https://experienceleague.adobe.com/N4-F6aO64EDtasmxMYrRF2bCUW-en2G9S2llv0T1soI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2:
  - id: d3f95e25-a50e-4fd0-bc23-9a22409a183b
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 196
ht-degree: 2%

---

# Conditions préalables à l’intégration

Pour utiliser Destination SDK, vérifiez que vous remplissez les conditions techniques et de partenariat répertoriées dans les sections ci-dessous.

## Conditions préalables techniques/API pour les destinations de streaming {#streaming-prerequisites}

1. Vous disposez d’un point d’entrée de l’API REST pour [!DNL Adobe Experience Platform] de fournir les types de données suivants à :
   * Informations sur l’appartenance à une audience
   * les informations d’identité du profil ;
   * (Facultatif) Attributs supplémentaires pour l’enrichissement des profils.
2. Votre point d’entrée de l’API REST prend en charge les protocoles d’authentification de base, de jeton porteur ou OAuth 2.0.
3. (Facultatif) Vous disposez d’une API ou d’un point d’entrée d’API de création/mise à jour/suppression d’audience pour la gestion programmatique des métadonnées.

## Conditions préalables techniques pour les destinations par lots {#batch-prerequisites}

1. Vous disposez d’un emplacement de destination hébergé sur [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud] ou une [!DNL Data Landing Zone] privée, où vous pouvez recevoir des fichiers exportés hors d’Experience Platform.
2. Votre plateforme de destination peut ingérer des fichiers au format configuré via les [options de formatage de fichier](functionality/destination-server/file-formatting.md) dans Destination SDK pour les destinations par lots.
3. (Facultatif) Vous disposez d’une API ou d’un point d’entrée d’API de création/récupération/mise à jour/suppression d’audience ([!DNL CRUD]) pour la gestion programmatique des métadonnées.

## Conditions préalables du partenariat {#partnership-prerequisites}

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) et que vous souhaitez utiliser Destination SDK, lisez les conditions requises pour les ISV et les SI dans la section [obtention de l’accès](overview.md#get-access).
