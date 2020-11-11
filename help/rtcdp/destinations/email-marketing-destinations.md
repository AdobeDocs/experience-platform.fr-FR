---
keywords: email;Email;e-mail;email destinations
title: Destinations de marketing par e-mail
seo-title: Destinations de marketing par e-mail
type: Tutorial
description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
seo-description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
translation-type: tm+mt
source-git-commit: 5238d98db0554d34c2b0bcd28b64354f544faa0f
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 44%

---


# Destinations de marketing par e-mail {#email-marketing-destinations}

Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. La plateforme de données client en temps réel Adobe s’intègre aux ESP en vous permettant d’activer des segments vers des destinations de marketing par e-mail.

La plateforme de données client (CDP) en temps réel Adobe doit se connecter à la destination avant de pouvoir envoyer des segments vers des destinations de marketing par e-mail pour vos campagnes.

La connexion aux destinations de marketing par e-mail est un processus en trois étapes. Chaque étape est décrite plus loin dans cette page.

Dans le flux de connexion à la destination, décrit dans la section ci-dessous, connectez-vous à Amazon S3 ou SFTP. La plateforme CDP en temps réel exporte vos segments sous forme de fichiers `.csv` ou `.txt` et les diffuse sur l’emplacement de votre choix. Planifiez l’importation des données dans la plateforme de marketing par e-mail à partir de l’emplacement de stockage activé dans la plateforme CDP en temps réel. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, consultez les articles de destinations individuelles.

## Configurer la destination {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select the email marketing destination that you want to connect to, then select **[!UICONTROL Configure]**.

![Se connecter à la destination](./assets/connect-email-marketing.png)

In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your email marketing destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your email marketing destination. Dans le sélecteur de type **** Connexion, vous pouvez choisir entre Amazon S3, SFTP avec mot de passe ou SFTP avec clé SSH. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

- For **S3 connections**, you must provide your Amazon Access Key ID and Secret Access Key.
- For **SFTP with Password** connections, you must provide Domain, Port, Username, and Password for your SFTP server.
- For **SFTP with SSH Key** connections, you must provide Domain, Port, Username, and SSH Key for your SFTP server.

À l’étape **[!UICONTROL Configuration]** , saisissez un nom et une description pour votre nouvelle destination, ainsi que le format de fichier des fichiers exportés.

Si vous avez sélectionné Amazon S3 en tant qu’option d’enregistrement à l’étape précédente, insérez le nom du compartiment et le chemin d’accès au dossier dans la destination de l’enregistrement cloud où les fichiers seront distribués. Pour l’option enregistrement SFTP, insérez le chemin d’accès au dossier dans lequel les fichiers seront distribués.

Cette étape vous permet également de sélectionner tout cas d’utilisation marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données.

![Etape de configuration du courrier électronique](./assets/email-setup-step.png)

## Sélectionner les membres de segment à inclure dans vos exportations de destination {#select-segments}

On the **[!UICONTROL Select Segments]** page, select which segments to send to the destination. Pour en savoir plus sur les champs des sections ci-dessous.

![Sélectionner des segments](/help/rtcdp/destinations/assets/email-select-segments.png)

## Configuration des noms de fichier

Pour plus d&#39;informations sur les options d&#39;édition des noms de fichier, reportez-vous à l&#39;étape [Configurer](/help/rtcdp/destinations/activate-destinations.md#configure) du didacticiel Activer les destinations.

## Select attributes - Select which schema fields to use as destination attributes in your exported files {#destination-attributes}

Au cours de cette étape, vous sélectionnez les champs à exporter vers les destinations marketing par courriel, ainsi que le marquage des champs obligatoires.

![Attributs de destination](/help/rtcdp/destinations/assets/recommended-attributes.png)

Pour plus d&#39;informations sur cette étape, reportez-vous à l&#39;étape [Sélectionner des attributs](/help/rtcdp/destinations/activate-destinations.md#select-attributes) du didacticiel Activer les destinations.

### Identité {#identity}

Nous vous recommandons de sélectionner un identifiant unique dans votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Il s’agit du champ dans lequel les identités de vos utilisateurs sont déclenchées. Généralement, ce champ correspond à l’adresse électronique, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Consultez le tableau ci-dessous pour connaître les identifiants uniques les plus courants et leur champ XDM dans le schéma.

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
| Appartenance à un segment | `segmentMembership.status` |

## Importer des données depuis l&#39;emplacement de votre enregistrement vers la destination

Consultez les articles de destination de marketing par e-mail individuelle pour découvrir comment importer des données de l’emplacement de stockage vers les destinations :

- [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
- [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
- [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
- [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Activer les segments vers les destinations de marketing par e-mail

Pour plus d’informations sur l’activation des segments vers les destinations de marketing par e-mail, consultez [Activation des données vers des destinations](/help/rtcdp/destinations/activate-destinations.md).

## Ressources supplémentaires

- [Activer les données vers les destinations](/help/rtcdp/destinations/activate-destinations.md)
- [Créez des destinations de marketing par courrier électronique et activez les données à l’aide de l’API du service de flux.](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)