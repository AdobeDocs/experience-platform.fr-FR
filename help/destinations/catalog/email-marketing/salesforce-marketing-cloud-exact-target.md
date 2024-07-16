---
title: (API) Connexion à Salesforce Marketing Cloud
description: La destination de Marketing Cloud Salesforce (anciennement connue sous le nom d’ExactTarget) vous permet d’exporter les données de votre compte et de les activer dans le Marketing Cloud Salesforce pour répondre aux besoins de votre entreprise.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2895'
ht-degree: 22%

---

# Connexion [!DNL (API) Salesforce Marketing Cloud]

## Présentation {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (anciennement [!DNL ExactTarget]) est une suite de marketing numérique qui vous permet de créer et de personnaliser des parcours pour que les visiteurs et les clients puissent personnaliser leur expérience.

>[!IMPORTANT]
>
> Notez la différence entre cette connexion et l’autre [[!DNL Salesforce Marketing Cloud] connexion](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) existant dans la section Catalogue des emails . L’autre connexion au Marketing Cloud Salesforce vous permet d’exporter des fichiers vers un emplacement de stockage spécifié, alors qu’il s’agit d’une connexion en continu basée sur l’API.

Par rapport à [!DNL Salesforce Marketing Cloud Account Engagement], plus axé sur le marketing **B2B**, la destination [!DNL (API) Salesforce Marketing Cloud] est idéale pour les cas d’utilisation **B2C** avec des cycles de décision transactionnels plus courts. Vous pouvez consolider des jeux de données plus volumineux représentant le comportement de votre audience cible pour ajuster et améliorer les campagnes marketing en hiérarchisant et en segmentant les contacts, en particulier à partir de jeux de données en dehors de [!DNL Salesforce]. *Remarque : l’Experience Platform a également une connexion pour [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’API [!DNL Salesforce Marketing Cloud] [mettre à jour les contacts](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), qui vous permet **d’ajouter des contacts et de mettre à jour les données de contact** pour vos besoins professionnels après les avoir activés dans un nouveau segment [!DNL Salesforce Marketing Cloud].

[!DNL Salesforce Marketing Cloud] utilise OAuth 2 avec les informations d’identification du client comme mécanisme d’authentification pour communiquer avec l’API [!DNL Salesforce Marketing Cloud]. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Salesforce Marketing Cloud] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL (API) Salesforce Marketing Cloud], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des emails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service des ventes d’une plateforme de location de maisons souhaite diffuser un email marketing à un public client ciblé. L’équipe marketing de la plateforme peut ajouter de nouveaux contacts/mettre à jour des contacts *(et leurs adresses électroniques)* via Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer ces audiences à [!DNL Salesforce Marketing Cloud], qui peuvent ensuite être utilisées pour envoyer le courrier électronique de la campagne marketing.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL (API) Salesforce Marketing Cloud], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre compte [!DNL Salesforce Marketing Cloud] :

#### Vous devez avoir un compte [!DNL Salesforce Marketing Cloud]. {#prerequisites-account}

Un compte [!DNL Salesforce Marketing Cloud] avec un abonnement au produit [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) est obligatoire pour continuer.

Contactez l’ [[!DNL Salesforce] assistance](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) si vous n’avez pas de compte [!DNL Salesforce Marketing Cloud] ou si l’abonnement au produit [!DNL Marketing Cloud Engagement] manque à votre compte.

#### Créer des attributs dans [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Lors de l’activation d’audiences vers la destination [!DNL (API) Salesforce Marketing Cloud], vous devez saisir une valeur dans le champ **[!UICONTROL ID de mappage]** pour chaque audience activée, à l’étape **[Planning d’audience](#schedule-segment-export-example)** .

[!DNL Salesforce] nécessite cette valeur pour lire et interpréter correctement les audiences provenant d’un Experience Platform et pour mettre à jour leur état d’audience dans [!DNL Salesforce Marketing Cloud]. Reportez-vous à la documentation Experience Platform du [ groupe de champs de schéma Détails de l’appartenance à l’audience ](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les états de l’audience.

Pour chaque audience que vous activez de Platform à [!DNL Salesforce], un attribut de type `Text` doit être associé à l’extension de données [!DNL Email Demographics] dans [!DNL Salesforce Marketing Cloud]. Utilisez [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] pour créer des attributs. Reportez-vous à la documentation [!DNL Salesforce Marketing Cloud] de [créer des attributs](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin d’instructions sur la création d’attributs.

Les noms des champs d’attribut sont utilisés pour le champ cible [!DNL (API) Salesforce Marketing Cloud] lors de l’étape **[!UICONTROL Mapping]** . Vous pouvez définir le caractère du champ avec un maximum de 4 000 caractères, en fonction des besoins de votre entreprise. Pour plus d’informations sur les types d’attributs, consultez la documentation [!DNL Salesforce Marketing Cloud] [ Types de données des extensions de données](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) .

Un exemple de l’écran du concepteur de données dans [!DNL Salesforce Marketing Cloud], dans lequel vous allez ajouter l’attribut est illustré ci-dessous :
![Concepteur de données de l’interface utilisateur de Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

La vue d&#39;un groupe d&#39;attributs [!DNL Salesforce Marketing Cloud] [!DNL Email Data] avec des attributs correspondant à l&#39;état de l&#39;audience dans l&#39;extension de données [!DNL Email Demographics] est présentée ci-dessous :
![Groupe d’attributs de données d’email de l’interface utilisateur de Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

La destination [!DNL (API) Salesforce Marketing Cloud] utilise l’ [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les extensions de données et leurs attributs liés définis dans [!DNL Salesforce Marketing Cloud].

Elles s’affichent dans la fenêtre de sélection **[!UICONTROL Champ cible]** lorsque vous configurez le [mapping](#mapping-considerations-example) dans le workflow pour [activer les audiences vers la destination](#activate).

>[!IMPORTANT]
>
> Dans [!DNL Salesforce Marketing Cloud], vous devez créer des attributs avec un **[!UICONTROL NOM DE CHAMP]** qui correspond exactement à la valeur spécifiée dans **[!UICONTROL ID de mappage]** pour chaque segment de plateforme activé. Par exemple, la capture d’écran ci-dessous montre un attribut nommé `salesforce_mc_segment_1`. Lors de l’activation d’une audience vers cette destination, ajoutez `salesforce_mc_segment_1` comme **[!UICONTROL ID de mappage]** pour renseigner les audiences d’audience de l’Experience Platform dans cet attribut.

Voici un exemple de création d’attributs dans [!DNL Salesforce Marketing Cloud] :
![ Copie d’écran de l’interface utilisateur de Marketing Cloud Salesforce présentant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * Lors de la création de l’attribut, n’incluez pas d’espace dans le nom du champ. Utilisez plutôt le caractère de soulignement `(_)` comme séparateur.
> * Pour faire la distinction entre les attributs utilisés pour les audiences Platform et d’autres attributs dans [!DNL Salesforce Marketing Cloud], vous pouvez inclure un préfixe ou un suffixe reconnaissable pour les attributs utilisés pour les segments d’Adobe. Par exemple, utilisez `Adobe_test_segment` ou `test_segment_Adobe` au lieu de `test_segment`.
> * Si d’autres attributs sont déjà créés dans [!DNL Salesforce Marketing Cloud], vous pouvez utiliser le même nom que le segment Platform pour identifier facilement l’audience dans [!DNL Salesforce Marketing Cloud].

#### Attribution de rôles utilisateur et d’autorisations dans [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Comme [!DNL Salesforce Marketing Cloud] prend en charge des rôles personnalisés en fonction de votre cas d’utilisation, les rôles appropriés doivent être attribués à votre utilisateur pour mettre à jour vos attributs dans [!DNL Salesforce Marketing Cloud]. Vous trouverez ci-dessous un exemple de rôles attribués à un utilisateur :
![Interface utilisateur de Marketing Cloud Salesforce pour un utilisateur sélectionné qui affiche les rôles qui lui sont attribués.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Selon les rôles attribués à votre utilisateur [!DNL Salesforce Marketing Cloud], vous devez également attribuer des autorisations à l’extension de données [!DNL Salesforce Marketing Cloud] liée aux champs que vous souhaitez mettre à jour.

Comme cette destination nécessite l’accès à `[!DNL data extension]`, vous devez les autoriser. Par exemple, pour `Email` [!DNL data extension] vous devez autoriser comme illustré ci-dessous :

![L&#39;interface utilisateur de Marketing Cloud Salesforce affiche l&#39;extension de données de messagerie avec les autorisations autorisées.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Pour restreindre le niveau d’accès, vous pouvez également remplacer l’accès individuel à l’aide de privilèges granulaires.
![L&#39;interface utilisateur de Marketing Cloud Salesforce affiche l&#39;extension des données de messagerie avec des autorisations granulaires.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Consultez les pages [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) et [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) pour obtenir des conseils détaillés.

#### Collectez les informations d’identification de [!DNL Salesforce Marketing Cloud]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL (API) Salesforce Marketing Cloud].

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Sous-domaine | Voir [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | Si votre domaine [!DNL Salesforce Marketing Cloud] est<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacte.target.com*, <br>vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| Identifiant client | Consultez la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | r23kxxxxxxxxxx0z05xxxxxx |
| Secret client | Consultez la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Mécanismes de sécurisation {#guardrails}

* Salesforce impose certaines [limites de taux](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Reportez-vous à la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) pour résoudre toutes les limites probables que vous pouvez rencontrer et réduire les erreurs lors de l’exécution.
   * Reportez-vous à la page [[!DNL Salesforce Marketing Cloud] Prix de l&#39;engagement](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) vers *Télécharger le graphique de comparaison de l&#39;édition complète* en tant que pdf qui détaille les limites imposées par votre plan.
   * La page [Présentation de l’API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) détaille les limites supplémentaires.
   * Consultez [ici](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) pour une page qui rassemble ces détails.
* Le nombre de *champs personnalisés autorisés par objet* varie en fonction de votre édition Salesforce.
   * Pour plus d&#39;informations, reportez-vous à la [!DNL Salesforce] [documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) .
   * Si vous avez atteint la limite définie pour les *champs personnalisés autorisés par objet* dans [!DNL Salesforce Marketing Cloud], vous devrez
      * Supprimez les anciens attributs avant d’ajouter de nouveaux attributs dans [!DNL Salesforce Marketing Cloud].
      * Mettez à jour ou supprimez toutes les audiences activées dans les destinations Platform qui utilisent ces anciens noms d’attribut comme valeur fournie pour **[!UICONTROL ID de mappage]** au cours de l’étape [planification d’audience](#schedule-segment-export-example) .

## Identités prises en charge {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Clé de contact. Reportez-vous à la [!DNL Salesforce Marketing Cloud] [documentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | Obligatoire |

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état de segment dans [!DNL Salesforce Marketing Cloud] est mis à jour avec l’état d’audience correspondant de Platform, en fonction de la valeur **[!UICONTROL ID de mappage]** fournie à l’étape [planification d’audience](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
> Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL (API) Salesforce Marketing Cloud]. Vous pouvez également la localiser sous la catégorie **[!UICONTROL Marketing par e-mail]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, remplissez les champs requis ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**. Pour obtenir des conseils, reportez-vous à la section [Rassembler [!DNL Salesforce Marketing Cloud] les informations d’identification](#gather-credentials) .

| [!DNL (API) Salesforce Marketing Cloud] destination | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Votre préfixe de domaine [!DNL Salesforce Marketing Cloud]. <br>Par exemple, si votre domaine est <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacte.target.com*, <br> vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| **[!UICONTROL Identifiant du client]** | Votre [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Secret du client]** | Votre [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Copie d’écran de l’interface utilisateur de Platform montrant comment s’authentifier sur le Marketing Cloud Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un état **[!UICONTROL Connecté]** avec une coche verte, vous pouvez passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
> * Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
> * Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL (API) Salesforce Marketing Cloud], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL (API) Salesforce Marketing Cloud], procédez comme suit.

>[!IMPORTANT]
>
> * Bien que vos noms d’attribut soient conformes à votre compte [!DNL Salesforce Marketing Cloud], les mappages pour `contactKey` et `personalEmail.address` sont obligatoires.
>
> * L’intégration à l’API [!DNL Salesforce Marketing Cloud] est soumise à une limite de pagination du nombre d’attributs que l’Experience Platform peut récupérer de Salesforce. Cela signifie que lors de l’étape **[!UICONTROL Mapping]**, le schéma de champ cible peut afficher un maximum de 2 000 attributs à partir de votre compte Salesforce.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’ajout d’un nouveau mappage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM ou l’attribut **[!UICONTROL Sélectionner l’espace de noms d’identité]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]** , choisissez l’espace de noms **[!UICONTROL Sélectionner l’identité]** et sélectionnez une identité ou la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez un attribut parmi les extensions de données affichées selon vos besoins. La destination [!DNL (API) Salesforce Marketing Cloud] utilise l’ [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les extensions de données et leurs attributs liés définis dans [!DNL Salesforce Marketing Cloud]. Elles s’affichent dans la fenêtre contextuelle **[!UICONTROL Champ cible]** lorsque vous configurez le [mappage](#mapping-considerations-example) dans le [workflow d’activation des audiences](#activate).

   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et [!DNL (API) Salesforce Marketing Cloud] :

     | Champ source | Champ cible | Obligatoire |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` à partir de l’extension de données [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses]. | `Mandatory`, lors de l’ajout de nouveaux contacts. |
     | `xdm: person.name.firstName` | `Attribute: First Name` de l’extension de données [!DNL Salesforce Marketing Cloud] souhaitée. | - |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Planification de l’export d’audience et exemple {#schedule-segment-export-example}

Lors de l’étape [Planification de l’export d’audience](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement les audiences Platform aux [attributs](#prerequisites-attribute) dans [!DNL Salesforce Marketing Cloud].

Pour ce faire, sélectionnez chaque segment, puis saisissez le nom de l’attribut [!DNL Salesforce Marketing Cloud] dans le champ [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** . Reportez-vous à la section [Créer un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) pour obtenir des conseils et connaître les bonnes pratiques en matière de création d’attributs dans [!DNL Salesforce Marketing Cloud].

Par exemple, si votre attribut [!DNL Salesforce Marketing Cloud] est `salesforce_mc_segment_1`, spécifiez cette valeur dans l’ [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** pour renseigner dans cet attribut les audiences d’audience provenant d’un Experience Platform.

Un exemple d’attribut de [!DNL Salesforce Marketing Cloud] est illustré ci-dessous :
![ Copie d’écran de l’interface utilisateur de Marketing Cloud Salesforce présentant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Un exemple indiquant l’emplacement de l’ [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation des audiences.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Comme illustré, l’ [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** doit correspondre exactement à la valeur spécifiée dans [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Répétez cette section pour chaque segment Platform activé.

Un exemple type basé sur l’image illustrée ci-dessus peut être.
| [!DNL (API) Salesforce Marketing Cloud] nom du segment | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DE CHAMP]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** |
| — | — | — |
| audience mc Salesforce 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| audience mc Salesforce 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant la navigation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Passez à l’onglet **[!DNL Activation data]**, puis sélectionnez un nom d’audience.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Surveillez la synthèse de l’audience et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Connectez-vous au site web [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/). Ensuite, accédez à la page **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** et vérifiez si les profils de l’audience ont été ajoutés.
   ![Capture d&#39;écran de l&#39;interface utilisateur de Marketing Cloud Salesforce montrant la page Contacts avec les profils utilisés dans le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Pour vérifier si des profils ont été mis à jour, accédez à la page **[!UICONTROL Email]** et vérifiez si les valeurs d’attribut du profil de l’audience ont été mises à jour. En cas de succès, vous pouvez constater que chaque état d’audience de [!DNL Salesforce Marketing Cloud] a été mis à jour avec l’état d’audience correspondant de Platform, en fonction de la valeur **[!UICONTROL ID de mappage]** fournie à l’étape [planification de l’audience](#schedule-segment-export-example).
   ![ Copie d&#39;écran de l&#39;interface utilisateur de Marketing Cloud Salesforce montrant la page de messagerie des contacts sélectionnée avec les statuts d&#39;audience mis à jour.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers le Marketing Cloud Salesforce {#unknown-errors}

* Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Pour corriger cette erreur, vérifiez que l’ **[!UICONTROL ID de mappage]** que vous avez fourni dans le workflow d’activation vers la destination [!DNL (API) Salesforce Marketing Cloud] correspond exactement au nom de l’attribut que vous avez créé dans [!DNL Salesforce Marketing Cloud]. Pour plus d’informations, reportez-vous à la section [Créer un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) .

* Lors de l’activation d’un segment, vous pouvez obtenir un message d’erreur : `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Pour corriger cette erreur, contactez l’administrateur de votre compte [!DNL Salesforce Marketing Cloud] pour ajouter [ adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) aux plages d’adresses IP de confiance de vos comptes [!DNL Salesforce Marketing Cloud]. Reportez-vous à la documentation [!DNL Salesforce Marketing Cloud] [Adresses IP pour l’inclusion sur les Listes autorisées dans Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Ressources supplémentaires {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) expliquant comment les contacts sont mis à jour avec les informations spécifiées.

### Journal des modifications {#changelog}

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Octobre 2023 | Mise à jour de la documentation | <ul><li>Nous avons mis à jour la section [Conditions préalables dans le Marketing Cloud Salesforce (API)](#prerequisites-destination) et, en général, supprimé les références inutiles aux groupes d’attributs dans le document.</li> <li>Mise à jour de la documentation pour indiquer que les attributs des états d’audience doivent être créés dans [!DNL Salesforce Marketing Cloud] dans l’extension de données [!DNL Email Demographics] uniquement.</li> <li>Nous avons mis à jour la table de mappage dans la section [Considérations relatives au mappage et exemple](#mapping-considerations-example). Le mappage de l’attribut `Email Address` dans l’extension de données `Email Addresses` est marqué comme obligatoire. Cette exigence a été mentionnée dans la légende marquée IMPORTANT, mais a été omise dans la table.</li></ul> |
| Avril 2023 | Mise à jour de la documentation | <ul><li>Nous avons corrigé un lien d’instruction et de référence dans la section [Conditions préalables dans le Marketing Cloud Salesforce (API)](#prerequisites-destination) pour signaler que [!DNL Salesforce Marketing Cloud Engagement] est un abonnement obligatoire pour utiliser cette destination. La section précédente mentionnait par erreur que les utilisateurs ont besoin d’un abonnement au Marketing Cloud **Account** Engagement pour continuer.</li> <li>Nous avons ajouté une section sous [conditions préalables](#prerequisites) pour que [ rôles et autorisations](#prerequisites-roles-permissions) soient attribués à l’utilisateur [!DNL Salesforce] afin que cette destination fonctionne. (PLATIR-26299)</li></ul> |
| Février 2023 | Mise à jour de la documentation | Nous avons mis à jour la section [Conditions préalables dans le Marketing Cloud Salesforce (API)](#prerequisites-destination) afin d’inclure un lien de référence précisant que [!DNL Salesforce Marketing Cloud Engagement] est un abonnement obligatoire pour utiliser cette destination. |
| Février 2023 | Mise à jour des fonctionnalités | Correction d’un problème en raison duquel une configuration incorrecte dans la destination provoquait l’envoi d’un JSON incorrect à Salesforce. Cela entraînait l’échec de certains utilisateurs qui voyaient un grand nombre d’identités lors de l’activation. (PLATIR-26299) |
| Janvier 2023 | Mise à jour de la documentation | <ul><li>Nous avons mis à jour la section [Conditions préalables dans [!DNL Salesforce]](#prerequisites-destination) pour indiquer que les attributs doivent être créés du côté [!DNL Salesforce]. Cette section comprend désormais des instructions détaillées sur la manière de procéder et des bonnes pratiques concernant l’attribution de noms aux attributs dans [!DNL Salesforce]. (PLATIR-25602)</li><li>Nous avons ajouté des instructions claires sur l’utilisation de l’ID de mappage pour chaque audience activée à l’étape [planification de l’audience](#schedule-segment-export-example) . (PLATIR-25602)</li></ul> |
| Octobre 2022 | Version initiale | Version initiale de la destination et publication de la documentation. |

{style="table-layout:auto"}

+++
