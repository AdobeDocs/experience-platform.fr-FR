---
keywords: Experience Platform;accueil;rubriques les plus consultées;activer le jeu de données;jeu de données;jeu de données
solution: Experience Platform
title: Guide de l’interface utilisateur des jeux de données
description: Découvrez comment exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 141037fd844c78e98785ea2246026ac120961dd5
workflow-type: tm+mt
source-wordcount: '2745'
ht-degree: 17%

---

# Guide de l’interface utilisateur des jeux de données

Ce guide d’utilisation fournit des instructions permettant d’exécuter des actions courantes lors de l’utilisation de jeux de données dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Jeu de données](overview.md) : la structure de stockage et de gestion pour la persistance des données dans [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Éditeur de schéma](../../xdm/tutorials/create-schema-ui.md): découvrez comment créer vos propres schémas XDM personnalisés à l’aide du [!DNL Schema Editor] dans la fonction [!DNL Platform] de l’interface utilisateur.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garantissez la conformité aux réglementations, aux restrictions et aux politiques concernant l’utilisation des données clients.

## Affichage des jeux de données {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Nombres négatifs dans l&#39;activité du jeu de données"
>abstract="Les nombres négatifs dans les enregistrements ingérés signifient qu&#39;un utilisateur a supprimé certains lots au cours d&#39;une période sélectionnée."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Expiration du jeu de données"
>abstract="Cette colonne indique le nombre de jours restants au jeu de données cible avant son expiration automatique."

Dans le [!DNL Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour ouvrir la **[!UICONTROL Jeux de données]** tableau de bord. Le tableau de bord répertorie tous les jeux de données disponibles pour votre organisation. Des détails s’affichent pour chaque jeu de données répertorié, notamment son nom, le schéma auquel le jeu de données adhère et l’état de l’exécution d’ingestion la plus récente.

![Image qui met en surbrillance l’élément Jeux de données dans la barre de navigation de gauche.](../images/datasets/user-guide/browse-datasets.png)

Sélectionnez le nom d’un jeu de données dans la [!UICONTROL Parcourir] pour accéder à ses **[!UICONTROL Activité du jeu de données]** et afficher les détails du jeu de données que vous avez sélectionné. L’onglet activité contient un graphique qui permet de visualiser le taux de messages consommé ainsi qu’une liste des lots réussis et en échec.

![Les détails du jeu de données sélectionné sont mis en surbrillance.](../images/datasets/user-guide/dataset-activity-1.png)
![Les exemples de lots appartenant à votre jeu de données sélectionné sont mis en surbrillance.](../images/datasets/user-guide/dataset-activity-2.png)

## Actions de jeux de données intégrés {#inline-actions}

L’interface utilisateur des jeux de données propose désormais des collections d’actions intégrées pour chaque jeu de données disponible. Sélectionnez les points de suspension (...) d’un jeu de données que vous souhaitez gérer pour afficher les options disponibles dans un menu contextuel. Les actions disponibles sont les suivantes : [[!UICONTROL Prévisualisation d’un jeu de données]](#preview), [[!UICONTROL Gestion des données et des étiquettes d’accès]](#manage-and-enforce-data-governance), [[!UICONTROL Activer le profil unifié]](#enable-profile), [[!UICONTROL Gestion des balises]](#add-tags), [[!UICONTROL Déplacer vers des dossiers]](#move-to-folders), et [[!UICONTROL Supprimer]](#delete). Vous trouverez plus d’informations sur ces actions disponibles dans les sections respectives.

### Ajout de balises de jeu de données {#add-tags}

Ajoutez des balises personnalisées créées pour organiser les jeux de données et améliorer les fonctionnalités de recherche, de filtrage et de tri. Dans la [!UICONTROL Parcourir] de la [!UICONTROL Jeux de données] workspace, sélectionnez les points de suspension d’un jeu de données à gérer, suivi de **[!UICONTROL Gestion des balises]** dans le menu déroulant.

![L’onglet Parcourir de l’espace de travail des jeux de données avec les options Points de suspension et Gérer les balises mises en surbrillance pour le jeu de données sélectionné.](../images/datasets/user-guide/manage-tags.png)

La variable [!UICONTROL Gestion des balises] s’affiche. Entrez une brève description pour créer une balise personnalisée ou faites votre choix parmi une balise préexistante pour étiqueter votre jeu de données. Cliquez sur **[!UICONTROL Enregistrer]** pour confirmer les paramètres.

![La boîte de dialogue Gérer les balises avec les balises personnalisées est mise en surbrillance.](../images/datasets/user-guide/manage-tags-dialog.png)

La variable [!UICONTROL Gestion des balises] dialog peut également supprimer des balises existantes d’un jeu de données. Il vous suffit de sélectionner le &quot;x&quot; en regard de la balise que vous souhaitez supprimer et de sélectionner **[!UICONTROL Enregistrer]**.

Une fois qu’une balise a été ajoutée à un jeu de données, les jeux de données peuvent être filtrés en fonction de la balise correspondante. Consultez la section sur la façon de [filtrer les jeux de données par balises](#enable-profile) pour plus d’informations.

Pour plus d’informations sur la classification des objets commerciaux en vue d’une découverte et d’une catégorisation plus simples, consultez le guide sur [gestion des taxonomies des métadonnées](../../administrative-tags/ui/managing-tags.md). Ce guide explique comment un utilisateur disposant des autorisations appropriées peut créer des balises prédéfinies, affecter des catégories aux balises et effectuer toutes les opérations CRUD associées sur des balises et des catégories de balises dans l’interface utilisateur de Platform.

## Recherche et filtrage de jeux de données {#search-and-filter}

Pour rechercher ou filtrer la liste des jeux de données disponibles, sélectionnez l’icône de filtre (![L’icône de filtre.](../images/datasets/user-guide/icon.png)) en haut à gauche de l’espace de travail. Un ensemble d’options de filtre dans le rail de gauche s’affiche. Il existe plusieurs méthodes pour filtrer vos jeux de données disponibles. Il s’agit notamment : [[!UICONTROL Afficher les jeux de données système]](#show-system-datasets), [[!UICONTROL Inclus dans le profil]](#filter-profile-enabled-datasets), [[!UICONTROL Balises]](#filter-by-tag), [[!UICONTROL Date de création]](#filter-by-creation-date), [[!UICONTROL Date de modification], [!UICONTROL Créé par]](#filter-by-creation-date), et [[!UICONTROL Schéma]](#filter-by-schema).

La liste des filtres appliqués s’affiche au-dessus des résultats filtrés.

![Onglet Parcourir de l’espace de travail des jeux de données avec la liste des filtres appliqués mise en surbrillance.](../images/datasets/user-guide/applied-filters.png)

### Affichage des jeux de données système {#show-system-datasets}

Par défaut, seuls les jeux de données dans lesquels vous avez ingéré des données s’affichent. Si vous souhaitez afficher les jeux de données générés par le système, sélectionnez la variable **[!UICONTROL Oui]** dans la [!UICONTROL Affichage des jeux de données système] . Les jeux de données générés par le système ne sont utilisés que pour traiter d’autres composants. Par exemple, le jeu de données d’exportation de profil généré par le système est utilisé pour traiter le tableau de bord du profil.

![Les options de filtre de l’espace de travail des jeux de données avec la variable [!UICONTROL Affichage des jeux de données système] en surbrillance.](../images/datasets/user-guide/show-system-datasets.png)

### Filtrage des jeux de données activés Profile {#filter-profile-enabled-datasets}

Les jeux de données qui ont été activés pour les données de profil sont utilisés pour renseigner les profils clients une fois les données ingérées. Voir la section sur [activation de jeux de données pour Profile](#enable-profile) pour en savoir plus.

Pour filtrer votre jeu de données selon qu’il a été activé ou non pour Profile, sélectionnez la variable [!UICONTROL Oui] dans les options de filtrage.

![Les options de filtre de l’espace de travail des jeux de données avec la variable [!UICONTROL Inclus dans Profile] en surbrillance.](../images/datasets/user-guide/included-in-profile.png)

### Filtrage des jeux de données par balise {#filter-by-tag}

Saisissez votre nom de balise personnalisé dans le champ [!UICONTROL Balises] saisissez , puis sélectionnez votre balise dans la liste des options disponibles pour rechercher et filtrer les jeux de données qui correspondent à cette balise.

![Les options de filtre de l’espace de travail des jeux de données avec la variable [!UICONTROL Balises] icône d’entrée et de filtre mise en surbrillance.](../images/datasets/user-guide/filter-tags.png)

### Filtrage des jeux de données par date de création {#filter-by-creation-date}

Les jeux de données peuvent être filtrés par date de création sur une période personnalisée. Vous pouvez l’utiliser pour exclure les données historiques ou pour générer des informations et des rapports chronologiques spécifiques. Choisissez une [!UICONTROL Date de début] et un [!UICONTROL Date de fin] en sélectionnant l&#39;icône de calendrier pour chaque champ. Ensuite, seuls les jeux de données conformes à ce critère s’affichent dans l’onglet Parcourir .

### Filtrage des jeux de données par date de modification {#filter-by-modified-date}

Tout comme le filtre pour la date de création, vous pouvez filtrer vos jeux de données en fonction de la date de leur dernière modification. Dans le [!UICONTROL Date de modification] , choisissez une [!UICONTROL Date de début] et un [!UICONTROL Date de fin] en sélectionnant l&#39;icône de calendrier pour chaque champ. Après quoi, seuls les jeux de données modifiés au cours de cette période s’affichent dans l’onglet Parcourir .

### Filtrage par schéma {#filter-by-schema}

Vous pouvez filtrer les jeux de données en fonction du schéma qui définit leur structure. Sélectionnez l’icône de liste déroulante ou saisissez le nom du schéma dans le champ de texte. Une liste des correspondances potentielles s’affiche. Sélectionnez le schéma approprié dans la liste.

## Tri des jeux de données par date de création {#sort}

Jeux de données dans [!UICONTROL Parcourir] peut être triée par date ascendante ou descendante. Sélectionnez la variable [!UICONTROL Créé] ou [!UICONTROL Dernière mise à jour] en-têtes de colonne pour alterner entre croissant et décroissant. Une fois la colonne sélectionnée, une flèche vers le haut ou vers le bas s’affiche sur le côté de l’en-tête de colonne.

![L’onglet Parcourir de l’espace de travail des jeux de données avec la colonne Créé et Dernière mise à jour mise en surbrillance.](../images/datasets/user-guide/ascending-descending-columns.png)

## Prévisualisation d’un jeu de données {#preview}

Vous pouvez prévisualiser des données d’exemple de jeu de données à partir des deux options intégrées de la variable [!UICONTROL Parcourir] et également [!UICONTROL Activité du jeu de données] vue. Dans la [!UICONTROL Parcourir] , sélectionnez les ellipses (...) en regard du nom du jeu de données que vous souhaitez prévisualiser. Une liste d’options s’affiche. Ensuite, sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]** dans la liste des options disponibles. Si le jeu de données est vide, le lien de prévisualisation est désactivé et indique à la place que l’aperçu n’est pas disponible.

![L’onglet Parcourir de l’espace de travail des jeux de données avec les points de suspension et l’option Prévisualiser le jeu de données mise en surbrillance pour le jeu de données sélectionné.](../images/datasets/user-guide/preview-dataset-option.png)

La fenêtre d’aperçu s’ouvre alors, dans laquelle la vue hiérarchique du schéma du jeu de données s’affiche à droite.

![La boîte de dialogue d’aperçu du jeu de données contient des informations sur la structure, ainsi que des exemples de valeurs, pour le jeu de données.](../images/datasets/user-guide/preview-dataset.png)

Vous pouvez également utiliser la variable **[!UICONTROL Activité du jeu de données]** écran, sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]** près du coin supérieur droit de votre écran pour prévisualiser jusqu’à 100 lignes de données.

![Le bouton Prévisualiser le jeu de données est mis en surbrillance.](../images/datasets/user-guide/select-preview.png)

Pour des méthodes plus robustes d’accès à vos données, [!DNL Experience Platform] fournit des services en aval tels que [!DNL Query Service] et [!DNL JupyterLab] pour explorer et analyser les données. Pour plus d’informations, consultez les documents suivants :

* [Présentation de Query Service](../../query-service/home.md)
* [Guide d’utilisation de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Créer un jeu de données {#create}

Pour créer un jeu de données, commencez par sélectionner **[!UICONTROL Créer un jeu de données]** dans le tableau de bord Jeux de données.****

![Le bouton Créer un jeu de données est mis en surbrillance.](../images/datasets/user-guide/select-create.png)

Sur l’écran suivant, les deux options de création d’un nouveau jeu de données suivantes vous sont proposées :

* [Créer un jeu de données à partir d’un schéma](#schema)
* [Créer un jeu de données à partir d’un fichier CSV](#csv)

### Création d’un jeu de données à partir d’un schéma existant {#schema}

Dans le **[!UICONTROL Création d’un jeu de données]** écran, sélectionnez **[!UICONTROL Création d’un jeu de données à partir d’un schéma]** pour créer un nouveau jeu de données vide.

![Le bouton Créer un jeu de données à partir d’un schéma est mis en surbrillance.](../images/datasets/user-guide/create-dataset-schema.png)

L’étape **[!UICONTROL Sélectionner un schéma]** apparaît. Parcourez la liste des schémas et sélectionnez le schéma auquel le jeu de données doit se conformer avant de sélectionner **[!UICONTROL Suivant]**.

![Une liste des schémas s’affiche. Le schéma qui sera utilisé pour créer le jeu de données est mis en surbrillance.](../images/datasets/user-guide/select-schema.png)

L’étape **[!UICONTROL Configurer le jeu de données]** apparaît. Attribuez un nom et une description facultative au jeu de données, puis sélectionnez **[!UICONTROL Terminer]** pour créer le jeu de données.

![Les détails de configuration du jeu de données sont insérés. Cela inclut des détails tels que le nom et la description du jeu de données.](../images/datasets/user-guide/configure-dataset-schema.png)

Les jeux de données peuvent être filtrés à partir de la liste des jeux de données disponibles dans l’interface utilisateur avec le filtre de schéma. Consultez la section sur la façon de [filtrer les jeux de données par schéma](#filter-by-schema) pour plus d’informations.

### Création d’un jeu de données à partir d’un fichier CSV {#csv}

Lorsque vous créez un jeu de données à l’aide d’un fichier CSV, un schéma ad hoc est créé pour fournir une structure au jeu de données qui correspond au fichier CSV fourni. Dans le **[!UICONTROL Création d’un jeu de données]** écran, sélectionnez **[!UICONTROL Création d’un jeu de données à partir d’un fichier CSV]**.

![Le bouton Créer un jeu de données à partir d’un fichier CSV est mis en surbrillance.](../images/datasets/user-guide/create-dataset-csv.png)

L’étape **[!UICONTROL Configurer]** apparaît. Attribuez un nom et une description facultative au jeu de données, puis sélectionnez **[!UICONTROL Suivant]**.

![Les détails de configuration du jeu de données sont insérés. Cela inclut des détails tels que le nom et la description du jeu de données.](../images/datasets/user-guide/configure-dataset-csv.png)

L’étape **[!UICONTROL Ajouter les données]** apparaît. Téléchargez le fichier CSV en le faisant glisser et en le déposant au centre de votre écran ou sélectionnez **[!UICONTROL Parcourir]** pour explorer votre répertoire de fichiers. La taille du fichier peut aller jusqu’à 10 gigaoctets. Une fois le fichier CSV chargé, sélectionnez **[!UICONTROL Enregistrer]** pour créer le jeu de données.

>[!NOTE]
>
>Les noms de colonne CSV doivent commencer par des caractères alphanumériques et ne peuvent contenir que des lettres, des chiffres et des traits de soulignement.

![L&#39;écran Ajouter des données s&#39;affiche. L’emplacement où vous pouvez charger le fichier CSV pour le jeu de données est mis en surbrillance.](../images/datasets/user-guide/add-csv-data.png)

## Activation d’un jeu de données pour Real-time Customer Profile {#enable-profile}

Chaque jeu de données a la possibilité d’enrichir les profils clients des données qu’ils ingèrent. Pour ce faire, le schéma auquel le jeu de données adhère doit être compatible pour être utilisé dans [!DNL Real-Time Customer Profile]. Un schéma compatible répond aux critères suivants :

* Le schéma comporte au moins un attribut défini comme propriété d’identité.
* Le schéma comporte au moins une propriété d’identité définie comme identité principale.

Pour plus d’informations sur l’activation d’un schéma pour [!DNL Profile], voir [Guide d’utilisation de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

Vous pouvez activer un jeu de données pour Profile à partir des deux options intégrées de la variable [!UICONTROL Parcourir] et également [!UICONTROL Activité du jeu de données] vue. Dans la [!UICONTROL Parcourir] de la [!UICONTROL Jeux de données] workspace, sélectionnez les points de suspension d’un jeu de données que vous souhaitez activer pour Profile. Une liste d’options s’affiche. Ensuite, sélectionnez **[!UICONTROL Activer le profil unifié]** dans la liste des options disponibles.

![L’onglet Parcourir de l’espace de travail des jeux de données avec les ellipses et Activer le profil unifié mis en surbrillance.](../images/datasets/user-guide/enable-for-profile.png)

Vous pouvez également, à partir du du jeu de données **[!UICONTROL Activité du jeu de données]** sélectionnez l’écran **[!UICONTROL Profil]** bascule dans la fonction **[!UICONTROL Propriétés]** colonne . Une fois activées, les données ingérées dans le jeu de données seront également utilisées pour générer les profils clients.

>[!NOTE]
>
>Si un jeu de données contient déjà des données et est activé pour [!DNL Profile], les données existantes ne sont pas automatiquement utilisées par [!DNL Profile]. Une fois qu’un jeu de données est activé pour [!DNL Profile], il est recommandé d’ingérer à nouveau toutes les données existantes pour qu’elles contribuent aux profils client.

![Le bouton bascule Profil est mis en surbrillance dans la page des détails du jeu de données.](../images/datasets/user-guide/enable-dataset-profiles.png)

Les jeux de données qui ont été activés pour Profile peuvent également être filtrés selon ce critère. Consultez la section sur la façon de [filtrer les jeux de données activés Profile](#filter-profile-enabled-datasets) pour plus d’informations.

## Gestion et application de la gouvernance des données sur un jeu de données {#manage-and-enforce-data-governance}

Vous pouvez gérer les étiquettes de gouvernance des données d’un jeu de données en sélectionnant les options intégrées de la variable [!UICONTROL Parcourir] . Sélectionnez les points de suspension (...) en regard du nom du jeu de données que vous souhaitez gérer, suivi de **[!UICONTROL Gestion des données et des étiquettes d’accès]** dans le menu déroulant.

Les libellés d’utilisation des données, appliqués au niveau du schéma, vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Voir [Présentation de la gouvernance des données](../../data-governance/home.md) pour en savoir plus sur les étiquettes, ou reportez-vous à la section [guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour obtenir des instructions sur la manière d’appliquer des libellés aux schémas pour la propagation aux jeux de données.

### Déplacer vers des dossiers {#move-to-folders}

Vous pouvez placer des jeux de données dans des dossiers pour une meilleure gestion des jeux de données. Pour déplacer un jeu de données dans un dossier, sélectionnez les ellipses (...) en regard du nom du jeu de données que vous souhaitez gérer, suivies de **[!UICONTROL Déplacer vers le dossier]** dans le menu déroulant.

![La variable [!UICONTROL Jeux de données] tableau de bord avec les ellipses et [!UICONTROL Déplacer vers le dossier] surlignée.](../images/datasets/user-guide/move-to-folder.png)

La variable [!UICONTROL Déplacer] la boîte de dialogue dataset to folder s’affiche. Sélectionnez le dossier vers lequel vous souhaitez déplacer l’audience, puis sélectionnez **[!UICONTROL Déplacer]**. Une notification contextuelle vous informe que le déplacement du jeu de données a réussi.

![La variable [!UICONTROL Déplacer] Boîte de dialogue du jeu de données [!UICONTROL Déplacer] surlignée.](../images/datasets/user-guide/move-dialog.png)

>
>
>Vous pouvez également créer des dossiers directement à partir de la boîte de dialogue Déplacer le jeu de données . Pour créer un dossier, sélectionnez l’icône de création de dossier (![Icône Créer un dossier .](../images/datasets/user-guide/create-folder-icon.png)) en haut à droite de la boîte de dialogue.
>
>![La variable [!UICONTROL Déplacer] Boîte de dialogue du jeu de données avec l’icône de création de dossier mise en surbrillance.](/help/catalog/images/datasets/user-guide/create-folder.png)

Une fois que le jeu de données se trouve dans un dossier, vous pouvez choisir d’afficher uniquement les jeux de données appartenant à un dossier spécifique. Pour ouvrir la structure de dossiers, sélectionnez l’icône Afficher les dossiers (![Icône Afficher les dossiers](../images/datasets/user-guide/show-folders-icon.png)). Sélectionnez ensuite le dossier de votre choix pour afficher tous les jeux de données associés.

![La variable [!UICONTROL Jeux de données] tableaux de bord avec la structure de dossiers des jeux de données affichée, l’icône afficher les dossiers et un dossier sélectionné en surbrillance.](../images/datasets/user-guide/folder-structure.png)

## Suppression d’un jeu de données {#delete}

Vous pouvez supprimer un jeu de données des actions en ligne du jeu de données dans le [!UICONTROL Parcourir] ou dans le coin supérieur droit de la [!UICONTROL Activité du jeu de données] vue. Dans la [!UICONTROL Parcourir] sélectionnez les ellipses (...) en regard du nom du jeu de données que vous souhaitez supprimer. Une liste d’options s’affiche. Ensuite, sélectionnez **[!UICONTROL Supprimer]** dans le menu déroulant.

![L’onglet Parcourir de l’espace de travail des jeux de données avec les points de suspension et l’option Supprimer mise en surbrillance pour le jeu de données sélectionné.](../images/datasets/user-guide/inline-delete-dataset.png)

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer.

Vous pouvez également sélectionner **[!UICONTROL Suppression d’un jeu de données]** de la **[!UICONTROL Activité du jeu de données]** écran.

>[!NOTE]
>
>Jeux de données créés et utilisés par les applications et services Adobe (tels qu’Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) ne peut pas être supprimé.

![Le bouton Supprimer le jeu de données est mis en surbrillance dans la page des détails du jeu de données.](../images/datasets/user-guide/delete-dataset.png)

Une boîte de confirmation s’affiche alors. Sélectionner **[!UICONTROL Supprimer]** pour confirmer la suppression du jeu de données.

![Le modal de confirmation de suppression s’affiche, le bouton Supprimer étant surligné.](../images/datasets/user-guide/confirm-delete.png)

## Suppression d’un jeu de données activé par Profile

Si un jeu de données est activé pour Profile, la suppression de ce jeu de données via l’interface utilisateur le supprime du lac de données, d’Identity Service et de la banque de données Profile dans Platform.

Vous pouvez supprimer un jeu de données du [!DNL Profile] ne stocker que (en laissant les données dans le lac de données) à l’aide de l’API Real-time Customer Profile. Pour plus d’informations, consultez le [guide relatif au point d’entrée de l’API du système de profils](../../profile/api/profile-system-jobs.md).

## Surveiller l’ingestion des données

Dans le [!DNL Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche. Le tableau de bord **[!UICONTROL Surveillance]** vous permet de consulter les états des données entrantes soit depuis le lot soit depuis l’ingestion par flux. Pour afficher les états de lots individuels, sélectionnez l’une des options suivantes : **[!UICONTROL Lot de bout en bout]** ou **[!UICONTROL Diffusion en continu de bout en bout]**. Les tableaux de bord répertorient toutes les exécutions d’ingestion par lots ou par flux, y compris celles qui ont réussi, échoué ou qui sont toujours en cours. Chaque liste fournit des détails sur le lot, notamment l’identifiant de lot, le nom du jeu de données cibles et le nombre d’enregistrements ingérés. Si le jeu de données cible est activé pour [!DNL Profile], le nombre d’identités ingérées et d’enregistrements de profil s’affiche également.

![L’écran de surveillance du lot de bout en bout s’affiche. La surveillance et l’association lot à lot sont mises en surbrillance.](../images/datasets/user-guide/batch-listing.png)

Vous pouvez effectuer une sélection sur un seul **[!UICONTROL Identifiant de lot]** pour accéder au **[!UICONTROL Présentation du lot]** tableau de bord et afficher les détails du lot, y compris les journaux d’erreurs en cas d’échec de l’ingestion du lot.

![Les détails du lot sélectionné s’affichent. Cela inclut le nombre d’enregistrements ingérés, le nombre d’enregistrements ayant échoué, l’état du lot, la taille du fichier, les heures de début et de fin de l’ingestion, le jeu de données et les identifiants de lot, l’identifiant de l’organisation, le nom du jeu de données et les informations d’accès.](../images/datasets/user-guide/batch-overview.png)

Si vous souhaitez supprimer le lot, sélectionnez **[!UICONTROL Supprimer le lot]** près du coin supérieur droit du tableau de bord. La suppression d’un lot supprime également ses enregistrements du jeu de données auquel le lot a été ingéré à l’origine.

![Le bouton Supprimer le lot est mis en surbrillance sur la page des détails du jeu de données.](../images/datasets/user-guide/delete-batch.png)

## Étapes suivantes

Ce guide d’utilisation a fourni des instructions sur l’exécution d’actions courantes lors de l’utilisation de jeux de données dans le [!DNL Experience Platform] de l’interface utilisateur. Pour les étapes à suivre [!DNL Platform] workflows impliquant des jeux de données, reportez-vous aux tutoriels suivants :

* [Création d’un jeu de données à l’aide d’API](create.md)
* [Interrogation des données d’un jeu de données à l’aide de l’API Data Access](../../data-access/home.md)
* [Configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../../profile/tutorials/dataset-configuration.md)
