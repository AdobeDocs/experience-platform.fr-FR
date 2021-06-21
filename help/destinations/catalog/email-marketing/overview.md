---
keywords: e-mail;e-mail;destinations d’e-mail
title: Présentation des destinations du marketing par email
type: Tutorial
description: Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 21%

---

# Présentation des destinations du marketing par email {#email-marketing-destinations}

Les fournisseurs de service de messagerie électronique (ESP, Email Service Providers) vous permettent de gérer vos activités de marketing par e-mail, comme l’envoi de campagnes promotionnelles par e-mail. Adobe Experience Platform s’intègre aux ESP en vous permettant d’activer des segments vers des destinations de marketing par e-mail.

Pour envoyer des segments aux destinations de marketing par e-mail pour vos campagnes, Platform doit d’abord se connecter à la destination.

La connexion aux destinations de marketing par e-mail est un processus en trois étapes ([configurer la destination](#connect-destination), [activer les segments](#select-segments), [importer les données de l’emplacement de stockage vers la destination](#import-data-into-destination)). Chaque étape est décrite plus loin dans cette page.

Dans le flux de connexion à la destination, décrit dans la section ci-dessous, connectez-vous à [!DNL Amazon S3] ou [!DNL SFTP]. Platform exporte vos segments sous la forme de fichiers `.csv` et les diffuse à l’emplacement de votre choix. Planifiez l’importation des données dans votre plateforme de marketing par e-mail à partir de l’emplacement de stockage activé dans [!DNL Platform]. Le processus d’importation des données varie pour chaque partenaire. Pour plus d’informations, consultez les articles sur les destinations individuelles.

## Configurer la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez la destination de marketing par e-mail à laquelle vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Configurer]**.

![Se connecter à la destination](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

À l’étape **[!UICONTROL Compte]**, si vous aviez auparavant configuré une connexion à votre destination de marketing par e-mail, sélectionnez **[!UICONTROL Compte existant]** et sélectionnez votre connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de marketing par e-mail. Dans le sélecteur **[!UICONTROL Type de connexion]**, vous pouvez choisir entre [!UICONTROL Amazon S3], [!UICONTROL Azure Blob], [!UICONTROL SFTP avec mot de passe] ou [!UICONTROL SFTP avec clé SSH]. Renseignez les informations ci-dessous, en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter]**.

- Pour les **connexions S3**, vous devez fournir votre identifiant de clé d’accès Amazon et votre clé d’accès secrète.
- Pour les connexions **SFTP avec mot de passe**, vous devez fournir le domaine, le port, le nom d’utilisateur et le mot de passe pour votre serveur SFTP.
- Pour les connexions **SFTP avec clé SSH**, vous devez fournir le domaine, le port, le nom d’utilisateur et la clé SSH pour votre serveur SFTP.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés sous la section **[!UICONTROL Clé]** . Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].

À l’étape **[!UICONTROL Authentification]**, saisissez un nom et une description pour votre nouvelle destination, ainsi que le format de fichier des fichiers exportés.

Si vous avez sélectionné Amazon S3 comme option de stockage à l’étape précédente, insérez le nom du compartiment et le chemin du dossier dans la destination de stockage dans le cloud où les fichiers seront distribués. Pour l’option de stockage SFTP, insérez le chemin du dossier dans lequel les fichiers seront distribués.

À cette étape, vous pouvez également sélectionner toute action marketing qui doit s’appliquer à cette destination. Les actions marketing indiquent l’intention pour laquelle les données seront exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, consultez la [Présentation des stratégies d’utilisation des données](../../../data-governance/policies/overview.md).

![Étape de configuration des emails](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Sélectionnez les membres de segment à inclure dans vos exportations de destination {#select-segments}

Sur la page **[!UICONTROL Sélectionner les segments]** , sélectionnez les segments à envoyer à la destination. Pour plus d’informations sur les champs, reportez-vous aux sections ci-dessous.

![Sélection de segments](../../assets/common/email-select-segments.png)

## Configuration des noms de fichier

Pour plus d’informations sur les options d’édition de la planification des segments et des noms de fichier, reportez-vous à l’étape [Configurer](../../ui/activate-destinations.md#configure) du tutoriel Activer les destinations .

## Sélectionner des attributs : sélectionnez les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés {#destination-attributes}

Au cours de cette étape, vous sélectionnez les champs à exporter vers les destinations de marketing par e-mail et vous devez marquer les champs obligatoires.
Pour plus d’informations sur cette étape, reportez-vous à l’étape [Sélectionner les attributs](../../ui/activate-destinations.md#select-attributes) du tutoriel Activer les destinations .

## Identité {#identity}

Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Il s’agit du champ dont vos identités utilisateur sont saisies. Généralement, ce champ correspond à l’adresse électronique, mais il peut également s’agir d’un identifiant du programme de fidélité ou d’un numéro de téléphone. Reportez-vous au tableau ci-dessous pour connaître les identifiants uniques les plus courants et leur champ XDM dans le schéma.

| Identifiant unique | Champ XDM dans le schéma unifié |
|----------------- | ---------------------------|
| Adresse électronique | `personalEmail.address` |
| Téléphone | `mobilePhone.number` |
| Identifiant du programme de fidélité | `Customer-defined XDM field` |

## Autres attributs de destination

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

## Importez des données de l’emplacement de stockage vers la destination {#import-data-into-destination}

Lisez les articles de destination de marketing par e-mail individuels pour savoir comment importer des données de l’emplacement de stockage vers les destinations :

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Activer les segments vers les destinations de marketing par e-mail

Pour plus d’informations sur l’activation des segments vers les destinations de marketing par e-mail, voir [Activation des profils et des segments vers une destination](../../ui/activate-destinations.md).

## Ressources supplémentaires

- [Activation des données vers les destinations](../../ui/activate-destinations.md)
- [Création de destinations de marketing par e-mail et activation des données à l’aide de l’API Flow Service](../../api/email-marketing.md)
