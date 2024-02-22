---
title: Importation des données de prospection Acxiom
description: Découvrez comment connecter les données de prospection Acxiom à Adobe Experience Platform et Adobe Real-time Customer Data Platform à l’aide de l’interface utilisateur.
last-substantial-update: 2024-02-21T00:00:00Z
badge: Version Beta
source-git-commit: bf7e2e08d54f113c6e2cc5060f51725555c2c049
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 13%

---

# Créez un [!DNL Acxiom Prospecting Data Import] connexion source et flux de données dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Acxiom Prospecting Data Import] est en version Beta. Veuillez lire la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL Acxiom]L’ importation de données de prospection pour Adobe Real-time Customer Data Platform est un processus permettant de fournir les audiences de prospects les plus productives possible. [!DNL Acxiom] prend les données propriétaires Real-Time CDP par le biais d’un export sécurisé et exécute ces données par le biais d’un système primé d’hygiène et de résolution d’identité. Un fichier de données est alors utilisé comme liste de suppression. Ce fichier de données est ensuite comparé à la base de données Acxiom Global, ce qui permet de personnaliser les listes de prospects pour les importer.

Vous pouvez utiliser la variable [!DNL Acxiom] source permettant de récupérer et de mapper les réponses du service prospect Acxiom à l’aide d’Amazon S3 comme point de dépôt.

Lisez ce tutoriel pour apprendre à créer une [!DNL Acxiom Prospecting Data Import] connexion source et flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Prospect Profile]](../../../../../profile/ui/prospect-profile.md): découvrez comment créer et utiliser le profil de prospect pour recueillir des informations sur les clients inconnus à l’aide d’informations tierces.

### Collecter les informations d’identification requises

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| [!DNL Acxiom] clé d&#39;authentification | Clé d’authentification. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| [!DNL Amazon S3] clé d&#39;accès | Identifiant de la clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Clé secrète [!DNL Amazon S3] | Identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |

>[!IMPORTANT]
>
>Vous devez disposer des deux **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]** autorisations activées pour votre compte afin de connecter [!DNL Acxiom] compte à Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez la section [guide de l’interface utilisateur du contrôle d’accès](../../../../../access-control/ui/overview.md).

## Connecter votre compte [!DNL Acxiom]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Partenaires Data &amp; Identity]** catégorie, sélectionnez **[!UICONTROL Importation des données de prospection Acxiom]** puis sélectionnez **[!UICONTROL Configuration]**.

>[!TIP]
>
>Carte source qui affiche **[!UICONTROL Ajouter des données]** signifie que la source dispose déjà d’un compte authentifié. D’un autre côté, une carte source qui affiche **[!UICONTROL Configuration]** signifie que vous devez fournir des informations d’identification et créer un compte pour utiliser cette source.

![Catalogue des sources avec la source Acxiom sélectionnée.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-catalog.png)

### Création d’un compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et votre [!DNL Acxiom] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir la nouvelle connexion.

![Nouvelle interface de compte du workflow des sources.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-account.png)

| Informations d’identification | Description |
| --- | --- |
| Nom de compte | Nom du compte. |
| Description | (Facultatif) Une brève explication de l’objectif du compte. |
| [!DNL Acxiom] clé d&#39;authentification | La variable [!DNL Acxiom]Clé fournie requise pour l’approbation du compte. Cette valeur doit correspondre à la valeur correcte pour qu’une connexion à la base de données puisse être établie.  Cette clé doit comporter 24 caractères et ne peut contenir que : A-Z, a-z et 0-9. |
| Clé d’accès S3 | La clé d’accès S3 référence l’emplacement Amazon S3. Cela est fourni par votre administrateur lorsque les autorisations de rôle S3 sont définies. |
| Clé secrète S3 | La clé secrète S3 référence l’emplacement Amazon S3. Cela est fourni par votre administrateur lorsque les autorisations de rôle S3 sont définies. |
| s3SessionToken | (Facultatif) La valeur du jeton d’authentification lors de la connexion à S3. |
| serviceUrl | (Facultatif) L’emplacement URL à utiliser lors de la connexion à S3 dans un emplacement non standard. |
| Nom du compartiment | (Facultatif) Le nom du compartiment S3 configuré sur S3 qui sert de chemin de départ dans la sélection des données. |
| Chemin du dossier | Si des sous-répertoires d’un compartiment sont utilisés, vous pouvez également spécifier un chemin d’accès comme chemin de départ dans la sélection des données. |

### Utiliser un compte existant

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]**.

Sélectionnez un compte dans la liste pour afficher les détails sur ce compte. Une fois le compte sélectionné, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Interface de compte existante du workflow des sources.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-existing-account.png)

## Sélectionner les données

Sélectionnez le fichier à ingérer dans le compartiment et le sous-répertoire souhaités. Un aperçu des données peut être fourni une fois que le délimiteur et le type de compression sont définis. Une fois le fichier sélectionné, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![L&#39;interface de prévisualisation des données et des fichiers du workflow des sources.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-preview.png)

>[!NOTE]
>
>Bien que les types de fichiers JSON et Parquet soient répertoriés, vous n’êtes pas tenu de les utiliser pendant la [!DNL Acxiom] workflow source.

## Fournir des détails sur les jeux de données et les flux de données

Ensuite, vous devez fournir des informations concernant votre jeu de données et votre flux de données.

### Informations sur le jeu de données

>[!BEGINTABS]

>[!TAB Utiliser un nouveau jeu de données]

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les données correctement ingérées dans Experience Platform sont conservées en tant que jeux de données dans le lac de données. Pour utiliser un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]**.

![Nouvelle interface de jeu de données.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-dataset.png)

| Détails du nouveau jeu de données | Description |
| --- | --- |
| Nom du jeu de données de sortie | Nom du nouveau jeu de données. |
| Description | (Facultatif) Une brève explication de l’objectif du jeu de données. |
| Schéma | Liste déroulante des schémas qui existent dans votre organisation. Vous pouvez également créer votre propre schéma avant le processus de configuration de la source. Pour plus d’informations, consultez le guide sur [création de schéma dans l’interface utilisateur](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Utiliser un jeu de données existant]

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**.

Vous pouvez sélectionner **[!UICONTROL Recherche avancée]** pour afficher une fenêtre de tous les jeux de données de votre entreprise, y compris leurs détails respectifs, comme s’ils sont activés pour l’ingestion dans Real-time Customer Profile.

![Interface du jeu de données existant.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset.png)

>[!ENDTABS]

### Détails du flux de données

Au cours de cette étape, si votre jeu de données est activé pour Profile, vous pouvez sélectionner la variable **[!UICONTROL Jeu de données de profil]** Activez les données pour l’ingestion par profil. Vous pouvez également activer [!UICONTROL Diagnostics d’erreur] et [!UICONTROL Ingestion partielle].

* **Diagnostics d’erreur** - Sélectionner **Diagnostics d’erreur** pour demander à la source de produire des diagnostics d’erreur que vous pourrez ensuite référencer à l’aide des API. Pour plus d’informations, consultez la section [présentation des diagnostics d’erreur](../../../../../ingestion/quality/error-diagnostics.md)
* **Activation de l’ingestion partielle** - L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, tandis que toutes leurs données incorrectes sont traitées par lots séparément, avec des détails sur les raisons de leur non-validité.  Pour plus d’informations, consultez la section [Présentation de l’ingestion partielle](../../../../../ingestion/batch-ingestion/partial.md)

![Interface des configurations des détails du flux de données.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset-details.png)

| Configurations de flux de données | Description |
| --- | --- |
| Nom du flux de données | Nom du flux de données.  Par défaut, le nom du fichier importé sera utilisé. |
| Description | (Facultatif) Une brève description de votre flux de données. |
| Alertes | Experience Platform peut produire des alertes basées sur des événements auxquelles les utilisateurs peuvent s’abonner. Ces options sont toutes des flux de données en cours d’exécution pour les déclencher.  Pour plus d’informations, consultez la section [aperçu des alertes](../../alerts.md) <ul><li>**Démarrage de l’exécution du flux de données sources**: sélectionnez cette alerte pour recevoir une notification au début de l’exécution du flux de données.</li><li>**Réussite de l’exécution du flux de données sources**: sélectionnez cette alerte pour recevoir une notification si votre flux de données se termine sans erreur.</li><li>**Échec de l’exécution des flux de données sources**: sélectionnez cette alerte pour recevoir une notification si l’exécution de votre flux de données se termine en erreur.</li></ul> |

## Mappage

Utilisez l’interface de mappage pour mapper vos données source aux champs de schéma appropriés avant d’ingérer des données vers Experience Platform.  Pour plus d’informations, consultez la section [guide de mappage dans l’interface utilisateur](../../../../../data-prep/ui/mapping.md)

![Interface de mappage.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-mapping.png)

## Planification de l’ingestion de vos flux de données

Utilisez l’interface de planification pour définir le planning d’ingestion de votre flux de données.

* **Fréquence**: configurez la fréquence pour indiquer la fréquence d’exécution du flux de données. Vous pouvez définir votre fréquence sur : une fois, une minute, une heure, un jour ou une semaine.
* **Intervalle**: une fois que vous avez sélectionné une fréquence, vous pouvez configurer le paramètre d’intervalle pour établir la période entre chaque ingestion. Par exemple, si vous définissez votre fréquence sur &quot;jour&quot; et configurez l’intervalle sur 15, votre flux de données s’exécute tous les 15 jours. L’intervalle ne peut pas être défini sur zéro et doit être défini sur au moins 15.
* **Heure de début** - Horodatage de l’exécution projetée, présenté dans le fuseau horaire UTC.
* **Renvoi** - Le renvoi détermine les données ingérées initialement. Si le renvoi est activé, tous les fichiers actuels du chemin spécifié seront ingérés lors de la première ingestion planifiée. Si le renvoi est désactivé, seuls les fichiers chargés entre la première exécution de l’ingestion et l’heure de début seront ingérés. Les fichiers chargés avant l’heure de début ne seront pas ingérés.

![Interface de configuration de la planification.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-scheduling.png)

## Vérifier le flux de données

Utilisez la page de révision pour obtenir un résumé de votre flux de données avant l’ingestion. Les détails sont regroupés dans les catégories suivantes :

* **Connexion** - Affiche le type de source, le chemin d’accès approprié du fichier source choisi et la quantité de colonnes qu’il contient.
* **Attribution de champs de jeu de données et de mappage** - Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
* **Planification** : indique la période, la fréquence et l’intervalle actifs du planning d’ingestion.
Une fois que vous avez examiné votre flux de données, cliquez sur Terminer et laissez un certain temps au flux de données pour qu’il soit créé.

![Page de révision.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-review.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données par lots de votre [!DNL Acxiom] source à Experience Platform. Pour obtenir des ressources supplémentaires, consultez la documentation décrite ci-dessous.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données qui sont ingérées par celui-ci pour afficher des informations sur les taux d’ingestion, la réussite et les erreurs. Pour plus d’informations sur la surveillance du flux de données, consultez le tutoriel sur [surveillance des comptes et des flux de données dans l’interface utilisateur](../../monitor.md).

### Mettre à jour votre flux de données

Pour mettre à jour les configurations de la planification, du mappage et des informations générales de vos flux de données, consultez le tutoriel sur [mise à jour des flux de données de sources dans l’interface utilisateur](../../update-dataflows.md)

### Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur [suppression de flux de données dans l’interface utilisateur](../../delete.md).

## Ressources supplémentaires {#additional-resources}

[!DNL Acxiom] Données d’audience et distribution : https://www.acxiom.com/customer-data/audience-data-distribution/
