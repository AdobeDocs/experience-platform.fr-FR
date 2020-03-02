---
title: Destinations de marketing par e-mail
seo-title: Destinations de marketing par e-mail
description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
seo-description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
translation-type: ht
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# Destinations de marketing par e-mail {#email-marketing-destinations}

Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. La plateforme de données client en temps réel Adobe s’intègre aux ESP en vous permettant d’activer des segments vers des destinations de marketing par e-mail.

La plateforme de données client (CDP) en temps réel Adobe doit se connecter à la destination avant de pouvoir envoyer des segments vers des destinations de marketing par e-mail pour vos campagnes.

La connexion aux destinations de marketing par e-mail est un processus en trois étapes. Chaque étape est décrite plus loin dans cette page.

Dans le flux de connexion à la destination, décrit dans la section ci-dessous, connectez-vous à Amazon S3 ou SFTP. La plateforme CDP en temps réel exporte vos segments sous forme de fichiers `.csv` ou `.txt` et les diffuse sur l’emplacement de votre choix. Planifiez l’importation des données dans la plateforme de marketing par e-mail à partir de l’emplacement de stockage activé dans la plateforme CDP en temps réel. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, consultez les articles de destinations individuelles.

## Étape 1 - Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez la destination de marketing par e-mail à laquelle vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

   ![Se connecter à la destination](/help/rtcdp/destinations/assets/connect-destination.png)

2. Dans l’assistant de connexion, sélectionnez le **[!UICONTROL Type de connexion]** de votre emplacement de stockage. Vous pouvez choisir parmi **Amazon S3**, **le protocole SFTP avec mot de passe** et **le protocole SFTP avec clé SSH**. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

Pour les **connexions S3**, vous devez fournir un identifiant de clé d’accès et une clé d’accès secrète.

Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe.

Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH.

## Étape 2 - Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés {#destination-attributes}

Au cours de cette étape, vous sélectionnez les champs à exporter vers des destinations de marketing par e-mail.

![Attributs de destination](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identité {#identity}

Nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Il s’agit du champ dans lequel les identités de vos utilisateurs sont déclenchées. Généralement, ce champ correspond à l’adresse électronique, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Consultez le tableau ci-dessous pour connaître les identifiants uniques les plus courants et leur champ XDM dans le schéma unifié.

| Identifiant unique | Champ XDM dans le schéma unifié |
---------|----------
| Adresse électronique | `personalEmail.address` |
| Téléphone | `mobilePhone.number` |
| Identifiant du programme de fidélité | `Customer-defined XDM field` |

### Autres attributs de destination

Dans le sélecteur de champ Schéma, choisissez les autres champs à exporter vers la destination de courriel. Voici quelques options recommandées :

| Schéma | Champ XDM |
---------|----------
| Prénom | `person.name.firstName` |
| Nom | `person.name.lastName` |
| Téléphone | `mobilePhone.number` |
| Ville de l’adresse | `homeAddress.city` |
| État de l’adresse | `homeAddress.stateProvince` |
| Code postal de l’adresse | `homeAddress.postalCode` |
| Date de naissance | `person.birthDayAndMonth` |

## Étape 3 - Importer les données de l’emplacement de stockage vers la destination

Consultez les articles de destination de marketing par e-mail individuelle pour découvrir comment importer des données de l’emplacement de stockage vers les destinations :

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Activer les segments vers les destinations de marketing par e-mail

Pour plus d’informations sur l’activation des segments vers les destinations de marketing par e-mail, consultez [Activation des données vers des destinations](/help/rtcdp/destinations/activate-destinations.md).