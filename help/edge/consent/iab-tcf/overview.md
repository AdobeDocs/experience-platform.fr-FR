---
title: Prise en charge d’IAB TCF 2.0 dans le SDK Web Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement IAB TCF 2.0 à l’aide du Adobe Experience Platform Web SDK
keywords: consentement ; setConsent ; Mélange de confidentialité des Profils ; Mélange de confidentialité des Événements d’expérience ; Mélange de confidentialité ; IAB TCF 2.0 ; CDP en temps réel ; Profil de données client en temps réel
translation-type: tm+mt
source-git-commit: 1c6238a0cf72230e019fd10d9a72f30444bd9fb9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# Prise en charge d’IAB TCF 2.0 dans le SDK Web Adobe Experience Platform

Le SDK Web Adobe Experience Platform prend en charge Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Ce guide présente les exigences de prise en charge d’IAB TCF 2.0 via Adobe Experience Platform Web SDK en intégration avec la plateforme de données client en temps réel, l’Audience Manager, les Événements d’expérience, Adobe Analytics et Experience Edge.

De plus, les guides suivants sont disponibles pour vous aider à apprendre comment intégrer IAB TCF 2.0 avec et sans Adobe Experience Platform Launch.

- [Avec Adobe Experience Platform Launch](./with-launch.md)
- [Sans Adobe Experience Platform Launch](./without-launch.md)

## Prise en main

Pour mettre en oeuvre le SDK Web avec IAB TCF 2.0, vous devez maîtriser le fonctionnement du modèle de données d’expérience (XDM) et des Événements d’expérience. Avant de début, veuillez consulter le document suivant :

- [Présentation](../../../xdm/home.md) du système du modèle de données d’expérience (XDM) : La normalisation et l&#39;interopérabilité sont des concepts clés de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

## Intégration Experience Platform

Pour envoyer des données de consentement à Adobe Experience Platform à l’aide du SDK, les éléments suivants sont requis :

- Jeu de données dont le schéma est basé sur la classe [!DNL XDM Individual Profile] et contient les champs de consentement TCF 2.0, activé pour l&#39;utilisation dans [!DNL Real-time Customer Profile].
- Une configuration de périphérie configurée avec Plateforme et le jeu de données activé par Profil mentionné ci-dessus.

Pour obtenir des instructions sur la création des jeux de données requis et sur la configuration des arêtes, consultez le guide sur la [conformité à la norme TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md).

## Intégration des Audiences Manager

Adobe Audience Manager (AAM) comprend la prise en charge d’IAB TCF 2.0, qui vous permet d’évaluer, d’honorer et de transmettre les choix de confidentialité des clients aux partenaires en aval. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Pour l&#39;intégrer à l&#39;Audience Manager via Adobe Experience Platform Web SDK, assurez-vous que vous disposez d&#39;une configuration de périphérie configurée pour transférer vers Adobe Audience Manager.

## Événements d’expérience et intégration Adobe Analytics

Alors que les audiences CDP et d’Audience Manager en temps réel suivent les préférences de consentement actuelles d’un client, les Événements d’expérience peuvent conserver les préférences de consentement d’un client qui étaient principales lors de la collecte du événement.

Pour recueillir des renseignements sur le consentement des événements, il faut :

- Jeu de données basé sur la classe [!DNL XDM Experience Event], avec le mixin de confidentialité [!DNL Experience Event].
- Une configuration de bord configurée avec le jeu de données [!DNL XDM Experience Event] ci-dessus.

Pour plus d’informations sur la conversion d’un Événement d’expérience XDM en accès Analytics, début en lisant la documentation [Présentation d’Analytics](../../data-collection/adobe-analytics/analytics-overview.md).

## Intégration du SDK Web Adobe Experience Platform

Les sections ci-dessous décrivent les principaux points d’intégration entre IAB TCF 2.0 et Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Même sans CDP ou Audience Manager en temps réel configuré, vous pouvez toujours intégrer IAB TCF 2.0 au SDK Web. Les préférences de consentement peuvent être utilisées pour contrôler la collecte des Événements d’expérience et la définition d’un cookie d’identité.

### Consentement par défaut

Le consentement par défaut est utilisé lorsqu’aucune préférence de consentement n’est déjà enregistrée pour un client. Cela signifie que les options de consentement par défaut peuvent contrôler le comportement du SDK Web Adobe Experience Platform et modifier en fonction de la région du client.

Par exemple, si vous avez un client qui n&#39;est pas dans la juridiction du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`, mais dans la juridiction du RGPD, le consentement par défaut peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

Pour plus d’informations sur le consentement par défaut, consultez la section [consentement par défaut](../../fundamentals/configuring-the-sdk.md#default-consent) de la documentation de configuration du SDK.

### Définition du consentement lors de la modification

Adobe Experience Platform Web SDK comporte une commande `setConsent` qui communique les préférences de consentement de votre client à tous les services d’Adobe à l’aide d’IAB TCF 2.0. Si vous effectuez une intégration avec CDP en temps réel, cela met à jour le profil de votre client. Si vous vous intégrez à l’Audience Manager, les informations de vos clients sont mises à jour. L’appel de cette méthode définit également un cookie avec une préférence de consentement tout ou rien qui contrôle si les futurs Événements d’expérience sont autorisés à être envoyés. Il est prévu que cette action soit appelée chaque fois que le consentement change. Lors des prochains chargements de page, le cookie de consentement Experience Edge sera lu pour déterminer si des Événements d’expérience peuvent être envoyés et si un cookie d’identité peut être défini.

Tout comme l’intégration d’IAB TCF 2.0 de l’Audience Manager, Experience Edge donne son consentement lorsqu’un client a donné son consentement explicite aux fins suivantes :

- **Objectif 1 :** Stocker et/ou accéder aux informations sur un périphérique
- **Objectif 10 :** Développer et améliorer les produits
- **Objectif spécial 1 :** assurer la sécurité, prévenir les fraudes et déboguer. (Conformément à la réglementation du CCI relative au TCF, celle-ci est toujours consentante)
- **Adobe Fournisseur Autorisation :** Consentement pour Adobe (Fournisseur 565)

Pour plus d&#39;informations sur la commande `setConsent`, consultez la documentation sur [Supporting Consent](../../consent/supporting-consent.md).

### Ajouter le consentement aux Événements d’expérience

Adobe Experience Platform Web SDK comporte une commande `sendEvent` qui collecte un Événement d’expérience. Si vous effectuez une intégration avec les Événements d’expérience ou Adobe Analytics et souhaitez obtenir les préférences de consentement pour chaque Événement d’expérience, vous devez ajouter les informations de consentement à chaque commande `sendEvent`.

Pour plus d&#39;informations sur la commande `sendEvent`, consultez la documentation relative aux [événements de suivi](../../fundamentals/tracking-events.md).

## Étapes suivantes

Maintenant que vous avez une connaissance de base de la structure de transparence et de consentement IAB 2.0, consultez l&#39;un des guides sur l&#39;utilisation de la structure de transparence et de consentement IAB TCF 2.0 [avec Adobe Experience Platform Launch](./with-launch.md) ou [sans Adobe Experience Platform Launch](./without-launch.md).
