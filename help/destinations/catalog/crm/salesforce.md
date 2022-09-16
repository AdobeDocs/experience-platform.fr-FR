---
keywords: crm;CRM;destinations crm;salesforce crm;destination Salesforce crm
title: Connexion CRM Salesforce
description: La destination Salesforce CRM vous permet d’exporter les données de votre compte et de les activer dans Salesforce CRM pour vos besoins professionnels.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 7d8b25b25b53edd7de836fc508de15cfa2a5a3a2
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 6%

---

# Connexion [!DNL Salesforce CRM]

## Présentation {#overview}

[Salesforce CRM](https://www.salesforce.com/) est une plateforme de gestion de la relation client (CRM) populaire.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [API REST Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts), qui vous permet de mettre à jour les identités d’un segment dans Salesforce CRM.

Salesforce CRM utilise OAuth 2 avec l’octroi de mot de passe comme mécanisme d’authentification pour communiquer avec l’API REST Salesforce. Les instructions d’authentification à votre instance Salesforce CRM sont présentées ci-dessous, dans la section [Authentification à la destination](#authenticate) .

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, vous pouvez proposer des expériences personnalisées à vos utilisateurs en fonction des attributs de leurs profils Adobe Experience Platform. Vous pouvez créer des segments à partir de vos données hors ligne et envoyer ces segments à Salesforce CRM, afin qu’ils s’affichent dans les flux des utilisateurs dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Conditions préalables dans Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer les données vers la destination Salesforce CRM, vous devez disposer d’un [schema](/help/xdm/schema/composition.md), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) créé dans [!DNL Experience Platform].

### Conditions préalables dans Salesforce CRM {#prerequisites-destination}

Notez les conditions préalables suivantes dans Salesforce, afin d’exporter des données de Platform vers votre compte Salesforce :

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

Créer un champ personnalisé de type `Text Area Long` l’Experience Platform utilisé pour mettre à jour l’état du segment dans Salesforce CRM.
Reportez-vous à la documentation de Salesforce pour [créer des champs personnalisés](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) si vous avez besoin de conseils supplémentaires.

>[!IMPORTANT]
>
> Assurez-vous qu’il n’y a aucun espace dans le nom du champ. Utilisez plutôt le trait de soulignement. `(_)` comme séparateur.

>[!NOTE]
>
> * Les objets de Salesforce sont limités à 25 champs externes. Voir [Attributs de champ personnalisés](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
> * Cette restriction implique que vous ne pourrez disposer qu’à tout moment d’un maximum de 25 adhésions au segment Experience Platform principales.
> * Si vous avez atteint cette limite dans Salesforce, vous devez supprimer l’attribut personnalisé de Salesforce qui a été utilisé pour stocker l’état du segment par rapport aux segments plus anciens dans Experience Platform avant de pouvoir utiliser un nouveau mappingId.


Reportez-vous à la documentation Adobe Experience Platform pour [Groupe de champs Détails de l’appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin d’instructions sur les états de segment.

#### Collecte des informations d’identification Salesforce {#gather-credentials}

Notez les éléments ci-dessous avant de vous authentifier à la destination Salesforce CRM :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| <ul><li>Préfixe de domaine Salesforce</li></ul> | Voir [Préfixe de domaine Salesforce](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) pour plus d’informations. | <ul><li>Si votre domaine est tel que ci-dessous, vous avez besoin de la valeur mise en surbrillance.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Clé client</li><li>Secret du client</li></ul> | Reportez-vous à la section [Documentation de Salesforce](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) si vous avez besoin de conseils supplémentaires. | <ul><li>r23kxxxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxx</li></ul> |

## Identités prises en charge {#supported-identities}

Salesforce CRM prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| SalesforceId | Identifiant CRM Salesforce personnalisé qui prend en charge le mappage de n’importe quelle identité. | Obligatoire. Vous pouvez envoyer n’importe quel [identité](../../../identity-service/namespaces.md) au [!DNL Salesforce CRM] tant que vous le mappez à la variable `SalesforceId`. |

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités. *(par exemple : adresse email, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> Les statuts des segments de Platform sont exportés vers [!DNL Salesforce CRM] en spécifiant l’attribut de champ personnalisé correspondant dans [!DNL Salesforce CRM] dans le **[!UICONTROL Activer la destination]** > **[!UICONTROL Planification de l’exportation de segments]** > **[!UICONTROL ID de mappage]** champ .</li></ul> |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

![Catalogue](../../assets/catalog/crm/salesforce/catalog.png)

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Exemple de capture d’écran montrant comment s’authentifier auprès de Salesforce CRM](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Mot de passe]**: Votre mot de passe du compte Salesforce.
* **[!UICONTROL ID client]**: Votre Clé de consommateur de l’application connectée Salesforce.
* **[!UICONTROL Secret du client]**: Votre application connectée Salesforce Consumer Secret.
* **[!UICONTROL Nom d’utilisateur]**: Votre nom d’utilisateur de compte Salesforce.

Si les détails fournis sont valides, l’interface utilisateur affiche une **Connecté** avec une coche verte, vous pouvez ensuite passer à l’étape suivante.

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Exemple de capture d’écran montrant comment remplir les détails pour Salesforce CRM](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Domaine personnalisé]**: Votre domaine Salesforce.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Considérations sur le mappage et exemple {#mapping-considerations-example}

Pour envoyer correctement les données d’audience de Adobe Experience Platform vers la destination Salesforce CRM, vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible. Pour mapper correctement vos champs XDM aux champs de destination Salesforce CRM, procédez comme suit :

1. À l’étape Mappage , cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**, une nouvelle ligne de mappage s’affiche à l’écran.

   ![Ajouter un nouveau mappage](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. Dans la fenêtre de sélection du champ source, lors de la sélection du champ source, choisissez la variable **[!UICONTROL Sélectionner des attributs]** et ajoutez les mappages souhaités.

   ![Mappage des sources](../../assets/catalog/crm/salesforce/source-mapping.png)

1. Dans la fenêtre de sélection du champ cible , sélectionnez le champ cible et choisissez l&#39;option **[!UICONTROL Sélectionner un espace de noms d’identité]** et ajoutez les mappages souhaités.

   ![Mappage de ciblage à l’aide de SalesforceId](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

1. Pour les attributs personnalisés, dans la fenêtre de sélection du champ cible , sélectionnez le champ cible et choisissez l&#39;option **[!UICONTROL Sélectionner des attributs personnalisés]** catégorie, indiquez ensuite le nom de l’attribut cible souhaité et ajoutez les mappages souhaités.

   ![Mappage de la cible à l’aide de LastName](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

1. Par exemple, vous pouvez ajouter le mappage suivant entre votre schéma de profil XDM et votre [!DNL Salesforce CRM] instance :

   |  | Schéma de profil XDM | [!DNL Salesforce CRM] Instance | Obligatoire |
   |---|---|---|---|
   | Attributs | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>E-mail</code></li></ul> |
   | Identités | <ul><li>crmID</code></li></ul> | <ul><li>SalesforceId</code></li></ul> | Oui |

1. Un exemple d’utilisation de ces mappages est illustré ci-dessous :

   ![Mapping de ciblage](../../assets/catalog/crm/salesforce/mappings.png)

### Planification de l’exportation de segments et exemple {#schedule-segment-export-example}

Lors de l’exécution de la variable [Planification de l’exportation de segments](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) vous devez mapper manuellement les segments Platform à l’attribut de champ personnalisé dans Salesforce.

Pour ce faire, sélectionnez chaque segment, puis saisissez l’attribut de champ personnalisé correspondant à partir de Salesforce dans la variable **[!UICONTROL ID de mappage]** champ .

>[!IMPORTANT]
>
>* La valeur utilisée pour la variable **[!UICONTROL ID de mappage]** doit correspondre exactement au nom de l’attribut de champ personnalisé créé dans Salesforce.
>* Assurez-vous que le nom de l’attribut de champ personnalisé que vous avez créé dans Salesforce n’utilise pas d’espace.


Voici un exemple :
![Planification de l’exportation de segments](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## Validation de l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![Parcourir les destinations](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Sélectionnez la destination et vérifiez que l’état est **[!UICONTROL enabled]**.
   ![Exécution du flux de données des destinations](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Basculez vers le **[!DNL Activation data]** , puis sélectionnez un nom de segment.
   ![Données d’activation des destinations](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Surveillez le résumé du segment et assurez-vous que le nombre de profils correspond au nombre créé dans le segment.
   ![Segment](../../assets/catalog/crm/salesforce/segment.png)

1. Connectez-vous au site web Salesforce, puis accédez à la **[!DNL Apps]** > **[!DNL Contacts]** et vérifiez si les profils du segment ont été ajoutés.
   ![Contacts Salesforce](../../assets/catalog/crm/salesforce/contacts.png)

1. Cliquez sur un contact et vérifiez si les champs sont mis à jour. Vous remarquerez que l’état du segment de l’Experience Platform a été mis à jour par rapport à l’attribut de champ personnalisé correspondant fourni dans la variable **ID de mappage** pendant la **[!UICONTROL Activer la destination]** > **[!UICONTROL Planification de l’exportation de segments]** étape .
   ![Contacts Salesforce](../../assets/catalog/crm/salesforce/contact-info.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

### Erreurs inconnues rencontrées lors de la publication d’événements vers la destination {#unknown-errors}

Lors de la vérification d’une exécution de flux de données, si le message d’erreur ci-dessous s’affiche, vérifiez que l’ID de mappage que vous avez fourni dans [!DNL Salesforce CRM] pour votre segment Platform valide et existe dans [!DNL Salesforce CRM].
![Erreur](../../assets/catalog/crm/salesforce/error.png)

## Ressources supplémentaires {#additional-resources}

Informations utiles supplémentaires de la [Portail de développement Salesforce](https://developer.salesforce.com/) est ci-dessous :
* [Création d’un enregistrement](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Audiences de recommandations personnalisées](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Utilisation de ressources composites](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* [Démarrage rapide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)

### Limites {#limits}

Salesforce équilibre les charges de transaction en imposant des limites de demande, de taux et de délai d’expiration. Reportez-vous à la section [Limites de requête d’API et affectations](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) pour plus d’informations.
