---
title: Guide de l’API MTLS
description: Découvrez comment utiliser l’API du service mTLS pour récupérer et vérifier en toute sécurité les certificats publics émis par Adobe.
role: Developer
exl-id: eb40691a-a866-4acb-849b-c5dce2d74224
TQID: https://experienceleague.adobe.com/L-uQyr67fW6dlb5we7u9reemDlZ-FU3ymIkT6vbx8-c
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 196
ht-degree: 1%

---

# Présentation de l’API du service MTLS

Utilisez l’API du service MTLS pour récupérer en toute sécurité les certificats publics émis par Adobe pour les applications de votre organisation. Cette API garantit que les échanges de données entre vos clients et Adobe Experience Platform sont authentifiés et chiffrés, fournissant ainsi une couche de sécurité supplémentaire. En vérifiant l’authenticité des certificats en externe, vous pouvez améliorer la confiance et protéger les informations sensibles.

## Certificat public

Un certificat public est un document numérique utilisé pour authentifier l’identité d’un serveur ou d’un client dans des communications sécurisées. Dans le cadre de l’API du service mTLS, ces certificats garantissent que les échanges de données avec Adobe Experience Platform sont authentifiés et chiffrés. La récupération et la vérification de ces certificats par le biais de l’API confirment leur authenticité, ce qui renforce la sécurité et la fiabilité de vos transactions de données et protège les informations sensibles. Pour savoir comment récupérer votre certificat public, consultez le [guide du point d’entrée](./public-certificate-endpoint.md) pour savoir comment effectuer des appels.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API du service MTLS, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture des exemples d’appels d’API, etc.
