---
keywords: Experience Platform;home;popular topics;consent;Consent
solution: Experience Platform
title: FAQ relative à la CCPA
topic: troubleshooting
description: Ce document répond aux questions les plus fréquemment posées à propos de la Loi sur la protection de la confidentialité des consommateurs (CCPA) de Californie et de sa mise en œuvre dans Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 81%

---


# FAQ relative à la CCPA

This document provides answers to frequently asked questions about the [!DNL California Consumer Protection Act] (CCPA) and its implementation in Adobe Experience Cloud.

## Qu’est-ce que la CCPA ?

The [!DNL California Consumer Privacy Act] (CCPA) is California’s new privacy law that provides its residents with new rights regarding their personal information, and imposes data protection responsibilities on certain entities who conduct business in California.

>[!NOTE]
>
>Bien qu’elle soit techniquement entrée en vigueur en janvier 2020, la CCPA est encore peaufinée par les législateurs. En outre, d’importants détails concernant sa mise en œuvre et d’autres indications seront précisés dans des règles qui n’ont pas encore été écrites par l’autorité de régulation californienne.

Bien que la CCPA partage certains concepts énoncés dans le Règlement général sur la protection des données (RGPD) de l’Union Européenne, comme le droit d’accès et d’effacement des données à caractère personnel d’un individu, la CCPA diffère du RGPD sur plusieurs points majeurs. Par exemple, la CCPA accorde aux clients un droit d’opposition concernant certains échanges de données considérés comme étant de la « vente » d’informations personnelles à un tiers, plutôt que d’exiger un consentement préalable.

## Que signifie la notion d’informations personnelles dans le cadre de la CCPA ?

Les informations personnelles sont des renseignements « qui identifient, se rapportent à, décrivent, peuvent être associés à ou pourraient raisonnablement être liés, directement ou indirectement, à un client ou à un ménage ».

## Quels types d’informations personnelles ou d’identifiants utilisés dans Adobe Experience Cloud sont soumis à ces nouvelles exigences ?

The following identifiers are commonly used in [!DNL Experience Cloud] applications and could be subject to CCPA requirements:

- Nom
- Adresse postale
- Identifiant personnel unique
- Identifiant en ligne
- Adresse IP
- Adresse électronique
- Nom du compte

Les informations personnelles peuvent aussi inclure les renseignements liés à l’activité sur Internet ou sur d’autres réseaux électroniques. Cela inclut, entre autres :

- L’historique de navigation
- L’historique des recherches
- Les informations relatives à l’interaction d’un client avec un site web, une application ou une publicité

Even though CCPA covers a wide set of personal information, Adobe’s standard contract terms dictate that sensitive personal information (such as SSN, driver’s license information, financial account information, and biometric data) is generally prohibited from import and use in [!DNL Experience Cloud] applications.

## Comment les différents rôles et responsabilités de la CCPA s’appliquent-ils à [!DNL Experience Cloud]?

Selon la définition de la CCPA, s’appliquent à Adobe et à ses clients les rôles suivants :

- Les clients Adobe (la partie demandant la collecte et l’utilisation d’informations personnelles auprès des résidents de Californie) seraient considérés comme une **Entreprise**.
- Adobe, qui fournit le service, serait considéré comme un **Fournisseur de services**.

Compte tenu de cette relation et du langage contractuel d’Adobe, les divulgations à Adobe ne seraient probablement pas considérées comme une « vente » pour laquelle les entreprises auraient besoin de produire un avertissement et de proposer un droit d’opposition.

Cependant, les services Adobe peuvent être utilisés pour activer certains partages et transferts de données vers des tiers. Ces transferts vers des tiers pourraient être considérés comme une « vente » et nécessiter légalement un avertissement et un droit d’opposition.  Les clients doivent se rapprocher de leur service juridique pour examiner des cas d’utilisation spécifiques afin d’évaluer les exigences applicables.

## Combien de jours une entreprise a-t-elle pour répondre à la demande d’un client souhaitant consulter ou supprimer des informations personnelles ?

En supposant que l’entreprise ait recueilli des informations personnelles et qu’elle puisse authentifier ou vérifier l’identité d’un client californien particulier, la CCPA permet un délai de 45 jours pour satisfaire aux demandes des clients (sauf quelques exceptions).

## Quel est le rôle d’Adobe dans le cadre de la CCPA ?

En tant que Fournisseur de services, Adobe collecte et traite des informations personnelles pour le compte de l’Entreprise. Il est contractuellement tenu d’utiliser ces informations uniquement aux finalités spécifiques définies dans le contrat.

Compte tenu de cette relation et du langage contractuel d’Adobe, les divulgations à Adobe sont régies par les dispositions de la loi concernant les Fournisseurs de services et ne seraient probablement pas considérées comme une « vente » pour laquelle les entreprises doivent avertir leurs clients et leur proposer un droit d’opposition.

Les services Adobe peuvent être utilisés pour activer certains partages et transferts de données vers des tiers. Ces transferts vers des tiers pourraient être considérés comme une « vente » et nécessiter légalement un avertissement et un droit d’opposition.  Les clients doivent se rapprocher de leur service juridique pour examiner des cas d’utilisation spécifiques afin d’évaluer les exigences applicables.

## Comment puis-je remplir les exigences en matière de protection de la vie privée des clients que détermine la CCPA si je conserve certains types de données couverts par ces exigences ?

Once you have taken the necessary steps to authenticate CA consumers, Adobe Experience Platform [!DNL Privacy Service] allows you to submit consumer privacy requests to compatible [!DNL Experience Cloud] applications. Pour plus d’informations, consultez la [Présentation de Privacy Service](../home.md). For information on how your particular [!DNL Experience Cloud] applications can honor privacy requests, please refer to the guide on [Privacy Service and Experience Cloud applications](../experience-cloud-apps.md).

>[!NOTE]
>
>L’autorité de régulation californienne donnera prochainement des indications supplémentaires sur les types de données concernés par les demandes de protection de la vie privée des clients.

## Adobe propose-t-il d’autres outils pouvant être utiles pour répondre aux exigences de la CCPA ?

Les applications Adobe Experience Cloud fournissent des fonctionnalités de gestion et de gouvernance qui peuvent être utiles pour les besoins de confidentialité des entreprises. Parmi ces outils figurent l’étiquetage de l’utilisation des données, les contrôles d’accès basés sur les rôles, l’obscurcissement de l’adresse IP et les fonctions de hachage.

Adobe a reçu diverses certifications pour ses pratiques en matière de confidentialité et de sécurité, telles qu’une certification ISO 27001 et une validation RGPD de TrustArc.