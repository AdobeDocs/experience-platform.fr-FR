---
keywords: SFTP;sftp
title: Connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: fa393b2bd8085a17653962b5a8b112a5db10df83
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# Connexion SFTP

## Présentation {#overview}

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités de Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien qu’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL Azure Blob].

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d&#39;export | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Type d’exportation SFTP basé sur un profil](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que chaîne codée Base64."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clé SSH"
>abstract="La clé SSH requiert une chaîne Base64."

When [connexion](../../ui/connect-destination.md) vers cette destination, vous devez fournir les informations suivantes :

#### Informations d’authentification {#authentication-information}

Si vous sélectionnez la variable **[!UICONTROL Authentification de base]** saisissez pour vous connecter à votre emplacement SFTP :

![Authentification de base de la destination SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Hôte]**: l’adresse de votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Mot de passe]**: Mot de passe pour se connecter à l’emplacement de stockage de votre SFTP.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.


Si vous sélectionnez la variable **[!UICONTROL SFTP avec clé SSH]** type d’authentification pour se connecter à votre emplacement SFTP :

![Authentification de clé SSH de destination SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domaine]**: Indiquez l’adresse IP ou le nom de domaine de votre compte SFTP.
* **[!UICONTROL Port]**: le port utilisé par votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour se connecter à l’emplacement de stockage SFTP ;
* **[!UICONTROL Clé SSH]**: Clé SSH permettant de se connecter à l’emplacement de stockage de votre SFTP.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64] chaîne codée.

#### Détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à l’emplacement SFTP, fournissez les informations suivantes pour la destination :

![Détails de la destination disponible pour la destination SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination dans l’interface utilisateur de l’Experience Platform ;
* **[!UICONTROL Description]**: saisissez une description pour cette destination ;
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier dans votre emplacement SFTP où les fichiers seront exportés.

## Données exportées {#exported-data}

Pour [!DNL SFTP] destinations, Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.

## LISTE AUTORISÉE d’adresses IP

Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud](ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à une liste autorisée.
