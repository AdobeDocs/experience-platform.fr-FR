---
keywords: SFTP;sftp
title: Connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 715533352e84573f60f012504988595af6146e2f
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 7%

---

# Connexion SFTP

## Présentation {#overview}

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien qu’Experience Platform prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL Azure Blob].

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Type d’exportation SFTP basé sur un profil](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que chaîne codée Base64."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clé SSH privée"
>abstract="La clé SSH privée doit être formatée en tant que chaîne codée en Base64 et ne doit pas être protégée par un mot de passe. "

When [connexion](../../ui/connect-destination.md) vers cette destination, vous devez fournir les informations suivantes :

#### Informations d’authentification {#authentication-information}

Si vous sélectionnez la variable **[!UICONTROL Authentification de base]** saisissez pour vous connecter à votre emplacement SFTP :

![Authentification de base de la destination SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Hôte]**: l’adresse de votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Mot de passe]**: Mot de passe pour se connecter à l’emplacement de stockage de votre SFTP.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
   * Exemple: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Voir ci-dessous un exemple de clé PGP correctement formatée, avec la partie centrale raccourcie pour plus de concision.

      ![Clé PGP](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


Si vous sélectionnez la variable **[!UICONTROL SFTP avec clé SSH]** type d’authentification pour se connecter à votre emplacement SFTP :

![Authentification de clé SSH de destination SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domaine]**: Indiquez l’adresse IP ou le nom de domaine de votre compte SFTP.
* **[!UICONTROL Port]**: le port utilisé par votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Clé SSH]**: Clé SSH privée utilisée pour se connecter à l’emplacement de stockage de votre SFTP. La clé privée doit être formatée en tant que chaîne codée en Base64 et ne doit pas être protégée par un mot de passe.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.
   * Exemple: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Voir ci-dessous un exemple de clé PGP correctement formatée, avec la partie centrale raccourcie pour plus de concision.

      ![Clé PGP](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à l’emplacement SFTP, fournissez les informations suivantes pour la destination :

![Détails de la destination disponible pour la destination SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination dans l’interface utilisateur de l’Experience Platform ;
* **[!UICONTROL Description]**: saisissez une description pour cette destination ;
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier dans votre emplacement SFTP où les fichiers seront exportés.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Pour [!DNL SFTP] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.

## Liste autorisée d’adresses IP

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à une liste autorisée.
