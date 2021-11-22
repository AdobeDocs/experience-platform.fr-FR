---
keywords: activer les destinations de profil ; activer les destinations ; activer les données ; activer les destinations de marketing par e-mail ; Activation des destinations de stockage dans le cloud
title: Activation des données d’audience vers des destinations d’exportation de profils par lots
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en envoyant des segments vers des destinations basées sur un profil de lot.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 822276890b6ebed922d359f8dece58d8c90dea24
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 7%

---

# Activation des données d’audience vers des destinations d’exportation de profils par lots

## Présentation {#overview}

Cet article explique le processus requis pour activer les données d’audience dans des destinations basées sur des profils de lot Adobe Experience Platform, telles que l’espace de stockage dans le cloud et les destinations de marketing par e-mail.

## Conditions préalables {#prerequisites}

Pour activer les données vers les destinations, vous devez avoir réussi [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez la variable **[!UICONTROL Catalogue]** .

   ![Onglet Catalogue de destinations](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activation des segments]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Bouton Activer les segments](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer vos segments, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Sélectionner la destination](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner vos segments ;](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Planification de l’exportation de segments {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Planning"
>abstract="Le type d’exportation de fichier (fichiers complets ou incrémentiels) et la planification ne peuvent pas être modifiés une fois le segment enregistré."
>additional-url="https://www.adobe.com/go/destinations-profile-batch-en" text="En savoir plus dans la documentation"

[!DNL Adobe Experience Platform] exporte des données pour les destinations de marketing par e-mail et de stockage dans le cloud sous la forme de [!DNL CSV] fichiers . Dans le **[!UICONTROL Planification]** , vous pouvez configurer le planning et les noms des fichiers pour chaque segment que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divise automatiquement les fichiers d’exportation à 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil.
>
>Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’un export plus important, en tant que tel : `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Sélectionnez la **[!UICONTROL Créer un planning]** bouton correspondant au segment que vous souhaitez envoyer à votre destination.

![Bouton Créer un planning](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exporter les fichiers complets {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Options d’exportation de fichiers"
>abstract="Sélectionner **Exporter les fichiers complets** pour exporter un instantané complet de tous les profils qualifiés pour le segment. <br> Sélectionner **Exportation de fichiers incrémentiels** pour n&#39;exporter que les profils qualifiés pour le segment depuis le dernier export. La première exportation de fichier incrémentielle comprend tous les profils qui remplissent les critères pour le segment, agissant comme un renvoi. Les futurs fichiers incrémentiels incluent uniquement les profils qualifiés pour le segment depuis le premier export de fichier incrémentiel."
>additional-url="https://www.adobe.com/go/destinations-profile-batch-en" text="En savoir plus dans la documentation"

Sélectionner **[!UICONTROL Exporter les fichiers complets]** pour déclencher l’exportation d’un fichier contenant un instantané complet de toutes les qualifications de profil pour le segment sélectionné.

![Exporter les fichiers complets](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Utilisez la variable **[!UICONTROL Fréquence]** sélecteur permettant de sélectionner la fréquence d&#39;export :

   * **[!UICONTROL Une fois]**: planifier une exportation de fichiers complète à la demande unique.
   * **[!UICONTROL Quotidien]**: planifier des exportations complètes de fichiers une fois par jour, tous les jours, au moment que vous spécifiez.

1. Utilisez la variable **[!UICONTROL Heure]** pour choisir l’heure, dans [!DNL UTC] format, date à laquelle l’exportation doit avoir lieu.

   >[!IMPORTANT]
   >
   >En raison de la configuration des processus Experience Platform internes, la première exportation incrémentielle ou complète de fichier peut ne pas contenir toutes les données de renvoi. <br> <br> Pour garantir une exportation complète et à jour des données de renvoi pour les fichiers complets et incrémentiels, Adobe recommande de définir l’heure d’exportation du premier fichier après 12h GMT le jour suivant. Cette limitation sera corrigée dans les prochaines versions.

1. Utilisez la variable **[!UICONTROL Date]** pour choisir le jour ou l’intervalle d’exportation.
   >[!TIP]
   >
   > Pour les exportations quotidiennes, définissez les dates de début et de fin afin de correspondre à la durée de vos campagnes sur vos plateformes en aval.
1. Sélectionner **[!UICONTROL Créer]** pour enregistrer le planning.


### Exportation de fichiers incrémentiels {#export-incremental-files}

Sélectionner **[!UICONTROL Exportation de fichiers incrémentiels]** pour déclencher une exportation où le premier fichier est un instantané complet de toutes les qualifications de profil pour le segment sélectionné, et les fichiers suivants sont des qualifications de profil incrémentielles depuis l’exportation précédente.

>[!IMPORTANT]
>
>Le premier fichier incrémentiel exporté comprend tous les profils qui remplissent les critères d’un segment et qui fonctionnent comme un renvoi.

![Exportation de fichiers incrémentiels](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Utilisez la variable **[!UICONTROL Fréquence]** sélecteur permettant de sélectionner la fréquence d&#39;export :

   * **[!UICONTROL Quotidien]**: planifier des exportations incrémentielles de fichiers une fois par jour, tous les jours, au moment que vous spécifiez.
   * **[!UICONTROL Horaire]**: planifier des exportations incrémentielles de fichiers toutes les 3, 6, 8 ou 12 heures.

1. Utilisez la variable **[!UICONTROL Heure]** pour choisir l’heure, dans [!DNL UTC] format, date à laquelle l’exportation doit avoir lieu.

   >[!IMPORTANT]
   >
   >En raison de la configuration des processus Experience Platform internes, la première exportation incrémentielle ou complète de fichier peut ne pas contenir toutes les données de renvoi. <br> <br> Pour garantir une exportation complète et à jour des données de renvoi pour les fichiers complets et incrémentiels, Adobe recommande de définir l’heure d’exportation du premier fichier après 12h GMT le jour suivant. Cette limitation sera corrigée dans les prochaines versions.

1. Utilisez la variable **[!UICONTROL Date]** pour choisir le jour ou l’intervalle d’exportation.
   >[!TIP]
   >
   >Définissez les dates de début et de fin pour correspondre à la durée de vos campagnes sur vos plateformes en aval.
1. Sélectionner **[!UICONTROL Créer]** pour enregistrer le planning.

### Configuration des noms de fichier {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Configuration du nom de fichier"
>abstract="Pour les destinations basées sur des fichiers, un nom de fichier unique est généré par segment. Utilisez l’éditeur de nom de fichier pour créer et modifier un nom de fichier unique ou conserver le nom par défaut."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#file-names" text="En savoir plus dans la documentation"

Les noms de fichier par défaut sont composés du nom de destination, de l’identifiant de segment et d’un indicateur de date et d’heure. Vous pouvez, par exemple, modifier les noms des fichiers exportés afin de faire la distinction entre les différentes campagnes ou d’ajouter le temps d’exportation des données aux fichiers.

Sélectionnez l’icône en forme de crayon pour ouvrir une fenêtre modale et modifier les noms des fichiers. Les noms de fichier sont limités à 255 caractères.

![configurer le nom du fichier](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Dans l’éditeur de nom de fichier, vous pouvez sélectionner différents composants à ajouter au nom du fichier.

![modifier les options de nom de fichier ;](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Le nom de destination et l’identifiant de segment ne peuvent pas être supprimés des noms de fichier. Vous pouvez en outre ajouter les éléments suivants :

* **[!UICONTROL Nom du segment]**: Vous pouvez ajouter le nom du segment au nom du fichier.
* **[!UICONTROL Date et heure]**: Effectuez une sélection entre l’ajout d’une `MMDDYYYY_HHMMSS` format ou horodatage Unix à 10 chiffres de l’heure de génération des fichiers. Choisissez l’une de ces options si vous souhaitez que vos fichiers aient un nom de fichier dynamique généré avec chaque export incrémentiel.
* **[!UICONTROL Texte personnalisé]**: Ajoutez du texte personnalisé aux noms des fichiers.

Sélectionner **[!UICONTROL Appliquer les modifications]** pour confirmer votre sélection.

>[!IMPORTANT]
> 
>Si vous ne sélectionnez pas l’option **[!UICONTROL Date et heure]** , les noms de fichier seront statiques et le nouveau fichier exporté remplacera le fichier précédent de votre emplacement de stockage par chaque exportation. Lors de l’exécution d’une tâche d’importation récurrente depuis un emplacement de stockage vers une plateforme de marketing par e-mail, il s’agit de l’option recommandée.

Une fois que vous avez terminé de configurer tous les segments, sélectionnez **[!UICONTROL Suivant]** pour continuer.

## Sélection des attributs de profil {#select-attributes}

Pour les destinations basées sur un profil, vous devez sélectionner les attributs de profil à envoyer à la destination cible.


1. Dans le **[!UICONTROL Sélectionner des attributs]** page, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Ajouter un nouveau mappage](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Sélectionnez la flèche située à droite du **[!UICONTROL Champ de schéma]** entrée .

   ![Sélectionner le champ source](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. Dans le **[!UICONTROL Sélectionner un champ]** , sélectionnez les attributs XDM à envoyer à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Sélectionner la page du champ source](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Pour ajouter d’autres mappages, répétez les étapes 1 à 3.

>[!NOTE]
>
> Adobe Experience Platform préremplit votre sélection avec quatre attributs recommandés couramment utilisés de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient comme suit, selon que `segmentMembership.status` est sélectionné :
* Si la variable `segmentMembership.status` champ sélectionné, les fichiers exportés incluent **[!UICONTROL Principal]** membres dans l’instantané complet initial et **[!UICONTROL Principal]** et **[!UICONTROL Expiré]** membres dans les exportations incrémentielles suivantes.
* Si la variable `segmentMembership.status` champ non sélectionné, les fichiers exportés incluent uniquement **[!UICONTROL Principal]** membres dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

![attributs recommandés](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Attributs obligatoires {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="A propos des attributs obligatoires"
>abstract="Sélectionnez les attributs de schéma XDM que tous les profils exportés doivent inclure. Les profils sans clé obligatoire ne sont pas exportés vers la destination. Si vous ne sélectionnez pas de clé obligatoire, tous les profils qualifiés sont exportés, quels que soient leurs attributs."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="En savoir plus dans la documentation"

Un attribut obligatoire est une case à cocher activée par l’utilisateur qui garantit que tous les enregistrements de profil contiennent l’attribut sélectionné. Par exemple : tous les profils exportés contiennent une adresse email. &#x200B;

Vous pouvez marquer les attributs comme étant obligatoires pour vous assurer que [!DNL Platform] exporte uniquement les profils qui incluent l’attribut spécifique. Par conséquent, il peut être utilisé comme une forme supplémentaire de filtrage. Le marquage d’un attribut comme obligatoire est **not** obligatoire.

Si vous ne sélectionnez pas d’attribut obligatoire, tous les profils qualifiés sont exportés, quels que soient leurs attributs.

Il est recommandé que l’un des attributs soit un [identifiant unique](../../destinations/catalog/email-marketing/overview.md#identity) de votre schéma. Pour plus d’informations sur les attributs obligatoires, reportez-vous à la section Identité de la section [Destinations de marketing par e-mail](../../destinations/catalog/email-marketing/overview.md#identity) documentation.

### Clés de déduplication {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="A propos des clés de déduplication"
>abstract="Éliminez plusieurs occurrences du même profil dans les fichiers dʼexportation en sélectionnant une clé de déduplication. Sélectionnez un espace de noms unique ou jusqu’à deux attributs de schéma XDM comme clé de déduplication. Si vous ne sélectionnez pas de clé de déduplication, il se peut que des entrées de profil soient dupliquées dans les fichiers d’exportation."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="En savoir plus dans la documentation"

Une clé de déduplication est une clé Principale définie par l’utilisateur qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils. &#x200B;

Les clés de déduplication éliminent la possibilité dʼavoir plusieurs enregistrements du même profil dans un fichier dʼexportation.

Vous pouvez utiliser les clés de déduplication de trois manières différentes dans [!DNL Platform]:

* Utilisation d’un espace de noms d’identité unique comme [!UICONTROL clé de déduplication]
* Utilisation d’un attribut de profil unique à partir d’un [!DNL XDM] profile as a [!UICONTROL clé de déduplication]
* Utilisation de deux attributs de profil d’une [!DNL XDM] profile as a composite key

>[!IMPORTANT]
>
> Vous pouvez exporter un espace de noms d’identité unique vers une destination et l’espace de noms est automatiquement défini comme clé de déduplication. L’envoi de plusieurs espaces de noms à une destination n’est pas pris en charge.
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
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
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
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
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

### Cas d’utilisation 1 de la déduplication : pas de déduplication {#deduplication-use-case-1}

Sans dédoublonnage, le fichier d&#39;export contiendrait les entrées suivantes.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Cas d’utilisation 2 de la déduplication : déduplication basée sur l’espace de noms d’identité {#deduplication-use-case-2}

En supposant une déduplication par le [!DNL Email] , le fichier d’exportation contiendra les entrées suivantes. Le profil B est le dernier qui a rempli les critères pour le segment. Il est donc le seul à être exporté.

| Adresse e-mail* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Cas d’utilisation 3 de la déduplication : déduplication basée sur un attribut de profil unique {#deduplication-use-case-3}

En supposant une déduplication par le `personal Email` , le fichier d’exportation contiendra l’entrée suivante. Le profil B est le dernier qui a rempli les critères pour le segment. Il est donc le seul à être exporté.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Cas d’utilisation 4 de la déduplication : déduplication basée sur deux attributs de profil {#deduplication-use-case-4}

Considérer la déduplication par la clé composite `personalEmail + lastName`, le fichier d’exportation contiendra les entrées suivantes.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe recommande de sélectionner un espace de noms d’identité, tel qu’un [!DNL CRM ID] ou adresse email comme clé de déduplication, pour s’assurer que tous les enregistrements de profil sont identifiés de manière unique.

>[!NOTE]
> 
>Si des libellés d’utilisation des données ont été appliqués à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu de données), l’application de ces libellés au niveau du champ lors de l’activation se produit dans les conditions suivantes :
>
>* Les champs sont utilisés dans la définition de segment.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination cible.

>
> Par exemple, si le champ `person.name.firstName` comporte certains libellés d’utilisation des données qui entrent en conflit avec l’action marketing de la destination. une violation de la stratégie d’utilisation des données s’afficherait dans l’étape de révision. Pour plus d’informations, voir [Gouvernance des données dans Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le workflow d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de stratégie, voir [Application des stratégies](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section documentation sur la gouvernance des données .

![violation de la politique de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

![Révision](../assets/ui/activate-batch-profile-destinations/review.png)

## Vérification de l’activation des segments {#verify}


Pour les destinations de marketing par e-mail et de stockage dans le cloud, Adobe Experience Platform crée une `.csv` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. Le format de fichier par défaut est le suivant :
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Les fichiers que vous pouvez recevoir pendant trois jours consécutifs peuvent ressembler à ceux-ci :

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation de la réussite de l’activation. Pour comprendre la structure des fichiers exportés, vous pouvez : [télécharger un exemple de fichier .csv](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Ce fichier d’exemple comprend les attributs de profil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, et `personalEmail.address`.
