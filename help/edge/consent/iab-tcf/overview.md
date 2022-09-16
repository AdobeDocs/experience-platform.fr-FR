---
title: Prise en charge du TCF 2.0 de l’IAB dans le SDK Web de Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement du TCF 2.0 de l’IAB à l’aide du SDK Web de Adobe Experience Platform
keywords: consentement;setConsent;groupe de champs de confidentialité du profil;groupe de champs de confidentialité des événements d’expérience;groupe de champs de confidentialité;IAB TCF 2.0;plateforme de données clients en temps réel;profil de données client en temps réel
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Prise en charge du TCF 2.0 de l’IAB dans le SDK Web de Adobe Experience Platform

Le SDK web Adobe Experience Platform prend en charge la version 2.0 de l’Interactive Advertising Bureau Transparency &amp; Consent Framework (IAB TCF 2.0). Ce guide présente les exigences relatives à la prise en charge du TCF 2.0 de l’IAB par le biais du SDK web Adobe Experience Platform grâce à l’intégration à Real-time Customer Data Platform, à l’Audience Manager, aux événements d’expérience, à Adobe Analytics et à Experience Edge.

En outre, les guides suivants sont disponibles pour vous aider à apprendre comment intégrer IAB TCF 2.0 avec et sans balises.

- [Avec des balises](./with-launch.md)
- [Sans balises](./without-launch.md)

## Prise en main

Pour mettre en oeuvre le SDK Web avec IAB TCF 2.0, vous devez avoir une compréhension pratique du modèle de données d’expérience (XDM) et des événements d’expérience. Avant de commencer, consultez le document suivant :

- [Présentation du système de modèle de données d’expérience (XDM)](../../../xdm/home.md): La normalisation et l’interopérabilité sont les concepts clés de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], piloté par Adobe, est un effort de normalisation des données d’expérience client et de définition de schémas pour la gestion de l’expérience client.

## Intégration des Experience Platform

Pour envoyer des données de consentement à Adobe Experience Platform à l’aide du SDK, les conditions suivantes sont requises :

- Un jeu de données dont le schéma est basé sur la variable [!DNL XDM Individual Profile] et contient des champs de consentement TCF 2.0, activés pour une utilisation dans [!DNL Real-time Customer Profile].
- Un flux de données configuré avec Platform et le jeu de données activé pour Profile mentionné ci-dessus.

Reportez-vous au guide sur la [Conformité TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) pour obtenir des instructions sur la création des jeux de données et de la chaîne de données requis.

## Intégration des Audiences Manager

Adobe Audience Manager (AAM) prend en charge IAB TCF 2.0, qui vous permet d’évaluer, d’honorer et de transférer les choix de confidentialité des clients aux partenaires en aval. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Pour l’intégrer à Audience Manager via le SDK Web de Adobe Experience Platform, assurez-vous qu’un flux de données est configuré pour être transféré vers Adobe Audience Manager.

## Événements d’expérience et intégration d’Adobe Analytics

Alors que la plateforme de données clients en temps réel et les audiences de l’Audience Manager effectuent le suivi des préférences de consentement actuelles d’un client, les événements d’expérience peuvent contenir les préférences de consentement d’un client qui étaient principales lorsque l’événement a été collecté.

Pour collecter des informations de consentement sur les événements, vous devez :

- Un jeu de données basé sur la variable [!DNL XDM Experience Event] , avec la propriété [!DNL Experience Event] groupe de champs de schéma de confidentialité.
- Un flux de données configuré avec la variable [!DNL XDM Experience Event] jeu de données ci-dessus.

Pour plus d’informations sur la conversion d’un événement d’expérience XDM en accès Analytics, commencez par lire le [Présentation d’Analytics](../../data-collection/adobe-analytics/analytics-overview.md) documentation.

## Intégration du SDK Web Adobe Experience Platform

Les sections ci-dessous décrivent les principaux points d’intégration entre IAB TCF 2.0 et Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Même sans la configuration de la plateforme de données clients en temps réel ou de l’Audience Manager, vous pouvez toujours intégrer IAB TCF 2.0 au SDK Web. Les préférences de consentement peuvent être utilisées pour contrôler la collecte des événements d’expérience et la définition d’un cookie d’identité.

### Consentement par défaut

Le consentement par défaut est utilisé lorsqu’aucune préférence de consentement n’est déjà enregistrée pour un client. Cela signifie que les options de consentement par défaut peuvent contrôler le comportement du SDK Web de Adobe Experience Platform et changer en fonction de la région du client.

Par exemple, si vous avez un client qui n’est pas sous la juridiction du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`, mais dans la juridiction du RGPD, le consentement par défaut peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

Pour plus d’informations sur le consentement par défaut, reportez-vous à la section [section de consentement par défaut](../../fundamentals/configuring-the-sdk.md#default-consent) dans la documentation sur la configuration du SDK.

### Définition du consentement lors de la modification

Le SDK Web de Adobe Experience Platform comporte une `setConsent` qui communique les préférences de consentement de votre client à tous les services Adobe à l’aide du TCF 2.0 de l’IAB. Si vous intégrez la plateforme de données clients en temps réel, cela met à jour le profil de votre client. Si vous effectuez une intégration à Audience Manager, les informations de votre client sont mises à jour. L’appel de cette méthode définit également un cookie avec une préférence de consentement &quot;tout ou rien&quot; qui contrôle si les futurs événements d’expérience sont autorisés à être envoyés. Cette action est appelée chaque fois que le consentement est modifié. Lors des chargements ultérieurs de la page, le cookie de consentement Experience Edge sera lu pour déterminer si des événements d’expérience peuvent être envoyés et si un cookie d’identité peut être défini.

Tout comme l’intégration du TCF 2.0 de l’IAB à l’Audience Manager, Experience Edge donne son consentement lorsqu’un client a fourni son consentement explicite aux fins suivantes :

- **Objectif 1 :** Stocker et/ou accéder aux informations sur un appareil
- **Objectif 10 :** Développement et amélioration des produits
- **Objectif spécial 1 :** Assurez la sécurité, évitez les fraudes et déboguez. (Conformément aux réglementations du TCF de l’IAB, cela est toujours accepté)
- **Autorisation du fournisseur d’Adobe :** Consentement pour l’Adobe (fournisseur 565)

Pour plus d’informations sur la variable `setConsent` , lisez la documentation sur [Prise en charge du consentement](../../consent/supporting-consent.md).

### Ajout de consentement aux événements d’expérience

Le SDK Web de Adobe Experience Platform comporte une `sendEvent` qui collecte un événement d’expérience. Si vous intégrez des événements d’expérience ou Adobe Analytics et souhaitez connaître les préférences de consentement pour chaque événement d’expérience, vous devez ajouter les informations de consentement à chaque événement d’expérience. `sendEvent` .

Pour plus d’informations sur la variable `sendEvent` , lisez la documentation sur [suivi des événements](../../fundamentals/tracking-events.md).

## Étapes suivantes

Maintenant que vous connaissez de base le Transparency &amp; Consent Framework 2.0 de l’IAB, consultez l’un des guides sur l’utilisation du TCF 2.0 de l’IAB. [avec des balises](./with-launch.md) ou [sans balises](./without-launch.md).
