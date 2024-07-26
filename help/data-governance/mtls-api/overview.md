---
title: Guide de l’API MTLS
description: Découvrez comment utiliser l’API du service mTLS pour récupérer et vérifier en toute sécurité les certificats publics émis par Adobe.
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Présentation de l’API du service MTLS

Utilisez l’API du service MTLS pour récupérer en toute sécurité les certificats publics émis par Adobe pour les applications de votre entreprise. Cette API garantit que les exchanges de données entre vos clients et Adobe Experience Platform sont authentifiés et chiffrés, fournissant ainsi une couche de sécurité supplémentaire. En vérifiant de manière externe l’authenticité des certificats, vous pouvez améliorer la confiance et protéger les informations sensibles.

## Certificat public

Un certificat public est un document numérique utilisé pour authentifier l’identité d’un serveur ou d’un client dans le cadre de communications sécurisées. Dans le contexte de l’API du service mTLS, ces certificats garantissent que les exchanges de données avec Adobe Experience Platform sont authentifiés et chiffrés. La récupération et la vérification de ces certificats via l’API confirme leur authenticité, renforce la sécurité et la fiabilité de vos transactions de données et protège les informations sensibles. Pour savoir comment récupérer votre certificat public, consultez le [guide de point de terminaison](./public-certificate-endpoint.md) pour savoir comment effectuer des appels.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API du service MTLS, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d’exemples d’appels API, etc.
