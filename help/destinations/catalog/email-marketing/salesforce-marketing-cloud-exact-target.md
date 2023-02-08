---
keywords: e-mail;e-mail;destinations d’e-mail;salesforce;api salesforce destination marketing cloud
title: (API) Connexion à Salesforce Marketing Cloud
description: La destination de Marketing Cloud Salesforce (anciennement connue sous le nom d’ExactTarget) vous permet d’exporter les données de votre compte et de les activer dans le Marketing Cloud Salesforce pour répondre aux besoins de votre entreprise.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: d75c272b3c86e25d3f162c630963c10e8206bd9d
workflow-type: tm+mt
source-wordcount: '2434'
ht-degree: 29%

---

# Connexion [!DNL (API) Salesforce Marketing Cloud]

## Présentation {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (anciennement connu sous le nom de [!DNL ExactTarget]) est une suite de marketing numérique qui vous permet de créer et de personnaliser des parcours pour que les visiteurs et les clients puissent personnaliser leur expérience.

>[!IMPORTANT]
>
>Notez la différence entre cette connexion et l’autre [[!DNL Salesforce Marketing Cloud] connection](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) qui se trouve dans la section Catalogue des emails . L’autre connexion au Marketing Cloud Salesforce vous permet d’exporter des fichiers vers un emplacement de stockage spécifié, alors qu’il s’agit d’une connexion en continu basée sur l’API.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [!DNL Salesforce Marketing Cloud] [mettre à jour les contacts](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API qui vous permet d’ajouter des contacts/de mettre à jour les données de contact pour vos besoins professionnels après les avoir activés dans une nouvelle [!DNL Salesforce Marketing Cloud] segment.

[!DNL Salesforce Marketing Cloud] utilise OAuth 2 avec les informations d’identification du client comme mécanisme d’authentification pour communiquer avec le [!DNL Salesforce Marketing Cloud] API. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Salesforce Marketing Cloud] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL (API) Salesforce Marketing Cloud] destination, voici un exemple de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service des ventes d’une plateforme de location de maisons souhaite diffuser un email marketing à un public client ciblé. L’équipe marketing de la plateforme peut ajouter de nouveaux contacts/mettre à jour des contacts existants *(et leurs adresses électroniques)* via Adobe Experience Platform, créez des segments à partir de leurs propres données hors ligne et envoyez ces segments à [!DNL Salesforce Marketing Cloud], qui peut ensuite être utilisé pour envoyer l’email de la campagne marketing.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL (API) Salesforce Marketing Cloud], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=fr) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre [!DNL Salesforce Marketing Cloud] compte :

#### Vous devez avoir un compte [!DNL Salesforce Marketing Cloud]. {#prerequisites-account}

Contactez votre [!DNL Salesforce Account Executive] pour vous abonner au [!DNL Salesforce Marketing Cloud Account Engagement] produit si vous ne l’avez pas déjà.

#### Création d’attributs dans [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Lors de l’activation de segments dans la variable [!DNL (API) Salesforce Marketing Cloud] destination, vous devez saisir une valeur dans la variable **[!UICONTROL ID de mappage]** pour chaque segment activé, dans la variable **[Planification du segment](#schedule-segment-export-example)** étape .

[!DNL Salesforce] nécessite que cette valeur lise et interprète correctement les segments provenant d’un Experience Platform et mette à jour leur état de segment dans [!DNL Salesforce Marketing Cloud]. Reportez-vous à la documentation Experience Platform pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

Pour chaque segment que vous activez de Platform à [!DNL Salesforce Marketing Cloud], vous devez créer un attribut du type `Text` dans [!DNL Salesforce]. Utilisez la variable [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] pour créer des attributs. Les noms des champs d’attribut sont utilisés pour la variable [!DNL (API) Salesforce Marketing Cloud] champ de destination et doit être créé sous `[!DNL Email Demographics system attribute-set]`. Vous pouvez définir le caractère du champ avec un maximum de 4 000 caractères, en fonction des besoins de votre entreprise. Voir [!DNL Salesforce Marketing Cloud] [Types de données des extensions de données](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) page de documentation pour plus d’informations sur les types d’attributs.

Reportez-vous à la section [!DNL Salesforce Marketing Cloud] documentation à [créer des attributs](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin de conseils sur la création d’attributs.

Exemple de l’écran du concepteur de données dans [!DNL Salesforce Marketing Cloud], dans lequel vous allez ajouter l’attribut est illustré ci-dessous :
![Concepteur de données de l’interface utilisateur de Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Une vue [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] attribute-set est illustré ci-dessous :
![Jeu d’attributs démographiques des emails de l’interface utilisateur de Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

Le [!DNL (API) Salesforce Marketing Cloud] destination utilise la variable [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les attributs et leurs jeux d’attributs définis dans [!DNL Salesforce Marketing Cloud].

Elles s’affichent dans la **[!UICONTROL Champ cible]** de la fenêtre de sélection lors de la configuration de [mapping](#mapping-considerations-example) dans le workflow de [activation des segments vers la destination](#activate). Notez que seuls les mappages pour les attributs définis dans la variable [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` Les ensembles d’attributs sont pris en charge.

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud], vous devez créer des attributs avec un **[!UICONTROL NOM DU CHAMP]** qui correspond exactement à la valeur spécifiée dans **[!UICONTROL ID de mappage]** pour chaque segment Platform activé. Par exemple, la capture d’écran ci-dessous montre un attribut nommé `salesforce_mc_segment_1`. Lors de l’activation d’un segment vers cette destination, ajoutez `salesforce_mc_segment_1` as **[!UICONTROL ID de mappage]** pour renseigner dans cet attribut les audiences de segments d’Experience Platform.

Exemple de création d’attributs dans [!DNL Salesforce Marketing Cloud], est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur de Marketing Cloud Salesforce présentant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Lors de la création de l’attribut, n’incluez pas d’espace dans le nom du champ. Utilisez plutôt le trait de soulignement. `(_)` comme séparateur.
>* Pour distinguer les attributs utilisés pour les segments Platform des autres attributs dans [!DNL Salesforce Marketing Cloud], vous pouvez inclure un préfixe ou un suffixe reconnaissable pour les attributs utilisés pour les segments d’Adobe. Par exemple, au lieu de `test_segment`, utilisez `Adobe_test_segment` ou `test_segment_Adobe`.
>* Si d’autres attributs sont déjà créés dans [!DNL Salesforce Marketing Cloud], vous pouvez utiliser le même nom que le segment Platform pour identifier facilement le segment dans [!DNL Salesforce Marketing Cloud].


#### Collectez les informations d’identification de [!DNL Salesforce Marketing Cloud]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la variable [!DNL (API) Salesforce Marketing Cloud] destination.

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Sous-domaine | Voir [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce Marketing Cloud] . | Si votre [!DNL Salesforce Marketing Cloud] domain est<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.accuracy.target.com*, <br>vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| Identifiant client | Voir [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce Marketing Cloud] . | r23kxxxxxxxx0z05xxxxxx |
| Secret client | Voir [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce Marketing Cloud] . | ipxxxxxxxxxxT4xxxxxxxxxx |

{style=&quot;table-layout:auto&quot;}

### Mécanismes de sécurisation {#guardrails}

* Salesforce impose certains [limites de taux](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Reportez-vous à la section [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) pour résoudre toutes les limites probables que vous pourriez rencontrer et réduire les erreurs lors de l’exécution.
   * Reportez-vous à la section [[!DNL Salesforce Marketing Cloud] Prix de l&#39;engagement](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) page à *Téléchargement du graphique de comparaison de l’édition complète* en pdf qui détaille les limites imposées par votre plan.
   * Le [Présentation des API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) détails de la page des limites supplémentaires.
   * Voir [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) pour une page qui rassemble ces détails.
* Le nombre de *champs personnalisés autorisés par objet* varie en fonction de votre édition Salesforce.
   * Reportez-vous à la section [!DNL Salesforce] [documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) pour plus d’informations.
   * Si vous avez atteint la limite définie pour *champs personnalisés autorisés par objet* dans [!DNL Salesforce Marketing Cloud] vous devrez
      * Supprimer les anciens attributs avant d’ajouter de nouveaux attributs dans [!DNL Salesforce Marketing Cloud].
      * Mettez à jour ou supprimez tous les segments activés dans les destinations Platform qui utilisent ces anciens noms d’attribut comme valeur fournie pour **[!UICONTROL ID de mappage]** pendant la [planification des segments](#schedule-segment-export-example) étape .

## Identités prises en charge {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Clé de contact. Reportez-vous à la section [!DNL Salesforce Marketing Cloud] [documentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | Obligatoire |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque statut du segment dans [!DNL Salesforce Marketing Cloud] est mis à jour avec le statut du segment correspondant de Platform, en fonction de la valeur de l’**[!UICONTROL identifiant de mappage]** fournie pendant l’étape de [planification des segments](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL (API) Salesforce Marketing Cloud]. Vous pouvez également la localiser sous le **[!UICONTROL Marketing par e-mail]** catégorie.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs obligatoires ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**. Reportez-vous à la section [ [!DNL Salesforce Marketing Cloud] Collecter des informations d’identification ](#gather-credentials) pour obtenir des conseils.

| [!DNL (API) Salesforce Marketing Cloud] destination | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Sous-domaine]** | Votre [!DNL Salesforce Marketing Cloud] préfixe de domaine. <br>Par exemple, si votre domaine est <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.accuracy.target.com*, <br> vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| **[!UICONTROL Identifiant client]** | Votre [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Secret client]** | Votre [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Capture d’écran de l’interface utilisateur de Platform montrant comment s’authentifier sur le Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche une **[!UICONTROL Connecté]** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL (API) Salesforce Marketing Cloud], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible.

Pour mapper correctement vos champs XDM à [!DNL (API) Salesforce Marketing Cloud] pour les champs de destination, procédez comme suit.

>[!IMPORTANT]
>
>Bien que vos noms d’attribut soient conformes à [!DNL Salesforce Marketing Cloud] , les mappages des deux `contactKey` et `personalEmail.address` sont obligatoires. Lors du mappage des attributs, seuls les attributs de l’Experience Platform `Email Demographics` attribute-set doit être utilisé dans les champs cibles.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’ajout d’un nouveau mappage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM ou choisissez l’option **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité.
1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité ou choisissez **[!UICONTROL Sélectionner des attributs personnalisés]** et sélectionnez un attribut dans la catégorie `Email Demographics` les attributs s’affichaient selon les besoins. Le [!DNL (API) Salesforce Marketing Cloud] destination utilise la variable [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les attributs et leurs jeux d’attributs définis dans [!DNL Salesforce Marketing Cloud]. Elles s’affichent dans la **[!UICONTROL Champ cible]** lorsque vous configurez la variable [mapping](#mapping-considerations-example) dans le [activation des segments dans le workflow](#activate). Remarque : Seuls les mappages pour les attributs définis dans la variable [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` Les jeux d’attributs sont pris en charge.

   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et [!DNL (API) Salesforce Marketing Cloud]: |Champ source|Champ cible| Obligatoire| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Une fois les mappages fournis pour la connexion à la destination, sélectionnez **[!UICONTROL Suivant]**.

### Planifier l’exportation de segments et exemple {#schedule-segment-export-example}

Lors de l’exécution de la variable [Planification de l’exportation de segments](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement les segments Platform à la variable [Attributs](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Pour ce faire, sélectionnez chaque segment, puis saisissez le nom de l’attribut depuis [!DNL Salesforce Marketing Cloud] dans le [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** champ . Reportez-vous à la section [Création d’un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) pour obtenir des conseils sur la création d’attributs dans [!DNL Salesforce Marketing Cloud].

Par exemple, si la variable [!DNL Salesforce Marketing Cloud] attribute is `salesforce_mc_segment_1`, indiquez cette valeur dans la variable [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** pour renseigner dans cet attribut les audiences de segments d’Experience Platform.

Un exemple d’attribut de [!DNL Salesforce Marketing Cloud] est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur de Marketing Cloud Salesforce présentant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Un exemple indiquant l’emplacement de la variable [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation de segments.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Comme illustré [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** doit correspondre exactement à la valeur spécifiée dans [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DU CHAMP]**.

Répétez cette section pour chaque segment Platform activé.

Selon le cas d’utilisation, tous les segments activés peuvent être mappés sur le même [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DU CHAMP]** ou différent **[!UICONTROL NOM DU CHAMP]** in [!DNL (API) Salesforce Marketing Cloud]. Un exemple type basé sur l’image illustrée ci-dessus peut être.
| [!DNL (API) Salesforce Marketing Cloud] nom du segment | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DU CHAMP]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** | | — | — | — | | segment 1 Salesforce mc | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc Segment 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant la navigation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Basculez vers l’onglet **[!DNL Activation data]**, puis sélectionnez un nom de segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Connectez-vous au [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) site web. Accédez ensuite à la **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** et vérifiez si les profils du segment ont été ajoutés.
   ![Capture d’écran de l’interface utilisateur du Marketing Cloud Salesforce montrant la page Contacts avec les profils utilisés dans le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Pour vérifier si des profils ont été mis à jour, accédez au **[!UICONTROL Email]** et vérifiez si les valeurs d’attribut du profil du segment ont été mises à jour. En cas de réussite, vous pouvez voir que chaque état de segment dans [!DNL Salesforce Marketing Cloud] a été mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie dans la variable [planification des segments](#schedule-segment-export-example) étape .
   ![Capture d’écran de l’interface utilisateur de Marketing Cloud Salesforce montrant la page Courrier électronique des contacts sélectionnée avec les statuts de segment mis à jour.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers le Marketing Cloud Salesforce {#unknown-errors}

* Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Pour corriger cette erreur, vérifiez que la variable **[!UICONTROL ID de mappage]** que vous avez fourni dans le workflow d’activation à la variable [!DNL (API) Salesforce Marketing Cloud] destination correspond exactement au nom de l’attribut que vous avez créé dans [!DNL Salesforce Marketing Cloud]. Reportez-vous à la section [Création d’un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) pour plus d’informations.

* Lors de l’activation d’un segment, un message d’erreur peut s’afficher : `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Pour corriger cette erreur, contactez votre [!DNL Salesforce Marketing Cloud] administrateur de compte à ajouter [Adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) à [!DNL Salesforce Marketing Cloud] plages d’adresses IP de confiance des comptes. Reportez-vous à la section [!DNL Salesforce Marketing Cloud] [Adresses IP à inclure sur les Listes autorisées en Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Ressources supplémentaires {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) expliquant comment les contacts sont mis à jour avec les informations spécifiées dans les groupes d’attributs spécifiés.