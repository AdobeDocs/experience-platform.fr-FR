---
keywords: email;E-mail;e-mail;destinations d’email
title: Présentation des destinations du marketing par e-mail
type: Tutorial
description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 9d2e98c834eddcacf67de7caafef4717e38d80f8
workflow-type: ht
source-wordcount: '387'
ht-degree: 100%

---

# Présentation des destinations du marketing par e-mail {#email-marketing-destinations}

## Présentation {#overview}

Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. Adobe Experience Platform s’intègre aux ESP en vous permettant d’activer des segments vers des destinations de marketing par e-mail.

Platform exporte vos segments sous forme de fichiers `.csv` et les diffuse vers votre emplacement préféré. Planifiez l’importation des données dans la plateforme de marketing par e-mail à partir de l’emplacement de stockage activé dans [!DNL Platform]. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, consultez les articles de destinations individuelles.

## Destinations de marketing par e-mail prises en charge {#supported-destinations}

Adobe Experience Platform prend en charge les destinations de marketing par e-mail suivantes :

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Se connecter à une nouvelle destination de marketing par e-mail {#connect-destination}

La plateforme doit tout d’abord se connecter à la destination avant de pouvoir envoyer des segments vers des destinations de marketing par e-mail pour vos campagnes. Voir le [tutoriel sur la création de destinations](../../ui/connect-destination.md) pour des informations détaillées sur la configuration d’une nouvelle destination.

## Bonnes pratiques lors de l’activation d’audiences vers des destinations de marketing par e-mail {#best-practices}

### Sélection d’identités {#identity}

Adobe recommande de sélectionner un identifiant unique à partir de votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Il s’agit du champ dans lequel les identités de vos utilisateurs sont déclenchées. Généralement, ce champ correspond à l’adresse e-mail, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Consultez le tableau ci-dessous pour connaître les identifiants uniques les plus courants ainsi que leur champ XDM dans le schéma.

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
| Appartenance à un segment | `segmentMembership.status` |

## Importer les données de l’emplacement de stockage vers la destination {#import-data-into-destination}

Consultez les articles de destination de marketing par e-mail individuels pour découvrir comment importer des données de l’emplacement de stockage vers les destinations :

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Activer les segments vers des destinations de marketing par e-mail {#activate}

Pour plus d’informations sur l’activation des segments vers les destinations de marketing par e-mail, reportez-vous à la section [Activer les données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md).

## Ressources supplémentaires

* [Activer les données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md)
* [Créer des destinations de marketing par e-mail et activer des données à l’aide de l’API Flow Service](../../api/connect-activate-batch-destinations.md)
