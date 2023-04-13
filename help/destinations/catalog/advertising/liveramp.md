---
title: (Alpha) [!DNL LiveRamp SFTP] connection
description: Découvrez comment utiliser le connecteur LiveRamp pour intégrer des audiences d’Adobe Real-time Customer Data Platform à LiveRamp Connect.
hidefromtoc: true
hide: true
source-git-commit: 367ef59f623acc38e636a6cae0c85f186eaccfda
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 19%

---


# (Alpha) [!DNL LiveRamp - SFTP] connection {#liveramp-destination}

Utilisation de la connexion LiveRamp pour intégrer des audiences depuis Adobe Real-time Customer Data Platform vers [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Cette connexion de destination est actuellement en phase alpha et n’est disponible que pour une sélection limitée de clients. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.</p>
&gt;<p>La version finale de cette connexion de destination peut nécessiter la migration des clients.</p>


## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL LiveRamp SFTP] destination, voici un exemple de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

En tant que marketeur, je souhaite envoyer des audiences de Adobe Experience Platform vers des identités intégrées dans [!DNL LiveRamp Connect] afin que je puisse cibler les utilisateurs sur [!DNL CTV] plateformes, à l’aide de [!DNL Ramp ID] identifiant.

## Conditions préalables {#prerequisites}

Le [!DNL LiveRamp - SFTP] exporte les fichiers de connexion à l’aide de [SFTP de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) stockage.

Avant d’envoyer des données de l’Experience Platform vers [!DNL LiveRamp SFTP], vous avez besoin de [!DNL LiveRamp] informations d’identification. Veuillez contacter votre [!DNL LiveRamp] représentant pour obtenir vos informations d’identification, si vous ne les avez pas déjà.

## Identités prises en charge {#supported-identities}

LiveRamp SFTP prend en charge l’activation d’identités telles que les identifiants basés sur des informations d’identification personnelles, les identifiants connus et les identifiants personnalisés, décrits dans la section officielle [Documentation LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

Dans le [étape de mappage](#map) dans le workflow d’activation, vous devez définir les mappages de la cible en tant qu’attributs personnalisés.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la variable [!DNL LiveRamp SFTP] destination. |
| Fréquence des exportations | **[!UICONTROL batch quotidien]** | Les profils étant mis à jour en Experience Platform en fonction de l’évaluation des segments, les profils (identités) sont mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

**Authentification SFTP avec mot de passe** {#sftp-password}

![Exemple de capture d’écran montrant comment s’authentifier à la destination à l’aide du protocole SFTP avec mot de passe](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Nom d’utilisateur]**: Le nom d’utilisateur de votre [!DNL LiveRamp SFTP] emplacement de stockage.
* **[!UICONTROL Mot de passe]**: Le mot de passe de votre [!DNL LiveRamp SFTP] emplacement de stockage.
* **[!UICONTROL Clé de chiffrement PGP/GPG]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Affichez un exemple de clé de chiffrement correctement formatée dans l’image ci-dessous. Si vous fournissez une clé de chiffrement, vous devez également fournir une **[!UICONTROL Cryptage de l’ID de sous-clé]** dans le [détails de la destination](#destination-details) .

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP avec authentification par clé SSH** {#sftp-ssh}

![Exemple de capture d’écran montrant comment s’authentifier à la destination à l’aide de la clé SSH](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Nom d’utilisateur]**: Le nom d’utilisateur de votre [!DNL LiveRamp SFTP] emplacement de stockage.
* **[!UICONTROL Clé SSH]**: Le privé [!DNL SSH] clé utilisée pour se connecter à votre [!DNL LiveRamp SFTP] emplacement de stockage. La clé privée doit être formatée en tant que [!DNL Base64]Chaîne encodée et ne doit pas être protégée par un mot de passe.

   * Pour connecter votre [!DNL SSH] de la clé [!DNL LiveRamp SFTP] serveur, vous devez envoyer un ticket via [!DNL LiveRamp]Portail d’assistance technique de et fournissez votre clé publique. Pour plus d’informations, voir [Documentation LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Clé de chiffrement PGP/GPG]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Si vous fournissez une clé de chiffrement, vous devez également fournir une **[!UICONTROL Cryptage de l’ID de sous-clé]** dans le [détails de la destination](#destination-details) . Affichez un exemple de clé de chiffrement correctement formatée dans l’image ci-dessous.

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="Cryptage de l’ID de sous-clé"
>abstract="Identifiant de sous-clé utilisé pour le chiffrement, basé sur la clé de chiffrement publique LiveRamp. Ce champ est obligatoire si vous avez fourni une clé de chiffrement à l’étape d’authentification."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Découvrez comment obtenir l’identifiant de sous-clé"

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Copie d’écran de l’interface utilisateur de Platform montrant comment remplir les détails pour votre destination](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Chemin du dossier]**: Le chemin d’accès à [!DNL LiveRamp] `uploads` sous-dossier qui hébergera les fichiers exportés. Le `uploads` est automatiquement ajouté au chemin du dossier.
   * Par exemple, si vous souhaitez exporter vos fichiers vers `uploads/my_export_folder`, saisissez `my_export_folder` dans le **[!UICONTROL Chemin du dossier]** champ .
* **[!UICONTROL Format de compression]**: Sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés. Les options disponibles sont **[!UICONTROL GZIP]** ou **[!UICONTROL Aucun]**.
* **[!UICONTROL Cryptage de l’ID de sous-clé]**: La sous-clé utilisée pour le chiffrement, en fonction de la variable [!DNL LiveRamp] clé de chiffrement publique. Ce champ est obligatoire si vous avez fourni une clé de chiffrement dans la variable [authentication](#authenticate) étape . Voir [!DNL LiveRamp] [documentation sur le chiffrement](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) pour savoir comment obtenir l’identifiant de sous-clé.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification {#scheduling}

Dans le [!UICONTROL Planification] créez une planification d’exportation pour chaque segment, avec les paramètres présentés ci-dessous.

>[!IMPORTANT]
>
>Tous les segments activés vers cette destination doivent être configurés avec le même planning, comme illustré ci-dessous.

* **[!UICONTROL Options d’exportation de fichiers]**: [!UICONTROL Exporter les fichiers complets]. [Exports incrémentiels de fichiers](../../ui/activate-batch-profile-destinations.md#export-incremental-files) ne sont actuellement pas pris en charge pour le [!DNL LiveRamp] destination.
* **[!UICONTROL Fréquence]**: [!UICONTROL Quotidien]
* Définissez l’heure d’exportation sur **[!UICONTROL Après l’évaluation du segment]**. Exports de segments planifiés et [Exports de fichiers à la demande](../../ui/export-file-now.md) ne sont actuellement pas pris en charge pour le [!DNL LiveRamp] destination.
* **[!UICONTROL Date]**: Sélectionnez les heures de début et de fin de l&#39;export comme vous le souhaitez.

![Capture d’écran de l’interface utilisateur de Platform montrant l’étape de planification des segments.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

Le nom de fichier exporté ne peut actuellement pas être configuré par l’utilisateur. Tous les fichiers exportés vers [!DNL LiveRamp SFTP] Les destinations sont automatiquement nommées en fonction du modèle suivant :

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Copie d’écran de l’interface utilisateur de Platform présentant le modèle de nom de fichier exporté.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Par exemple, le nom d’un fichier exporté pour une organisation nommée [!DNL Luma] pourrait ressembler à ceci :

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mapper les attributs et les identités {#map}

Dans le **[!UICONTROL Mappage]** vous pouvez sélectionner les attributs et les identités à exporter pour vos profils.

>[!IMPORTANT]
>
>Cette destination prend en charge l’activation d’un espace de noms d’identité source par flux d’activation. Si vous devez exporter plusieurs espaces de noms d’identité, comme `Email` et `Phone`, vous devez [créer un flux d’activation distinct ;](../../ui/activate-batch-profile-destinations.md) pour chaque identité.

Dans le **[!UICONTROL Mappage]** , l’étape **[!UICONTROL Champ cible]** mapping définit le nom de l’en-tête de colonne dans le fichier CSV exporté. Vous pouvez remplacer les en-têtes de colonne CSV du fichier exporté par n’importe quel nom convivial, en fournissant un nom personnalisé pour la variable **[!UICONTROL Champ cible]**.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.

   ![Capture d’écran de l’interface utilisateur Experience Platform affichant l’écran Mappage .](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM à mapper, ou choisissez l’attribut **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité à mapper à votre destination.

   ![Capture d’écran de l’interface utilisateur Experience Platform affichant l’écran de mappage source.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. Dans le **[!UICONTROL Sélectionner le champ cible]** , saisissez le nom de l’attribut auquel vous souhaitez mapper le champ source sélectionné. Le nom d’attribut défini ici se reflète dans le fichier CSV exporté sous la forme d’un en-tête de colonne.

   ![Capture d’écran de l’interface utilisateur Experience Platform affichant l’écran Mappage cible.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Vous pouvez également saisir le nom de l’attribut en le saisissant directement dans la variable **[!UICONTROL Champ cible]**.

   ![Capture d’écran de l’interface utilisateur Experience Platform affichant l’écran Mappage cible.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Une fois que vous avez ajouté tous les mappages souhaités, sélectionnez **[!UICONTROL Suivant]** et terminez le workflow d’activation.

## Données exportées / Validation de l’exportation des données {#exported-data}

Vos données sont exportées vers la variable [!DNL LiveRamp SFTP] emplacement de stockage que vous avez configuré, sous la forme de fichiers CSV.

Lors de l’exportation de fichiers vers le [!DNL LiveRamp SFTP] destination, Platform génère un fichier CSV pour chaque [ID de stratégie de fusion](../../../profile/merge-policies/overview.md).

Prenons par exemple les segments suivants :

* Segment A (stratégie de fusion 1)
* Segment B (stratégie de fusion 2)
* Segment C (stratégie de fusion 1)
* Segment D (stratégie de fusion 1)

Platform exportera deux fichiers CSV vers [!DNL LiveRamp SFTP]:

* un fichier CSV contenant les segments A, C et D ;
* Un fichier CSV contenant le segment B.

Les fichiers CSV exportés contiennent des profils avec les attributs sélectionnés et l’état du segment correspondant, sur des colonnes distinctes, avec le nom d’attribut et les identifiants de segment comme en-têtes de colonne.

Les profils inclus dans les fichiers exportés peuvent correspondre à l’un des états de qualification de segment suivants :

* `Active`: Le profil est actuellement qualifié pour le segment.
* `Expired`: Le profil n’est plus qualifié pour le segment, mais il l’a déjà été.
* `""`(chaîne vide) : Le profil n’a jamais été qualifié pour le segment.


Par exemple, un fichier CSV exporté avec un `email` et 3 segments peuvent ressembler à ceci :

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Comme Platform génère un fichier CSV pour chaque [ID de stratégie de fusion](../../../profile/merge-policies/overview.md), il génère également une exécution de flux de données distincte pour chaque ID de stratégie de fusion.

Cela signifie que la variable **[!UICONTROL Identités activées]** et **[!UICONTROL Profils reçus]** des [exécutions de flux de données](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) sont agrégées pour chaque groupe de segments qui utilisent la même stratégie de fusion, au lieu d’être affichées pour chaque segment.

Du fait de la génération d’exécutions de flux de données pour un groupe de segments qui utilisent la même stratégie de fusion, les noms de segment ne s’affichent pas dans la variable [tableau de bord de surveillance](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Capture d’écran de l’interface utilisateur Experience Platform affichant la mesure identités activées.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Chargement des données exportées vers LiveRamp {#upload-to-liveramp}

Une fois vos données exportées vers le [!DNL LiveRamp - SFTP] stockage, vous devez transférer les données vers le [!DNL LiveRamp] plateforme.

Pour plus d’informations sur la manière de charger vos fichiers à partir du [!DNL LiveRamp - SFTP] stockage dans un [!DNL LiveRamp] pour l’audience, consultez la documentation suivante : [Remarques concernant le téléchargement du premier fichier vers une audience](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur la configuration de votre stockage SFTP LiveRamp, reportez-vous à la section [documentation officielle](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
