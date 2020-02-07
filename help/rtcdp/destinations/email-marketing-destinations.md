---
title: Destinations marketing par courrier électronique
seo-title: Destinations marketing par courrier électronique
description: Les fournisseurs de services de messagerie électronique (ESP) vous permettent de gérer vos activités de marketing par courrier électronique, comme l’envoi de campagnes par courrier électronique promotionnel.
seo-description: Les fournisseurs de services de messagerie électronique (ESP) vous permettent de gérer vos activités de marketing par courrier électronique, comme l’envoi de campagnes par courrier électronique promotionnel.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# Destinations marketing par courrier électronique {#email-marketing-destinations}

Les fournisseurs de services de messagerie (ESP) vous permettent de gérer vos activités de marketing par courrier électronique, telles que l’envoi de campagnes par courrier électronique promotionnel. La plate-forme de données clientes Adobe en temps réel s’intègre aux services de messagerie électronique (ESP) en vous permettant d’activer des segments vers des destinations de marketing par courrier électronique.

Pour envoyer des segments vers des destinations marketing par courrier électronique pour vos campagnes, Adobe Real-time CDP doit d’abord se connecter à la destination.

La connexion aux destinations de marketing par courrier électronique est un processus en trois étapes. Chacune des étapes est décrite plus loin dans cette page.

Dans le flux de destination de la connexion, décrit dans la section ci-dessous, connectez-vous à Amazon S3 ou SFTP. Le CDP en temps réel exporte vos segments sous forme `.csv` de fichiers `.txt` et les diffuse à l’emplacement souhaité. Planifiez l’importation de vos données dans votre plateforme de marketing par courrier électronique à partir de l’emplacement de stockage activé dans le CDP en temps réel. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, voir les articles de destination individuels.

## Étape 1 - Connecter la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez la destination marketing par courrier électronique à laquelle vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Connexion à la destination]**.

   ![Se connecter à la destination](/help/rtcdp/destinations/assets/connect-destination.png)

2. Dans l’assistant de connexion, sélectionnez le type **[!UICONTROL de]** connexion de votre emplacement de stockage. Vous pouvez choisir entre **Amazon S3**, **SFTP avec mot de passe**, **SFTP avec clé** SSH. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Connexion]**.

Pour les connexions **** S3, vous devez fournir votre ID de clé d&#39;accès et votre clé d&#39;accès secrète.

Pour le **protocole SFTP avec les connexions Mot de passe** , vous devez fournir Domaine, Port, Nom d’utilisateur et Mot de passe.

Pour **SFTP avec des connexions de clé** SSH, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

## Etape 2 - Sélection des champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés {#destination-attributes}

Au cours de cette étape, vous sélectionnez les champs à exporter vers des destinations marketing par courrier électronique.

![Attributs de destination](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identité {#identity}

Nous vous recommandons de sélectionner un identifiant unique dans votre schéma [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)d&#39;union. Il s’agit du champ dont l’identité des utilisateurs est masquée. Le plus souvent, ce champ correspond à l’adresse électronique, mais il peut également s’agir d’un ID de programme de fidélité ou d’un numéro de téléphone. Consultez le tableau ci-dessous pour connaître les identifiants uniques les plus courants et leur champ XDM dans le schéma unifié.

| Identifiant unique | Champ XDM dans le schéma unifié |
---------|----------
| Email Address | `personalEmail.address` |
| Téléphone | `mobilePhone.number` |
| Identifiant du programme de fidélité | `Customer-defined XDM field` |

### Autres attributs de destination

Dans le sélecteur de champ Schéma, choisissez les autres champs à exporter vers la destination du courrier électronique. Voici quelques options recommandées :

| Schéma | Champ XDM |
---------|----------
| Prénom | `person.name.firstName` |
| Nom | `person.name.lastName` |
| Téléphone | `mobilePhone.number` |
| Ville d&#39;adresse | `homeAddress.city` |
| État de l&#39;adresse | `homeAddress.stateProvince` |
| Adresse Code postal | `homeAddress.postalCode` |
| Anniversaire | `person.birthDayAndMonth` |

## Étape 3 - Importez les données de votre emplacement de stockage vers la destination

Consultez les articles de destination marketing par courrier électronique pour savoir comment importer des données de votre emplacement de stockage vers des destinations :

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Activer les segments vers les destinations marketing par courrier électronique

Pour plus d’informations sur la manière d’activer les segments vers les destinations marketing par courrier électronique, voir [Activation des données vers les destinations](/help/rtcdp/destinations/activate-destinations.md).