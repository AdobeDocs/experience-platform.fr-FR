---
keywords: SFTP;sftp
title: Connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 16%

---

# Connexion SFTP

## Journal des modifications de destination {#changelog}

>[!IMPORTANT]
>
>Avec la version bêta de la fonctionnalité d’exportation des jeux de données et la fonctionnalité améliorée d’exportation de fichiers, vous pouvez maintenant voir deux [!DNL SFTP] cartes dans le catalogue des destinations.
>* Si vous exportez déjà des fichiers vers le **[!UICONTROL SFTP]** destination : Créez de nouveaux flux de données dans le nouveau **[!UICONTROL Version bêta SFTP]** destination.
>* Si vous n’avez pas encore créé de flux de données pour la variable **[!UICONTROL SFTP]** destination, veuillez utiliser la nouvelle **[!UICONTROL Version bêta SFTP]** carte pour exporter des fichiers vers **[!UICONTROL SFTP]**.


![Image des deux cartes de destination SFTP dans une vue côte à côte.](/help/destinations/assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Améliorations de la nouvelle [!DNL SFTP] carte de destination :

* [Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md).
* Additional [options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via le [étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilité de personnaliser le formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Présentation {#overview}

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien qu’Experience Platform prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL SFTP].

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Type d’exportation SFTP basé sur un profil](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Informations d’authentification {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que chaîne codée Base64."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clé SSH privée"
>abstract="La clé SSH privée doit être formatée en tant que chaîne codée en Base64 et ne doit pas être protégée par un mot de passe."

Si vous sélectionnez la variable **[!UICONTROL Authentification de base]** saisissez pour vous connecter à votre emplacement SFTP :

![Authentification de base de la destination SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Hôte]**: l’adresse de votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Mot de passe]**: Mot de passe pour se connecter à l’emplacement de stockage de votre SFTP.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64-encoded] chaîne. Affichez un exemple d’une clé codée en base64 correctement formatée dans le lien de documentation ci-dessous. La partie centrale est raccourcie par concision.

![Image montrant un exemple d’une clé PGP correctement formatée et chiffrée en base64 dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Si vous sélectionnez la variable **[!UICONTROL SFTP avec clé SSH]** type d’authentification pour se connecter à votre emplacement SFTP :

![Authentification de clé SSH de destination SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domaine]**: Indiquez l’adresse IP ou le nom de domaine de votre compte SFTP.
* **[!UICONTROL Port]**: le port utilisé par votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Clé SSH]**: Clé SSH privée utilisée pour se connecter à l’emplacement de stockage de votre SFTP. La clé privée doit être formatée en tant que chaîne codée en Base64 et ne doit pas être protégée par un mot de passe.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
   * Exemple: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Voir ci-dessous un exemple de clé PGP correctement formatée, avec la partie centrale raccourcie pour plus de concision.

      ![Clé PGP](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à l’emplacement SFTP, fournissez les informations suivantes pour la destination :

![Détails de la destination disponible pour la destination SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination dans l’interface utilisateur de l’Experience Platform ;
* **[!UICONTROL Description]**: saisissez une description pour cette destination ;
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier dans votre emplacement SFTP où les fichiers seront exportés.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## (Version bêta) Exportation de jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Données exportées {#exported-data}

Pour [!DNL SFTP] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.

## Liste autorisée d’adresses IP

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à une liste autorisée.
