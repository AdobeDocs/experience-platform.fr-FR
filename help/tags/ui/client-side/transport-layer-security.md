---
title: Informations TLS (Transport Layer Security)
description: Informations sur les versions et les chiffrements TLS utilisés
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 24%

---

# Informations TLS (Transport Layer Security)

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Pour consulter une référence consolidée des modifications terminologiques, reportez-vous au document [mises à jour de termes](../../term-updates.md) .

Transport Layer Security (TLS) est un protocole cryptographique qui fournit une sécurité de bout en bout pour les données envoyées entre les applications sur Internet. Pour plus d’informations sur TLS, consultez la documentation [Notions de base sur TLS](https://www.internetsociety.org/deploy360/tls/basics/) .

Dans Adobe Experience Platform, les balises représentent un système de gestion des balises conçu pour charger dynamiquement des scripts sur votre site web. TLS sécurise la communication entre l’hôte d’Adobe `assets.adobedtm.com` et votre site web lorsque ces scripts sont chargés.

Plusieurs versions de TLS sont disponibles et prennent en charge plusieurs chiffrements différents. Toutes les versions et les chiffrements ne sont pas identiques, car certains sont considérés comme moins ou plus sécurisés que d’autres.

## Versions TLS et Ciphers pris en charge

L’option Adobe host prend actuellement en charge les versions et les chiffrements TLS suivants :

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

Si vous [ auto-hébergement](../publishing/hosts/self-hosting-libraries.md) de votre bibliothèque, les versions TLS prises en charge seront déterminées par votre propre service d’hébergement.

## TLS Ciphers à supprimer le 1er mai 2024

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```
