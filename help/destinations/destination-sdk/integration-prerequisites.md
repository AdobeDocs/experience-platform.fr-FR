---
description: Pour utiliser Destination SDK, une société partenaire doit remplir les conditions préalables répertoriées dans ce document.
title: Conditions préalables à l’intégration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# Conditions préalables à l’intégration

Pour utiliser Destination SDK, veillez à respecter les conditions préalables techniques et de partenariat répertoriées dans les sections ci-dessous.

## Conditions préalables techniques/API

1. Vous disposez d’un point de terminaison d’API REST pour que Adobe Experience Platform puisse fournir les types de données suivants à :
   * Informations sur l’appartenance à un segment ;
   * Informations sur l’identité du profil ;
   * (Facultatif) Attributs supplémentaires pour l’enrichissement du profil.
2. Votre point de terminaison API REST prend en charge l’authentification du porteur de jeton API ou le protocole d’authentification OAuth 2.0.
3. (Facultatif) Vous disposez d’une API de création/mise à jour/suppression de segment ou d’un point de terminaison d’API pour la gestion programmatique des métadonnées.

## Conditions préalables du partenariat

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) qui souhaite utiliser Destination SDK, lisez les exigences de partenariat pour les ISV et les SI dans la [section accès](./overview.md#get-access).
