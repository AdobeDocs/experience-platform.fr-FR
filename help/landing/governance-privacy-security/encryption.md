---
title: Chiffrement des données dans Adobe Experience Platform
description: Découvrez comment les données sont chiffrées en transit et au repos dans Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 8%

---

# Cryptage des données dans Adobe Experience Platform

Adobe Experience Platform est un système puissant et extensible qui centralise et normalise les données d’expérience client dans les solutions d’entreprise. Toutes les données utilisées par Platform sont chiffrées en transit et au repos pour préserver la sécurité de vos données. Ce document décrit les processus de cryptage de Platform à un niveau élevé.

Le diagramme de flux de processus suivant illustre la manière dont Experience Platform ingère, chiffre et conserve les données :

![Diagramme illustrant la manière dont les données sont ingérées, chiffrées et conservées par l’Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Données en transit {#in-transit}

Toutes les données en transit entre Platform et tout composant externe sont effectuées sur des connexions sécurisées et chiffrées à l’aide du protocole HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En règle générale, les données sont introduites dans Platform de trois façons :

- Les fonctionnalités de [collecte de données](../../collection/home.md) permettent aux sites web et aux applications mobiles d’envoyer des données à l’Edge Network Platform pour l’évaluation et la préparation à l’ingestion.
- [Les connecteurs Source](../../sources/home.md) diffusent directement des données vers Platform à partir d’applications Adobe Experience Cloud et d’autres sources de données d’entreprise.
- Les outils ETL (extraction, transformation, chargement) non Adobes envoient des données à l’ [ API d’ingestion par lots](../../ingestion/batch-ingestion/overview.md) pour être utilisés.

Une fois les données introduites dans le système et [cryptées au repos](#at-rest), les services Platform enrichissent et exportent les données de la manière suivante :

- Les [destinations](../../destinations/home.md) vous permettent d’activer des données pour Adobe des applications et des applications partenaires.
- Les applications Platform natives telles que [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/ajo-home) peuvent également utiliser les données.

### Prise en charge du protocole mTLS {#mtls-protocol-support}

Vous pouvez désormais utiliser Mutual Transport Layer Security (mTLS) pour garantir une sécurité renforcée dans les connexions sortantes à la [ destination d’API HTTP](../../destinations/catalog/streaming/http-destination.md) et aux [ actions personnalisées ](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) de Adobe Journey Optimizer. Le protocole mTLS est une méthode de sécurité de bout en bout pour une authentification mutuelle qui garantit que les deux parties qui partagent des informations sont celles qu’elles prétendent être avant que les données ne soient partagées. Le protocole mTLS inclut une étape supplémentaire par rapport à TLS, dans laquelle le serveur demande également le certificat du client et le vérifie de son côté.

Si vous souhaitez [ utiliser mTLS avec des actions personnalisées Adobe Journey Optimizer ](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) et des workflows de destination d’API HTTP Experience Platform, l’adresse du serveur que vous avez placée dans l’interface utilisateur d’action du client Adobe Journey Optimizer ou l’interface utilisateur des destinations doit avoir les protocoles TLS désactivés et uniquement mTLS activé. Si le protocole TLS 1.2 est toujours activé sur ce point de terminaison, aucun certificat n’est envoyé pour l’authentification du client. Cela signifie que pour utiliser mTLS avec ces workflows, votre point d’entrée de serveur &quot;réception&quot; doit être un point d’entrée de connexion activé mTLS **uniquement**.

>[!IMPORTANT]
>
>Aucune configuration supplémentaire n’est requise dans votre action personnalisée Adobe Journey Optimizer ou votre destination d’API HTTP pour activer mTLS. Ce processus se produit automatiquement lorsqu’un point d’entrée compatible mTLS est détecté. Les noms communs (CN) et les noms de remplacement du sujet (SAN) pour chaque certificat sont disponibles dans la documentation dans le cadre du certificat et peuvent être utilisés comme une couche supplémentaire de validation de la propriété si vous le souhaitez.
>
>La norme RFC 2818, publiée en mai 2000, rend obsolète l’utilisation du champ Nom commun (CN) dans les certificats HTTPS pour la vérification du nom du sujet. Il recommande plutôt d’utiliser l’extension SAN (Subject Alternative Name) du type &quot;dns name&quot;.

### Téléchargement de certificats {#download-certificates}

>[!NOTE]
>
>Il vous appartient de garder le certificat public à jour. Veillez à consulter régulièrement le certificat, en particulier à l’approche de sa date d’expiration. Vous devez mettre cette page en signet afin de conserver la dernière copie dans votre environnement.

Si vous souhaitez vérifier le CN ou le SAN pour effectuer une validation tierce supplémentaire, vous pouvez télécharger les certificats pertinents ici :

- [Certificat public Adobe Journey Optimizer](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [Certificat public du service Destinations](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

Vous pouvez également récupérer les certificats publics en toute sécurité en effectuant une requête GET sur le point de terminaison MTLS. Pour plus d’informations, consultez la [documentation du point d’entrée de certificat public](../../data-governance/mtls-api/public-certificate-endpoint.md) .

## Données au repos {#at-rest}

Les données ingérées et utilisées par Platform sont stockées dans le lac de données, un entrepôt de données hautement granulaire contenant toutes les données gérées par le système, indépendamment de l’origine ou du format de fichier. Toutes les données conservées dans le lac de données sont chiffrées, stockées et gérées dans une instance [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) isolée, propre à votre organisation.

Pour plus d’informations sur la façon dont les données au repos sont chiffrées dans Azure Data Lake Storage, consultez la [documentation Azure officielle](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Étapes suivantes

Ce document fournit un aperçu général de la manière dont les données sont chiffrées dans Platform. Pour plus d’informations sur les procédures de sécurité dans Platform, consultez la présentation de [gouvernance, confidentialité et sécurité](./overview.md) sur Experience League ou consultez le [livre blanc de sécurité de Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
