---
title: Connexion SFTP
description: Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 45f22addbff9ec81d64e9e756e4c27e8af4b477d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Connexion SFTP

## Journal des modifications de destination {#changelog}

Avec la version d’Experience Platform de juillet 2023, la destination SFTP offre de nouvelles fonctionnalités, comme indiqué ci-dessous :

* [Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md).
* [Options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) supplémentaires.
* Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via l’[étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilité de personnaliser le formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Présentation {#overview}

Créez une connexion sortante active à votre serveur SFTP afin d’exporter périodiquement des fichiers de données délimités à partir d’Adobe Experience Platform.

>[!IMPORTANT]
>
> Bien qu’Experience Platform prenne en charge les exportations de données vers des serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter les données sont [!DNL Amazon S3] et [!DNL Azure Blob].

## Connexion à SFTP via l’API ou l’interface utilisateur {#connect-api-or-ui}

* Pour vous connecter à l’emplacement de stockage de votre SFTP à l’aide de l’interface utilisateur d’Experience Platform, lisez les sections [Se connecter à la destination](#connect) et [Activer des audiences vers cette destination](#activate) ci-dessous.
* Pour vous connecter à votre emplacement de stockage SFTP par programmation, lisez le tutoriel [ Activer des audiences vers des destinations basées sur des fichiers à l’aide de l’API Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Type d’exportation basé sur un profil SFTP mis en surbrillance dans le catalogue des destinations.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez les tutoriels :

* Comment [exporter des jeux de données à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-datasets.md).
* Comment [exporter des jeux de données par programmation à l’aide de l’API Flow Service](/help/destinations/api/export-datasets.md).

## Format des données exportées {#file-format}

Lors de l’exportation de *données d’audience*, Experience Platform crée un fichier `.csv`, `parquet` ou `.json` à l’emplacement de stockage indiqué. Pour plus d’informations sur les fichiers, consultez la section [formats de fichiers pris en charge pour l’exportation](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) dans le tutoriel sur l’activation des audiences.

Lors de l’exportation de *jeux de données*, Experience Platform crée un fichier `.parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [vérifier la réussite de l’exportation du jeu de données](../../ui/export-datasets.md#verify) dans le tutoriel sur l’exportation des jeux de données.

## Exigences de connexion au serveur SFTP {#sftp-connection-requirements}

Pour réussir les exportations de données, vous devez configurer votre serveur SFTP cible pour autoriser un nombre suffisant de connexions simultanées. Si votre serveur SFTP limite le nombre de connexions simultanées, vous pouvez rencontrer des échecs de tâche d’exportation, en particulier lors de l’exportation simultanée de plusieurs audiences ou jeux de données.

**Recommandation**
Pour des performances optimales, votre serveur SFTP doit autoriser au moins une connexion simultanée pour chaque audience ou jeu de données exporté. Au minimum, le serveur doit prendre en charge au moins 30 % du nombre total d’audiences ou de jeux de données planifiés pour l’exportation au même moment.

**Exemple**\
Si vous planifiez des exportations pour 100 audiences ou jeux de données simultanément, votre serveur SFTP doit autoriser au moins 30 connexions simultanées.

La configuration correcte des limites de connexion de votre serveur SFTP permet d’éviter les échecs d’exportation et d’assurer une diffusion fiable des données depuis Adobe Experience Platform.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Informations d’authentification {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Affichez un exemple de clé correctement formatée dans le lien de documentation ci-dessous."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clé SSH privée"
>abstract="La clé SSH privée doit être une chaîne codée en Base64 et formatée pour le RSA, et ne doit pas être protégée par un mot de passe."

Si vous sélectionnez le type d’authentification **[!UICONTROL SFTP avec mot de passe]** pour vous connecter à votre emplacement SFTP :

![Authentification de base de la destination SFTP avec mot de passe.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domaine]** : adresse de l’emplacement de stockage de votre SFTP ;
* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour se connecter à l’emplacement de stockage de votre SFTP ;
* **[!UICONTROL Port]** : le port utilisé par votre emplacement de stockage SFTP ;
* **[!UICONTROL Mot de passe]** : mot de passe pour se connecter à l’emplacement de stockage de votre SFTP.
* **[!UICONTROL Clé de chiffrement]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

  ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Si vous sélectionnez le type d’authentification **[!UICONTROL SFTP avec clé SSH]** pour vous connecter à votre emplacement SFTP :

![Authentification de la clé SSH de la destination SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domaine]** : indiquez l’adresse IP ou le nom de domaine de votre compte SFTP ;
* **[!UICONTROL Port]** : le port utilisé par votre emplacement de stockage SFTP ;
* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour se connecter à l’emplacement de stockage de votre SFTP ;
* **[!UICONTROL Clé SSH]** : clé SSH privée utilisée pour se connecter à l’emplacement de stockage de votre SFTP. La clé privée doit être une chaîne au format RSA et codée en Base64, et ne doit pas être protégée par un mot de passe.
* **[!UICONTROL Clé de chiffrement]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

  ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à l’emplacement SFTP, fournissez les informations suivantes pour la destination :

![Champs de détails de la destination pour la destination SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nom]** : saisissez un nom qui vous aide à identifier cette destination dans l’interface utilisateur d’Experience Platform ;
* **[!UICONTROL Description]** : saisissez une description pour cette destination ;
* **[!UICONTROL Chemin du dossier]** : saisissez le chemin du dossier de votre emplacement SFTP où les fichiers seront exportés.
* **[!UICONTROL Type de fichier]** : sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Lors de la sélection de l’option [!UICONTROL CSV], vous pouvez également [configurer les options de formatage des fichiers](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]** : sélectionnez le type de compression qu’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Inclure le fichier manifeste]** : activez cette option si vous souhaitez que les exportations incluent un fichier JSON de manifeste contenant des informations sur l’emplacement d’exportation, la taille d’exportation, etc. Le manifeste est nommé à l’aide du format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Affichez un [exemple de fichier de manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier manifeste comprend les champs suivants :
   * `flowRunId` : exécution [flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.
   * `scheduledTime` : heure en UTC à laquelle le fichier a été exporté.
   * `exportResults.sinkPath` : chemin d’accès à l’emplacement de stockage où le fichier exporté est déposé.
   * `exportResults.name` : nom du fichier exporté.
   * `size` : taille du fichier exporté, en octets.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [ Activer les données d’audience vers des destinations d’exportation de profils par lots ](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez votre stockage SFTP et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Liste autorisée d’adresses IP {#ip-address-allow-list}

Reportez-vous à l’article [Adresse IP](ip-address-allow-list.md) de la place sur la liste autorisée si vous devez ajouter des adresses IP Adobe à un place sur la liste autorisée.
