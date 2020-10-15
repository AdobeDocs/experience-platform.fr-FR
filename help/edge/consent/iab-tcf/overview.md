---
title: Présentation de la structure de transparence et de consentement IAB 2.0
seo-title: Prise en charge des préférences de consentement du SDK Web Adobe Experience Platform par Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Découvrez comment prendre en charge les préférences de consentement IAB TCF 2.0 avec le SDK Web Experience Platform
seo-description: Découvrez comment prendre en charge les préférences de consentement IAB TCF 2.0 avec le SDK Web Experience Platform
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: b82ee2508558f76e3ad56cbb8405abe9bfb235f6
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# Présentation de la structure de transparence et de consentement IAB 2.0

Le Adobe Experience Platform Web SDK (AEP Web SDK) prend en charge Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Ce guide présente les exigences de prise en charge d’IAB TCF 2.0 par le biais du SDK Web AEP, en les intégrant à la plateforme de données client en temps réel, à l’Audience Manager, aux Événements d’expérience, au Adobe Analytics et à Experience Edge.

De plus, les guides suivants sont disponibles pour vous aider à apprendre comment intégrer IAB TCF 2.0 avec et sans Adobe Experience Platform Launch.

- [Avec Adobe Experience Platform Launch](./with-launch.md)
- [Sans Adobe Experience Platform Launch](./without-launch.md)

## Prise en main

Pour mettre en oeuvre le SDK Web AEP avec IAB TCF 2.0, vous devez maîtriser le fonctionnement du modèle de données d’expérience (XDM) et des Événements d’expérience. Avant de début, veuillez consulter le document suivant :

- [Présentation](../../../xdm/home.md)du système du modèle de données d’expérience (XDM) : La normalisation et l&#39;interopérabilité sont des concepts clés de Adobe Experience Platform. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

## Intégration en temps réel de la plateforme de données clientes

Basée sur Adobe Experience Platform, la plateforme de données client en temps réel Adobe (CDP en temps réel) vous permet de rassembler des données connues et anonymes provenant de plusieurs sources d’entreprise. Cela vous permet de créer des profils clients qui peuvent être utilisés pour fournir des expériences client personnalisées sur tous les canaux et appareils en temps réel. Pour envoyer des données de consentement au CDP en temps réel par l’intermédiaire du SDK Web AEP, les éléments suivants sont requis :

- Jeu de données basé sur la [!DNL XDM Individual Profile] classe, activé pour une utilisation dans [!DNL Real-time Customer Profile], avec le mixin de confidentialité du Profil.
- Une configuration de périphérie configurée avec le CDP en temps réel et le jeu de données de profil mentionné ci-dessus.

Consultez le didacticiel sur la [création de jeux de données pour capturer le consentement](../../../rtcdp/privacy/iab/dataset-preparation.md) TCF 2.0 pour savoir comment créer le jeu de données requis.

Pour obtenir des instructions sur la création de la configuration de bord, reportez-vous à la présentation [de la conformité](../../../rtcdp/privacy/privacy-overview.md) IAB TCF 2.0.

## Intégration des Audiences Manager

Adobe Audience Manager (AAM) comprend la prise en charge d’IAB TCF 2.0, qui vous permet d’évaluer, d’honorer et de transmettre les choix de confidentialité des clients aux partenaires en aval. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Pour l’intégrer à l’Audience Manager via le SDK Web AEP, assurez-vous que vous disposez d’une configuration de périphérie configurée pour le transfert vers Adobe Audience Manager.

## Événements d’expérience et intégration Adobe Analytics

Alors que les audiences CDP et d’Audience Manager en temps réel suivent les préférences de consentement actuelles d’un client, les Événements d’expérience peuvent conserver les préférences de consentement d’un client qui étaient principales lors de la collecte du événement.

Pour recueillir des renseignements sur le consentement des événements, il faut :

- Jeu de données basé sur la [!DNL XDM Experience Event] classe, avec le mixin [!DNL Experience Event] vie privée.
- Une configuration de bord configurée avec le jeu de données [!DNL XDM Experience Event] ci-dessus.

Pour plus d’informations sur la conversion d’un Événement d’expérience XDM en accès Analytics, début en lisant la documentation d’aperçu [d’](../../data-collection/adobe-analytics/analytics-overview.md) Analytics.

## Intégration du SDK Web AEP

Les sections ci-dessous décrivent les principaux points d’intégration entre l’IAB TCF 2.0 et le SDK Web AEP.

>[!NOTE]
>
>Même sans CDP ou Audience Manager en temps réel configuré, vous pouvez toujours intégrer IAB TCF 2.0 au SDK Web. Les préférences de consentement peuvent être utilisées pour contrôler la collecte des Événements d’expérience et la définition d’un cookie d’identité.

### Consentement par défaut

Le consentement par défaut est utilisé lorsqu’aucune préférence de consentement n’est déjà enregistrée pour un client. En d’autres termes, les options de consentement par défaut peuvent contrôler le comportement du SDK Web AEP et les modifier en fonction de la région du client.

Par exemple, si vous avez un client qui n&#39;est pas dans la juridiction du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`, mais dans la juridiction du RGMD, le consentement par défaut peut être défini sur `pending`. Votre plate-forme de gestion des cloud (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à l’IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

Pour plus d’informations sur le consentement par défaut, reportez-vous à la section [de consentement par](../../fundamentals/configuring-the-sdk.md#default-consent) défaut de la documentation de configuration du SDK.

### Définition du consentement lors de la modification

Le SDK Web AEP comporte une `setConsent` commande qui communique les préférences de consentement de votre client à tous les services d’Adobe à l’aide d’IAB TCF 2.0. Si vous effectuez une intégration avec le CDP en temps réel, cela met à jour le profil de votre client. Si vous vous intégrez à l’Audience Manager, les informations de vos clients sont mises à jour. L’appel de cette méthode définit également un cookie avec une préférence de consentement tout ou rien qui contrôle si les futurs Événements d’expérience sont autorisés à être envoyés. Il est prévu que cette action soit appelée chaque fois que le consentement change. Lors des prochains chargements de page, le cookie de consentement Experience Edge sera lu pour déterminer si des Événements d’expérience peuvent être envoyés et si un cookie d’identité peut être défini.

Tout comme l’intégration d’IAB TCF 2.0 de l’Audience Manager, Experience Edge donne son consentement lorsqu’un client a donné son consentement explicite aux fins suivantes :

- **Objectif 1 :** Stocker et/ou accéder aux informations sur un périphérique
- **Objet 10 :** Développer et améliorer les produits
- **But spécial 1 :** Assurer la sécurité, prévenir les fraudes et déboguer. (Conformément à la réglementation du CCI relative au TCF, celle-ci est toujours consentante)
- **Adobe Fournisseur Autorisation :** Consentement pour Adobe (fournisseur 565)

Pour plus d&#39;informations sur la `setConsent` commande, lisez la documentation sur [Supporting Consent](../../consent/supporting-consent.md).

### Ajouter le consentement aux Événements d’expérience

Le SDK Web AEP comporte une `sendEvent` commande qui collecte un Événement d’expérience. Si vous effectuez une intégration avec les Événements d’expérience ou Adobe Analytics et souhaitez que les préférences de consentement s’appliquent à chaque Événement d’expérience, vous devez ajouter les informations de consentement à chaque `sendEvent` commande.

Pour plus d&#39;informations sur la `sendEvent` commande, consultez la documentation sur les événements [de](../../fundamentals/tracking-events.md)suivi.

## Étapes suivantes

Maintenant que vous avez une connaissance de base du Cadre de transparence et de consentement de l’IAB 2.0, veuillez consulter l’un des guides sur l’utilisation de l’IAB TCF 2.0 [avec Adobe Experience Platform Launch](./with-launch.md) ou [sans Adobe Experience Platform Launch](./without-launch.md).
