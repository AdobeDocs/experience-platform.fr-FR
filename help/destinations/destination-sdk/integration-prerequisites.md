---
description: Pour utiliser le SDK de destination, une société partenaire doit remplir les conditions préalables répertoriées dans ce document.
title: Conditions préalables à l’intégration
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Conditions préalables à l’intégration

Pour utiliser le SDK de destination, assurez-vous de respecter les conditions préalables techniques et de partenariat répertoriées dans les sections ci-dessous.

## Conditions préalables techniques/API

1. Vous disposez d’un point de terminaison d’API REST pour que Adobe Experience Platform puisse fournir les types de données suivants à :
   * Informations sur l’appartenance à un segment ;
   * Informations sur l’identité du profil ;
   * (Facultatif) Attributs supplémentaires pour l’enrichissement du profil.
2. Votre point de terminaison API REST prend en charge l’authentification du porteur de jeton API ou le protocole d’authentification OAuth 2.0.
3. (Facultatif) Vous disposez d’une API de création/mise à jour/suppression de segment ou d’un point de terminaison d’API pour la gestion programmatique des métadonnées.

## Conditions préalables du partenariat

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) qui souhaite utiliser le SDK de destination, lisez les exigences de partenariat pour les ISV et les SI dans la section [Accès](./overview.md#get-access).
