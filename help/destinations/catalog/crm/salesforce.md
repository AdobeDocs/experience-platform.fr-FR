---
keywords: crm;CRM;destinations crm;salesforce crm;destination Salesforce crm
title: Connexion CRM Salesforce
description: La destination Salesforce CRM vous permet d’exporter les données de votre compte et de les activer dans Salesforce CRM pour vos besoins professionnels.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: b243a5f88cadc238ac3edd3bf45a54564598bbf0
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 4%

---

# Connexion [!DNL Salesforce CRM]

## Présentation {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) est une plateforme de gestion de la relation client (CRM) populaire qui prend en charge les éléments suivants :

* [Pistes](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Un prospect est le nom d’une personne ou d’une société qui peut (ou non) être intéressée par les produits ou services que vous vendez.
* [Contacts](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Un contact est une personne avec laquelle l’un de vos représentants a établi une relation et a été qualifié de client potentiel.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), qui prend en charge les deux types de profils décrits ci-dessus.

When [activation des segments](#activate), vous pouvez choisir entre des pistes ou des contacts et mettre à jour les attributs et les données de segment dans [!DNL Salesforce CRM].

[!DNL Salesforce CRM] utilise OAuth 2 avec l’octroi de mot de passe comme mécanisme d’authentification pour communiquer avec l’API REST Salesforce. Instructions pour vous authentifier à votre [!DNL Salesforce CRM] sont plus loin, dans la section [Authentification à la destination](#authenticate) .

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des segments à partir de vos données hors ligne et envoyer ces segments à Salesforce CRM, afin qu’ils s’affichent dans les flux des utilisateurs dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer les données vers la destination Salesforce CRM, vous devez disposer d’un [schema](/help/xdm/schema/composition.md), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) créé dans [!DNL Experience Platform].

### Conditions préalables dans [!DNL Salesforce CRM] {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL Salesforce CRM], afin d’exporter des données de Platform vers votre compte Salesforce :

#### Vous devez disposer d’un compte Salesforce. {#prerequisites-account}

Accédez à Salesforce [essai](https://www.salesforce.com/in/form/signup/freetrial-sales/) pour enregistrer et créer un compte Salesforce, le cas échéant.

#### Configuration d’une application connectée {#prerequisites-connected-app}

Ensuite, vous devez configurer une [application connectée](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) dans votre compte Salesforce, le cas échéant.

Dans l’application connectée, assurez-vous que [Paramètres OAuth](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) est activée.

Assurez-vous également que la variable [portées](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) mentionnés ci-dessous sont sélectionnés.

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

#### Créer un champ personnalisé dans Salesforce {#prerequisites-custom-field}

Créer un champ personnalisé de type `Text Area Long`, que l’Experience Platform utilisera pour mettre à jour l’état du segment dans [!DNL Salesforce CRM].
Reportez-vous à la documentation de Salesforce pour [créer des champs personnalisés](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

>[!IMPORTANT]
>
>Assurez-vous qu’il n’y a aucun espace dans le nom du champ. Utilisez plutôt le trait de soulignement. `(_)` comme séparateur.

>[!NOTE]
>
>* Les objets de Salesforce sont limités à 25 champs externes. Voir [Attributs de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Cette restriction implique que vous ne pouvez avoir qu’un maximum de 25 appartenances aux segments Experience Platform principales à tout moment.
>* Si vous avez atteint cette limite dans Salesforce, vous devez supprimer l’attribut personnalisé de Salesforce qui a été utilisé pour stocker l’état du segment par rapport aux segments plus anciens dans Experience Platform avant un nouveau **[!UICONTROL ID de mappage]** peut être utilisé.


Reportez-vous à la documentation Adobe Experience Platform pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

#### Collecte des informations d’identification Salesforce {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la variable [!DNL Salesforce CRM] destination :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| <ul><li>Préfixe de domaine Salesforce</li></ul> | Voir [Préfixe de domaine Salesforce](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) pour plus d’informations. | <ul><li>Si votre domaine est tel que ci-dessous, vous avez besoin de la valeur mise en surbrillance.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Clé client</li><li>Secret du client</li></ul> | Reportez-vous à la section [Documentation de Salesforce](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | <ul><li>r23kxxxxxxxxxx0z05xxxxxx</code></li><li>ipxxxxxxxxxxT4xxxxxxxxxx</code></li></ul> |

### Éléments de sécurité {#guardrails}

Salesforce équilibre les charges de transaction en imposant des limites de demande, de taux et de délai d’expiration. Reportez-vous à la section [Limites de requête d’API et affectations](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) pour plus d’informations.

>[!IMPORTANT]
>
>When [activation des segments](#activate) vous devez choisir entre *Contact* ou *prospect* types. Vous devez vous assurer que vos segments disposent du mappage de données approprié en fonction du type sélectionné.

## Identités prises en charge {#supported-identities}

[!DNL Salesforce CRM] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `SalesforceId` | Le [!DNL Salesforce CRM] identifiant des identités de contact ou de prospect que vous exportez ou mettez à jour par le biais de votre segment. | Obligatoire |

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités. *(par exemple : adresse email, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Chaque état de segment dans [!DNL Salesforce CRM] est mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des segments](#schedule-segment-export-example) étape .</li></ul> |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]** rechercher [!DNL Salesforce CRM]. Vous pouvez également la localiser sous le **[!UICONTROL CRM]** catégorie.

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Capture d’écran de l’interface utilisateur de Platform montrant comment vous authentifier.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Mot de passe]**: Votre mot de passe du compte Salesforce.
* **[!UICONTROL Domaine personnalisé]**: Votre domaine Salesforce.
* **[!UICONTROL ID client]**: Votre Clé de consommateur de l’application connectée Salesforce.
* **[!UICONTROL Secret du client]**: Votre application connectée Salesforce Consumer Secret.
* **[!UICONTROL Nom d’utilisateur]**: Votre nom d’utilisateur de compte Salesforce.

Si les détails fournis sont valides, l’interface utilisateur affiche une **[!UICONTROL Connecté]** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Type d’identifiant Salesforce]**: Sélectionner **[!UICONTROL Contact]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *Contact*. Sélectionner **[!UICONTROL prospect]** si les identités que vous souhaitez exporter ou mettre à jour sont de type *prospect*.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement vos données d’audience de Adobe Experience Platform vers le [!DNL Salesforce CRM] destination, vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible. Pour mapper correctement vos champs XDM à [!DNL Salesforce CRM] champs de destination, procédez comme suit :

1. Dans le **[!UICONTROL Mappage]** étape, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**, une nouvelle ligne de mappage s’affiche à l’écran.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform pour Ajouter un nouveau mappage.](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. Dans le **[!UICONTROL Sélectionner le champ source]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** ou **[!UICONTROL Sélectionner des attributs]** catégorie et sélectionnez `crmID`.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform pour le mappage source.](../../assets/catalog/crm/salesforce/source-mapping.png)

1. Dans le **[!UICONTROL Sélectionner le champ cible]** , choisissez la **[!UICONTROL Sélectionner un espace de noms d’identité]** catégorie et sélectionnez `SalesforceId`.
   ![Copie d’écran de l’interface utilisateur de Platform montrant le mappage de Target pour SalesforceId.](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

   * Ajoutez le mappage suivant entre votre schéma de profil XDM et votre [!DNL Salesforce CRM] instance :
   | Schéma de profil XDM | [!DNL Salesforce CRM] Instance | Obligatoire |
   |---|---|---|
   | `crmID` | `SalesforceId` | Oui |

   * **[!UICONTROL Sélectionner des attributs personnalisés]**: sélectionnez cette option pour mapper votre champ source à un attribut personnalisé que vous avez défini dans la variable **[!UICONTROL Nom de l’attribut]** champ . Reportez-vous à la section [[!DNL Salesforce CRM] documentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) pour plus d’informations sur les attributs pris en charge.
      ![Copie d’écran de l’interface utilisateur de Platform montrant le mappage de Target pour le nom de famille.](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

   * Si vous utilisez des *Contacts* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [Contact](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) pour définir les mappages des champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire*, qui est mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et votre [!DNL Salesforce CRM] instance :

   | Schéma de profil XDM | [!DNL Salesforce CRM] Instance | Remarques |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Nom du contact (maximum 80 caractères). |
   | `person.name.firstName` | `FirstName` | Prénom du contact (40 caractères maximum). |
   | `personalEmail.address` | `Email` | Adresse électronique du contact. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les mappages Target.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   * Si vous utilisez des *Pistes* dans votre segment, reportez-vous à la référence d’objet dans Salesforce pour [prospect](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) pour définir les mappages des champs à mettre à jour.
   * Vous pouvez identifier les champs obligatoires en recherchant le mot *Obligatoire*, qui est mentionné dans la description des champs du lien ci-dessus.
   * Selon les champs que vous souhaitez exporter ou mettre à jour, ajoutez des mappages entre votre schéma de profil XDM et votre [!DNL Salesforce CRM] instance :

   | Schéma de profil XDM | [!DNL Salesforce CRM] Instance | Remarques |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Nom du contact (maximum 80 caractères). |
   | `b2b.companyName` | `Company` | `Required`. La compagnie du prospect. |
   | `personalEmail.address` | `Email` | Adresse électronique du contact. |

   * Un exemple d’utilisation de ces mappages est illustré ci-dessous :
      ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les mappages Target.](../../assets/catalog/crm/salesforce/mappings-leads.png)




### Planification de l’exportation de segments et exemple {#schedule-segment-export-example}

Lors de l’exécution de la variable [Planification de l’exportation de segments](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) vous devez mapper manuellement les segments Platform à l’attribut de champ personnalisé dans Salesforce.

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut de champ personnalisé correspondant à partir de Salesforce dans la variable **[!UICONTROL ID de mappage]** champ .

>[!IMPORTANT]
>
>* La valeur utilisée pour la variable **[!UICONTROL ID de mappage]** doit correspondre exactement au nom de l’attribut de champ personnalisé créé dans Salesforce.
>* Assurez-vous que le nom de l’attribut de champ personnalisé que vous avez créé dans Salesforce n’utilise pas d’espace.


Voici un exemple :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Planification de l’exportation de segments.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## Validation de l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Capture d’écran de l’interface utilisateur de Platform montrant Parcourir les destinations.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que l’état est **[!UICONTROL enabled]**.
   ![Capture d’écran de l’interface utilisateur de Platform montrant l’exécution du flux de données des destinations.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Basculez vers le **[!UICONTROL Données d’activation]** , puis sélectionnez un nom de segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant les données d’activation des destinations.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Exemple de capture d’écran de l’interface utilisateur de Platform montrant Segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Enfin, connectez-vous au site web Salesforce et vérifiez si les profils du segment ont été ajoutés ou mis à jour.
   * Si vous aviez *Contacts* dans votre segment Platform, accédez au **[!DNL Apps]** > **[!DNL Contacts]** page.
      ![Capture d’écran Salesforce CRM affichant la page Contacts avec les profils du segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Sélectionnez une *Contact* et vérifiez si les champs sont mis à jour. Vous pouvez voir que chaque état de segment dans [!DNL Salesforce CRM] a été mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des segments](#schedule-segment-export-example).
      ![Capture d’écran Salesforce CRM affichant la page Détails du contact avec les états de segment mis à jour.](../../assets/catalog/crm/salesforce/contact-info.png)

   * Si vous aviez *Pistes* dans votre segment Platform, puis accédez au **[!DNL Apps]** > **[!DNL Leads]** page.
      ![Capture d’écran Salesforce CRM affichant la page Pistes avec les profils du segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Sélectionnez une *prospect* et vérifiez si les champs sont mis à jour. Vous pouvez voir que chaque état de segment dans [!DNL Salesforce CRM] a été mis à jour avec l’état du segment correspondant de Platform, en fonction de la variable **[!UICONTROL ID de mappage]** valeur fournie pendant la [planification des segments](#schedule-segment-export-example).
      ![Capture d’écran Salesforce CRM affichant la page Détails de l’piste avec les états de segment mis à jour.](../../assets/catalog/crm/salesforce/lead-info.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers la destination {#unknown-errors}

Lors de la vérification d’une exécution de flux de données, si vous obtenez le message d’erreur suivant : `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../assets/catalog/crm/salesforce/error.png)

Pour corriger cette erreur, vérifiez que la variable **[!UICONTROL ID de mappage]** vous avez fourni dans [!DNL Salesforce CRM] pour votre segment Platform valide et existe dans [!DNL Salesforce CRM].

## Ressources supplémentaires {#additional-resources}

Informations utiles supplémentaires de la [Portail de développement Salesforce](https://developer.salesforce.com/) est ci-dessous :
* [Démarrage rapide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Création d’un enregistrement](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Audiences de recommandations personnalisées](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Utilisation de ressources composites](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Cette destination tire parti de la variable [Mettre à jour plusieurs enregistrements](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API au lieu de [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) appel API.