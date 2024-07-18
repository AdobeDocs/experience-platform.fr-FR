---
keywords: crm;CRM;destinations crm;salesforce crm;destination Salesforce crm
title: Connexion CRM à Salesforce
description: La destination Salesforce CRM vous permet d’exporter les données de votre compte et de les activer dans Salesforce CRM pour vos besoins professionnels.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: d9ff92138a5de774f011dd9b2e5f1cdc3371bacf
workflow-type: tm+mt
source-wordcount: '2821'
ht-degree: 21%

---

# Connexion [!DNL Salesforce CRM]

## Présentation {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) est une plateforme de gestion de la relation client (CRM) populaire qui prend en charge les types de profils décrits ci-dessous :

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Une prospect est le nom d&#39;une personne ou d&#39;une société qui peut (ou non) être intéressée par les produits ou services que vous vendez.
* [Contacts](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Un contact est une personne avec laquelle l’un de vos représentants a établi une relation et a été qualifié de client potentiel.

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) exploite [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), qui prend en charge les deux types de profils décrits ci-dessus.

Lors de l&#39; [activation des segments](#activate), vous pouvez choisir entre les pistes ou les contacts et mettre à jour les attributs et les données d&#39;audience dans [!DNL Salesforce CRM].

[!DNL Salesforce CRM] utilise OAuth 2 avec l’octroi de mot de passe comme mécanisme d’authentification pour communiquer avec l’API REST Salesforce. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Salesforce CRM] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

En tant que professionnel du marketing, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des audiences à partir de vos données hors ligne et envoyer ces audiences à Salesforce CRM, afin de mettre à jour l’appartenance CRM dès que les audiences et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer les données vers la destination Salesforce CRM, vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) et des [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créés dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL Salesforce CRM] {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL Salesforce CRM], afin d’exporter des données de Platform vers votre compte Salesforce :

#### Vous devez avoir un compte [!DNL Salesforce]. {#prerequisites-account}

Accédez à la page [!DNL Salesforce] [try](https://www.salesforce.com/in/form/signup/freetrial-sales/) pour vous enregistrer et créer un compte [!DNL Salesforce] si vous n&#39;en avez pas déjà un.

#### Configurer une application connectée dans [!DNL Salesforce] {#prerequisites-connected-app}

Tout d&#39;abord, vous devez configurer une [[!DNL Salesforce] application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) dans votre compte [!DNL Salesforce], si ce n&#39;est déjà fait. [!DNL Salesforce CRM] exploitera l’application connectée pour se connecter à [!DNL Salesforce].

Ensuite, activez [!DNL OAuth Settings for API Integration] pour le [!DNL Salesforce connected app]. Consultez la documentation [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) pour obtenir des conseils.

Assurez-vous également que les [portées](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) mentionnées ci-dessous sont sélectionnées pour l’élément [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Enfin, assurez-vous que la subvention `password` est activée dans votre compte [!DNL Salesforce]. Reportez-vous à la documentation [!DNL Salesforce] [Flux de nom d’utilisateur-mot de passe OAuth 2.0 pour les scénarios spéciaux](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) si vous avez besoin d’instructions.

>[!IMPORTANT]
>
>Si l&#39;administrateur de votre compte [!DNL Salesforce] a restreint l&#39;accès aux plages d&#39;adresses IP de confiance, vous devez les contacter pour que [les adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) soient placées sur la liste autorisée. Reportez-vous à la documentation [!DNL Salesforce] [Limiter l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

#### Créer des champs personnalisés dans [!DNL Salesforce] {#prerequisites-custom-field}

Lors de l’activation d’audiences vers la destination [!DNL Salesforce CRM], vous devez saisir une valeur dans le champ **[!UICONTROL ID de mappage]** pour chaque audience activée, à l’étape **[Planning d’audience](#schedule-segment-export-example)** .

[!DNL Salesforce CRM] nécessite cette valeur pour lire et interpréter correctement les audiences provenant d’un Experience Platform et pour mettre à jour leur état d’audience dans [!DNL Salesforce]. Reportez-vous à la documentation Experience Platform du [ groupe de champs de schéma Détails de l’appartenance à l’audience ](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les états de l’audience.

Pour chaque audience que vous activez de Platform à [!DNL Salesforce CRM], vous devez créer un champ personnalisé de type `Text Area (Long)` dans [!DNL Salesforce]. Vous pouvez définir la longueur des caractères d’un champ d’une taille comprise entre 256 et 131 072 caractères en fonction des besoins de votre entreprise. Pour plus d’informations sur les types de champ personnalisés, consultez la page de documentation [!DNL Salesforce] [Types de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) . Reportez-vous également à la documentation [!DNL Salesforce] pour [créer des champs personnalisés](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin d’aide sur la création de champs.

>[!IMPORTANT]
>
>N’incluez pas d’espaces dans le nom du champ. Utilisez plutôt le caractère de soulignement `(_)` comme séparateur.
>Dans [!DNL Salesforce], vous devez créer des champs personnalisés avec un **[!UICONTROL nom de champ]** qui correspond exactement à la valeur spécifiée dans **[!UICONTROL ID de mappage]** pour chaque segment de plateforme activé. Par exemple, la capture d’écran ci-dessous montre un champ personnalisé nommé `crm_2_seg`. Lors de l’activation d’une audience vers cette destination, ajoutez `crm_2_seg` comme **[!UICONTROL ID de mappage]** pour renseigner les audiences d’audience de l’Experience Platform dans ce champ personnalisé.

Voici un exemple de création de champ personnalisé dans [!DNL Salesforce], *Etape 1 - Sélectionner le type de données* :
![Copie d’écran de l’interface utilisateur Salesforce montrant la création de champs personnalisés, Étape 1 - Sélectionnez le type de données.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Un exemple de création de champ personnalisé dans [!DNL Salesforce], *Etape 2 - Saisissez les détails du champ personnalisé*, est illustré ci-dessous :
![Copie d’écran de l’interface utilisateur Salesforce montrant la création de champs personnalisés, Étape 2 - Saisissez les détails du champ personnalisé.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Pour faire la distinction entre les champs personnalisés utilisés pour les audiences Platform et d’autres champs personnalisés dans [!DNL Salesforce], vous pouvez inclure un préfixe ou un suffixe reconnaissable lors de la création du champ personnalisé. Par exemple, au lieu de `test_segment`, utilisez `Adobe_test_segment` ou `test_segment_Adobe`
>* Si d’autres champs personnalisés sont déjà créés dans [!DNL Salesforce], vous pouvez utiliser le même nom que le segment Platform pour identifier facilement l’audience dans [!DNL Salesforce].

>[!NOTE]
>
>* Les objets de Salesforce sont limités à 25 champs externes. Voir [Attributs de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Cette restriction signifie que vous ne pouvez avoir qu’un maximum de 25 appartenances à une audience Experience Platform actives à tout moment.
>* Si vous avez atteint cette limite dans Salesforce, vous devez supprimer les attributs personnalisés de Salesforce qui ont été utilisés pour stocker l’état de l’audience par rapport aux audiences plus anciennes dans Experience Platform avant de pouvoir utiliser un nouvel **[!UICONTROL ID de mappage]**.

#### Collectez les informations d’identification de [!DNL Salesforce CRM]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination [!DNL Salesforce CRM] :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Username` | Votre nom d&#39;utilisateur de compte [!DNL Salesforce]. | |
| `Password` | Votre mot de passe de compte [!DNL Salesforce]. | |
| `Security Token` | Votre jeton de sécurité [!DNL Salesforce] que vous ajouterez ultérieurement à la fin de votre mot de passe [!DNL Salesforce] pour créer une chaîne concaténée à utiliser comme **[!UICONTROL mot de passe]** lors de l’ [authentification à la destination](#authenticate).<br> Reportez-vous à la documentation [!DNL Salesforce] pour [réinitialiser votre jeton de sécurité](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) afin d’apprendre à le régénérer à partir de l’interface [!DNL Salesforce] si vous ne disposez pas du jeton de sécurité. |  |
| `Custom Domain` | Votre préfixe de domaine [!DNL Salesforce]. <br> Consultez la [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce]. | Si votre domaine [!DNL Salesforce] est<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> vous aurez besoin de `d5i000000isb4eak-dev-ed` comme valeur. |
| `Client ID` | Votre Salesforce `Consumer Key`. <br> Reportez-vous à la [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce]. | |
| `Client Secret` | Votre Salesforce `Consumer Secret`. <br> Reportez-vous à la [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) pour savoir comment obtenir cette valeur à partir de l’interface [!DNL Salesforce]. | |

### Mécanismes de sécurisation {#guardrails}

[!DNL Salesforce] équilibre les charges de transaction en imposant des limites de requête, de débit et de délai d’expiration. Pour plus d’informations, reportez-vous à la section [Limites de requête d’API et Allocations](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) .

Si l&#39;administrateur de votre compte [!DNL Salesforce] a appliqué des restrictions d&#39;adresse IP, vous devrez ajouter [ adresses IP Experience Platform ](/help/destinations/catalog/streaming/ip-address-allow-list.md) aux plages d&#39;adresses IP de confiance de vos comptes [!DNL Salesforce]. Reportez-vous à la documentation [!DNL Salesforce] [Limiter l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

>[!IMPORTANT]
>
>Lorsque vous [activez des segments](#activate), vous devez choisir entre les types *Contact* ou *Lead*. Vous devez vous assurer que vos audiences disposent du mappage de données approprié en fonction du type sélectionné.

## Identités prises en charge {#supported-identities}

[!DNL Salesforce CRM] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `SalesforceId` | L’identifiant [!DNL Salesforce CRM] des identités de contact ou de prospect que vous exportez ou mettez à jour par le biais de votre segment. | Obligatoire |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état d’audience de [!DNL Salesforce CRM] est mis à jour avec l’état d’audience correspondant de Platform, en fonction de la valeur **[!UICONTROL ID de mappage]** fournie à l’étape [planification d’audience](#schedule-segment-export-example).</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Salesforce CRM]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, remplissez les champs requis ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**. Pour obtenir des conseils, reportez-vous à la section [Rassembler [!DNL Salesforce CRM] les informations d’identification](#gather-credentials) .

| Informations d’identification | Description |
| --- | --- |
| **[!UICONTROL Nom d’utilisateur]** | Votre nom d&#39;utilisateur de compte [!DNL Salesforce]. |
| **[!UICONTROL Mot de passe]** | Chaîne concaténée composée du mot de passe de votre compte [!DNL Salesforce] ajouté à votre jeton de sécurité [!DNL Salesforce].<br>La valeur concaténée prend la forme `{PASSWORD}{TOKEN}`.<br> Remarque : n’utilisez pas d’accolades ni d’espaces.<br>Par exemple, si votre [!DNL Salesforce] mot de passe est `MyPa$$w0rd123` et que le [!DNL Salesforce] jeton de sécurité est `TOKEN12345....0000`, la valeur concaténée que vous utiliserez dans le champ **[!UICONTROL Mot de passe]** est `MyPa$$w0rd123TOKEN12345....0000`. |
| **[!UICONTROL Domaine personnalisé]** | Votre préfixe de domaine [!DNL Salesforce]. <br>Par exemple, si votre domaine est *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, vous devez fournir `d5i000000isb4eak-dev-ed` comme valeur. |
| **[!UICONTROL Identifiant du client]** | Votre [!DNL Salesforce] application connectée `Consumer Key`. |
| **[!UICONTROL Secret du client]** | Votre [!DNL Salesforce] application connectée `Consumer Secret`. |

![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un état **[!UICONTROL Connecté]** avec une coche verte, vous pouvez passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’identifiant Salesforce]** :
   * Sélectionnez **[!UICONTROL Contact]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *Contact*.
   * Sélectionnez **[!UICONTROL Lead]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *Lead*.

![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/salesforce/destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Salesforce CRM], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Les attributs spécifiés dans le **[!UICONTROL champ cible]** doivent être nommés exactement comme décrit dans la table des mappages d’attributs, car ces attributs formeront le corps de la requête.

Les attributs spécifiés dans le **[!UICONTROL champ Source]** ne suivent aucune restriction de ce type. Vous pouvez le mapper en fonction de vos besoins, mais assurez-vous que le format des données d’entrée est valide conformément à la [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Si les données d’entrée ne sont pas valides, l’appel de mise à jour vers [!DNL Salesforce] échoue et vos contacts/pistes ne sont pas mis à jour.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL (API) Salesforce CRM], procédez comme suit :

1. À l’étape **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**, une nouvelle ligne de mappage s’affiche à l’écran.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’ajout d’un nouveau mappage.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM ou l’attribut **[!UICONTROL Sélectionner l’espace de noms d’identité]** et sélectionnez une identité.
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]** , choisissez l’espace de noms **[!UICONTROL Sélectionner l’identité]** et sélectionnez une identité ou sélectionnez la catégorie **[!UICONTROL Sélectionner des attributs personnalisés]** et sélectionnez un attribut ou définissez-en un à l’aide du champ **[!UICONTROL Nom de l’attribut]** si nécessaire. Reportez-vous à la [[!DNL Salesforce CRM] documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) pour obtenir des conseils sur les attributs pris en charge.
   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM] :

   **Utilisation des contacts**

   * Si vous travaillez avec *Contacts* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [Contact](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) afin de définir les mappages des champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire* mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM] :

     | Champ source | Champ cible | Notes |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Nom du contact (maximum 80 caractères). |
     | `xdm: person.name.firstName` | `Attribute: FirstName` | Prénom du contact (40 caractères maximum). |
     | `xdm: personalEmail.address` | `Attribute: Email` | Adresse électronique du contact. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Utilisation de pistes**

   * Si vous utilisez *Leads* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) afin de définir des mappages pour les champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire* mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM] :

     | Champ source | Champ cible | Notes |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Nom de famille de l’avance (80 caractères maximum). |
     | `xdm: b2b.companyName` | `Attribute: Company` | `Mandatory`. La compagnie du prospect. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Adresse électronique du prospect. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Planification de l’export d’audience et exemple {#schedule-segment-export-example}

Lors de l’étape [Planification de l’export d’audience](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement les audiences activées à partir de Platform vers le champ personnalisé correspondant dans [!DNL Salesforce].

Pour ce faire, sélectionnez chaque segment, puis saisissez le nom du champ personnalisé [!DNL Salesforce] dans le champ [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** . Reportez-vous à la section [Créer des champs personnalisés dans [!DNL Salesforce]](#prerequisites-custom-field) pour obtenir des conseils et connaître les bonnes pratiques relatives à la création de champs personnalisés dans [!DNL Salesforce].

Par exemple, si votre champ personnalisé [!DNL Salesforce] est `crm_2_seg`, spécifiez cette valeur dans l’ [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** pour renseigner dans ce champ personnalisé les audiences d’audience provenant d’un Experience Platform.

Un exemple de champ personnalisé de [!DNL Salesforce] est illustré ci-dessous :
![[!DNL Salesforce] Copie d’écran de l’interface utilisateur affichant un champ personnalisé.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Un exemple indiquant l’emplacement de l’ [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation des audiences.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Comme illustré ci-dessus, [!DNL Salesforce] **[!UICONTROL Nom du champ]** correspond exactement à la valeur spécifiée dans [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]**.

Selon votre cas d’utilisation, toutes les audiences activées peuvent être mappées au même champ personnalisé [!DNL Salesforce] ou à un **[!UICONTROL nom du champ]** différent dans [!DNL Salesforce CRM]. Un exemple type basé sur l’image illustrée ci-dessus peut être.

| [!DNL Salesforce CRM] nom du segment | [!DNL Salesforce] **[!UICONTROL Nom du champ]** | [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** |
| --- | --- | --- |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Répétez cette section pour chaque segment Platform activé.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant la navigation des destinations.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Passez à l’onglet **[!UICONTROL Données d’activation]** , puis sélectionnez un nom d’audience.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Surveillez la synthèse de l’audience et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Enfin, connectez-vous au site web Salesforce et vérifiez si les profils de l’audience ont été ajoutés ou mis à jour.

   **Utilisation des contacts**

   * Si vous avez sélectionné *Contacts* dans votre segment Platform, accédez à la page **[!DNL Apps]** > **[!DNL Contacts]** .
     ![Capture d&#39;écran Salesforce CRM affichant la page Contacts avec les profils du segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Sélectionnez un *Contact* et vérifiez si les champs sont mis à jour. Vous pouvez constater que chaque état d’audience de [!DNL Salesforce CRM] a été mis à jour avec l’état d’audience correspondant de Platform, en fonction de la valeur **[!UICONTROL ID de mappage]** fournie pendant la [planification d’audience](#schedule-segment-export-example).
     ![ Copie d&#39;écran Salesforce CRM affichant la page Détails du contact avec les statuts d&#39;audience mis à jour.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Utilisation de pistes**

   * Si vous avez sélectionné *Pistes* dans votre segment Platform, accédez à la page **[!DNL Apps]** > **[!DNL Leads]** .
     ![Capture d&#39;écran Salesforce CRM affichant la page Pistes avec les profils du segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Sélectionnez une *piste* et vérifiez si les champs sont mis à jour. Vous pouvez constater que chaque état d’audience de [!DNL Salesforce CRM] a été mis à jour avec l’état d’audience correspondant de Platform, en fonction de la valeur **[!UICONTROL ID de mappage]** fournie pendant la [planification d’audience](#schedule-segment-export-example).
     ![ Copie d&#39;écran Salesforce CRM affichant la page Détails de l&#39;avance avec les statuts d&#39;audience mis à jour.](../../assets/catalog/crm/salesforce/lead-info.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers la destination {#unknown-errors}

* Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../assets/catalog/crm/salesforce/error.png)

   * Pour corriger cette erreur, vérifiez que l’ **[!UICONTROL ID de mappage]** que vous avez fourni dans le workflow d’activation vers la destination [!DNL Salesforce CRM] correspond exactement à la valeur du type de champ personnalisé que vous avez créé dans [!DNL Salesforce]. Pour plus d’informations, reportez-vous à la section [Créer des champs personnalisés dans [!DNL Salesforce]](#prerequisites-custom-field) .

* Lors de l’activation d’un segment, vous pouvez obtenir un message d’erreur : `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Pour corriger cette erreur, contactez l’administrateur de votre compte [!DNL Salesforce] pour ajouter [ adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) aux plages d’adresses IP de confiance de vos comptes [!DNL Salesforce]. Reportez-vous à la documentation [!DNL Salesforce] [Limiter l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Ressources supplémentaires {#additional-resources}

Vous trouverez ci-dessous des informations utiles supplémentaires sur le [portail développeur Salesforce](https://developer.salesforce.com/) :
* [Démarrage rapide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Créer un enregistrement](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Audiences de recommandation personnalisées](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Utilisation de ressources composites](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Cette destination utilise l’API [Upsert Multiple Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) au lieu de l’appel de l’API [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts).
