---
title: (API) Connexion à Salesforce Marketing Cloud
description: La destination Salesforce Marketing Cloud (anciennement appelée ExactTarget) vous permet d’exporter les données de votre compte et de les activer dans Salesforce Marketing Cloud en fonction des besoins de votre entreprise.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 20%

---

# Connexion [!DNL (API) Salesforce Marketing Cloud]

## Présentation {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (anciennement appelée [!DNL ExactTarget]) est une suite marketing numérique qui vous permet de créer et de personnaliser des parcours pour que les visiteurs et les clients puissent personnaliser leur expérience.

>[!IMPORTANT]
>
> Notez la différence entre cette connexion et l’autre [[!DNL Salesforce Marketing Cloud] connexion](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) qui existe dans la section Catalogue marketing par e-mail. L’autre connexion Marketing Cloud Salesforce vous permet d’exporter des fichiers vers un emplacement de stockage spécifié, alors qu’il s’agit d’une connexion en continu basée sur l’API.

Par rapport à [!DNL Salesforce Marketing Cloud Account Engagement] qui est plus orienté vers le marketing **B2B**, la destination [!DNL (API) Salesforce Marketing Cloud] est idéale pour les cas d’utilisation **B2C** avec des cycles de prise de décision transactionnelle plus courts. Vous pouvez consolider des jeux de données plus volumineux représentant le comportement de votre audience cible afin d’ajuster et d’améliorer les campagnes marketing en hiérarchisant et en segmentant les contacts, en particulier à partir de jeux de données en dehors de l’[!DNL Salesforce]. *Notez qu’Experience Platform dispose également d’une connexion pour le [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’API [!DNL Salesforce Marketing Cloud] [mettre à jour les contacts](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), qui vous permet d’**ajouter des contacts et mettre à jour les données de contact** pour les besoins de votre entreprise après les avoir activés dans un nouveau segment de [!DNL Salesforce Marketing Cloud].

[!DNL Salesforce Marketing Cloud] utilise OAuth 2 avec les informations d’identification du client comme mécanisme d’authentification pour communiquer avec l’API [!DNL Salesforce Marketing Cloud]. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Salesforce Marketing Cloud] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL (API) Salesforce Marketing Cloud], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Envoyer des e-mails aux contacts pour les campagnes marketing {#use-case-send-emails}

Le service commercial d’une plateforme de location d’habitations souhaite diffuser un e-mail marketing à un public ciblé. L’équipe marketing de la plateforme peut ajouter de nouveaux contacts ou mettre à jour les contacts existants *(et leurs adresses e-mail)* via Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer ces audiences à [!DNL Salesforce Marketing Cloud], qui peut ensuite être utilisée pour envoyer l’e-mail de campagne marketing.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL (API) Salesforce Marketing Cloud], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), ainsi que des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données d’Experience Platform vers votre compte [!DNL Salesforce Marketing Cloud] :

#### Vous devez avoir un compte [!DNL Salesforce Marketing Cloud]. {#prerequisites-account}

Un compte [!DNL Salesforce Marketing Cloud] avec un abonnement au produit [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) est obligatoire pour continuer.

Contactez l’[[!DNL Salesforce] assistance technique](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) si vous ne disposez pas d’un compte [!DNL Salesforce Marketing Cloud] ou si votre compte ne dispose pas de l’abonnement au produit [!DNL Marketing Cloud Engagement].

#### Création d’attributs dans [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Lors de l’activation des audiences vers la destination [!DNL (API) Salesforce Marketing Cloud], vous devez saisir une valeur dans le champ **[!UICONTROL Identifiant de mappage]** pour chaque audience activée, à l’étape **[Planning des audiences](#schedule-segment-export-example)**.

[!DNL Salesforce] a besoin de cette valeur pour lire et interpréter correctement les audiences provenant d’Experience Platform et pour mettre à jour leur statut d’audience dans [!DNL Salesforce Marketing Cloud]. Reportez-vous à la documentation Experience Platform pour le groupe de champs de schéma [Détails sur l’appartenance à une audience](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les statuts de l’audience.

Pour chaque audience activée d’Experience Platform vers [!DNL Salesforce], vous devez disposer d’un attribut de type `Text` lié à l’extension de données [!DNL Email Demographics] dans [!DNL Salesforce Marketing Cloud]. Utilisez le [!DNL Contact Builder] [!DNL Salesforce Marketing Cloud] pour créer des attributs. Reportez-vous à la documentation [!DNL Salesforce Marketing Cloud] pour [créer des attributs](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin de conseils sur la création d’attributs.

Les noms des champs d’attribut sont utilisés pour le champ cible [!DNL (API) Salesforce Marketing Cloud] lors de l’étape **[!UICONTROL Mappage]**. Vous pouvez définir le caractère du champ avec un maximum de 4 000 caractères, en fonction des besoins de votre entreprise. Consultez la page de documentation [!DNL Salesforce Marketing Cloud] [Types de données des extensions de données](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) pour plus d’informations sur les types d’attributs.

Voici un exemple d’écran du concepteur de données dans [!DNL Salesforce Marketing Cloud], auquel vous allez ajouter l’attribut :
![Concepteur de données de l’interface utilisateur de Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Une vue d’un groupe d’attributs [!DNL Salesforce Marketing Cloud] [!DNL Email Data] avec des attributs correspondant au statut de l’audience dans l’extension de données [!DNL Email Demographics] est affichée ci-dessous :
![Groupe d’attributs de données d’e-mail de l’interface utilisateur de Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

La destination [!DNL (API) Salesforce Marketing Cloud] utilise la [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les extensions de données et leurs attributs liés&#39; définis dans [!DNL Salesforce Marketing Cloud].

Elles s’affichent dans la fenêtre de sélection **[!UICONTROL Champ cible]** lorsque vous configurez le [mapping](#mapping-considerations-example) du workflow pour [activer les audiences vers la destination](#activate).

>[!IMPORTANT]
>
> Dans [!DNL Salesforce Marketing Cloud], vous devez créer des attributs avec un **[!UICONTROL NOM DU CHAMP]** qui correspond exactement à la valeur spécifiée dans **[!UICONTROL Identifiant de mappage]** pour chaque segment Experience Platform activé. Par exemple, la capture d’écran ci-dessous montre un attribut nommé `salesforce_mc_segment_1`. Lors de l’activation d’une audience vers cette destination, ajoutez des `salesforce_mc_segment_1` en tant qu’**[!UICONTROL ID de mappage]** pour renseigner les audiences d’Experience Platform dans cet attribut.

Un exemple de création d’attributs dans [!DNL Salesforce Marketing Cloud] est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur de Salesforce Marketing Cloud montrant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * Lors de la création de l’attribut, n’incluez pas de caractères blancs dans le nom du champ. Utilisez plutôt le caractère de soulignement `(_)` comme séparateur.
> * Pour faire la distinction entre les attributs utilisés pour les audiences Experience Platform et les autres attributs dans [!DNL Salesforce Marketing Cloud], vous pouvez inclure un préfixe ou un suffixe reconnaissable pour les attributs utilisés pour les segments Adobe. Par exemple, au lieu de `test_segment`, utilisez `Adobe_test_segment` ou `test_segment_Adobe`.
> * Si d’autres attributs ont déjà été créés dans [!DNL Salesforce Marketing Cloud], vous pouvez utiliser le même nom que le segment Experience Platform pour identifier facilement l’audience dans [!DNL Salesforce Marketing Cloud].

#### Attribuer des rôles utilisateur et des autorisations dans [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Comme [!DNL Salesforce Marketing Cloud] prend en charge des rôles personnalisés en fonction de votre cas d’utilisation, les rôles appropriés doivent être attribués à votre utilisateur pour mettre à jour vos attributs dans [!DNL Salesforce Marketing Cloud]. Voici un exemple de rôles affectés à un utilisateur :
![Interface utilisateur de Salesforce Marketing Cloud pour un utilisateur sélectionné, qui affiche les rôles qui lui sont attribués.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

En fonction des rôles qui ont été attribués à votre utilisateur [!DNL Salesforce Marketing Cloud], vous devez également attribuer des autorisations à l’extension de données [!DNL Salesforce Marketing Cloud] qui sont liées aux champs que vous souhaitez mettre à jour.

Comme cette destination nécessite l’accès aux `[!DNL data extension]`, vous devez les autoriser. Par exemple, pour les [!DNL data extension] de `Email` que vous devez autoriser, comme illustré ci-dessous :

![Interface utilisateur de Salesforce Marketing Cloud affichant l’extension de données d’e-mail avec les autorisations autorisées.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Pour restreindre le niveau d’accès, vous pouvez également remplacer l’accès individuel à l’aide de privilèges granulaires.
![Interface utilisateur de Salesforce Marketing Cloud affichant l’extension de données d’e-mail avec des autorisations granulaires.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Reportez-vous aux pages [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) et [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) pour obtenir des conseils détaillés.

#### Collectez les informations d’identification de [!DNL Salesforce Marketing Cloud]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL (API) Salesforce Marketing Cloud].

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Sous-domaine | Voir [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | Si votre domaine de [!DNL Salesforce Marketing Cloud] est <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| Identifiant client | Consultez la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | r23kxxxxxxxx0z05xxxxxx |
| Secret client | Consultez la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce Marketing Cloud]. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Mécanismes de sécurisation {#guardrails}

* Salesforce impose certaines [limites de taux](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Reportez-vous à la [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) pour prendre en compte les limites probables que vous pouvez rencontrer et réduire les erreurs lors de l’exécution.
   * Reportez-vous à la page [[!DNL Salesforce Marketing Cloud] Tarification de l’engagement](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pour *Télécharger le graphique comparatif de l’édition complète* au format PDF, qui détaille les limites imposées par votre plan.
   * La page [Aperçu de l’API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) détaille les limites supplémentaires.
   * Reportez-vous [ici](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) pour une page qui regroupe ces détails.
* Le nombre de *champs personnalisés autorisés par objet* varie en fonction de votre édition Salesforce.
   * Reportez-vous à la [!DNL Salesforce] [documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) pour plus d’informations.
   * Si vous avez atteint la limite définie pour *champs personnalisés autorisés par objet* dans [!DNL Salesforce Marketing Cloud], vous devrez :
      * Supprimez les anciens attributs avant d’ajouter de nouveaux attributs dans [!DNL Salesforce Marketing Cloud].
      * Mettez à jour ou supprimez toutes les audiences activées dans les destinations Experience Platform qui utilisent ces anciens noms d’attribut comme valeur fournie pour **[!UICONTROL ID de mappage]** lors de l’étape [planification des audiences](#schedule-segment-export-example).

## Identités prises en charge {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] la clé de contact. Reportez-vous à la [!DNL Salesforce Marketing Cloud] [documentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | Obligatoire |

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque statut du segment dans [!DNL Salesforce Marketing Cloud] est mis à jour avec le statut de l’audience correspondant d’Experience Platform, en fonction de la valeur **[!UICONTROL Identifiant de mappage]** fournie lors de l’étape [planification de l’audience](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
> Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL (API) Salesforce Marketing Cloud]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL Marketing par e-mail]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs obligatoires ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**. Reportez-vous à la section [Collecter [!DNL Salesforce Marketing Cloud] informations d’identification](#gather-credentials) pour obtenir des conseils.

| [!DNL (API) Salesforce Marketing Cloud] destination | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Sous-domaine]** | Votre préfixe de domaine [!DNL Salesforce Marketing Cloud]. <br>Par exemple, si votre domaine est <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> vous devez fournir `mcq4jrssqdlyc4lph19nnqgzzs84` comme valeur. |
| **[!UICONTROL Identifiant du client]** | Votre `Client ID` [!DNL Salesforce Marketing Cloud]. |
| **[!UICONTROL Secret du client]** | Votre `Client Secret` [!DNL Salesforce Marketing Cloud]. |

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant comment s’authentifier sur Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte, vous pouvez alors passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur d’Experience Platform affichant les détails de la destination.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
> * Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
> * Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL (API) Salesforce Marketing Cloud], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Experience Platform et leurs équivalents issus de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL (API) Salesforce Marketing Cloud], procédez comme suit.

>[!IMPORTANT]
>
> * Bien que les noms d’attributs correspondent à votre compte [!DNL Salesforce Marketing Cloud], les mappages pour `contactKey` et `personalEmail.address` sont obligatoires.
>
> * L’intégration à l’API [!DNL Salesforce Marketing Cloud] est soumise à une limite de pagination du nombre d’attributs qu’Experience Platform peut récupérer de Salesforce. Cela signifie que pendant l’étape **[!UICONTROL Mappage]**, le schéma des champs cibles peut afficher un maximum de 2 000 attributs de votre compte Salesforce.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.
   ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform pour Ajouter un nouveau mappage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM ou choisissez l’espace de noms d’identité **[!UICONTROL Sélectionner]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]**, choisissez la catégorie **[!UICONTROL Sélectionner l’espace de noms d’identité]** et sélectionnez une identité ou choisissez **[!UICONTROL Sélectionner des attributs]** et sélectionnez un attribut parmi les extensions de données affichées, le cas échéant. La destination [!DNL (API) Salesforce Marketing Cloud] utilise la [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) pour récupérer dynamiquement les extensions de données et leurs attributs liés&#39; définis dans [!DNL Salesforce Marketing Cloud]. Elles s’affichent dans la fenêtre contextuelle **[!UICONTROL Champ cible]** lorsque vous configurez le [mapping](#mapping-considerations-example) dans le workflow [Activer les audiences](#activate).

   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et [!DNL (API) Salesforce Marketing Cloud] :

     | Champ source | Champ cible | Obligatoire |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` de l’extension de données [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses]. | `Mandatory`, lors de l’ajout de nouveaux contacts. |
     | `xdm: person.name.firstName` | `Attribute: First Name` de l’extension de données [!DNL Salesforce Marketing Cloud] souhaitée. | - |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :

     ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant les mappings de ciblage.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Planifier l’exportation de l’audience et exemple {#schedule-segment-export-example}

Lors de l’exécution de l’étape [ Planifier l’exportation d’audience ](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement les audiences Experience Platform aux [ attributs ](#prerequisites-attribute) dans [!DNL Salesforce Marketing Cloud].

Pour ce faire, sélectionnez chaque segment, puis saisissez le nom de l’attribut à partir de [!DNL Salesforce Marketing Cloud] dans le champ [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]**. Reportez-vous à la section [Créer un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) pour obtenir des conseils et connaître les bonnes pratiques sur la création d’attributs dans [!DNL Salesforce Marketing Cloud].

Par exemple, si votre attribut [!DNL Salesforce Marketing Cloud] est `salesforce_mc_segment_1`, spécifiez cette valeur dans l’[!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mappage]** pour renseigner les audiences d’Experience Platform dans cet attribut.

Un exemple d’attribut de [!DNL Salesforce Marketing Cloud] est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur de Salesforce Marketing Cloud montrant un attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Un exemple indiquant l’emplacement de l’[!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL identifiant de mappage]** est illustré ci-dessous :

![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant la planification de l’exportation de l’audience.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Comme indiqué, la [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Identifiant de mappage]** doit correspondre exactement à la valeur spécifiée dans [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DU CHAMP]**.

Répétez cette section pour chaque segment Experience Platform activé.

Un exemple type basé sur l’image affichée ci-dessus pourrait être .

| [!DNL (API) Salesforce Marketing Cloud] le nom du segment | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOM DU CHAMP]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| salesforce mc audience 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| salesforce mc audience 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform montrant la navigation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Passez à l’onglet **[!DNL Activation data]** , puis sélectionnez un nom d’audience.
   ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant les données d’activation des destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Surveillez le résumé de l’audience et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform montrant le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Connectez-vous au site Web [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/). Accédez ensuite à la page **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** et vérifiez si les profils de l’audience ont été ajoutés.
   ![Capture d’écran de l’interface utilisateur de Salesforce Marketing Cloud présentant la page Contacts avec les profils utilisés dans le segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Pour vérifier si des profils ont été mis à jour, accédez à la page **[!UICONTROL E-mail]** et vérifiez si les valeurs d’attribut du profil de l’audience ont été mises à jour. En cas de réussite, vous pouvez constater que chaque statut d’audience dans [!DNL Salesforce Marketing Cloud] a été mis à jour avec le statut d’audience correspondant d’Experience Platform, en fonction de la valeur **[!UICONTROL Identifiant de mappage]** fournie à l’étape [planification de l’audience](#schedule-segment-export-example).
   ![Capture d’écran de l’interface utilisateur de Salesforce Marketing Cloud montrant la page d’e-mail des contacts sélectionnés avec les statuts d’audience mis à jour.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements dans Salesforce Marketing Cloud {#unknown-errors}

* Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Capture d’écran de l’interface utilisateur d’Experience Platform affichant une erreur.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Pour corriger cette erreur, vérifiez que l’**[!UICONTROL identifiant de mappage]** que vous avez fourni dans le workflow d’activation vers la destination [!DNL (API) Salesforce Marketing Cloud] correspond exactement au nom de l’attribut que vous avez créé dans [!DNL Salesforce Marketing Cloud]. Reportez-vous à la section [Créer un attribut dans [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) pour obtenir des conseils.

* Lors de l’activation d’un segment, vous pouvez obtenir un message d’erreur : `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Pour corriger cette erreur, contactez l’administrateur de votre compte [!DNL Salesforce Marketing Cloud] pour ajouter [des adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) aux plages d’adresses IP approuvées de vos comptes [!DNL Salesforce Marketing Cloud]. Reportez-vous à la documentation [!DNL Salesforce Marketing Cloud] [Adresses IP à inclure sur les Places sur la liste autorisée dans Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Ressources supplémentaires {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [ API ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) expliquant comment les contacts sont mis à jour avec les informations spécifiées.

### Journal des modifications {#changelog}

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Octobre 2023 | Mise à jour de la documentation | <ul><li>Nous avons mis à jour la section [ Conditions préalables dans (API) Salesforce Marketing Cloud](#prerequisites-destination) et avons, en général, supprimé les références inutiles aux groupes d’attributs dans le document.</li> <li>Mise à jour de la documentation afin d’indiquer que les attributs des statuts des audiences doivent être créés dans [!DNL Salesforce Marketing Cloud] uniquement dans l’extension de données [!DNL Email Demographics].</li> <li>Nous avons mis à jour la table de mappage dans la section [Considérations sur le mappage et exemple](#mapping-considerations-example). Le mappage de `Email Address`’attribut dans l’extension de données `Email Addresses` est marqué comme obligatoire. Cette exigence a été mentionnée dans la légende marquée COMME IMPORTANTE, mais elle a été omise de la table.</li></ul> |
| Avril 2023 | Mise à jour de la documentation | <ul><li>Nous avons corrigé une instruction et un lien de référence dans la section [Conditions préalables dans le Marketing Cloud Salesforce (API)](#prerequisites-destination) pour indiquer qu’[!DNL Salesforce Marketing Cloud Engagement] est un abonnement obligatoire pour utiliser cette destination. La section a précédemment indiqué à tort que les utilisateurs ont besoin d’un abonnement au Marketing Cloud **Compte** Engagement pour continuer.</li> <li>Nous avons ajouté une section sous [conditions préalables](#prerequisites) pour [rôles et autorisations](#prerequisites-roles-permissions) à affecter à l’utilisateur [!DNL Salesforce] pour que cette destination fonctionne. (PLATIR-26299)</li></ul> |
| Février 2023 | Mise à jour de la documentation | Nous avons mis à jour la section [Conditions préalables dans le Marketing Cloud Salesforce (API)](#prerequisites-destination) afin d’inclure un lien de référence indiquant qu’[!DNL Salesforce Marketing Cloud Engagement] est un abonnement obligatoire pour utiliser cette destination. |
| Février 2023 | Mise à jour des fonctionnalités | Nous avons corrigé un problème en raison duquel une configuration incorrecte dans la destination provoquait l’envoi d’un fichier JSON incorrect à Salesforce. Certains utilisateurs et utilisatrices ont ainsi constaté un grand nombre d’échecs d’identités lors de l’activation. (PLATIR-26299) |
| Janvier 2023 | Mise à jour de la documentation | <ul><li>Nous avons mis à jour la section [ Conditions préalables dans  [!DNL Salesforce]](#prerequisites-destination) pour indiquer que les attributs doivent être créés côté [!DNL Salesforce]. Cette section comprend désormais des instructions détaillées sur la manière de procéder et les bonnes pratiques concernant le nommage des attributs dans [!DNL Salesforce]. (PLATIR-25602)</li><li>Nous avons ajouté des instructions claires sur l’utilisation de l’identifiant de mappage pour chaque audience activée dans l’étape [planification des audiences](#schedule-segment-export-example). (PLATIR-25602)</li></ul> |
| Octobre 2022 | Version initiale | Publication de la destination initiale et de la documentation. |

{style="table-layout:auto"}

+++
