---
title: Activer les audiences vers des destinations d’export de profils par lots
type: Tutorial
description: Découvrez comment activer les audiences que vous avez dans Adobe Experience Platform en les envoyant vers des destinations basées sur un profil de lot.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: d7a530c5ec2cad37b93273f5843609110d61cbfc
workflow-type: tm+mt
source-wordcount: '4077'
ht-degree: 55%

---


# Activer les audiences vers des destinations d’export de profils par lots

>[!IMPORTANT]
> 
> * Pour activer les audiences et activer l’ [ étape de mappage](#mapping) du workflow, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès.
> * Pour activer les audiences sans passer par l’[ étape de mappage](#mapping) du workflow, vous avez besoin des autorisations **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer le segment sans mappage]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le processus requis pour activer les audiences dans Adobe Experience Platform vers des destinations basées sur des fichiers de profil par lot, telles que l’espace de stockage dans le cloud et les destinations de marketing par e-mail.

## Conditions préalables {#prerequisites}

Pour activer les audiences vers les destinations, [ doit être connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Formats de fichiers pris en charge pour l’exportation {#supported-file-formats-export}

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="Mettre à jour la date de fin de ce flux de données"
>abstract="Mettre à jour la date de fin de ce flux de données"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="Mettre à jour la date de fin de ce corps de flux de données"
>abstract="En raison des mises à jour récentes apportées à cette destination, le flux de données nécessite désormais une date de fin. Adobe a défini une date de fin par défaut sur le 1er mars 2025. Mettez à jour à la date de fin souhaitée, sinon les exportations de données s’arrêteront à la date par défaut."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Modifier le chemin du dossier"
>abstract="Utilisez plusieurs macros fournies pour personnaliser le chemin du dossier dans lequel les jeux de données sont exportés."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Aperçu du chemin du dossier du jeu de données"
>abstract="Obtenez un aperçu de la structure de dossiers créée à l’emplacement de stockage en fonction des macros que vous avez ajoutées dans cette fenêtre."

Les formats de fichiers suivants sont pris en charge lors de l’exportation d’audiences :

* CSV
* JSON
* Parquet

Notez que l’exportation de fichiers CSV vous offre une plus grande flexibilité en termes de structure de vos fichiers exportés. En savoir plus sur la [configuration de formatage de fichier pour les fichiers CSV](/help/destinations/ui/batch-destinations-file-formatting-options.md#file-configuration).

Sélectionnez le format de fichier souhaité pour l’exportation lors de la [création d’une connexion à la destination basée sur les fichiers](/help/destinations/ui/connect-destination.md).

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Image montrant comment accéder à l’onglet Catalogue de destinations.](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les audiences]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos audiences, comme illustré dans l’image ci-dessous.

   ![Activer le contrôle des audiences mis en surbrillance dans la page du catalogue.](../assets/ui/activate-batch-profile-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination que vous souhaitez utiliser pour activer vos audiences, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Des cases à cocher mises en surbrillance pour sélectionner une ou plusieurs destinations pour activer les audiences.](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Passez à la section suivante pour [sélectionner vos audiences](#select-audiences).

## Sélectionner vos audiences {#select-audiences}

Pour sélectionner les audiences que vous souhaitez activer vers la destination, utilisez les cases à cocher à gauche des noms d’audience, puis sélectionnez **[!UICONTROL Suivant]**.

Vous pouvez sélectionner plusieurs types d’audiences, selon leur origine :

* **[!UICONTROL Service de segmentation]** : audiences générées dans Experience Platform par le service de segmentation. Pour plus d’informations, consultez la [documentation sur la segmentation](../../segmentation/ui/overview.md) .
* **[!UICONTROL Téléchargement personnalisé]** : audiences générées en dehors de l’Experience Platform et téléchargées dans Platform sous la forme de fichiers CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur l&#39; [import d&#39;une audience](../../segmentation/ui/audience-portal.md#import-audience).
* Autres types d’audiences, provenant d’autres solutions d’Adobe, telles que [!DNL Audience Manager].

![Des cases à cocher s’affichent lors de la sélection d’une ou de plusieurs audiences à activer.](../assets/ui/activate-batch-profile-destinations/select-audiences.png)

>[!TIP]
>
>La sélection d’audiences provenant de **[!UICONTROL téléchargements personnalisés]** active automatiquement l’étape [Sélectionner les attributs d’enrichissement](#select-enrichment-attributes).

>[!TIP]
>
>Vous pouvez supprimer des audiences des flux d’activation existants de la page **[!UICONTROL Données d’activation]** . Pour plus d’informations, consultez la [documentation dédiée](../ui/destination-details-page.md#bulk-remove) .

## Planifier l’export d’audience {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Planning"
>abstract="Utilisez l’icône en forme de crayon pour définir le type d’exportation de fichier (fichiers complets ou incrémentiels) et la fréquence d’exportation."

[!DNL Adobe Experience Platform] exporte les données pour les destinations de marketing par e-mail et de stockage dans le cloud sous la forme de [différents types de fichiers](#supported-file-formats-export). Sur la page **[!UICONTROL Planification]** , vous pouvez configurer le planning et les noms des fichiers pour chaque audience que vous exportez.

Experience Platform définit automatiquement un planning par défaut pour chaque export de fichier. Vous pouvez modifier la planification par défaut selon vos besoins, en cliquant sur l’icône en forme de crayon en regard de chaque planification, puis en définissant une planification personnalisée.

![Modifier le contrôle de planification en surbrillance dans l’étape de planification.](../assets/ui/activate-batch-profile-destinations/edit-default-schedule.png)

>[!TIP]
>
>Vous pouvez modifier les calendriers d’activation de l’audience pour les flux d’activation existants à partir de la page **[!UICONTROL Données d’activation]** . Pour plus d’informations, consultez la documentation sur la [modification en masse des plannings d’activation](../ui/destination-details-page.md#bulk-edit-schedule) .

>[!IMPORTANT]
>
>[!DNL Adobe Experience Platform] divise automatiquement les fichiers d’exportation à 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil.
>
>Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`.

### Exporter des fichiers complets {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Options d’exportation de fichiers"
>abstract="Sélectionnez **Exporter des fichiers complets** pour exporter une capture instantanée complète de tous les profils qui remplissent les critères pour l’audience. Sélectionnez **Exporter des fichiers incrémentiels** pour n’exporter que les profils qui remplissent les critères pour l’audience depuis le dernier export. <br> Le premier export de fichier incrémentiel comprend tous les profils qui remplissent les critères pour l’audience, agissant comme un renvoi. Les futurs fichiers incrémentiels incluent uniquement les profils qui remplissent les critères pour l’audience depuis le premier export de fichier incrémentiel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=fr#export-incremental-files" text="Exporter des fichiers incrémentiels"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Activer après l’évaluation des audiences"
>abstract="L’activation s’exécute immédiatement une fois la tâche de segmentation quotidienne terminée. Ainsi, les profils les plus à jour sont exportés."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Activation planifiée"
>abstract="L’activation s’exécute à une heure fixe de la journée."

Sélectionnez **[!UICONTROL Exporter les fichiers complets]** pour déclencher l’exportation d’un fichier contenant un instantané complet de toutes les qualifications de profil pour l’audience sélectionnée.

![Bascule de l’export des fichiers complets sélectionné.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Utilisez le sélecteur **[!UICONTROL Fréquence]** pour sélectionner la fréquence d’exportation :

   * **[!UICONTROL Une fois]** : planifiez une exportation de fichiers complets sur demande unique.
   * **[!UICONTROL Tous les jours]** : planifiez des exportations de fichiers complets une fois par jour, tous les jours, au moment choisi.

2. Utilisez le bouton d’activation/désactivation **[!UICONTROL Time]** pour sélectionner si l’exportation doit avoir lieu immédiatement après l’évaluation de l’audience ou sur une base planifiée, à une heure donnée. Lorsque vous sélectionnez la variable **[!UICONTROL Planifié]**, vous pouvez utiliser le sélecteur pour choisir l’heure du jour à laquelle l’exportation doit avoir lieu, au format [!DNL UTC].

   >[!NOTE]
   >
   >L’option **[!UICONTROL Après l’évaluation du segment]** décrite ci-dessous est disponible uniquement pour sélectionner les clients Beta.

   Utiliser l’option **[!UICONTROL Après l’évaluation du segment]** pour que le traitement d’activation s’exécute immédiatement après la fin du traitement quotidien de segmentation par lots de Platform. Cette option garantit que lorsque la tâche d’activation s’exécute, les profils les plus récents sont exportés vers votre destination.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Image mettant en surbrillance l’option Après l’évaluation du segment dans le flux d’activation pour les destinations par lots.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Utilisez l’option **[!UICONTROL Planifié]** pour que la tâche d’activation s’exécute à une heure déterminée. Cette option garantit que les données de profil Experience Platform sont exportées simultanément chaque jour. Toutefois, les profils que vous exportez peuvent ne pas être les plus à jour, selon que la tâche de segmentation par lots est terminée avant le lancement de la tâche d’activation.

   ![Image mettant en surbrillance l’option Planifié dans le flux d’activation pour les destinations par lots et affichant le sélecteur de l’heure.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

3. Utilisez le sélecteur **[!UICONTROL Date]** pour choisir le jour ou l’intervalle d’exportation. Pour les exportations quotidiennes, il est recommandé de définir les dates de début et de fin de sorte qu’elles correspondent à la durée de vos campagnes sur vos plateformes en aval.

   >[!IMPORTANT]
   >
   > Lors de la sélection d’un intervalle d’exportation, le dernier jour de l’intervalle n’est pas inclus dans les exportations. Par exemple, si vous sélectionnez un intervalle entre le 4 et le 11 janvier, la dernière exportation de fichier aura lieu le 10 janvier.

4. Sélectionnez **[!UICONTROL Créer]** pour enregistrer le planning.

### Exporter des fichiers incrémentiels

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_something"
>title="Configurer le nom d’un fichier"
>abstract="Pour les destinations basées sur des fichiers, un nom de fichier unique est généré par audience. Utilisez l’éditeur de nom de fichier pour créer et modifier un nom de fichier unique ou conserver le nom par défaut."

Sélectionnez **[!UICONTROL Exporter les fichiers incrémentiels]** pour déclencher une exportation où le premier fichier est un instantané complet de toutes les qualifications de profil pour l’audience sélectionnée, et les fichiers suivants sont des qualifications de profil incrémentielles depuis l’exportation précédente.

>[!IMPORTANT]
>
>Le premier fichier incrémentiel exporté comprend tous les profils qui remplissent les critères d’une audience et qui fonctionnent comme un renvoi.

![Bascule de l’export des fichiers incrémentiels sélectionné.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Utilisez le sélecteur **[!UICONTROL Fréquence]** pour sélectionner la fréquence d’exportation :

   * **[!UICONTROL Tous les jours]** : planification d’exportations de fichiers incrémentiels une fois par jour, tous les jours, au moment choisi.
   * **[!UICONTROL Par heure]** : planification d’exportations de fichiers incrémentiels toutes les 3, 6, 8 ou 12 heures.

2. Utilisez le sélecteur **[!UICONTROL Heure]** pour choisir l’heure de la journée, au format [!DNL UTC], à laquelle l’exportation doit avoir lieu.

3. Utilisez le sélecteur **[!UICONTROL Date]** pour choisir l’intervalle au cours duquel l’exportation doit avoir lieu. La bonne pratique consiste à définir les dates de début et de fin de sorte qu’elles correspondent à la durée de vos campagnes sur vos plateformes en aval.

   >[!IMPORTANT]
   >
   >Le dernier jour de l’intervalle n’est pas inclus dans les exportations. Par exemple, si vous sélectionnez un intervalle entre le 4 et le 11 janvier, la dernière exportation de fichier aura lieu le 10 janvier.

4. Sélectionnez **[!UICONTROL Créer]** pour enregistrer le planning.

### Configurer les noms de fichiers

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Configurer le nom d’un fichier"
>abstract="Pour les destinations basées sur des fichiers, un nom de fichier unique est généré par audience. Utilisez l’éditeur de nom de fichier pour créer et modifier un nom de fichier unique ou conserver le nom par défaut."

Pour la plupart des destinations, les noms de fichier par défaut se composent du nom de destination, de l’ID d’audience et d’un indicateur de date et d’heure. Vous pouvez, par exemple, modifier les noms des fichiers exportés afin de faire la distinction entre les différentes campagnes ou pour ajouter le temps d’exportation des données aux fichiers. Remarque : certains développeurs peuvent choisir d’ajouter différentes options de nom de fichier par défaut pour leurs destinations. 

Pour ouvrir une fenêtre modale et modifier les noms de fichier, sélectionnez l’icône représentant un crayon. Les noms de fichier sont limités à 255 caractères.

>[!NOTE]
>
>L’image ci-dessous montre comment les noms de fichiers peuvent être modifiés pour les destinations [!DNL Amazon S3], mais le processus est identique pour toutes les destinations par lots (par exemple, SFTP, [!DNL Azure Blob Storage] ou [!DNL Google Cloud Storage]).

![Image mettant en surbrillance l’icône représentant un crayon, utilisée pour configurer les noms de fichier.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Dans l’éditeur de nom de fichier, vous pouvez sélectionner différents composants à ajouter au nom du fichier.

![Image montrant toutes les options de nom de fichier disponibles.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Le nom de destination et l’ID d’audience ne peuvent pas être supprimés des noms de fichier. Outre ces options, vous pouvez ajouter les options suivantes :

| Option de nom de fichier | Description |
|---------|----------|
| **[!UICONTROL Nom de l’audience]** | Nom de l’audience exportée. |
| **[!UICONTROL Date et heure]** | Choisissez entre l’ajout d’un format `MMDDYYYY_HHMMSS` ou d’un horodatage UNIX à 10 chiffres de l’heure de génération des fichiers. Choisissez l’une de ces options si vous souhaitez que vos fichiers aient un nom de fichier dynamique généré avec chaque exportation de fichier incrémentiel. |
| **[!UICONTROL Texte personnalisé]** | Tout texte personnalisé que vous souhaitez ajouter aux noms de fichier. |
| **[!UICONTROL Identifiant de destination]** | L’identifiant du flux de données de destination que vous utilisez pour exporter l’audience. |
| **[!UICONTROL Nom de la destination]** | Nom du flux de données de destination que vous utilisez pour exporter l’audience. |
| **[!UICONTROL Nom de l’organisation]** | Nom de votre organisation dans Experience Platform. |
| **[!UICONTROL Nom du sandbox]** | ID de l’environnement de test que vous utilisez pour exporter l’audience. |

{style="table-layout:auto"}

Sélectionnez **[!UICONTROL Appliquer les modifications]** pour confirmer votre sélection.

>[!IMPORTANT]
> 
>Si vous ne sélectionnez pas l’option **[!UICONTROL Date et heure]**, les noms de fichier seront statiques et le nouveau fichier exporté remplacera le fichier précédent de votre emplacement de stockage à chaque exportation. L’option recommandée consiste à exécuter une tâche d’importation récurrente depuis un emplacement de stockage vers une plateforme de marketing par e-mail.

Une fois la configuration de toutes vos audiences terminée, sélectionnez **[!UICONTROL Suivant]** pour continuer.

## Mappage {#mapping}

Au cours de cette étape, vous devez sélectionner les attributs de profil à ajouter aux fichiers exportés vers la destination cible. Pour sélectionner les attributs de profil et les identités à exporter :

1. Sur la page **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Ajouter un nouveau mapping]**.

   ![Ajouter un nouveau contrôle de champ en surbrillance dans le workflow de mappage.](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Champ source]**.

   ![Sélectionnez le contrôle du champ source en surbrillance dans le workflow de mappage.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. Sur la page **[!UICONTROL Sélectionner le champ source]**, sélectionnez les attributs et les identités de profil à inclure dans les fichiers exportés vers la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   >[!TIP]
   > 
   >Vous pouvez utiliser le champ de recherche pour affiner votre sélection, comme illustré dans l’image ci-dessous.

   Utilisez le bouton d’activation/désactivation **[!UICONTROL Afficher uniquement les champs avec données]** pour n’afficher que les champs de schéma renseignés avec des valeurs. Par défaut, seuls les champs de schéma renseignés sont affichés.

   ![Fenêtre modale présentant les attributs de profil qui peuvent être exportés vers la destination.](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. Le champ que vous avez sélectionné pour l’exportation apparaît désormais dans la vue de mappage. Si vous le souhaitez, vous pouvez modifier le nom de l’en-tête dans le fichier exporté. Pour cela, sélectionnez l’icône dans le champ cible.

   ![Fenêtre modale présentant les attributs de profil qui peuvent être exportés vers la destination.](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. Sur la page **[!UICONTROL Sélectionner le champ cible]**, saisissez le nom souhaité de l’en-tête dans le fichier exporté, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Fenêtre modale présentant un nom convivial saisi pour un en-tête.](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. Le champ que vous avez sélectionné pour l’exportation apparaît désormais dans la vue de mappage et affiche l’en-tête modifié dans le fichier exporté.

   ![Fenêtre modale présentant les attributs de profil qui peuvent être exportés vers la destination.](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Facultatif) L’ordre des champs mappés dans l’interface utilisateur se reflète dans l’ordre des colonnes du fichier CSV exporté, de haut en bas, la rangée supérieure étant la colonne la plus à gauche du fichier CSV. Vous pouvez réorganiser les champs mappés comme vous le souhaitez, en faisant glisser les lignes de mappage, comme illustré ci-dessous.

   >[!NOTE]
   >
   >Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe.

   ![Enregistrement présentant les champs de mappage réorganisés par glisser-déposer.](../assets/ui/activate-batch-profile-destinations/reorder-fields.gif)

1. (Facultatif) Vous pouvez sélectionner le champ exporté en tant que [clé obligatoire](#mandatory-keys) ou [clé de déduplication](#deduplication-keys).

   ![Fenêtre modale présentant les attributs de profil qui peuvent être exportés vers la destination.](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Pour ajouter d’autres champs à exporter, répétez les étapes ci-dessus.

### Attributs obligatoires {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="À propos des attributs obligatoires"
>abstract="Sélectionnez les attributs de schéma XDM que tous les profils exportés doivent inclure. Les profils sans clé obligatoire ne sont pas exportés vers la destination. Si vous ne sélectionnez pas de clé obligatoire, tous les profils qualifiés sont exportés, quels que soient leurs attributs."

Un attribut obligatoire est une case à cocher activée par l’utilisateur qui garantit que tous les enregistrements de profil contiennent l’attribut sélectionné. Par exemple : tous les profils exportés contiennent une adresse e-mail.

Vous pouvez marquer les attributs comme étant obligatoires afin de vous assurer que [!DNL Platform] exporte uniquement les profils qui incluent l’attribut spécifique. Par conséquent, cette action peut être utilisée comme une forme supplémentaire de filtrage. Le marquage d’un attribut comme étant obligatoire **n’est pas** requis.

Si vous ne sélectionnez pas d’attribut obligatoire, tous les profils qualifiés sont exportés, quels que soient leurs attributs.

Il est recommandé que l’un des attributs soit un [identifiant unique](../../destinations/catalog/email-marketing/overview.md#identity) de votre schéma. Pour plus d’informations sur les attributs obligatoires, consultez la section Identité dans la documentation [Destinations de marketing par e-mail](../../destinations/catalog/email-marketing/overview.md#identity).

### Clés de déduplication {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="À propos des clés de déduplication"
>abstract="Éliminez plusieurs occurrences du même profil dans les fichiers dʼexportation en sélectionnant une clé de déduplication. Sélectionnez un seul espace de noms ou jusquʼà deux attributs de schéma XDM comme clé de déduplication. Si vous ne sélectionnez pas de clé de déduplication, il se peut que des entrées de profil soient dupliquées dans les fichiers d’exportation."

Une clé de déduplication est une clé primaire définie par l’utilisateur qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils.

Les clés de déduplication empêchent dʼavoir plusieurs enregistrements du même profil dans un fichier dʼexportation.

Vous pouvez utiliser les clés de déduplication de trois manières différentes dans :[!DNL Platform]

* Utiliser un espace de noms d’identité unique comme [!UICONTROL clé de déduplication]
* Utiliser un attribut de profil unique à partir d’un profil [!DNL XDM] comme [!UICONTROL clé de déduplication]
* Utiliser une combinaison de deux attributs de profil à partir d’un profil [!DNL XDM] en tant que clé composite

>[!IMPORTANT]
>
> Vous pouvez exporter un espace de noms d’identité unique vers une destination, l’espace de noms étant alors automatiquement défini comme clé de déduplication. L’envoi de plusieurs espaces de noms vers une destination n’est pas pris en charge.
> 
> Vous ne pouvez pas utiliser une combinaison d’espaces de noms d’identité et d’attributs de profil comme clés de déduplication.

### Exemple de déduplication {#deduplication-example}

Cet exemple illustre le fonctionnement de la déduplication, en fonction des clés de déduplication sélectionnées.

Examinons les deux profils suivants.

**Profil A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "doejohn_1@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profil B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_2@example.com"
      },
      {
        "id": "doejohn_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Cas d’utilisation 1 de la déduplication : pas de déduplication {#deduplication-use-case-1}

Sans déduplication, le fichier d’exportation contiendrait les entrées suivantes.

| E-mail personnel | Prénom | Nom |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Cas d’utilisation 2 de la déduplication : déduplication basée sur l’espace de noms d’identité {#deduplication-use-case-2}

En supposant une déduplication par l’espace de noms [!DNL Email], le fichier d’exportation contiendra les entrées suivantes. Le profil B est le dernier qui s’est qualifié pour l’audience, c’est donc le seul à être exporté.

| Adresse e-mail* | E-mail personnel | Prénom | Nom |
|---|---|---|---|
| johndoe_2@example.com | johndoe@example.com | John | D |
| doejohn_2@example.com | johndoe@example.com | John | D |

### Cas d’utilisation 3 de la déduplication : déduplication basée sur un attribut de profil unique {#deduplication-use-case-3}

En supposant une déduplication par l’attribut `personal Email`, le fichier d’exportation contiendra l’entrée suivante. Le profil B est le dernier qui s’est qualifié pour l’audience, c’est donc le seul à être exporté.

| E-mail personnel* | Prénom | Nom |
|---|---|---|
| johndoe@example.com | John | D |


### Cas d’utilisation 4 de la déduplication : déduplication basée sur deux attributs de profil {#deduplication-use-case-4}

En supposant une déduplication par la clé composite `personalEmail + lastName`, le fichier d’exportation contiendra les entrées suivantes.

| E-mail personnel* | Nom* | Prénom |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |

Adobe recommande de sélectionner un espace de noms d’identité, tel qu’un [!DNL CRM ID] ou une adresse e-mail comme clé de déduplication, pour s’assurer que tous les enregistrements de profil sont identifiés de manière unique.

>[!NOTE]
> 
>Si des libellés d’utilisation des données ont été appliqués à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu), l’application de ces libellés au niveau du champ sur l’activation se fait dans les conditions suivantes :
>
>* Les champs sont utilisés dans la définition de l’audience.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination cible.
>
> Par exemple, si le champ `person.name.firstName` comporte certains libellés d’utilisation des données entrant en conflit avec l’action marketing de la destination, une violation de la politique d’utilisation des données s’afficherait dans l’étape de révision. Pour plus d’informations, voir [Gouvernance des données dans Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

### [!BADGE Beta]{type=Informative} Exporter des tableaux par le biais de champs calculés {#export-arrays-calculated-fields}

Certains clients bêta peuvent exporter des objets de tableau d’Experience Platform vers des destinations de stockage dans le cloud. Pour en savoir plus sur l’ [export de tableaux et de champs calculés](/help/destinations/ui/export-arrays-calculated-fields.md) et contactez votre représentant d’Adobe pour accéder à la fonctionnalité.

### Limites connues {#known-limitations}

La nouvelle page **[!UICONTROL Mappage]** présente les limitations connues suivantes :

#### L’attribut d’appartenance à une audience ne peut pas être sélectionné via le workflow de mappage.

En raison d’une limitation connue, vous ne pouvez actuellement pas utiliser la fenêtre **[!UICONTROL Sélectionner un champ]** pour ajouter `segmentMembership.seg_namespace.seg_id.status` à vos exportations de fichiers. Vous devez plutôt coller manuellement la valeur `xdm: segmentMembership.seg_namespace.seg_id.status` dans le champ de schéma, comme illustré ci-dessous.

![Enregistrement de l’écran montrant la solution de l’appartenance à l’audience à l’étape de mappage du workflow d’activation.](../assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)


>[!NOTE]
>
Pour les destinations de stockage dans le cloud, les attributs suivants sont ajoutés par défaut au mappage :
>
* `segmentMembership.seg_namespace.seg_id.status`
* `segmentMembership.seg_namespace.seg_id.lastQualificationTime`

Les exportations de fichiers varient comme suit, selon que `segmentMembership.seg_namespace.seg_id.status` est sélectionné :

* Si le champ `segmentMembership.seg_namespace.seg_id.status` est sélectionné, les fichiers exportés incluent des membres **[!UICONTROL Actif]** dans l’instantané complet initial et de nouveaux membres **[!UICONTROL Actif]** et **[!UICONTROL Expiré]** dans les exportations incrémentielles suivantes.
* Si le champ `segmentMembership.seg_namespace.seg_id.status` n’est pas sélectionné, les fichiers exportés incluent uniquement les membres **[!UICONTROL actifs]** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

En savoir plus sur le [comportement d’exportation de profils pour les destinations basées sur des fichiers](/help/destinations/how-destinations-work/profile-export-behavior.md#file-based-destinations).

#### Les espaces de noms d’identité ne peuvent actuellement pas être sélectionnés pour les exportations.

La sélection des espaces de noms d’identité à exporter, comme illustrée dans l’image ci-dessous, n’est actuellement pas prise en charge. La sélection des espaces de noms d’identité à exporter entraîne une erreur dans l’étape **[!UICONTROL Révision]**.

![ Mappage non pris en charge affichant les exportations d’identité.](../assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

En tant que solution temporaire, si vous devez ajouter des espaces de noms d’identité aux fichiers exportés au cours de la version bêta, vous pouvez effectuer l’une des opérations suivantes :
* Utiliser les destinations de stockage dans le cloud héritées pour les flux de données dans lesquels vous souhaitez inclure des espaces de noms d’identité dans les exportations.
* Charger les identités en tant qu’attributs dans Experience Platform, puis les exporter vers vos destinations de stockage dans le cloud.

## Sélectionner des attributs de profil {#select-attributes}

>[!IMPORTANT]
> 
Toutes les destinations de stockage dans le cloud du catalogue peuvent afficher une [[!UICONTROL étape de mappage]](#mapping) améliorée qui remplace l’étape **[!UICONTROL Sélectionner des attributs]** décrite dans cette section.
>
Cette étape **[!UICONTROL Sélectionner les attributs]** s’affiche toujours pour les destinations de marketing par e-mail Adobe Campaign, Oracle Responsys, Oracle Eloqua et Salesforce Marketing Cloud.

Pour les destinations basées sur un profil, vous devez sélectionner les attributs de profil à envoyer à la destination cible.

1. Sur la page **[!UICONTROL Sélectionner des attributs]**, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Image mettant en surbrillance le bouton Ajouter un nouveau champ.](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

2. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Champ de schéma]**.

   ![Image mettant en surbrillance comment sélectionner un champ source.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

3. Dans la page **[!UICONTROL Sélectionner un champ]**, sélectionnez les attributs XDM ou les espaces de noms d’identité à envoyer à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Image mettant en surbrillance les différents champs disponibles en tant que champs source.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

4. Pour ajouter d’autres mappages, répétez les étapes une à trois.

>[!NOTE]
>
Adobe Experience Platform préremplit votre sélection avec quatre attributs recommandés couramment utilisés de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.seg_namespace.seg_id.status`.

![Image montrant les attributs recommandés préremplis dans l’étape de mappage du workflow d’activation de l’audience.](../assets/ui/activate-batch-profile-destinations/prefilled-fields.png)

>[!IMPORTANT]
>
En raison d’une limitation connue, vous ne pouvez actuellement pas utiliser la fenêtre **[!UICONTROL Sélectionner un champ]** pour ajouter `segmentMembership.seg_namespace.seg_id.status` à vos exportations de fichiers. Au lieu de cela, vous devez coller manuellement la valeur `xdm: segmentMembership.seg_namespace.seg_id.status` dans le champ de schéma, comme illustré ci-dessous.
>
![Enregistrement de l’écran montrant la solution de l’appartenance à l’audience à l’étape de mappage du workflow d’activation.](..//assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Les exportations de fichiers varient comme suit, selon que `segmentMembership.seg_namespace.seg_id.status` est sélectionné ou non :
* Si le champ `segmentMembership.seg_namespace.seg_id.status` est sélectionné, les fichiers exportés incluent les membres **[!UICONTROL actifs]** dans l’instantané complet initial ainsi que les membres **[!UICONTROL actifs]** et **[!UICONTROL expirés]** dans les exportations incrémentielles suivantes.
* Si le champ `segmentMembership.seg_namespace.seg_id.status` n’est pas sélectionné, les fichiers exportés incluent uniquement les membres **[!UICONTROL actifs]** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

## Sélectionner les attributs d’enrichissement {#select-enrichment-attributes}

[!CONTEXTUALHELP]
id="platform_destinations_activate_exclude_enrichment_attributes"
title="Exclure les attributs d’enrichissement"
abstract="Activez cette option pour exporter les profils des audiences chargées personnalisées sélectionnées vers votre destination, tout en excluant leurs attributs."

>[!IMPORTANT]
>
Cette étape s’affiche uniquement si vous avez sélectionné des audiences **[!UICONTROL Téléchargement personnalisé]** au cours de l’étape [sélection d’audience](#select-audiences).

Les attributs d’enrichissement correspondent à des audiences téléchargées personnalisées ingérées dans Experience Platform sous la forme de **[!UICONTROL téléchargements personnalisés]**. Au cours de cette étape, vous pouvez sélectionner les attributs à exporter vers votre destination, pour chaque audience externe sélectionnée.

![Image de l&#39;interface utilisateur montrant l&#39;étape de sélection des attributs d&#39;enrichissement.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes-step.png)

Suivez les étapes ci-dessous pour sélectionner les attributs d’enrichissement pour chaque audience externe :

1. Dans la colonne **[!UICONTROL Attributs d&#39;enrichissement]**, sélectionnez le bouton ![Modifier](/help/images/icons/edit.png) (Modifier).
1. Sélectionnez **[!UICONTROL Ajouter un attribut d’enrichissement]**. Un nouveau champ de schéma vide s’affiche.
   ![Image de l&#39;interface utilisateur affichant l&#39;écran modal des attributs d&#39;enrichissement.](../assets/ui/activate-batch-profile-destinations/add-enrichment-attribute.png)
1. Sélectionnez le bouton situé à droite du champ vide pour ouvrir l’écran de sélection du champ.
1. Sélectionnez les attributs à exporter pour l’audience.
   ![Image de l&#39;interface utilisateur affichant la liste des attributs d&#39;enrichissement.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes.png)
1. Après avoir ajouté tous les attributs à exporter, sélectionnez **[!UICONTROL Enregistrer et fermer]**.
1. Répétez ces étapes pour chaque audience externe.

Si vous souhaitez activer des audiences externes vers vos destinations sans exporter d’attribut, activez le bouton d’activation/désactivation **[!UICONTROL Exclure les attributs d’enrichissement]** . Cette option exporte les profils des audiences externes, mais aucun de leurs attributs correspondants n’est envoyé vers votre destination.

![Image de l’interface utilisateur affichant le bouton d’activation/désactivation des attributs d’enrichissement d’exclusion.](../assets/ui/activate-batch-profile-destinations/exclude-enrichment-attributes.png)

Sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape [Révision](#review).

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Résumé de sélection affiché à l’étape de révision.](../assets/ui/activate-batch-profile-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

[!CONTEXTUALHELP]
id="platform_governance_policies_viewApplicableConsentPolicies"
title="Affichage des politiques de consentement applicables"
abstract="Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. Ce contrôle est désactivé si votre entreprise n&#39;a pas accès aux SKU mentionnés ci-dessus."

Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. Pour plus d’informations, consultez la section [Évaluation de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Vérifications des stratégies d’utilisation des données {#data-usage-policy-checks}

À l’étape **[!UICONTROL Réviser]**, Experience Platform recherche également toutes les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la façon de résoudre les violations de stratégie, reportez-vous à la section [Violations de stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) de la documentation sur la gouvernance des données.

![Exemple de violation de politique de données illustré dans le workflow d’activation.](../assets/common/data-policy-violation.png)

### Filtrage des audiences {#filter-audiences}

En outre, au cours de cette étape, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mapping a été mis à jour dans le cadre de ce workflow. Vous pouvez également basculer entre les colonnes du tableau que vous souhaitez afficher.

![Enregistrement de l’écran montrant les filtres d’audience disponibles dans l’étape de révision.](../assets/ui/activate-batch-profile-destinations/filter-audiences-batch-review.gif)

Si votre sélection vous satisfait et qu’aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

## Vérification de l’activation de l’audience {#verify}

Lors de l’exportation d’audiences vers des destinations de stockage dans le cloud, Adobe Experience Platform crée un fichier `.csv`, `.json` ou `.parquet` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce qu’un nouveau fichier soit créé dans votre emplacement de stockage selon le planning défini dans le workflow. Le format de fichier par défaut est illustré ci-dessous, mais vous pouvez [modifier les composants du nom de fichier](#file-names) :
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Par exemple, si vous avez sélectionné une fréquence d’exportation quotidienne, les fichiers que vous recevrez pendant trois jours consécutifs peuvent ressembler à ceci :

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation de la réussite de l’activation. Pour comprendre la structure des fichiers exportés, vous pouvez [télécharger un exemple de fichier .csv](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Cet exemple de fichier comprend les attributs de profil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` et `personalEmail.address`.
