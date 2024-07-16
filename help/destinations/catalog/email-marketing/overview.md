---
keywords: email;E-mail;e-mail;destinations d’email
title: Présentation des destinations du marketing par e-mail
type: Tutorial
description: Les fournisseurs de services de messagerie électronique (ESP) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. Découvrez quels ESP sont pris en charge en tant que destinations Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 4566d5241f287801569e0cfa5b86ea6210fd1638
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 60%

---

# Présentation des destinations du marketing par e-mail {#email-marketing-destinations}

## Présentation {#overview}

Les fournisseurs de service e-mail (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes par e-mail promotionnelles. Adobe Experience Platform s’intègre aux ESP en vous permettant d’activer les audiences vers les destinations de marketing par e-mail.

## Destinations de marketing par e-mail prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les destinations de marketing par e-mail suivantes :

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Catégories d’intérêt Mailchimp](mailchimp-interest-categories.md)
* [Balises Mailchimp](mailchimp-tags.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Fichiers) Oracle Eloqua](oracle-eloqua.md)
* [(Fichiers) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Se connecter à une nouvelle destination de marketing par e-mail {#connect-destination}

Pour envoyer des audiences vers des destinations de marketing par e-mail pour vos campagnes, Platform doit d’abord se connecter à la destination. Voir le [tutoriel sur la création de destinations](../../ui/connect-destination.md) pour des informations détaillées sur la configuration d’une nouvelle destination.

## Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail {#best-practices}

### Sélection d’identités {#identity}

Adobe recommande de sélectionner un identifiant unique à partir de votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Il s’agit du champ dans lequel les identités de vos utilisateurs sont déclenchées. Généralement, ce champ correspond à l’adresse e-mail, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Consultez le tableau ci-dessous pour connaître les identifiants uniques les plus courants ainsi que leur champ XDM dans le schéma.

| Identifiant unique | Champ XDM dans le schéma unifié |
|----------------- | ---------------------------|
| Adresse e-mail | `personalEmail.address` |
| Téléphone | `mobilePhone.number` |
| Identifiant du programme de fidélité | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Autres attributs de destination {#other-destination-attributes}

Dans le sélecteur de champ Schéma, choisissez les autres champs à exporter vers la destination de courriel. Voici quelques options recommandées :

| Schéma | Champ XDM |
|------ | ---------|
| Prénom | `person.name.firstName` |
| Nom | `person.name.lastName` |
| Téléphone | `mobilePhone.number` |
| Ville de l’adresse | `homeAddress.city` |
| État de l’adresse | `homeAddress.stateProvince` |
| Code postal de l’adresse | `homeAddress.postalCode` |
| Date de naissance | `person.birthDayAndMonth` |
| Appartenance à un segment | `segmentMembership.status` |

{style="table-layout:auto"}

## Activation des audiences vers les destinations de marketing par e-mail {#activate}

Certaines destinations de marketing par e-mail dans le catalogue exportent les profils en continu, via une intégration d’API à la destination.

D’autres destinations exportent les fichiers vers un emplacement de stockage dans le cloud. Une fois l’exportation terminée, vous devez importer les données de l’emplacement de stockage dans le cloud dans votre destination de marketing par e-mail.

Suivez les liens de la section [Destinations de marketing par e-mail prises en charge](#supported-destinations) pour savoir comment activer les audiences vers chaque destination de marketing par e-mail.

## Ressources supplémentaires {#additional-resources}

* [Activer les données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md)
* [Créer des destinations de marketing par e-mail et activer des données à l’aide de l’API Flow Service](../../api/connect-activate-batch-destinations.md)
