---
title: Informations TLS (Transport Layer Security)
description: Informations sur les versions et les chiffrements TLS utilisés
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
TQID: https://experienceleague.adobe.com/5O--Zh08C1aNcggoHxNsKZcRVBn1JPU-gmAKadUsH7g
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 164
ht-degree: 13%

---

# Informations TLS (Transport Layer Security)

Transport Layer Security (TLS) est un protocole cryptographique qui fournit une sécurité de bout en bout pour les données envoyées entre les applications sur Internet. Pour plus d’informations sur le protocole TLS, consultez la documentation [Principes de base du protocole TLS](https://www.internetsociety.org/deploy360/tls/basics/).

Dans Adobe Experience Platform, les balises représentent un système de gestion des balises conçu pour charger dynamiquement des scripts sur votre site web. TLS sécurise la communication entre le `assets.adobedtm.com` hôte Adobe et votre site web lorsque ces scripts sont chargés.

Il existe plusieurs versions de TLS disponibles et il prend en charge un certain nombre de chiffrements différents. Toutes les versions et tous les chiffrements ne sont pas identiques, car certains sont considérés comme moins ou plus sécurisés que d’autres.

## Versions et chiffrements TLS pris en charge

L’option d’hôte Adobe prend actuellement en charge les versions et chiffrements TLS suivants :

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Auto-hébergement

Si vous [auto-hébergement](../publishing/hosts/self-hosting-libraries.md) votre bibliothèque, les versions de TLS prises en charge seront déterminées par votre propre service d’hébergement.
