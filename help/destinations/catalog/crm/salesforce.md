---
keywords: crm;CRM;destinations crm;salesforce crm;destination Salesforce crm
title: Connexion CRM à Salesforce
description: La destination Salesforce CRM vous permet d’exporter les données de votre compte et de les activer dans Salesforce CRM pour vos besoins professionnels.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '2818'
ht-degree: 21%

---

# Connexion [!DNL Salesforce CRM]

## Présentation {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) est une plateforme de gestion de la relation client (CRM) populaire qui prend en charge les types de profils décrits ci-dessous :

* [Pistes](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Un prospect est le nom d’une personne ou d’une société qui peut (ou non) être intéressée par les produits ou services que vous vendez.
* [Contacts](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Un contact est une personne avec laquelle l’un de vos représentants a établi une relation et a été qualifié de client potentiel.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de la fonction [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), qui prend en charge les deux types de profils décrits ci-dessus.

When [activation des segments](#activate), vous pouvez choisir entre des pistes ou des contacts et mettre à jour les attributs et les données d’audience dans [!DNL Salesforce CRM].

[!DNL Salesforce CRM] utilise OAuth 2 avec l’octroi de mot de passe comme mécanisme d’authentification pour communiquer avec l’API REST Salesforce. Les instructions vous permettant de vous authentifier sur votre instance [!DNL Salesforce CRM] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

En tant que professionnel du marketing, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des audiences à partir de vos données hors ligne et envoyer ces audiences à Salesforce CRM, afin de mettre à jour l’appartenance CRM dès que les audiences et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer les données vers la destination Salesforce CRM, vous devez disposer d’un [schema](/help/xdm/schema/composition.md), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) créé dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL Salesforce CRM] {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL Salesforce CRM], afin d’exporter des données de Platform vers votre compte Salesforce :

#### Vous devez avoir un compte [!DNL Salesforce]. {#prerequisites-account}

Accédez au [!DNL Salesforce] [essai](https://www.salesforce.com/in/form/signup/freetrial-sales/) pour enregistrer et créer une [!DNL Salesforce] , si vous n’en avez pas déjà un.

#### Configuration d’une application connectée dans [!DNL Salesforce] {#prerequisites-connected-app}

Tout d’abord, vous devez configurer une [[!DNL Salesforce] application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) dans votre [!DNL Salesforce] , si vous n’en avez pas déjà un. [!DNL Salesforce CRM] exploite l’application connectée à laquelle se connecter [!DNL Salesforce].

Ensuite, activez [!DNL OAuth Settings for API Integration] pour le [!DNL Salesforce connected app]. Voir [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) documentation à titre indicatif.

Assurez-vous également que la variable [portées](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) mentionnés ci-dessous sont sélectionnés pour le [!DNL Salesforce connected app].

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

Enfin, assurez-vous que la variable `password` la subvention est activée dans votre [!DNL Salesforce] compte . Voir [!DNL Salesforce] [Flux OAuth 2.0 Username-Password pour des scénarios spécifiques](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) si vous avez besoin d’instructions.

>[!IMPORTANT]
>
>Si votre [!DNL Salesforce] l’administrateur de compte a un accès limité aux plages d’adresses IP de confiance. Vous devez les contacter pour obtenir [IP EXPERIENCE PLATFORM](/help/destinations/catalog/streaming/ip-address-allow-list.md) placé sur la liste autorisée. Voir [!DNL Salesforce] [Limitation de l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

#### Créer des champs personnalisés dans [!DNL Salesforce] {#prerequisites-custom-field}

Lors de l’activation d’audiences dans la variable [!DNL Salesforce CRM] destination, vous devez saisir une valeur dans la variable **[!UICONTROL ID de mappage]** pour chaque audience activée, dans la variable **[Planification de l’audience](#schedule-segment-export-example)** étape .

[!DNL Salesforce CRM] nécessite cette valeur pour lire et interpréter correctement les audiences provenant d’un Experience Platform et pour mettre à jour leur état d’audience dans [!DNL Salesforce]. Reportez-vous à la documentation Experience Platform pour [Groupe de champs Détails de l’appartenance à une audience](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les états d’audience.

Pour chaque audience que vous activez de Platform à [!DNL Salesforce CRM], vous devez créer un champ personnalisé de type `Text Area (Long)` dans [!DNL Salesforce]. Vous pouvez définir la longueur des caractères d’un champ d’une taille comprise entre 256 et 131 072 caractères en fonction des besoins de votre entreprise. Voir [!DNL Salesforce] [Types de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) page de documentation pour plus d’informations sur les types de champ personnalisés. Consultez également la section [!DNL Salesforce] documentation à [créer des champs personnalisés](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si vous avez besoin d’aide pour la création de champs.

>[!IMPORTANT]
>
>N’incluez pas d’espaces dans le nom du champ. Utilisez plutôt le trait de soulignement. `(_)` comme séparateur.
>Within [!DNL Salesforce] vous devez créer des champs personnalisés avec un **[!UICONTROL Nom du champ]** qui correspond exactement à la valeur spécifiée dans **[!UICONTROL ID de mappage]** pour chaque segment Platform activé. Par exemple, la capture d’écran ci-dessous illustre un champ personnalisé nommé `crm_2_seg`. Lorsque vous activez une audience sur cette destination, ajoutez `crm_2_seg` as **[!UICONTROL ID de mappage]** pour renseigner les audiences d’audience d’Experience Platform dans ce champ personnalisé.

Exemple de création de champ personnalisé dans [!DNL Salesforce], *Etape 1 - Sélection du type de données*, est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur Salesforce montrant la création de champs personnalisés, Étape 1 - Sélectionnez le type de données.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Exemple de création de champ personnalisé dans [!DNL Salesforce], *Etape 2 - Saisissez les détails du champ personnalisé*, est illustré ci-dessous :
![Copie d’écran de l’interface utilisateur Salesforce affichant la création de champ personnalisé, Étape 2 - Saisissez les détails du champ personnalisé.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Pour distinguer les champs personnalisés utilisés pour les audiences Platform des autres champs personnalisés dans [!DNL Salesforce] vous pouvez inclure un préfixe ou un suffixe reconnaissable lors de la création du champ personnalisé. Par exemple, au lieu de `test_segment`, utilisez `Adobe_test_segment` ou `test_segment_Adobe`
>* Si d’autres champs personnalisés sont déjà créés dans [!DNL Salesforce], vous pouvez utiliser le même nom que le segment Platform pour identifier facilement l’audience dans [!DNL Salesforce].

>[!NOTE]
>
>* Les objets de Salesforce sont limités à 25 champs externes. Voir [Attributs de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Cette restriction signifie que vous ne pouvez avoir qu’un maximum de 25 appartenances à une audience Experience Platform actives à tout moment.
>* Si vous avez atteint cette limite dans Salesforce, vous devez supprimer les attributs personnalisés de Salesforce qui ont été utilisés pour stocker l’état de l’audience par rapport aux audiences plus anciennes dans Experience Platform avant une nouvelle **[!UICONTROL ID de mappage]** peut être utilisé.

#### Collectez les informations d’identification de [!DNL Salesforce CRM]. {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la variable [!DNL Salesforce CRM] destination :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Username` | Votre [!DNL Salesforce] nom d’utilisateur du compte. | |
| `Password` | Votre [!DNL Salesforce] mot de passe du compte. | |
| `Security Token` | Votre [!DNL Salesforce] jeton de sécurité que vous ajouterez ultérieurement à la fin de votre [!DNL Salesforce] Mot de passe pour créer une chaîne concaténée à utiliser comme **[!UICONTROL Password]** when [authentification à la destination](#authenticate).<br> Voir [!DNL Salesforce] documentation à [réinitialiser votre jeton de sécurité](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) pour apprendre à le régénérer à partir de la [!DNL Salesforce] si vous ne disposez pas du jeton de sécurité. |  |
| `Custom Domain` | Votre [!DNL Salesforce] préfixe de domaine. <br> Voir [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce] . | Si votre [!DNL Salesforce] domain est<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> vous aurez besoin de `d5i000000isb4eak-dev-ed` comme valeur. |
| `Client ID` | Votre Salesforce `Consumer Key`. <br> Voir [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce] . | |
| `Client Secret` | Votre Salesforce `Consumer Secret`. <br> Voir [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) pour savoir comment obtenir cette valeur de la fonction [!DNL Salesforce] . | |

### Mécanismes de sécurisation {#guardrails}

[!DNL Salesforce] équilibre les charges de transaction en imposant des limites de requête, de débit et de délai d’expiration. Voir [Limites de requête d’API et affectations](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) pour plus d’informations.

Si votre [!DNL Salesforce] l’administrateur de compte a appliqué des restrictions d’adresse IP. Vous devrez ajouter [Adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) à votre [!DNL Salesforce] plages d’adresses IP de confiance des comptes. Voir [!DNL Salesforce] [Limitation de l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

>[!IMPORTANT]
>
>When [activation des segments](#activate) vous devez choisir entre *Contact* ou *prospect* types. Vous devez vous assurer que vos audiences disposent du mappage de données approprié en fonction du type sélectionné.

## Identités prises en charge {#supported-identities}

[!DNL Salesforce CRM] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `SalesforceId` | La variable [!DNL Salesforce CRM] identifiant des identités de contact ou de prospect que vous exportez ou mettez à jour par le biais de votre segment. | Obligatoire |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités, *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état d’audience dans [!DNL Salesforce CRM] est mis à jour avec l’état d’audience correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des audiences](#schedule-segment-export-example) étape .</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL Salesforce CRM]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs obligatoires ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**. Voir [Collecte [!DNL Salesforce CRM] informations](#gather-credentials) pour obtenir des conseils.
| Credential | Description | | — | — | | **[!UICONTROL Nom d’utilisateur]** | Votre [!DNL Salesforce] nom d’utilisateur du compte. | | **[!UICONTROL Password]** | Chaîne concaténée composée de votre [!DNL Salesforce] mot de passe du compte ajouté à votre [!DNL Salesforce] Jeton de sécurité.<br>La valeur concaténée prend la forme `{PASSWORD}{TOKEN}`.<br> Notez que n’utilisez pas d’accolades ni d’espaces.<br>Par exemple, si la variable [!DNL Salesforce] Le mot de passe est `MyPa$$w0rd123` et [!DNL Salesforce] Le jeton de sécurité est `TOKEN12345....0000`, la valeur concaténée que vous utiliserez dans la variable **[!UICONTROL Password]** est `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL Domaine personnalisé]** | Votre [!DNL Salesforce] préfixe de domaine. <br>Par exemple, si votre domaine est *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, vous devez fournir `d5i000000isb4eak-dev-ed` comme valeur. | | **[!UICONTROL ID client]** | Votre [!DNL Salesforce] application connectée `Consumer Key`. | | **[!UICONTROL Secret du client]** | Votre [!DNL Salesforce] application connectée `Consumer Secret`. |

![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche une **[!UICONTROL Connecté]** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’identifiant Salesforce]**:
   * Sélectionner **[!UICONTROL Contact]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *Contact*.
   * Sélectionner **[!UICONTROL prospect]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *prospect*.

![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/salesforce/destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL Salesforce CRM], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Attributs spécifiés dans la variable **[!UICONTROL Champ cible]** doit être nommé exactement comme décrit dans le tableau mappings d’attributs , car ces attributs forment le corps de la requête.

Attributs spécifiés dans la variable **[!UICONTROL Champ source]** ne suivez aucune restriction de ce type. Vous pouvez le mapper en fonction de vos besoins, mais assurez-vous que le format des données d’entrée est valide en fonction de la variable [[!DNL Salesforce] documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Si les données d’entrée ne sont pas valides, l’appel de mise à jour vers [!DNL Salesforce] échoue et vos contacts/prospects ne sont pas mis à jour.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL (API) Salesforce CRM], procédez comme suit :

1. Dans le **[!UICONTROL Mappage]** étape, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**, une nouvelle ligne de mappage s’affiche à l’écran.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’ajout d’un nouveau mappage.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM ou choisissez l’option **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité.
1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité ou choisissez **[!UICONTROL Sélectionner des attributs personnalisés]** et sélectionnez un attribut ou définissez-en un à l’aide de la fonction **[!UICONTROL Nom de l’attribut]** selon les besoins. Voir [[!DNL Salesforce CRM] documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) pour plus d’informations sur les attributs pris en charge.
   * Répétez ces étapes pour ajouter les mappages suivants entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM]:

   **Utilisation de contacts**

   * Si vous utilisez des *Contacts* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [Contact](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) pour définir les mappages des champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire*, qui est mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM]: |Champ source|Champ cible| Remarques | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Nom du contact (maximum 80 caractères). |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`| Prénom du contact jusqu’à 40 caractères. | |`xdm: personalEmail.address`|`Attribute: Email`| Adresse électronique du contact. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Utilisation de pistes**

   * Si vous utilisez des *Pistes* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [prospect](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) pour définir les mappages des champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire*, qui est mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et [!DNL (API) Salesforce CRM]: |Champ source|Champ cible| Remarques | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Nom de famille de l’avance (80 caractères maximum). |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. La compagnie du prospect. | |`xdm: personalEmail.address`|`Attribute: Email`| Adresse électronique du prospect. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
     ![Capture d’écran de l’interface utilisateur de Platform montrant les mappings de ciblage.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Une fois les mappages fournis pour la connexion à la destination, sélectionnez **[!UICONTROL Suivant]**.

### Planification de l’export d’audience et exemple {#schedule-segment-export-example}

Lors de l’exécution du [Planification de l’exportation des audiences](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) étape vous devez mapper manuellement les audiences activées à partir de Platform à leur champ personnalisé correspondant dans [!DNL Salesforce].

Pour ce faire, sélectionnez chaque segment, puis saisissez le nom du champ personnalisé de [!DNL Salesforce] dans le [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** champ . Voir [Créer des champs personnalisés dans [!DNL Salesforce]](#prerequisites-custom-field) pour obtenir des conseils sur la création de champs personnalisés dans [!DNL Salesforce].

Par exemple, si la variable [!DNL Salesforce] champ personnalisé `crm_2_seg`, indiquez cette valeur dans la variable [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** pour renseigner les audiences d’audience d’Experience Platform dans ce champ personnalisé.

Exemple de champ personnalisé à partir de [!DNL Salesforce] est illustré ci-dessous :
![[!DNL Salesforce] Copie d’écran de l’interface utilisateur affichant un champ personnalisé.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Un exemple indiquant l’emplacement de la variable [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation d’audience.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Comme illustré ci-dessus [!DNL Salesforce] **[!UICONTROL Nom du champ]** correspond exactement à la valeur spécifiée dans [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]**.

Selon le cas d’utilisation, toutes les audiences activées peuvent être mappées sur le même [!DNL Salesforce] champ personnalisé ou différent **[!UICONTROL Nom du champ]** in [!DNL Salesforce CRM]. Un exemple type basé sur l’image illustrée ci-dessus peut être.
| [!DNL Salesforce CRM] nom du segment | [!DNL Salesforce] **[!UICONTROL Nom du champ]** | [!DNL Salesforce CRM] **[!UICONTROL ID de mappage]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Répétez cette section pour chaque segment Platform activé.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant la navigation des destinations.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que le statut est **[!UICONTROL activé]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Basculez vers le **[!UICONTROL Données d’activation]** , puis sélectionnez un nom d’audience.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Surveillez la synthèse de l’audience et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Enfin, connectez-vous au site web Salesforce et vérifiez si les profils de l’audience ont été ajoutés ou mis à jour.

   **Utilisation de contacts**

   * Si vous avez sélectionné *Contacts* dans votre segment Platform, accédez au **[!DNL Apps]** > **[!DNL Contacts]** page.
     ![Capture d’écran Salesforce CRM affichant la page Contacts avec les profils du segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Sélectionnez une *Contact* et vérifiez si les champs sont mis à jour. Vous pouvez voir que chaque état d’audience dans [!DNL Salesforce CRM] a été mis à jour avec l’état d’audience correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des audiences](#schedule-segment-export-example).
     ![Capture d’écran Salesforce CRM affichant la page Détails du contact avec les statuts d’audience mis à jour.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Utilisation de pistes**

   * Si vous avez sélectionné *Pistes* dans votre segment Platform, puis accédez au **[!DNL Apps]** > **[!DNL Leads]** page.
     ![Capture d’écran Salesforce CRM affichant la page Pistes avec les profils du segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Sélectionnez une *prospect* et vérifiez si les champs sont mis à jour. Vous pouvez voir que chaque état d’audience dans [!DNL Salesforce CRM] a été mis à jour avec l’état d’audience correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des audiences](#schedule-segment-export-example).
     ![Capture d’écran Salesforce CRM affichant la page Détails du prospect avec les statuts d’audience mis à jour.](../../assets/catalog/crm/salesforce/lead-info.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers la destination {#unknown-errors}

* Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../assets/catalog/crm/salesforce/error.png)

   * Pour corriger cette erreur, vérifiez que la variable **[!UICONTROL ID de mappage]** que vous avez fourni dans le workflow d’activation au [!DNL Salesforce CRM] destination correspond exactement à la valeur du type de champ personnalisé que vous avez créé dans [!DNL Salesforce]. Voir [Créer des champs personnalisés dans [!DNL Salesforce]](#prerequisites-custom-field) pour plus d’informations.

* Lors de l’activation d’un segment, un message d’erreur peut s’afficher : `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Pour corriger cette erreur, contactez votre [!DNL Salesforce] administrateur de compte à ajouter [Adresses IP Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) à votre [!DNL Salesforce] plages d’adresses IP de confiance des comptes. Voir [!DNL Salesforce] [Limitation de l’accès aux plages d’adresses IP approuvées pour une application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

## Ressources supplémentaires {#additional-resources}

Informations utiles supplémentaires de la section [Portail de développement Salesforce](https://developer.salesforce.com/) est ci-dessous :
* [Démarrage rapide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Création d’un enregistrement](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Audiences de recommandations personnalisées](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Utilisation de ressources composites](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Cette destination tire parti de la variable [Mettre à jour plusieurs enregistrements](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API au lieu de [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) appel API.