---
title: Prise en charge d’IAB TCF 2.0 dans Adobe Experience Platform Web SDK
description: Découvrez comment prendre en charge les préférences de consentement IAB TCF 2.0 à l’aide de Adobe Experience Platform Web SDK
keywords: consentement;setConsent;Groupe de champs Confidentialité du profil;Groupe de champs Confidentialité des événements d’expérience;Groupe de champs Confidentialité;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Prise en charge d’IAB TCF 2.0 dans Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK prend en charge Interactive Advertising Bureau Transparency &amp; Consent Framework version 2.0 (IAB TCF 2.0). Ce guide décrit la configuration requise pour la prise en charge d’IAB TCF 2.0 via Adobe Experience Platform Web SDK, qui s’intègre à Adobe Real-Time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics et Edge Network.

En outre, les guides suivants sont disponibles pour vous aider à apprendre à intégrer IAB TCF 2.0 avec et sans balises.

- [Avec des balises](./with-tags.md)
- [Sans balises](./without-tags.md)

## Commencer

Pour mettre en œuvre le Web SDK avec IAB TCF 2.0, vous devez posséder une bonne compréhension du modèle de données d’expérience (XDM) et des événements d’expérience. Avant de commencer, veuillez consulter le document suivant :

- [Présentation du système de modèle de données d’expérience (XDM)](../../../xdm/home.md) : la normalisation et l’interopérabilité sont les concepts clés de Adobe Experience Platform. [!DNL Experience Data Model (XDM)], piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

## Intégration d’Experience Platform

Pour envoyer des données de consentement à Adobe Experience Platform à l’aide de SDK, les éléments suivants sont requis :

- Jeu de données dont le schéma est basé sur la classe [!DNL XDM Individual Profile] et contient des champs de consentement TCF 2.0, activés pour une utilisation dans [!DNL Real-Time Customer Profile].
- Un flux de données configuré avec Experience Platform et le jeu de données activé pour Profil mentionné ci-dessus.

Reportez-vous au guide sur la conformité [TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) pour obtenir des instructions sur la création des jeux de données et des trains de données requis.

## Intégration d’Audience Manager

Adobe Audience Manager (AAM) comprend la prise en charge de l’IAB TCF 2.0, qui vous permet d’évaluer, d’honorer et de transférer les choix de confidentialité des clients aux partenaires en aval. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Pour l’intégration à Audience Manager via Adobe Experience Platform Web SDK, assurez-vous qu’un flux de données est configuré pour être transféré vers Adobe Audience Manager.

## Événements d’expérience et intégration à Adobe Analytics

Alors que les audiences Real-Time CDP et Audience Manager effectuent le suivi des préférences de consentement actuelles d’un client, les événements d’expérience peuvent contenir les préférences de consentement d’un client qui étaient actives lors de la collecte de l’événement.

Pour collecter des informations de consentement sur les événements, les éléments suivants sont requis :

- Un jeu de données basé sur la classe [!DNL XDM Experience Event], avec le groupe de champs de schéma de confidentialité [!DNL Experience Event].
- Un flux de données configuré avec le jeu de données [!DNL XDM Experience Event] ci-dessus.

Pour plus d’informations sur la conversion d’un événement d’expérience XDM en accès Analytics, voir [Envoi de données à Adobe Analytics à l’aide de Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Intégration de Adobe Experience Platform Web SDK

Les sections ci-dessous décrivent les principaux points d’intégration entre IAB TCF 2.0 et Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Même sans configuration de Real-Time CDP ou d’Audience Manager, vous pouvez toujours intégrer IAB TCF 2.0 à Web SDK. Les préférences de consentement peuvent être utilisées pour contrôler la collecte des événements d’expérience et la définition d’un cookie d’identité.

### Consentement par défaut

Le consentement par défaut est utilisé lorsqu’aucune préférence de consentement n’est déjà enregistrée pour un client. Cela signifie que les options de consentement par défaut peuvent contrôler le comportement de Adobe Experience Platform Web SDK et changer en fonction de la région d’un client.

Par exemple, si vous avez un client qui ne relève pas de la juridiction du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`, mais dans la juridiction du RGPD, le consentement par défaut peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut. Voir [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) pour plus d’informations.

### Définition du consentement lorsqu’il change

Adobe Experience Platform Web SDK comporte une commande `setConsent` qui communique les préférences de consentement de votre client à tous les services Adobe à l’aide de l’IAB TCF 2.0. Si vous effectuez une intégration à Real-Time CDP, le profil de votre client est mis à jour. Si vous effectuez une intégration à Audience Manager, les informations de votre client sont mises à jour. L’appel à cette méthode définit également un cookie avec une préférence de consentement en tout ou rien qui contrôle si l’envoi de futurs événements d’expérience est autorisé. Il est prévu d’appeler cette action chaque fois que le consentement change. Lors des chargements futurs de la page, le cookie de consentement d’Edge Network sera lu pour déterminer si des événements d’expérience peuvent être envoyés et si un cookie d’identité peut être défini.

Tout comme l’intégration IAB TCF 2.0 d’Audience Manager, Edge Network donne son consentement lorsqu’un client a donné son consentement explicite aux fins suivantes :

- **Objectif 1 :** Stocker et/ou accéder à des informations sur un appareil
- **Objectif 10 :** développer et améliorer des produits
- **Objectif spécial 1 :** assurer la sécurité, prévenir la fraude et déboguer. (Conformément aux règlements du TCF de l&#39;IAB, ceci est toujours accepté)
- **Autorisation du fournisseur Adobe :** consentement pour Adobe (fournisseur 565)

Pour plus d’informations sur la commande `setConsent`, consultez la documentation dédiée de Web SDK sur [setConsent](../../../web-sdk/commands/setconsent.md).

### Ajout de consentement aux événements d’expérience

Adobe Experience Platform Web SDK comporte une commande [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) qui collecte un événement d’expérience. Si vous effectuez une intégration aux événements d’expérience ou à Adobe Analytics et que vous souhaitez connaître les préférences de consentement pour chaque événement d’expérience, ajoutez des informations de consentement à chaque commande `sendEvent`.

## Étapes suivantes

Maintenant que vous connaissez les principes de base du Transparency &amp; Consent Framework 2.0 de l’IAB, reportez-vous à l’un des guides sur l’utilisation du IAB TCF 2.0 [avec balises](./with-tags.md) ou [sans balises](./without-tags.md).
