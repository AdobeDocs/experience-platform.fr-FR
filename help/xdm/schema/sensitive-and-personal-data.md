---
title: Informations sensibles et personnelles dans XDM
description: Découvrez les principales considérations relatives aux informations personnelles sensibles (SPI) et aux informations d’identification personnelle (PII) dans le modèle de données d’expérience (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Informations sensibles et personnelles dans XDM

Le modèle de données d’expérience (XDM) fournit des structures de données standard à utiliser dans Adobe Experience Platform, ce qui vous permet de collecter des données sur les expériences client. Ces données peuvent inclure des informations personnelles sensibles (SPI) et des informations d’identification personnelle (PII) telles que l’adresse électronique, le nom, l’identifiant de compte d’un client et d’autres champs de données.

Les règles organisationnelles et les réglementations légales en matière de confidentialité, telles que le Règlement général sur la protection des données (RGPD), imposent des restrictions sur la manière dont les SPI et les PII peuvent être collectés, stockés, utilisés et partagés. Par conséquent, il est important de prendre en compte les champs qui représentent des informations sensibles ou personnelles dans votre modèle de données et de s’assurer que vos opérations respectent les directives organisationnelles et juridiques.

Ce document couvre les principales considérations concernant les données sensibles et personnelles dans XDM.

## Déterminer les champs qui contiennent des données sensibles ou personnelles

Ce qui constitue les SPI et les PII est très spécifique au contexte. C’est donc à vous de comprendre votre modèle de données, vos opérations commerciales et les réglementations applicables afin de déterminer les champs de schéma qui représentent des données sensibles ou personnelles.

Par exemple, la juridiction légale de vos clients a un effet direct sur les informations considérées comme sensibles. Le RGPD fournit des définitions fiables des SPI et des PII, mais les clients ne faisant pas partie de l’Espace économique européen (EEE) peuvent être soumis à des définitions et des restrictions différentes.

## Gestion des données sensibles et personnelles

Tout comme les définitions des données sensibles et personnelles elles-mêmes, les restrictions liées à la gestion de ces données sont également spécifiques au contexte.

Le consentement du client est souvent un facteur essentiel en termes de données qui peuvent être collectées et traitées, et à quelles fins. En fonction de la juridiction légale sous laquelle vos clients se trouvent, un consentement explicite peut être nécessaire pour que leurs données sensibles et personnelles soient collectées. Même dans les cas où le consentement explicite n’est pas requis, les restrictions de traitement des données sont toujours applicables en fonction de ce que l’avis de confidentialité indique au client.

Consultez votre équipe juridique pour déterminer comment les données personnelles et sensibles doivent être traitées pour vos cas d’utilisation professionnels.

## Limitation de l’utilisation des données sensibles et personnelles

XDM fournit divers groupes de champs et types de données standard pour décrire les structures de données pertinentes couramment utilisées pour alimenter les expériences client. Toutefois, si une ressource standard recommandée contient des champs restreints que vous ne souhaitez pas inclure dans vos schémas, il n’est pas nécessaire d’utiliser cette ressource.

Platform vous permet de définir vos propres groupes de champs et types de données personnalisés, ce qui vous permet de contrôler entièrement la structure de vos données si des ressources standard disponibles ne répondent pas à vos besoins. Pour plus d’informations sur la définition de ces ressources personnalisées, consultez la documentation suivante :

* [Créer un groupe de champs personnalisé](../ui/resources/field-groups.md#create)
* [Créer un type de données personnalisé](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI et PII ne doivent être enregistrés que dans les classes [XDM Individual Profile](../classes/individual-profile.md) et [XDM ExperienceEvent](../classes/experienceevent.md). En tant que bonne pratique à des fins de suppression des données, de confidentialité et de gouvernance, n’enregistrez pas SPI et PII dans aucune autre classe XDM personnalisée ou standard.

## Étapes suivantes

Ce document couvrait les principales considérations concernant les données sensibles et personnelles dans XDM. Pour plus d’informations sur la manière de modéliser vos schémas pour répondre au mieux à vos cas d’utilisation professionnels, consultez le guide sur les [bonnes pratiques pour la modélisation des données](./best-practices.md).

Pour plus d’informations sur les fonctionnalités de gouvernance et de confidentialité des données dans Experience Platform, consultez la présentation sur [la gouvernance, la confidentialité et la sécurité](../../landing/governance-privacy-security/overview.md).
