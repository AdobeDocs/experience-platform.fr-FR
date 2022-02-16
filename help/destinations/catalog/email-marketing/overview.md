---
keywords: e-mail;e-mail;destinations d’e-mail
title: Présentation des destinations du marketing par email
type: Tutorial
description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 9d2e98c834eddcacf67de7caafef4717e38d80f8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 39%

---

# Présentation des destinations du marketing par email {#email-marketing-destinations}

## Présentation {#overview}

Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. Adobe Experience Platform s’intègre aux ESP en vous permettant d’activer des segments vers des destinations de marketing par e-mail.

Platform exporte vos segments sous la forme `.csv` et les envoie à l’emplacement de votre choix. Planifiez l’importation des données dans votre plateforme de marketing par e-mail à partir de l’emplacement de stockage activé dans [!DNL Platform]. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, consultez les articles sur les destinations individuelles.

## Destinations de marketing par e-mail prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les destinations de marketing par e-mail suivantes :

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Connexion à une nouvelle destination de marketing par e-mail {#connect-destination}

Pour envoyer des segments aux destinations de marketing par e-mail pour vos campagnes, Platform doit d’abord se connecter à la destination. Voir [tutoriel sur la création de destination](../../ui/connect-destination.md) pour plus d’informations sur la configuration d’une nouvelle destination.

## Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail {#best-practices}

### Sélection d’identités {#identity}

Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Il s’agit du champ dont vos identités utilisateur sont saisies. Généralement, ce champ correspond à l’adresse e-mail, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Reportez-vous au tableau ci-dessous pour connaître les identifiants uniques les plus courants et leur champ XDM dans le schéma.

| Identifiant unique | Champ XDM dans le schéma unifié |
|----------------- | ---------------------------|
| Adresse e-mail | `personalEmail.address` |
| Téléphone | `mobilePhone.number` |
| Identifiant du programme de fidélité | `Customer-defined XDM field` |

### Autres attributs de destination

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
| abonnement au segment | `segmentMembership.status` |

## Importez des données de l’emplacement de stockage vers la destination. {#import-data-into-destination}

Lisez les articles de destination de marketing par e-mail individuels pour savoir comment importer des données de l’emplacement de stockage vers les destinations :

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Marketing Cloud Salesforce](salesforce-marketing-cloud.md)

## Activer les segments vers les destinations de marketing par e-mail {#activate}

Pour plus d’informations sur l’activation des segments vers les destinations de marketing par e-mail, reportez-vous à la section [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md).

## Ressources supplémentaires

* [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md)
* [Création de destinations de marketing par e-mail et activation des données à l’aide de l’API Flow Service](../../api/connect-activate-batch-destinations.md)
