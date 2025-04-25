---
title: Informations TLS (Transport Layer Security)
description: Informations sur les versions et les chiffrements TLS utilisés
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 25%

---

# Informations TLS (Transport Layer Security)

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Pour obtenir une référence consolidée des modifications terminologiques, reportez-vous au document [Mises à jour des termes](../../term-updates.md).

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
