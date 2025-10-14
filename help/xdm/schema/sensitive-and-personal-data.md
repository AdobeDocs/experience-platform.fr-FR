---
title: Informations sensibles et personnelles dans XDM
description: Découvrez les points clés concernant les informations personnelles sensibles (SPI) et les informations d’identification personnelle (PII) dans le modèle de données d’expérience (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---

# Informations sensibles et personnelles dans XDM

Le modèle de données d’expérience (XDM) fournit des structures de données standard à utiliser dans Adobe Experience Platform, ce qui vous permet de collecter des données sur les expériences client. Ces données peuvent inclure des informations personnelles sensibles (SPI) et des informations d’identification personnelle (PII) telles que l’adresse e-mail, le nom, l’ID de compte et d’autres champs de données d’un client.

Les règles d’organisation et les réglementations légales relatives à la confidentialité, telles que le Règlement général sur la protection des données (RGPD), imposent des restrictions sur la manière dont les informations SPI et PII peuvent être collectées, stockées, utilisées et partagées. Par conséquent, il est important de tenir compte des champs qui représentent des informations sensibles ou personnelles dans votre modèle de données et de s’assurer que vos opérations respectent les directives organisationnelles et juridiques.

Ce document couvre les points clés concernant les données sensibles et personnelles dans XDM.

## Détermination des champs qui contiennent des données sensibles ou personnelles

Ce qui constitue une SPI et des PII dépend beaucoup du contexte. C’est donc à vous de comprendre votre modèle de données, les opérations commerciales et les réglementations applicables afin de déterminer quels champs de schéma représentent des données sensibles ou personnelles.

Par exemple, la compétence juridique de vos clients a un effet direct sur les informations considérées comme sensibles. Le RGPD fournit des définitions fiables pour les informations d’identification personnelle et les informations d’identification personnelle, mais les clients situés en dehors de l’Espace économique européen (EEE) peuvent être soumis à des définitions et des restrictions différentes.

## Gestion des données sensibles et personnelles

Tout comme les définitions des données sensibles et personnelles elles-mêmes, les restrictions relatives au traitement de ces données sont également spécifiques au contexte.

Le consentement du client est souvent un facteur essentiel pour déterminer les données qui peuvent être collectées et traitées, et à quelles fins. Selon la juridiction légale sous laquelle se trouvent vos clients, un consentement explicite peut être nécessaire pour que leurs données sensibles et personnelles soient collectées. Même dans les cas où le consentement explicite n’est pas requis, les restrictions de gestion des données restent applicables en fonction de ce que la politique de confidentialité indique au client.

Veuillez consulter votre équipe juridique pour déterminer comment les données sensibles et personnelles doivent être traitées pour vos cas d’utilisation professionnels.

## Limiter l&#39;utilisation des données sensibles et personnelles

XDM fournit divers groupes de champs et types de données standard pour décrire les structures de données pertinentes et couramment utilisées pour alimenter les expériences client. Si une ressource standard recommandée contient des champs restreints que vous ne souhaitez pas inclure dans vos schémas, il n’est toutefois pas nécessaire d’utiliser cette ressource.

Experience Platform vous permet de définir vos propres groupes de champs et types de données personnalisés, ce qui vous permet de contrôler entièrement la structure de vos données si les ressources standard disponibles ne répondent pas à vos besoins. Pour plus d’informations sur la définition de ces ressources personnalisées, consultez la documentation suivante :

* [Créer un groupe de champs personnalisé](../ui/resources/field-groups.md#create)
* [Créer un type de données personnalisé](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>La SPI et les PII ne doivent être enregistrées que dans les classes [XDM Individual Profile](../classes/individual-profile.md) et [XDM ExperienceEvent](../classes/experienceevent.md). En règle générale, pour des raisons de suppression des données, de confidentialité et de gouvernance, n’enregistrez pas les SPI et les PII dans d’autres classes XDM personnalisées ou standard.

## Étapes suivantes

Ce document couvrait des considérations clés concernant les données sensibles et personnelles dans XDM. Pour plus d’informations sur la manière de modéliser vos schémas pour répondre au mieux à vos cas d’utilisation métier, reportez-vous au guide sur [les bonnes pratiques pour la modélisation des données](./best-practices.md).

Pour plus d’informations sur les fonctionnalités de gouvernance des données et de confidentialité dans Experience Platform, consultez la présentation de la [&#x200B; gouvernance, confidentialité et sécurité &#x200B;](../../landing/governance-privacy-security/overview.md).
